# 6. "Hello, world!" via Node.js & Yeoman

> _**Here be dragons! This section is probably out of date...**_

![1-node-js-and-yeoman](Part6/1-node-js-and-yeoman.png)

## Installing Node.js (via NVM)

We'll be using Node.js to scaffold our ASP.NET Core application via [Yeoman](http://yeoman.io/).

```
sudo apt-get install build-essential libssl-dev
```

![2-install-node-1](Part6/2-install-node-1.png)

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
```

![3-install-node-2](Part6/3-install-node-2.png)

__Note:__ Close and reopen your terminal to start using `NVM`.

Let's take a look to see which versions of Node.js we have installed.

```
nvm list
```

![4-install-node-3](Part6/4-install-node-3.png)

You guessed it, we don't have _any_ version of Node.js. Take a look at the versions of Node.js that are available to us.

```
nvm list-remote
```

![5-install-node-4](Part6/5-install-node-4.png)

![6-install-node-5](Part6/6-install-node-5.png)

Now we can install the latest (LTS) version of Node.

```
nvm install v4.4.0
```

![7-install-node-6](Part6/7-install-node-6.png)

Let's confirm that Node and NPM are installed.

```
node -v && npm -v
```

![8-install-node-7](Part6/8-install-node-7.png)

> Awesome! Oh wow! Like totally... ;)

#### Install Yeoman

> Yeoman is the web's scaffolding tool for modern webapps.

```
npm install -g gulp grunt-cli bower yo
```

![9-install-yo-1](Part6/9-install-yo-1.png)

![10-install-yo-2](Part6/10-install-yo-2.png)

#### Upgrade NPM

Yeoman is recommending that we upgrade NPM so let's do that.

```
npm install -g npm
```

![11-upgrade-npm](Part6/11-upgrade-npm.png)

#### Install the Yeoman ASP.NET Core generators

__Note:__ Yeoman generators are just regular NPM packages.

```
npm install -g generator-aspnet
```

![12-generator-aspnet](Part6/12-generator-aspnet.png)

#### Initialise some code

Now we're going to scaffold a new __ASP.NET Core Web API__ application.

```
yo aspnet
```

![13-yo-aspnet](Part6/13-yo-aspnet.png)

Run commands as directed to test your newly scaffolded application.

__TODO: (Tod) Work in progress => COMPLETE! ;)__
