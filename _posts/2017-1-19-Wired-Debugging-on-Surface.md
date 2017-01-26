---
layout: post
title: Wired Debugging on a Surface Tablet? Yes You Can!
publish: true
---

From a mobile developer's perspective, debugging on a Surface tablet is weird.  The first time I picked up the Surface and spotted the USB port on the side, I figured, cool - I'll just plug it into my laptop and run something!  No.  Sorry.  It's not that kind of USB port.  You can't just stick anything in there, man.

Like a lot of mobile developers, I work all day on a MacBook Pro and use Parallels that runs a Windows 10 Virtual Machine so I can use all my Windows tools side by side.


What won't work is a lightning to Ethernet dongle plugged into my Mac, because my Windows VM doesn't recognize that dongle.


# Basic Setup
- Install the Visual Studio Remote Debugger on your Surface


When Un-Bridging.  The Surface will show that the internet connection is lost right away and long before it gets a new IP, so wait for the USB Ethernet adapter to show that it has a new (different) IP before trying to debug to it in Visual Studio


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

Pro Tip:
 If you find yourself switching from connected in disconnected frequently, it's a pain to keep typing in the same 2 IP addresses. Undo (Ctrl + Z) works in that Remote Machine textbox.



Guiding Principles
 - Your Windows VM and Surface have to have matching IP addresses for the first two parts: (what is this called?) : 169.254.xxx.xxx
   - not sure about this actually.  IP of Windows 10 VM: 10.211.55.3, Surface: 192.168.1.132, and wireless debugging worked.  Had to enter manually tho
 - Don't live or die by what the "Remote Connections" dialog is able/unable to find. It's nice when it finds your device, but often it doesn't.  So if you've got this set up correctly, just type the IP + Port in the address box manually.
 - You must have the Visual Studio 2015 Remote Debugger app running on the Surface at all times.  the app will close after a certain period of inactivity.
 


errors

Error: Unable to connect to the Microsoft Visual Studio Remote Debugger named '10.211.55.5:4020'.  The Visual Studio Remote Debugger on the remote computer is running as a different user.
Fix: on the Surface, in the menu for the VS 2015 Remote Debugger app, go to Tools > Options, and check the "Allow any user to debug" option, under the "No Authentication" radio button.


*H1 Resources

https://msdn.microsoft.com/en-us/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps 


![_config.yml]({{ site.baseurl }}/images/config.png)

