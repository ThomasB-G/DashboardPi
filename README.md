# DashboardPi
My MagicMirror Dashboard Project

## Setup:

First step is connecting your micro USB to a computer and going to [RaspBerry Pi OS](https://www.raspberrypi.com/software/) to download the Raspberry Pi OS.

Second step is opening the imager.

![screenshot of imager](/process-for-github/Screenshot-2024-04-22-092748.png)

Choose your device, OS, and storage then hit next.

![screenshot of interlude](/process-for-github/Screenshot-2024-04-22-095138.png)

From here we want to edit the settings. I used

![screenshot of settings](/process-for-github/Screenshot-2024-04-22-095559.png)

Then hit yes and wait, once the process is done go ahead and eject the micro USB and move it over into your pi and plug it in. It should automatically boot.

Now that the pi is up and running we need to use another computer to [SSH](https://www.cloudflare.com/learning/access-management/what-is-ssh/) into it. 

I use [Advanced IP Scanner](https://www.advanced-ip-scanner.com/) which is a free IP scanning tool and [PuTTY](https://www.putty.org/) which is an SSH client.

![IP Scanner](/process-for-github/ScreenshotIPScanner.png)

Hit Scan and search
