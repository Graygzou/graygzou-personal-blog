---
Title: "Setup serveur Raspberry pie NAS"
Description: TODO
tags: ["raspberry pi"]
draft: true
---

# Setup the server
In this part, we will see what I've done in order to setup the server for both client Windows and Ubuntu.

## Table of content
1. Mounted the External Hard disk drive (HDD)  
    1.1. Study the current list device mount points  
    1.2. Find the UUID of the device you want to operate on  
    1.3. Add rules in `/etc/fstab`  
    1.4. Reload mounted devices  

2. Samba  
    2.1. Installation  
    2.2. Configuration  
    2.3. Add users to controls access  
    2.4. Restart the service  
    2.5. Encountered errors  
    
Acknowledgements  

## 1. Mounted the External Hard disk drive (HDD)
*Note:* If you want to sharing a file which is already in the system HDD you can skip this section.  

In order to have as much control as possible on the serve, I wanted to choose exactly where my external hard drive will be mounted.
By default, it was automatically mounted in the folder `/media/<username>` on my raspberry pi. But i wanted to make it automatically mount in `/mnt/ext`.

### 1.1. Study the current list device mount points
You can see where your devices are mounted with the following commands. 
The last one seams the best overall in term of output controls. 
```
$ mount       # mount a filesystem (used for general mount info too).
$ df          # report file system disk space usage.
$ lsblk       # list block devices.
$ findmnt     # will list all mounted filesytems or search for a filesystem.
```
(*Note*: the following will be based on the output of the last command : `findmnt`)

### 1.2. Find the UUID of the device you want to operate on
Once you have mapped the destionation (TARGET) and the device itself (SOURCE),
you can run the command:
```
$ ls -laF /dev/disk/by-uuid/
```

This command will give you the **UUID** of the device you want to control the mounting operation.
For example, if you have the following output:
```
total 0
lrwxrwxrwx 1 root root  10 mars  31 16:52 38D6-E887 -> ../../sda1
lrwxrwxrwx 1 root root  10 mars  31 16:52 3634D33CT45322BB -> ../../sda2
lrwxrwxrwx 1 root root  10 mars  31 16:52 54B8DYUFB8D93062 -> ../../sda8
lrwxrwxrwx 1 root root  10 mars  31 16:52 6022D63C28T616BE -> ../../sda4
lrwxrwxrwx 1 root root  10 mars  31 16:52 322F858C22D616BA -> ../../sda4
```
You will know that the device `/dev/sda1` have the UUID equals to `38D6-E887`.

### 1.3. Add rules in `/etc/fstab`
With this UUID, you can add a line in the file `/etc/fstab` that takes care of mouting automatically a partition at boot time.
To keep the UUID above, we can add the line:
```
UUID=38D6-E887	/media/special-folder	vfat	defaults	0	0
```
*Note*: `defaults` can be replace by a lot of options. 
See the aknowledgement section for more information about it.

### 1.4. Reload mounted devices
Finally, in order to update  mounted point with the new `/etc/fstab`, you have two choices:
- Either you can also run the command
```
$ mount -a      # causes all filesystems mentioned in /etc/fstab to be remounted, except the partitions with noauto option.
```
- Or you can reboot the system.  

-----

