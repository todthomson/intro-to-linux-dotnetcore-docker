# Step 3 - .NET Core "Hello, world!"

![1-dotnet-core-dev-stack](Step3/1-dotnet-core-dev-stack.png)

## .NET Core on Ubuntu GNU/Linux 14.04.4 LTS

__Note:__ In order to avoid excessive rehashing of work that's currently in a state of flux I will be providing _fast_ instructions on how to install .NET Core on Ubuntu GNU/Linux 14.04.4 LTS.

For more information see [here](http://dotnet.github.io/getting-started/). The following is practically verbatim from that source.

#### Add the .NET Core APT feed

```
sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/dotnet/ trusty main" \
> /etc/apt/sources.list.d/dotnetdev.list'
```

```
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
```

```
sudo apt-get update
```

![2-add-dotnet-core-apt-feed](Step3/2-add-dotnet-core-apt-feed.png)

#### Install .NET Core

```
sudo apt-get install dotnet=1.0.0.001598-1
```

![3-install-dotnet-core](Step3/3-install-dotnet-core.png)

#### Upgrade to latest

There's a newer version of .NET Core available so let's upgrade to that right away.

```
sudo apt-get update
```

```
sudo apt-get upgrade
```

![4-upgrade-dotnet-core](Step3/4-upgrade-dotnet-core.png)

#### .NET Core version

Let's check the version of `dotnet` that we've just upgraded to.

```
dotnet --version
```

![5-check-dotnet-version](Step3/5-check-dotnet-version.png)

Awesome! We now have version `1.0.0-beta-001673` of .NET Core.

#### Initialise some code

```
mkdir DotNetCoreTestApp
```

```
cd DotNetCoreTestApp
```

```
dotnet new
```

![6-dotnet-new-project](Step3/6-dotnet-new-project.png)

#### Run package restore

```
dotnet restore
```

![7-dotnet-restore-fail](Step3/7-dotnet-restore-fail.png)

#### Oh no!

So it turns out that `api.nuget.org` does not yet contain the .NET Core packages. You can find out more about this issue [here](https://github.com/dotnet/cli/issues/535). Let's try `dotnet restore` again, but this time we'll supply the package source as an extra parameter.

```
dotnet restore -s https://myget.org/f/dotnet-core
```

![8-dotnet-restore-success](Step3/8-dotnet-restore-success.png)

#### Run the application

```
dotnet run
```

![9-dotnet-run](Step3/9-dotnet-run.png)

## End of step 3

__Excellent!__ You have said hello to the world of _.NET Core_.

Have a quick break and then continue with [Step 4 - ASP.NET Core "Hello, world!"](Step4.md).
