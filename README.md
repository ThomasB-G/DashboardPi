# DashboardPi
My MagicMirror Dashboard Project

## Setup

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
$ sudo apt-get install -y npm
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

Navigate to interface, then VNC, and enable it. Wait a moment and when its finished exit the config screen.

Now open Tiger VNC:

![VNCScreen](/process-for-github/ScreenshotVNC.png)

Enter your username and password to ensure that it works.

Once you're finished you can close TigerVNC since we won't need it for now.

## MagicMirror

Now we are done with setup and ready for setup haha.

Start in the terminal and follow these steps:

Step 1: Clone the repository `$ git clone https://github.com/MagicMirrorOrg/MagicMirror`

Step 2: Change Directory to MagicMirror `$ cd MagicMirror`

Step 3: Install the application `$ npm run install-mm`

Step 4: To populate MagicMirror with some basics copy the sample to the main `$ cp config/config.js.sample config/config.js`

When you want to run this program now or in the future type `$ npm run start` when in the MagicMirror directory.

## Modules

Now that the basics are installed we are going to install any extra Modules that we want.

For my use case I'll be adding the following:

[MMM-AutoDimmer](https://github.com/Fifteen15Studios/MMM-AutoDimmer), This will dim the screen at night and brighten it back up in the morning.

[MMM-connection-status](https://github.com/sheyabernstein/MMM-connection-status), This will show a simple message at the top of the screen letting me know if the internet is working or not.

[MMM-ModuleScheduler](https://github.com/ianperrin/MMM-ModuleScheduler), This will allow me to hide other modules if I want to at specific times.

[MMM-CalendarExt3](https://github.com/MMRIZE/MMM-CalendarExt3), This will allow me to create a two week calendar on the screen in addition to the list provided by MagicMirror.

[MMM-Wallpaper](https://github.com/kolbyjack/MMM-Wallpaper), This will allow me to add a background image or images instead of a solid color.

To start this process we need to change our directory in the terminal. Do this by typing `$ cd` which will take you home, then type `$ MagicMirror` and finally `$ modules`. Or a faster method is simply typing `$ cd ~/MagicMirror/modules` from home.

Next we clone the git project, here are the ones I'll be using:

```
$ git clone https://github.com/Fifteen15Studios/MMM-AutoDimmer.git
$ git clone https://github.com/sheyabernstein/MMM-connection-status
$ git clone https://github.com/ianperrin/MMM-ModuleScheduler.git
$ git clone https://github.com/MMRIZE/MMM-CalendarExt3
$ git clone https://github.com/kolbyjack/MMM-Wallpaper.git
```

Now we have to go into each individual module. From home that looks like `$ cd ~/MagicMirror/modules/MMM-AutoDimmer` or from modules you simply type `$ cd MMM-CalendarExt3` for example.

This next part needs to be repeated for every module or they won't work. Once inside the module type `$ npm install`.

If any vulnerabilities pop up then type `$ npm audit fix`, if there are still vulnerabilities you may need to type `$ npm audit fix --force` but after that everything should be working.

## Starting Configuration

The next step for me involves utilizing TigerVNC to open up the Pi's desktop and then navigating through files to MagicMirror and then configuration. In this folder you'll find config.js.

![config folder](/process-for-github/Screenshotconfigfolder.png)

I've opened it in the native IDE Geany but if you have your own downloaded you can use that as well.

![Geany](/process-for-github/Screenshotgeany.png)

I'm starting by deleting the alert, compliments, and notification modules. I don't want them for my dashboard but you can do whatever you want with them.

Now we can run the program and see what we are dealing with.

![Base MagicMirror](/process-for-github/Screenshotbase.png)

Pretty ugly, also I'll be using a vertical screen but that's easily altered through the Pi's screen preferences.

Also due to the size of the screen I'll be using I'll need to change the size of the fonts. That happens in our custom.css file in the css folder found in the MagicMirror folder.

![CSS Folder](/process-for-github/Screenshotcssfolder.png)

In the CSS file I'll be adding this code:

```
.xsmall {
  font-size: 40px;
  line-height: 50px;
}

.small {
  font-size: 60px;
  line-height: 70px;
}

.medium {
  font-size: 80px;
  line-height: 95px;
}

.large {
  font-size: 110px;
  line-height: 125px;
}

.xlarge {
  font-size: 140px;
  line-height: 160px;
  letter-spacing: -6px;
}
```

It's important that the code is placed outside of the root. 

The reason we are working inside the custom.css file is that this is where we add code that will override anything from the various modules or the main.css file. Keep all of your changes here.

## Google Calendar

Now we work on changing the calendar to our google Calendar. 

Quick tip is to never forget your comma's when editing as that is the most common mistake that will kill your program followed by remembering parenthesis and brackets.

By the end of this part our Calendar section should look something like this:

```
config: {
	calendars: [
		{
			url: 'https://www.calendarlabs.com/templates/ical/US-Holidays.ics',
			symbol: 'calendar',
      name: 'CalendarName',
			auth: {
			    user: 'username',
			    pass: 'superstrongpassword',
			    method: 'basic'
			}
		},
	],
}
```

To start open up you're google calendar.

![Google Calendar](/process-for-github/Screenshotgooglecal.png)

Then open up settings.

![Google Settings](/process-for-github/Screenshotgooglesettings.png)

Navigate to the Calendar you want to show and scroll down until you see the secret iCal link.

![iCal Location](/process-for-github/Screenshotical.png)

Use that secret link for your calendar and put in the username and password. 

Make sure to name the Calendar as well because future modules that want calendar information can take just the name instead of filling out all that info again.

## Weather

The end result for this section will hopefully look like this:

```
{
			module: "weather",
			position: "top_right",
			config: {
				fade: false,
				weatherProvider: "openweathermap",
				type: "current",
				location: "your location",
				locationID: "yourlocationID", 
				apiKey: "yourapikey"
			}
		},
		{
			module: "weather",
			position: "top_right",
			header: "Weather Forecast",
			config: {
				fade: false,
				weatherProvider: "openweathermap",
				type: "forecast",
				location: "your location",
				locationID: "yourlocationID",
				apiKey: "yourapikey"
			}
		},
```

First thing's first is you need to travel to [Open Weather Map](https://openweathermap.org/) and create an account.

Once you have one navigate to your account's API keys. To do this simply click on your name at the top of the home screen and a drop down will appear with "My API Key's" as one option.

![Weather API key](/process-for-github/Screenshotopenweather.png)

Take your API key and put it in to both weather modules and you are good to go here.

Then comes the annoying part. You have to find your location ID in this big json file: [OpenWeather Locations](http://bulk.openweathermap.org/sample/city.list.json.gz)

Extract the file and I recommend you open it with wordpad instead of notepad. Wordpad handles the large file better than notepad which took a while to load for me.

Search the file and once you've found your location ID just slap it in to both weather sections and you are good on this section.

## MMM-CalendarExt3

When you're done with this section it should look something like this:

```
{
	module: "MMM-CalendarExt3",
	position: "lower_third",
	title: "Calendar",
	config: {
		mode: "week",
		weekIndex: 0,
		weeksInView: 2,
		fontSize: '40px',
		eventHeight: '50px',
		useMarquee: true,
		instanceId: "basicCalendar",
		locale: 'en-US',
		maxEventLines: 5,
		firstDayOfWeek: 7,
		calendarSet: ['calendar'],
		    
	}
},
```

Make sure this comes after the calendar module so that this will work correctly.

## MMM-Wallpaper

This section is pretty simple and should look like this:

```
{
	module: "MMM-Wallpaper",
	position: "fullscreen_below",
	config: { // See "Configuration options" for more information.
		source: "bing",
		slideInterval: 3600 * 1000 // Change slides every hour, minute would be 60 * 1000, and ten minutes would be 600 * 1000
		updateInterval: 12 * 3600 * 1000 // Checks for new slides every 12 hours
	}
}
```

## MMM-AutoDimmer

This section should look like this:

```
{
	module: 'MMM-AutoDimmer',
	position: 'fullscreen_above',
	header: '',
	// Don't change anything above this line
	config: {
		schedules: [{
			// Will dim completely from 11pm-3am every day
			maxDim: 1,
			dimTime: 2300,
			brightTime: 300
			// defaults are used for values that are not explicitly set
		}
					
		] 
	}
}
```

## MMM-connection-status

For this section the code should look something like this:

```
{
	module: 'MMM-connection-status',
	header: "Internet Connection",
	position: 'top_bar', // Or any valid MagicMirror position.
	config: {
		updateInterval: 60 * 1000, //every minute
		initialLoadDelay: 0, //time to wait before starting
		animationSpeed: 250, //animation speed
		connectedColor: '#228B22', //forest green
		disconnectedColor: '#8B0000' //Red
	}
},
```

## Custom CSS

My custom css file can be found [here](/custom.css)




