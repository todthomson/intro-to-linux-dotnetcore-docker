# Step 1

This is a tutorial on Linux, .NET Core and Docker.

## Linux

First we'll get a basic Linux installation up and running.

### prerequisites

1. Download the latest Ubuntu Desktop 64-bit ISO from your local Ubuntu mirror (to save your download quota and make the download as fast as possible) e.g. [ubuntu-15.10-desktop-amd64.iso](?).

2. Download the latest [VirtualBox](?) installer for your operating system of choice e.g. [VirtualBox-5.0.14-105127-OSX.dmg](?). Also download the corresponding VirtualBox [extension pack](?) e.g. [Oracle_VM_VirtualBox_Extension_Pack-5.0.14-105127.vbox-extpack](?). The extension pack contains necessary drivers for USB et al.

### Install and configure VirtualBox

1. Install VirtualBox by following the prompts. You should include _all_ options.

2. Double click on the VirtualBox extension pack and _accept_ to install. VirtualBox should now be open.

3. Open VirtualBox _Preferences... => Input => Virtual Machine_ and update the _Host Key Combination_ to "Right COMMAND" if you're on Mac or "Right CTRL" if you're on non-Mac hardware.

### Creating a new VM

1. Select _New_ in VirtualBox to begin the process of creating your new VM.

2. Give your VM a _name_ e.g. "Ubuntu", select _type_ "Linux", _version_ "Ubuntu (64-bit)" and _continue_.

3. Determine how much memory (RAM) to dedicate to your VM. I recommend a minimum of 2048MiB and a maximum of 50% of your host's physical memory e.g. in my case I have a MacBook Pro with 16GiB of memory so I chose to configure my new VM with 4096MiB of memory. Then select _continue_.

4. Leave the option "Create a virtual hard disk now" in place and select _continue_.

5. Leave the option "VDI (VirtualBox Disk Image)" in place and select _continue_.

6. Leave the option "Dynamically allocated" in place and select _continue_.

7. Determine the maximum size for your _dynamically allocated disk_. I recommend setting this to a reasonable size which is less than the currently available space on the host disk e.g. in my case I have 182GiB free so I set the maximum disk size to 128GB. The other option is to set it to 2TB and monitor actual `.vdi` file size yourself. This maximum size can be altered later via the command line tools so it's not "set in stone".

8. Once you are happy with all your settings select _create_ to build your new VM and VHDD.

### Configuring your new VM

Now you have a new _powered off_ VM we want to update the configuration using some more optimal defaults prior to installing Linux.

1. Select _settings_ to configure your new VM.

#### General => Advanced

1. Set _shared clipboard_ and _drag'n'drop_ to _bidirectional_.

#### System => Motherboard

1. Set _boot order_ to a) _floppy_ b) _network_ c) _optical_ d) _hard disk_ then disable _floppy_ and _network_.

2. Set _chipset_ to _ICH9_.

3. Set _pointing device_ to a selection which matches your host hardware e.g. I'm on a 2015 MacBook Pro so I set it to _USB multi-touch tablet_.

4. (REVIEW) Set _Enable EFI (special OSes only)_.

#### System => Processor

1. Determine how many _Processor(s)_ to assign to your new VM. I recommend a minimum of one and a maximum of half the number of logical CPU cores of your host machine e.g. in my case I have a MacBook Pro with four physical / eight logical CPU cores, so I could set the virtual CPU cores to four, but I selected just one as that's all I will really need.

2. Select _enable PAE/NX_.

#### Display => Screen

1. Increase the _video memory_ to the maximum available setting. In my case this is 128MB.

2. If you have a "retina" display then select _use unscaled HiDPI Output_.

3. Select _enable 3d accelleration_.

TODO => continue on from here...
