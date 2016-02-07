# Step 2 - GNU/Linux Configuration & Maintenance

Now we have a basic Ubuntu GNU/Linux installation up and running we'll look a few basic pieces of installation and configuration that will make your life easy.

## Background

Before we begin here's a little background.

#### Debian packages

Debian packages exist as either binary or source packages with the extension [`.deb`](https://en.wikipedia.org/wiki/Deb_(file_format)). Under the hood they contain two [`.tar`](https://en.wikipedia.org/wiki/Tar_(computing)) archives with optional compression. The program which handles the configuration, installation and removal of Debian packages is [`dpkg`](https://en.wikipedia.org/wiki/Dpkg).

#### APT (the Advanced Packaging Tool)

The [Advanced Packaging Tool](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) `APT` is the "package manager" of Debian GNU/Linux and its variants (e.g. Ubuntu). It provides for the almost completely automated discovery, retrieval, configuration, installation and removal of both binary and source packages. APT is wrapper around `dpkg` adding useful extra functionality like automated package download, bulk package update, automatic package dependency tree resolution, etc...

#### Aptitude

> Aptitude has Super Cow Powers

Yes. It is true. Aptitude has Super Cow Powers. Never. Forget. This. Ever.

[Aptitude](https://wiki.debian.org/Aptitude) is an [ncurses](https://en.wikipedia.org/wiki/Ncurses)-based terminal front-end to to APT. It also contains a "like for like" CLI-wrapper around `apt-get` and `apt-cache` e.g. `apt-get install foo` is the same as `aptitude install foo`.

_But why should I care?_ When you install package X `aptitude` (via `apt-get`) will recursively install all dependencies (same for both `apt-get` or `aptitude`). Then when you remove package X down the line with `aptitude` it will _remove all dependencies_ installed at the same time, without breaking other applications that are also using those dependencies or removing dependencies that you have explicitly installed previously. There are more reasons to prefer `aptitude` to `apt-get`, but this is all I will say about it for now.

## Updating your new system

CLOSE SOFTWARE UPDATER

OPEN NEW TERMINAL VIA "SUPER" KEY

`sudo apt-get update`

`sudo apt-get upgrade`

`sudo apt-get install aptitude`

NOW ONLY EVER USE APTITUDE










