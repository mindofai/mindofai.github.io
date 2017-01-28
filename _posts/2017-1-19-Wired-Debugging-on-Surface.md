---
layout: post
title: Wired Debugging on a Surface Tablet? Yes You Can!
publish: true
---

From a mobile developer's perspective, debugging on a Surface tablet is weird.  The first time I picked up the Surface and spotted the USB port on the side, I figured, cool - I'll just plug it into my laptop and run something!  Ah.... no.  Sorry.  It's not that kind of USB port.  You can't just stick anything in there, man.

To debug on a Surface you have to install the Visual Studio Remote Debugger client app on your device and then wirelessly communicate with it to debug from Visual Studio.  Directions to do that is here: https://msdn.microsoft.com/en-us/library/y7f5zaaa.aspx

The problem with this is that more and more apps we're building need to be offline capable.  So how are you supposed to debug in an offline scenario with wireless debugging?  That's where that USB port is going to come in handy. 

One thing to note. Like a lot of mobile developers, I work all day on a MacBook Pro and use Parallels that runs a Windows 10 Virtual Machine so I can use all my Windows tools side by side - so this is written from that perspective.

# Hardware Needed

In order to debug over a wired connection, you'll need a few things:

 - 2 USB to Ethernet dongles.  You can find them for pretty cheap on [Amazon](https://www.amazon.com/gp/product/B00ET4KHJ2/ref=oh_aui_detailpage_o08_s00?ie=UTF8&psc=1).
 - a length of cat 5 cable to connect the two dongles together.

<div>
    <p style="float: right;"><img src="{{site.baseurl}}/images/WiredSurfaceDebugging/thunderboldToEthernetAdapter.jpeg" width="150"></p>
    What won't work here is one of those fancy lightning to Ethernet dongles plugged into my Mac, because my Windows VM doesn't recognize it.  The USB adapter is the one Windows understands.
</div>

<br /><br />

<div>
    <p style="float: left;"><img src="{{site.baseurl}}/images/WiredSurfaceDebugging/WiredSetup.jpg" width="300px"></p>
    Connect the dongles together, and plug one into your laptop and other other into the Surface.
</div>

<br /><br /><br /><br /><br /><br />

# Debugging Online and Offline

For our app, we need to be online the first time a user logs in and syncs data with the server, but then we want to disconnect from the internet to test offline scenarios after that first login. 

The trickiest part was getting my laptop to share it's internet connection with the Surface over my wired ethernet connection.  When you first connect your Surface to your laptop, if you turn off the Surface WiFi connection you'll see an icon indicating that there is no internet connection.  

Thankfully, there's a nice Windows feature that allows you to do that called Adapter Bridging.  Here's how to do it:

1. Open Network Connections on Windows
2. Locate the adapter that is supplying your internet connection. With Parallels this is done by an Ethernet adapter
3. Select both the adapter from step #2 and the one for your plugged in USB dongle
4. Right click and select "Bridge Connections"



Start debugging connected:

1. Bridge adapters
2. Open browser on Surface to check for connectivity
3. Get the Surface's IP address (cmd > ipconfig)
4. Enter the IP address in the Remote Machine textbox in Visual Studio
5. Run on Remote device

Disconnected:

1. Select adapters, right click, select Remove from Bridge
2. Wait for Surface to get new IP
3. Type it in the Remote Machine textbox in VS



Pro Tips:
- When Un-Bridging.  The Surface will show that the internet connection is lost right away and long before it gets a new IP, so wait for the USB Ethernet adapter to show that it has a new (different) IP before trying to debug to it in Visual Studio
- Generally, you'll have your Solution build configuration set to deploy the UWP head project to your device each time you start debuggin the app (SHOW SCREENSHOT). That means the app will be installed over the old one on each deploy and that can be undesirable when testing offline behavior, so don't forget to uncheck that if needed after the initial deploy of the app to the device.
- If you find yourself switching from connected in disconnected frequently, it's a pain to keep typing in the same 2 IP addresses. Undo (Ctrl + Z) works in that Remote Machine textbox.



Guiding Principles
 - Your Windows VM and Surface have to have matching IP addresses for the first two parts: (what is this called?) : 169.254.xxx.xxx
   - not sure about this actually.  IP of Windows 10 VM: 10.211.55.3, Surface: 192.168.1.132, and wireless debugging worked.  Had to enter manually tho
 - Don't live or die by what the "Remote Connections" dialog is able/unable to find. It's nice when it finds your device, but often it doesn't.  So if you've got this set up correctly, just type the IP + Port in the address box manually.
 - You must have the Visual Studio 2015 Remote Debugger app running on the Surface at all times.  the app will close after a certain period of inactivity.
 


# Common Errors

Error: Unable to connect to the Microsoft Visual Studio Remote Debugger named '10.211.55.5:4020'.  The Visual Studio Remote Debugger on the remote computer is running as a different user.
Fix: on the Surface, in the menu for the VS 2015 Remote Debugger app, go to Tools > Options, and check the "Allow any user to debug" option, under the "No Authentication" radio button.


# Resources
- [https://msdn.microsoft.com/en-us/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps](https://msdn.microsoft.com/en-us/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps)

