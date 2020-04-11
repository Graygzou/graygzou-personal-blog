# Setup a NAS with a raspberry pi

## Introduction
I wrote this little tutorial because i wanted to create a [NAS](https://en.wikipedia.org/wiki/Network-attached_storage) (Network-Attached Storage) with my raspberry pi 3. 
My configuration was the following : 
- A raspberry pi 3 with an external hard drive plug in it (formated in [NTFS](https://fr.wikipedia.org/wiki/NTFS_(Microsoft)).
- A PC client on Ubuntu.
- A PC client on Windows.
Like said before, the purpose was to make every files on the raspberry pi and on the hard drive available for the two other pc in the same network. I did not care about remote connection right now but i guess the steps should be quit similar.

## Constraints
My NAS wasn't going to be read-only. Indeed, I wanted to have the right to add files and work on it 
(mostly add github bare repository in order to simulate a central repository).

That access constraint cause me some additional steps and also a bit more research to make it works.


## Table of content

### [Setup the server]()
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

### [Setup the client]()
