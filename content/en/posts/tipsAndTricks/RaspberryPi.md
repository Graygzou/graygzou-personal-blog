---
Title: "Raspberry Pi infos"
Description: TODO
date: 2020-04-11T18:26:10+02:00
tags: ["raspberry-pi", "troubleshootings"]
draft: true
---

# 

## Having troubles with your tv screen ?
1) Run the following commands to know what's going on with your screen and the raspberry pi
```
tvservice -s (or --status) # get HDMI status : will tell you what your current HDMI mode is.
tvservice -m CEA (or --modes=CEA) # get supported modes for CEA : will tell you the "CEA modes" available. (hdmi group 1)
tvservice -m DMT (or --modes=DMT) # get supported modes for DMT : will tell you the "DMT modes" available. (hdmi group 2)
```

### CEA vs DMT
- CEA modes are intended for TV, they include plenty of interlaced and progressive modes, 
usually with 25/50/100Hz (PAL) or 30/60/120Hz (NTSC) 
frame rates and TV resolutions of 288/480/576/720/1080 scan lines. 
- DMT modes are intended for computer monitors, therefore there are none of the interlaced modes, 
the resolutions are 640/720/800/1024/1280 and 
the frame rates are compatible with the computer monitors, something like 60/70/75/80/85/120Hz.

### /boot/config.sys
By modifying this file, you can hard code display data for the raspberry pi.
```
sudo nano /boot/config.sys
```
For example, you can change :
```
sdtv_aspect=3
```
in order to have 16:9 aspect and 
```
hdmi_safe=1.
```
to force getting a picture on HDMI for a default "safe" mode.

### Sources
- https://www.raspberrypi.org/forums/viewtopic.php?t=72871
- https://www.raspberrypi.org/forums/viewtopic.php?t=52309
- https://raspberrypi.stackexchange.com/questions/7332/what-is-the-difference-between-cea-and-dmt
- https://github.com/raspberrypi/userland/tree/master/host_applications/linux/apps/tvservice
