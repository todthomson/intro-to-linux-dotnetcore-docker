# 1. Ubuntu Linux Installation

![1-gnu-linux](Part1/1-gnu-linux.jpg)

First we'll get a basic Ubuntu Linux Installation up and running.

## Prerequisites

1. Download the latest [Ubuntu Desktop 64-bit ISO](https://launchpad.net/ubuntu/+cdmirrors) (e.g. `ubuntu-16.04-desktop-amd64.iso`) from your local Ubuntu mirror (so as to save your quota and to download it as fast as possible). We're using _Ubuntu Desktop 'Xenial Xerus' 16.04 LTS_ as it's "unofficially supported" (full support is coming in the RTW) and it's the primary Linux distribution (and version) being used by the .NET Core team.

2. Download the latest [VirtualBox installer](https://www.virtualbox.org/wiki/Downloads) for your operating system of choice (e.g. Windows `VirtualBox-5.0.22-108108-Win.exe` or MacOSX `VirtualBox-5.0.22-108108-OSX.dmg`). Also download the corresponding version of the [extension pack](https://www.virtualbox.org/wiki/Downloads) (e.g. for all operating systems `Oracle_VM_VirtualBox_Extension_Pack-5.0.22-108108.vbox-extpack`). This extension pack contains host drivers for USB etc.

## Installing and configuring VirtualBox

1. Install VirtualBox by following the prompts. You should include __all__ options.

2. Double-click the VirtualBox Extension Pack and click __accept__ to install.

3. VirtualBox should now be open.

4. Update the "host key combination" in VirtualBox Preferences as follows:

  a. (Macintosh) __Preferences... => Input => Virtual Machine__ and update the __Host Key Combination__ to _Right COMMAND_.

  b. (Wintel) __File => Preferences... => Input => Virtual Machine__ and update the __Host Key Combination__ to _Right CTRL_.

  ![2-virtualbox-host-key](Part1/2-virtualbox-host-key.png)

## Creating the new VM

1. Click __New__ in VirtualBox to begin the process of creating your new VM.

2. Give your VM a __name__ (e.g. Ubuntu), select __type__ _Linux_, __version__ _Ubuntu (64-bit)_ and then click __next__.

  ![3-name-and-os](Part1/3-name-and-os.png)

3. Determine how much memory (RAM) to dedicate to your VM. I recommend a minimum of `2048MiB` and a maximum of `50%` of your host's physical memory e.g. in my case I have a MacBook Pro with `16GiB` of memory so I chose to configure my new VM with `4096MiB` of memory. Then click __next__.

  ![4-memory-size](Part1/4-memory-size.png)

4. Leave the option _Create a virtual hard disk now_ in place and click __create__.

  ![5-create-hdd](Part1/5-create-hdd.png)

5. Leave the option _VDI (VirtualBox Disk Image)_ in place and click __next__.

  ![6-hdd-file-type](Part1/6-hdd-file-type.png)

6. Leave the option _Dynamically allocated_ in place and click __next__.

  ![7-dynamically-allocated-disk](Part1/7-dynamically-allocated-disk.png)

7. Determine the maximum size for your __dynamically allocated disk__. I recommend setting this to a reasonable size which is less than the currently available space on the host disk e.g. in my case I have `182GiB` free so I set the maximum disk size to `128GB`. The other option is to set it to `2TB` and monitor actual `.vdi` file size yourself. This maximum size can be altered later via the command line tools so it's not _set in stone_.

8. Once you are happy with all your settings click __create__ to build your new VM and VHDD.

  ![8-hdd-size](Part1/8-hdd-size.png)

## Configuring your new VM

You now have a new __powered off__ VM so we want to update the configuration using some "more-optimal" defaults prior to installing Linux. Click __settings__ to configure your new VM.

![9-powered-off](Part1/9-powered-off.png)

#### General => Advanced

1. Set __shared clipboard__ and __drag'n'drop__ to _bidirectional_.

  ![10-general-advanced](Part1/10-general-advanced.png)

#### System => Motherboard

1. Set __boot order__ to a) _floppy_ b) _network_ c) _optical_ d) _hard disk_ then disable _floppy_ and _network_.