## 2. Samba
In order to managed the windows client, I've installed Samba on my raspberry pi.
[Samba](https://help.ubuntu.com/lts/serverguide/samba.html.en) as nothing in common with the music style except his name.
It is a software used in order to share files and printers through a **local network** 
(if you want to use it in public network, you will have to use other tool since Samba is a LAN thing, not a WAN thing. See this [thread](https://superuser.com/questions/526258/connect-to-samba-server-remotely)).    

I used this software because of my architecture : 
Samba implements the SMB protocol and provides support for the Windows naming service (WINS) and for joining a Windows Workgroup.
So my windows client could also access the share folder.

### 2.1. Installation
*Quick Note:* A lot of those steps are prefectly described in the provided links (see [Acknowledgements](#acknowledgements) section)

Run the following command in order to install the Samba package
```
$ sudo apt-get update && apt-get upgrade        # Classic commands to update your packages
$ sudo apt-get install samba samba-common-bin   # Install samba and samba-common-bin packages
```
### 2.2. Configuration
To configure Samba you need to open the file `/etc/samba/smb.conf`
```
$ sudo nano /etc/samba/smb.conf         # You can replace nano with your favorite text editor
```
You can go through the file by yourself. A lot of comments (starting with `#` and `;`) are written in order to explain some options you can use.

#### Basic configuration
Before adding your own section in order to share a folder/a printer, you need to make sure your basic parameters are correct.
In the "header" of the file  
```
workgroup = WORKGROUP   # or your workgroup if you override it
wins support = yes      # This is useful only if you want to share with a client on windows.
```

#### Special Sections
*Note:* The file contains two special sections : the **Global** section, the **Homes** section and the **Printers** section.
- **Global section** : Parameters in the [global] section apply to the server as a whole, or are defaults for sections that do not specifically define certain items.
- **Homes section** : If a section called [homes] is included in the configuration file, services connecting clients to their home directories can be created on the fly by the server.
- **Printers section** : This section works like [homes], but for printers.

#### User Sections
You then have to add your custom space if you want to share it.
A basic configuration can be the following :
```
[basicShare]              ## This name will be printed in your client's explorer.
 comment = Raspberry Pi Share     ## This is an optionnal parameters. It will show when you put your mouse hover the folder.
 path = /home/pi/share            ## Specify the root of the folder you want to share. Here the root will start at `/home/pi/share`. So you have to create a folder `share` in the pi home folder.
 browseable = yes                 
 writeable = yes                  ## Allow the user, once loged in, to write into the shared space.
 only guest = no                  
 create mask = 0777               
 directory mask = 0777
 public = no                      ## this means that anyone wanting to access the shared folder must login with a valid user.
 valid users = greg, @pcusers
 ...
```
A few parameters description are given here :
- `browseable` : bool, This controls whether this share is seen in the list of available shares in a net view and in the browse list.  
Default: yes.
- `writeable` (Inverted synonym for `read only`) : bool, If this parameter is yes, then users of a service may create or modify files in the service's directory.  
Default: no
- `only guest` (synonym of `guest only`) : bool, If this parameter is yes for a service, then only guest connections to the service are permitted. This parameter will have no effect if guest ok is not set for the service.  
Default: no
- `public` (synonym of `guest ok`) : bool, if this parameter is yes for a service, then no password is required to connect to the service.  
Default: no
- `valid users` : list, This is a list of users that should be allowed to login to this service.  
Default : # No valid users list (anyone can login)

A details description of all parameters and configurations can be found in the link below (See [smb.conf - samba.org](#acknowledgements) in the Acknowledgements section)

#### Tips
1) If you use a share name (header of the share space) longer than 12 characters, it may not be accessible to some older clients.
2) To make sure your file doesn't contains errors you can run the command below. 
It will give you a recap of the configuration file your just changed
```
$ testparm      # Test the correctness of samba config file.
```

### 2.3 Add users to controls access
```
sudo smbpasswd -a bob
```
And then enter bob's password twice. This will create a samba user bob that you can use later in your `/etc/samba/smb.conf` file. In the case you forgot your password, you can re-run this command to add the user again to override the previous password.

You can list all the samba users but running the command where `-L` stands for list users and `-v` stands for verbose :
```
sudo pdbedit -L -v      # used to manage the passdb backend, as well as domain-wide account policy settings
```

### 2.4 Restart the service
Finally run the command in order to make your changes be take into account :
```
$ sudo /etc/init.d/samba restart            # This one should be enough
$ sudo /usr/sbin/service smbd restart       # But you can run both just to be sure
```

### 2.5 Encountered errors
* [X] **Make sure your config file use the same workspace than your client (windows)**  
by default, `workgroup = WORKGROUP` is enough since it's the basic setup that windows use as workgroup. 
But it is worth checking if it the same.
------------------
* [X] **Check your iptable rules**  
Make sure you didn't block the incoming connexion to your raspberry pi !
You can check that if you run those following debug commands :
```
systemctl status smbd.service
journalctl -xn
```
It should show you if your request was filter or not. It it was filtered, you should check your iptables config (see [Acknowledgements](#acknowledgements) section).
```
$ /etc/init.d/networking restart
```
or depending on your distribution:
```
$ /etc/init.d/iptables restart  
$ /etc/init.d/firewall restart
```
------------------
* [X] **Adding valid users**  
In order to specify valid users (but also invalid one) you need to create and use UNIX users. You can do it by running the command
```
$ sudo adduser user_name
  ## Enter your password when prompt

$ smbpasswd -a user_name
  ## Use the same password
```
You will be prompt to add a password for that user. **Warning** : Use the same when creating the samba user !
```

```
------------------
* [X] **Comeback to the default .conf file**  
If you mess up your samba configuration file, you can come back to the default one by taking the one store in `/usr/share/samba/smb.conf`. The following command should do the trick :
```
$ sudo cp /usr/share/samba/smb.conf /etc/samba/smb.conf
```
------------------
* [X] **Can't access file due to low pemissions**  
This error will show up on the client when trying to reach the path specified in the samba configuration file. 
In order to resolve this, you need to make sure the folder specified in the `path` option has the right permission to be shared with the client.  
*Note:* If you use an NTFS external drive, you will have to format it in ext4 before, or use FUSE and NTFS-3G if you're lazy like me :
```
$ sudo apt-get install fuse ntfs-3g
$ sudo mkdir /mnt/ext                           # You can create or choose any folder you want.
$ sudo mount -t ntfs-3g /dev/sda1 /mnt/ext/     # mount the sda1 on the specified path created earlier.
```
For more information see `NTFS External HDD Read Only File System link` below.

## <a name="acknowledgements"></a>Acknowledgements
### Mounting
#### Mounting and fstab links
* [mount and fstab (in french) - doc.ubuntu-fr.org](https://doc.ubuntu-fr.org/mount_fstab)
* [MultipleUsbSticks - cpmspectrepi.uk](http://www.cpmspectrepi.uk/raspberry_pi/MoinMoinExport/MultipleUsbSticks.html)
* [RPi Adding USB Drives - elinux.org](https://elinux.org/RPi_Adding_USB_Drives)

#### Common errors links
* [Mount a samba share on boot - askUbuntu](https://askubuntu.com/questions/157128/proper-fstab-entry-to-mount-a-samba-share-on-boot)
* [How do I check where devices are mounted? - askubuntu.com](https://askubuntu.com/questions/583909/how-do-i-check-where-devices-are-mounted)

### Samba
#### Samba configuration links
* [How to share folder raspberry pi - raspberrypihq.com](https://raspberrypihq.com/how-to-share-a-folder-with-a-windows-computer-from-a-raspberry-pi/)
* [Samba - raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/samba.md)
* [smb.conf - samba.org](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html#BROWSEABLE)

#### Common errors links
* [Connect to samba server remotely - superuser.com](https://superuser.com/questions/526258/connect-to-samba-server-remotely)
* [Raspberry Pi forum - Samba for RaspberryPi](https://www.raspberrypi.org/forums/viewtopic.php?t=196068)
* [Securing Your Raspberry Pi - madirish.net](https://www.madirish.net/566)
* [Add samba iptables rules - troy.jdmz.net](http://troy.jdmz.net/samba/fw/)
* [Configure itables in Ubuntu - upcloud.com](https://upcloud.com/community/tutorials/configure-iptables-ubuntu/)
* [Reloading iptables in Ubuntu - askubuntu.com](https://askubuntu.com/questions/91413/reloading-iptables)
* [NTFS External HDD Read Only File System - Raspberrypi.org](https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=30886)
