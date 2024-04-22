# DashboardPi
My MagicMirror Dashboard Project

## Setup:

First step is connecting your micro USB to a computer and going to [RaspBerry Pi OS](https://www.raspberrypi.com/software/) to download the Raspberry Pi OS.

Second step is opening the imager.

![screenshot of imager](/process-for-github/Screenshot-2024-04-22-092748.png)

Choose your device, OS, and storage then hit next.

![screenshot of interlude](/process-for-github/Screenshot-2024-04-22-095138.png)

From here we want to edit the settings. I used dashboardpi for the hostname since I want it to be easy to find later on.

![screenshot of settings](/process-for-github/Screenshot-2024-04-22-095559.png)

Then hit yes and wait, once the process is done go ahead and eject the micro USB and move it over into your pi and plug it in. It should automatically boot.

Now that the pi is up and running we need to use another computer to [SSH](https://www.cloudflare.com/learning/access-management/what-is-ssh/) into it. 

I use [Advanced IP Scanner](https://www.advanced-ip-scanner.com/) which is a free IP scanning tool and [PuTTY](https://www.putty.org/) which is an SSH client.

![IP Scanner](/process-for-github/ScreenshotIPScanner.png)

Hit Scan and search, this is where the host name dashboardpi comes in handy. When the scan finishes just find it and right click it to copy the IP address.

Open up PuTTY and put in the IP address.

![PuTTY](/process-for-github/ScreenshotPuTTY.png)

A terminal will appear, type in your username and password that you set up in the settings when flashing the image of the Raspberry Pi OS.

Now we need to install Nodejs. Type the following:

```
$ sudo apt-get update
$ sudo apt-get install nodejs
```

Note: the $ does not need to be copied from here just everything after it.

When the option appears type yes and hit enter.

The last step will be setting up VNC so we can manipulate the desktop of our Pi from our computer if we need to.

Start by downloading [TigerVNC](https://tigervnc.org/).

Next type in:

```
$ sudo raspi-config
```

This is what should popup in your terminal:

![ConfigScreen](/process-for-github/ScreenshotConfig.png)












