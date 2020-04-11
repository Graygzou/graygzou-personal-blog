---
Title: "Setup client Raspberry pie NAS"
Description: TODO
tags: ["raspberry pi"]
draft: true
---

# Setup the client
After setting up the server (see the dedicated file), I almost did all the job.
Indeed, with a little bit of work, I was able to connect to the samba server with both of my client.

## 1. On Windows
In order to map the raspberry with the windows system, you have to associated a letter (E: for example) to the share folder.

You can accomplished that with a WYSIWYG explorer interface :
1. Open a file explorer window.
2. On the left panel, click on the root folder named "This PC".
3. In the top view, click on the Computer tab
4. Click on the Map network drive icon.
5. Select the letter you want to use for the share space and give the link to it (something like `\\\192.168.X.X\share`)
6. Then, you should be prompt to enter your credentials in order to connect to that space.
7. You're done ! You just need to click on the icon that correspond to this share space, connect with your credential every time you need to 

## 2. On Ubuntu
What I did on Windows did not fit with my current workflow in Ubuntu. Unlike Windows, I did not open often the explorer window.
So I did not wanted a solution that rely heavily on user interface.

### fstab or not fstab ?
I decided to use the same previous technique I did on the server with fstab to automatically mount the shared folder.

It works perfectly! But I had a small issue : The connexion was not launched at boottime si I had to run manually `mount -a` every time.
But, as pointed in this [thread](https://doc.ubuntu-fr.org/autofs), if you use a wifi connection, fstab will not be able to load because the user didn't log in yet.
So a solution will be to use autofs.

### autofs
autofs control the deamon in charge of automount in the system. 
*Note:* All the information below come from this website. 
But sadly for most of you, it's in the language of Molière (french).

#### Installation
Install autofs and also cifs-utils in my case (because I'm using samba for my window client)
```
$ sudo apt-get update && apt-get upgrade     # Classic commands to update your packages
$ sudo apt-get install autofs cifs-utils     # Install samba and samba-common-bin packages
```

#### Setup 
Run the following command to modify the file `/etc/auto.master` and add the following line :
```
$ sudo nano /etc/auto.master
# Add the below line in the file
/<mounting_point> /etc/auto.<type> --ghost,--timeout=30
```

Create `/etc/auto.<type>` and rule for each share file :
```
<mon_partage>    -fstype=<type>,rw,options    <ip_serveur>/<dossier_du_partage_sur_le_serveur>
# Like the following example
<target_mounting_point> -fstype=cifs,credentials=/home/<user>/.cred-file,user=<user>,uid=1000,gid=1000 ://NasName/nasMountPoint
```

#### Restart autofs
As usual when you make changes, run the command :
```
$ sudo service autofs restart
```

#### Tips
- [X] Make sure the <mounting_point> in the `/etc/auto.master` needs to exist.
- [X] In the file `/etc/auto.<type>`, the <target_mounting_point> need to **not** exist. 
It will be created automatically when the shared folder is loaded.
- [X] NasName needs to be replaced by the server ip adress since Windows do not resolve server name automatically. **Don't forget the `:` character.**
- [X] uid=1000 corresponds to your linux uid on the client.
- [X] gid=100 corresponds of the `users` group in linux.

#### Encountered errors (mostly based on git work)
* [X] **Connect to server by hostname (instead of IP adresses)**  
I'm currently using the IP adress of the server to connect to it. Is there any way i can use the hostname name directly ?  
You can use [`avahi-daemon`](https://linux.die.net/man/8/avahi-daemon) package that will take care of mapping the server IP with his hostname and propagate this info to a daemon which will configures unicast DNS servers.
See the links below for more information on that.
---
* [X] **Permission denied**  
I have an error when running `mount -a` : `error 13 = Permission denied`. What is going on ?  
This can come from many reason. You might want to take a look at the following step: [mount error - stackexchange](https://unix.stackexchange.com/questions/124342/mount-error-13-permission-denied)
---
* [X] **`Error failed to push some refs to`**  
When I try to push I get the following log with `error: remote unpack failed: unable to create temporary object directory`.  
If you try to push and still get an error that contains the above message, it probably means you do not have access (write) to the mounted devices. To fix this, you need to change the permissions on the files you want to write to (by using `chmod` for example). An alternative could be to use `sudo [your command]` and see if it works. It that's a permission issue, the sudo command should work.

## Acknowledgment
#### autofs
* [autofs (in french) - doc.ubuntu-fr.org](https://doc.ubuntu-fr.org/autofs)

#### Others
* [ssh server by hostname - askubuntu.com](https://askubuntu.com/questions/144280/cannot-ssh-into-ubuntu-server-by-hostname)
* [uid, gid explanation - geek-university.com](https://geek-university.com/linux/uid-user-identifier-gid-group-identifier/)
* [permission denied - ubuntuforums.org](https://ubuntuforums.org/showthread.php?t=1871142)
* [mount cifs fstab non-read/write - superuser.com](https://superuser.com/questions/456243/mount-cifs-through-fstab-non-readable-writable)
