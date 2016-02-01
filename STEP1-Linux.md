# Step 1 => Linux

First we'll get a basic Linux installation up and running.

## Prerequisites

1. Download the latest [Ubuntu Desktop 64-bit ISO](https://launchpad.net/ubuntu/+cdmirrors) (e.g. `ubuntu-15.10-desktop-amd64.iso`) from your local Ubuntu mirror to save your quota and to download as fast as possible.

2. Download the latest [VirtualBox installer](https://www.virtualbox.org/wiki/Downloads) for your operating system of choice (e.g. for Mac OS X `VirtualBox-5.0.14-105127-OSX.dmg`). Also download the corresponding version of the [extension pack](https://www.virtualbox.org/wiki/Downloads) (e.g. for all operating systems `Oracle__VM__VirtualBox__Extension__Pack-5.0.14-105127.vbox-extpack`). This extension pack contains drivers for USB etc.

## Installing and configuring VirtualBox

1. Install VirtualBox by following the prompts. You should include __all__ options.

2. Double click on the VirtualBox extension pack and __accept__ to install. VirtualBox should now be open.

3. Open VirtualBox __Preferences... => Input => Virtual Machine__ and update the __Host Key Combination__ to _Right COMMAND_ if you're on Mac or _Right CTRL_ if you're on non-Mac hardware.

## Creating the new VM

1. Select __New__ in VirtualBox to begin the process of creating your new VM.

2. Give your VM a __name__ (e.g. Ubuntu), select __type__ _Linux_, __version__ _Ubuntu (64-bit)_ and __continue__.

3. Determine how much memory (RAM) to dedicate to your VM. I recommend a minimum of `2048MiB` and a maximum of `50%` of your host's physical memory e.g. in my case I have a MacBook Pro with `16GiB` of memory so I chose to configure my new VM with `4096MiB` of memory. Then select __continue__.

4. Leave the option _Create a virtual hard disk now_ in place and select __continue__.

5. Leave the option _VDI (VirtualBox Disk Image)_ in place and select __continue__.

6. Leave the option _Dynamically allocated_ in place and select __continue__.

7. Determine the maximum size for your __dynamically allocated disk__. I recommend setting this to a reasonable size which is less than the currently available space on the host disk e.g. in my case I have `182GiB` free so I set the maximum disk size to `128GB`. The other option is to set it to `2TB` and monitor actual `.vdi` file size yourself. This maximum size can be altered later via the command line tools so it's not _set in stone_.

8. Once you are happy with all your settings select __create__ to build your new VM and VHDD.

## Configuring your new VM

Now you have a new __powered off__ VM we want to update the configuration using some more optimal defaults prior to installing Linux. Click on __settings__ to configure your new VM.

### General => Advanced

1. Set __shared clipboard__ and __drag'n'drop__ to _bidirectional_.

### System => Motherboard

1. Set __boot order__ to a) _floppy_ b) _network_ c) _optical_ d) _hard disk_ then disable _floppy_ and _network_.

2. Set __chipset__ to _ICH9_.

3. Set __pointing device__ to a selection which matches your host hardware e.g. I'm on a `2015 MacBook Pro` so I set it to _USB multi-touch tablet_.

### System => Processor

1. Determine how many __Processor(s)__ to assign to your new VM. I recommend a minimum of `1` and a maximum of `half the number` of logical CPU cores of your host machine e.g. in my case I have a `2015 MacBook Pro` with `4 physical / 8 logical` CPU cores, so I _could_ set the virtual CPU cores to `4`, but I selected just `1` as that's all I will really need.

2. Select __enable PAE/NX__.

### Display => Screen

1. Increase the __video memory__ to the maximum available setting. In my case this is `128MB`.

2. If you have a _retina_ display then select __use unscaled HiDPI Output__.

3. Select __enable 3d acceleration__.

### Storage

1. Remove the __empty__ virtual optical drive from the __storage tree__ by selecting it and then clicking on the _subtract disk_ icon at the bottom (second from the left).

2. Remove the virtual __controller: ide__ from the __storage tree__ by selecting it and then clicking on the _subtract controller_ icon at the bottom (the rightmost icon).

3. Add a new virtual optical drive by selecting __controller: sata__ by clicking on the _add disk_ icon at the bottom (the leftmost icon). When the modal appears click on __choose disk__ and select `ubuntu-15.10-desktop-amd64.iso` downloaded earlier.

4. If your host has an SSD select __Ubuntu.vdi__ and select __solid-state drive__.

### Audio


