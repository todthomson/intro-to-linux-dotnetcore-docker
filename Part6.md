# 6. "Hello, world!" Node.js and Yeoman

![1-node-js-and-yeoman](Part4/1-node-js-and-yeoman.png)

## Installing Node.js (via NVM)

We'll be using Node.js to scaffold our ASP.NET Core application via [Yeoman](http://yeoman.io/).

```
sudo apt-get install build-essential libssl-dev
```

![26-install-node-1](Part4/26-install-node-1.png)

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
```

![27-install-node-2](Part4/27-install-node-2.png)

__Note:__ Close and reopen your terminal to start using `NVM`.

Let's take a look to see which versions of Node.js we have installed.

```
nvm list
```

![28-install-node-3](Part4/28-install-node-3.png)

You guessed it, we don't have _any_ version of Node.js. Take a look at the versions of Node.js that are available to us.

```
nvm list-remote
```

![29-install-node-4](Part4/29-install-node-4.png)

![30-install-node-5](Part4/30-install-node-5.png)

Now we can install the latest LTS version of Node.

```
nvm install v4.4.0
```

![31-install-node-6](Part4/31-install-node-6.png)

Let's confirm that Node and NPM are installed.

```
node -v && npm -v
```

![32-install-node-7](Part4/32-install-node-7.png)

> Awesome! Oh wow! Like totally... ;)

#### Install Yeoman

> Yeoman is the web's scaffolding tool for modern webapps.

```
npm install -g gulp grunt-cli bower yo
```

![33-install-yo-1](Part4/33-install-yo-1.png)

![34-install-yo-2](Part4/34-install-yo-2.png)

#### Upgrade NPM

Yeoman is recommending that we upgrade NPM so let's do that.

```
npm install -g npm
```

![35-upgrade-npm](Part4/35-upgrade-npm.png)

#### Install the Yeoman ASP.NET Core generators

__Note:__ Yeoman generators are just regular NPM packages.

```
npm install -g generator-aspnet
```

![36-generator-aspnet](Part4/36-generator-aspnet.png)

#### Initialise some code

Now we're going to scaffold a new __ASP.NET Core Web API__ application.

```
yo aspnet
```

![37-yo-aspnet](Part4/37-yo-aspnet.png)

As directed run the following commands to test your newly scaffolded application.

```
cd AspNetCoreWebApiTestApp
```

```
dnu restore
```

![38-dnu-restore-1](Part4/38-dnu-restore-1.png)

![39-dnu-restore-2](Part4/39-dnu-restore-2.png)

So far so good. Let's see what's next.

```
dnu build
```

![40-dnu-build-1](Part4/40-dnu-build-1.png)

![41-dnu-build-2](Part4/41-dnu-build-2.png)

That's not awesome. The first screenshot above should make the fix obvious. For some background information [see here](https://github.com/aspnet/Home/issues/1104).

```
dnu build --framework dnxcore50
```

![42-dnu-build-dnxcore50-1](Part4/42-dnu-build-dnxcore50-1.png)

![43-dnu-build-dnxcore50-2](Part4/43-dnu-build-dnxcore50-2.png)

__Note:__ Another option is to remove the line `"dnx451": {},` from the `frameworks` section of `project.json`.

#### Run the application

Running the application is simple.

```
dnx web
```

![44-dnx-web](Part4/44-dnx-web.png)

Open Firefox and navigate to `http://localhost:5000/api/values` to see your new _Web API_ in action.

![45-web-api-in-action](Part4/45-web-api-in-action.png)
