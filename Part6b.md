# Building applications with Docker

## Intro to problem

One i

## Installing node and Yeoman

[Node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)
[Yeoman](https://docs.asp.net/en/latest/client-side/yeoman.html)

## Build api and app

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


## Dockorizing

### Docker files/build

### Linking

```bash
    docker build . -t rethinklogs:latest
```

```bash
    docker run -itd -p 5000:5000 --link rethinkdb --name=rethinklogs rethinklogs
```

### Networking

Create backend network:

```docker network create backend```

Run Rethinklogs app (and RethinkDb) --todo add volume

```docker run -itd -p 8080:8080 -p 28015:28015 -p 29015:29015 --net=backend -v ~/rethinkdb_data --name=rethinkdb rethinkdb```

```docker run -itd -p 80:5000 --net=backend --name=rethinklogs rethinklogs
```



## Compose

## Distrubuted

## Swarm 

## Ensure containers run on startup

* Upstart
* Systemd
* ?

## Reference to Wolfy's repo
