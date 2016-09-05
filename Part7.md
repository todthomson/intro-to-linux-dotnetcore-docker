# Building applications with Docker

## Intro to problem

One i

## Installing node and Yeoman

[Node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)
[Yeoman](https://docs.asp.net/en/latest/client-side/yeoman.html)

## Build api and app

__or clone this repo [insert](https://guthub.com/?)__

### Api

```
    yo aspnet
```

Pick api

```
    dotnet retsotore
    dotnet run
```

test on [localhost:5000/api/values](http://localhost:5000/api/values)

### App

```
    yo aspnet
```

Pick basic web app

```
    dotnet retsotore
    dotnet run
```

test on [localhost:5000/api/values](http://localhost:5000/api/values)

### Modify web app to call api

First update the ```HomeController.cs``` to call the api

```
    insert code here
```

Modify ```Views/Home/Index``` and by insertign the following;

```
    Insert some view updates
```


Change the port of the web app to 5001 in the ```Program.cs``` file

```
.UseUrls("http://localhost:5001/")
```


Start both apps to test (two terminals, VS Code terminal etc.).

```
    Insert command(s)
```

### Make url's configurable

In both projects delete the ```Program.cs``` and insert the following in the ```Startup.cs``` instead of the ```xxx``` method

```
    public static void Main(string[] args)

        {

           Configuration = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsetings.json", optional: true, reloadOnChange: true)
                .AddEnvironmentVariables()
                .Build();

            var hostUrl = Configuration.GetValue<Uri>("HostUrl").ToString();

            var host = new WebHostBuilder()
                .UseConfiguration(Configuration)
                .UseKestrel()
                .UseContentRoot(Directory.GetCurrentDirectory())
                .UseIISIntegration()
                .UseStartup<Startup>()
                .UseUrls(hostUrl)
                .Build();

            host.Run();
        }

        public static IConfigurationRoot Configuration { get; set; }
```

In the ```HomeController``` update the hardcoded url with this:

```
    ViewData["Message"] = await new HttpClient().GetStringAsync(
                Startup.Configuration.GetValue<string>("ApiBaseUrl") + "/api/values");
```


###Adding the configuration settings

In the app project add config for the ```HostUrl``` in the ```appSettings.json``` like this:

```
    "HostUrl" : "http://localhost:5000"
```

For the app project add this;

```
    "HostUrl" : "http://localhost:5001",
    "ApiBaseUrl" : "http://localhost:5000"
```

## Dockorizing

First of all let's have look at the dockerfile that the yeoman scaffoldign added for the api project:

```
FROM microsoft/dotnet:latest

COPY . /app

WORKDIR /app

RUN ["dotnet", "restore"]

RUN ["dotnet", "build"]

EXPOSE 5000/tcp

ENTRYPOINT ["dotnet", "run", "--server.urls", "http://0.0.0.0:5000"]
```

Lets try to build and run that:

```
docker build -t myapi .
```

Let's run the api container

```
    docker run -itd -p 5000:5000 --name=myapi myapi
```

![screenshot](TODO)

Test your api on the host machine

```http://localhost:5000/api/values
```


Now do the same for the app

Build the image

```
docker build -t myapp .
```

Let's run the app container

```
    docker run -itd -p 5001:5001 --name=myapp myapp
```

![screenshot](TODO)

Test your app on the host machine

```http://localhost:5001
```



### Linking

That didn't work... The reason is that the two containers are not able to see each other. Let's fix that. THe easiest way is by linking.

```bash
    docker run -itd -p 5001:5001 --link myapi --name=myapp myapp
```

### Networking

Well linking is just so last yeah, and the new way is to create shared networks. So let's do that.

Create backend network:

```docker network create backend
```

And then start the two containers

```docker run -itd -p 5000:5000 --net=backend --name=myapi myapi
```

```docker run -itd -p 5001:5001 --net=backend --name=myapp myapp
```


## Compose

Docker compose is a tool for stitching together docker containers in a declaraive way. Composer runs confifurations specifies in docker-compose.yaml files. For our example app we need a docker-compose file like this.

```
version: '2'
services:
    api:
        build: ./myapi
        container_name: myapi
        ports:
            - "5000:5000"
        networks:
            - backend

    app:
        build: ./myapp
        container_name: myapp
        ports:
            - "5001:5001"
        depends_on:
            - api
        networks:
            - backend

networks:
    backend:
        driver: bridge
```

## Distrubuted

## Swarm 

## Ensure containers run on startup

* Upstart
* Systemd
* ?

## Reference to Wolfy's repo
