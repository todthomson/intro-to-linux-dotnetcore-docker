# 3. "Hello, world!" .NET Core

![1-dotnet-core-dev-stack](Part3/1-dotnet-core-dev-stack.png)

## .NET Core on Ubuntu Linux

__Note:__ In order to avoid excessive rehashing of work that's currently in a state of flux I will be providing _fast_ instructions on how to install .NET Core on Ubuntu Linux.

For more information see [here](https://www.microsoft.com/net/core#ubuntu). The following is practically verbatim from that source, except that we're installing it on Ubuntu 16.04 LTS (the latest) not 14.04.4 LTS (from two years ago).

#### Are we up to date?

First let's check we're completely up to date.

```
sudo apt-get update && sudo apt-get upgrade
```

__Note:__ If you see any errors here please resolve them before continuing.

#### Adding the .NET Core APT feed

Now we're up to date let's add the .NET Core APT feed.

__Note:__ That we are specifying `xenial main` not `trusty main` here as we're using Ubuntu 16.04 LTS ([Xenial Xerus](https://wiki.ubuntu.com/XenialXerus/ReleaseNotes)) rather than Ubuntu 14.04.4 LTS ([Trusty Tahr](https://wiki.ubuntu.com/TrustyTahr/ReleaseNotes)).

```
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
```

```
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
```

```
sudo apt-get update
```

![2-add-dotnet-core-apt-feed](Part3/2-add-dotnet-core-apt-feed.png)

#### Checking Available .NET Core Versions

Next let's see what .NET Core versions are now available.

![3-list-dotnet-core-versions](Part3/3-list-dotnet-core-versions.png)

#### Installing .NET Core

OK now we can install the _newest_ version of .NET Core.

```
sudo apt-get install dotnet-dev-1.0.0-preview2-003119
```

![4-install-latest-dotnet-core-1](Part3/4-install-latest-dotnet-core-1.png)

![5-install-latest-dotnet-core-2](Part3/5-install-latest-dotnet-core-2.png)

You can find more information about versions of the .NET CLI [here](https://github.com/dotnet/cli).

#### Smoke Testing .NET Core

Let's check the version of `dotnet` that we now have available.

```
dotnet --version
```

![6-checking-dotnet-core-version](Part3/6-checking-dotnet-core-version.png)

Awesome! We now have version `1.0.0-preview2-003119` of .NET Core.

__TODO: (Tod) CONTINUE UPDATING FROM HERE...__

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

![6-dotnet-new-project](Part3/6-dotnet-new-project.png)

#### Run package restore

```
dotnet restore
```

![7-dotnet-restore-fail](Part3/7-dotnet-restore-fail.png)

#### Oh no!

So it turns out that `api.nuget.org` does not yet contain the .NET Core packages. You can find out more about this issue [here](https://github.com/dotnet/cli/issues/535). Let's try `dotnet restore` again, but this time we'll supply the package source as an extra parameter.

```
dotnet restore -s https://myget.org/f/dotnet-core
```

![8-dotnet-restore-success](Part3/8-dotnet-restore-success.png)

#### Run the application

```
dotnet run
```

![9-dotnet-run](Part3/9-dotnet-run.png)

## End of Part 3

__Excellent!__ You have said hello to the world of _.NET Core_.

Have a quick break and then continue with [4. "Hello, world!" ASP.NET Core](Part4.md).
