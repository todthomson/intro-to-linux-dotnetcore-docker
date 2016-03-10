# Step 4 - ASP.NET Core "Hello, world!"

![1-aspnet-core](Step4/1-aspnet-core.png)

## ASP.NET Core on Ubuntu GNU/Linux 14.04.4 LTS

__Note:__ In order to avoid excessive rehashing of work that's currently in a state of flux I will be providing _fast_ instructions on how to install ASP.NET Core on Ubuntu GNU/Linux 14.04.4 LTS.

For more information see [here](https://docs.asp.net/en/latest/getting-started/installing-on-linux.html#installing-on-ubuntu-14-04). The following is practically verbatim from that source.

#### Install the .NET version manager

```
curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.sh | \
DNX_BRANCH=dev sh && source ~/.dnx/dnvm/dnvm.sh
```

![2-dnvm-install](Step4/2-dnvm-install.png)

```
source ~/.dnx/dnvm/dnvm.sh
```

```
dnvm --version
```

![3-dnvm-version](Step4/3-dnvm-version.png)

#### Install the .NET execution environment (DNX)

```
sudo aptitude update
```

```
sudo aptitude install libunwind8 gettext libssl-dev libcurl4-openssl-dev zlib1g libicu-dev uuid-dev
```

![4-dnx-prerequisites](Step4/4-dnx-prerequisites.png)

```
dnvm upgrade -r coreclr
```

![5-upgrade-latest-coreclr](Step4/5-upgrade-latest-coreclr].png)

#### Install DNX for Mono

```
sudo aptitude install mono-complete
```

TODO: REDO THIS AS I DIDN'T GET A SCREENSHOT :(


HOW TO `ca-certificates-mono`???



TODO: CONTINUE FROM HERE



## End of step 4

TODO: FIX THE BELOW!

Excellent! You have said `HELO` to the world of ASP.NET Core ;)

Have a quick break and then continue with [Step 5 - LXC/Docker](Step5.md).