2. Set __chipset__ to _ICH9_.

3. Set __pointing device__ to a setting which matches your host hardware e.g. I'm on a `2015 MacBook Pro` so I set it to _USB multi-touch tablet_ when in MacOSX. When in Windows I set it to _PS/2 Mouse_ (as I'm using just a mouse).

4. If the _only_ host operating system you run on your PC is Windows __unselect__ _Hardware Clock in UTC Time_.

  ![11-system-motherboard](Part1/11-system-motherboard.png)

  __Note:__ Windows generally expects its hardware clock in to be in _local time_. Macintosh (and most other operating systems) run their hardware clocks in _UTC by default_. Windows can be told it's hardware clock is in UTC using via the registry as described [here](http://superuser.com/a/975764/120578).

#### System => Processor

1. Determine how many __Processor(s)__ to assign to your new VM. I recommend a minimum of `1` and a maximum of `half the number` of __logical__ CPU cores of your host machine e.g. in my case I have a `2015 MacBook Pro` with `4 physical / 8 logical` CPU cores, so I _could_ set the virtual CPU cores to `4`, however I just selected `1` as that's all I will need for Linux.

2. Check __enable PAE/NX__.

  ![12-system-processor](Part1/12-system-processor.png)

#### System => Acceleration

1. Set __paravirtualization interface__ to _KVM_ which is the recommended setting for Linux guests. When using a Windows guest you should set it to _Hyper-V_.

  ![13-system-acceleration](Part1/13-system-acceleration.png)

  > VirtualBox allows exposing a paravirtualization interface to facilitate accurate and efficient execution of software within a virtual machine. These interfaces require the guest operating system to recognize their presence and make use of them in order to leverage the benefits of communicating with the VirtualBox hypervisor.

  > Most mainstream, modern guest operating systems, including Windows and Linux, ship with support for one or more paravirtualization interfaces. Hence, there is typically no need to install additional software in the guest (including VirtualBox Guest Additions) to make use of this feature.

  > Exposing a [paravirtualization provider](https://www.virtualbox.org/manual/ch10.html#gimproviders) to the guest operating system does not rely on the choice of host platforms. For example, the Hyper-V paravirtualization provider can be used for VMs to run on any host platform (supported by VirtualBox) and not just Windows.

  __Note:__ The option __default__ _should_ have the same effect i.e. _default_ will automatically set the optimal __paravirtualization interface__ setting dependent on the guest operating system selected.

#### Display => Screen

1. Increase the __video memory__ to the maximum available setting. In my case this is `128MB`.

2. Check __enable 3D acceleration__.

  ![14-display-screen](Part1/14-display-screen.png)

#### Storage

1. Remove the __empty__ virtual optical drive from the __storage tree__ by selecting it and then clicking the _subtract disk_ icon at the bottom (second from the left).

2. Remove the virtual __controller: ide__ from the __storage tree__ by selecting it and then clicking the _subtract controller_ icon at the bottom (the rightmost icon).

3. Add a new virtual optical drive by selecting __controller: sata__ and clicking the _add disk_ icon at the bottom (the leftmost icon). When the modal appears click __choose disk__ and select `ubuntu-14.04.4-desktop-amd64.iso` downloaded earlier. Also check __use host i/o cache__.

4. If your host has an SSD select __Ubuntu.vdi__ and check __solid-state drive__.

  ![15-storage](Part1/15-storage.png)

#### Audio

1. Set __audio controller__ to _Intel HD Audio_.

  ![16-audio.png](Part1/16-audio.png)

#### Network => Adapter 1

1. Expand the __advanced__ section and set the __adapter type__ to _paravirtualized network (virtio-net)_.

  > [Virtio](http://wiki.libvirt.org/page/Virtio) is a virtualization standard for network and disk device drivers where just the guest's device driver "knows" it is running in a virtual environment, and cooperates with the hypervisor. This enables guests to get high performance network and disk operations, and gives most of the performance benefits of paravirtualization.

2. If you are on "wired network" (e.g. ethernet) set __attached to__ to _bridged adapter_. If you're on a "wireless network" (e.g. `802.11abgn` or `4G` etc) leave __attached to__ as _NAT_ as a lot of wireless access points will not allow multiple DCHP allocations to the same physical device (so the virtual device will fail to get an IP address).

  ![17-network-adapter-1](Part1/17-network-adapter-1.png)

#### Ports => USB

1. Select __USB 3.0 (xHCI) Controller__.

  ![18-ports-usb](Part1/18-ports-usb.png)

__Done!__ Click __OK__ to save the VM settings.

## Booting your new VM and installing Linux

1. Double-click your new VM labelled __Ubuntu => Powered Off__ to boot the VM and begin the installation.

  ![9-powered-off](Part1/9-powered-off.png)

  __Note:__ While your new VM is booting into the installation screen, if your are using a host with a "retina" screen select __View => Scale Factor => 200%__ so you can actually see your VM while it's installing.

2. Once you arrive at the first screen labelled __Install__ click _Install Ubuntu_.

  ![19-install-ubuntu](Part1/19-install-ubuntu.png)

3. Check _download updates while installing Ubuntu_. If you want to be able to play _patent-encumbered audio formats_ et al you should also check _install this third-party software..._. Once you're happy click _continue_.

  ![20-preparing-to-install](Part1/20-preparing-to-install.png)

4. To keep things simple leave the default option __Erase disk and install Ubuntu__ in place and click _install now_.

  ![21-erase-disk-and-install](Part1/21-erase-disk-and-install.png)

5. Confirm the partition table changes by clicking _continue_.

  ![22-write-changes-to-disk](Part1/22-write-changes-to-disk.png)

6. _Where are you?_ should have automatically detected and configured your location via the Internet. If this didn't happen stop and check the "up and down" arrows in the task bar (top right corner) to confirm you have internet access through _NAT_ or _Bridged Mode_ via the host. If you don't have any Internet access that's OK just type in to the autocomplete the name of your closet capital city e.g. _Brisbane (Queensland, Australia)_ or your timezone e.g. _Lord Howe Time (Australia)_ and then click _continue_.

  ![23-where-are-you](Part1/23-where-are-you.png)

7. Leave the left pane set to __English (US)__. If you're using Windows hardware also leave the right pane set to __English (US)__. If you're using Mac hardware select __English (US) - English (Macintosh)__ in the right pane. Then click on _continue_.

  ![24-keyboard-layout](Part1/24-keyboard-layout.png)

8. _Who are you?_ Use the following guide to fill in these details:

  a. __Your name:__ e.g. Tod Nicholas Thomson

  b. __Your computer's name:__ e.g. apsalar

    __Note:__ Feel free to take a look at [RFC1178](https://tools.ietf.org/html/rfc1178) or __TL;DR__ Use all lower case (Unix is case-sensitive). Don't use random combinations of letters and numbers that "encode" some information about the location or function of the computer which are hard to "talk about". At the other end of the spectrum don't use names that will clash or sound like real people's names.

  c. __Pick a username:__ e.g. tnt

    _Note:__ The "Unix way" is to use all your initials for your username. You need to type your username a lot so it's good for it to be short.

  d. __Choose a password__ and __confirm your password__. You will need to remember this password as you'll need it when you want to run things as _root_ (administrator).

  e. For ease of use (and as this is just a VM) select __log in automatically__.

  f. click __next__ to begin the process of installing your new Linux system.

  ![25-who-are-you](Part1/25-who-are-you.png)

    __Note:__ While you wait, expand the lower section to take a look at the installation _under the hood_. Also _use the left and right arrows_ to explore some user-facing parts of your new Ubuntu install.

9. Once you see the message __installation complete__ click _restart now_.

10. If you see an error with `snd_hda_intel` then select __Machine => Reset => Do not show this message again => Reset__. We will fix this in part 2.

![26-intel-hd-audio-reboot-error](Part1/26-intel-hd-audio-reboot-error.png)

## End of Part 1

__Congrats!__ You now have fresh Linux VM.

Take a 5 minute coffee break and then head over to [2. Ubuntu Linux Configuration & Maintenance](Part2.md).
