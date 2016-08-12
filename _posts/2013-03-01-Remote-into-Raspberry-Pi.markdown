---
layout: post
---
<img src="/images/fulls/ssh.png" class="fit image"> Setting up SSH to Raspberry Pi via MAC

Things you will need:

1.	Raspberry Pi
2.	HDMI tv connected to the Pi (Temporary)
3.	Keyboard and Mouse connected to the Pi (Temporary)
4.	Ethernet cable connected to the Pi
5.	Power connected to the Pi
6.	A Mac Computer

Set up your Pi according to the listed items above, just be sure to have internet connected above all things. Within the Raspbian Desktop interface launch the LXTerminal. Once that is launched go to the Terminal window and type 

`sudo raspi-config`

Pressing enter should yield a blue screen configuration menu similar to the configuration screen when your Raspbian OS booted up for the first time. 


Scroll down to 8. Advanced Options and then to A4 SSH - this window should now give you the option to either enable or disable. Highlight Enable and then either exit or hit finish on the beginning configuration screen.  Raspbian may or may not ask you to reboot your Pi at this time, if it does, hit enter and let it boot up again. Once the Pi has finished rebooting (or it ends up not asking you at all) open up the LXTerminal once more and type in

`ifconfig`

and hit enter. The text should display something along the lines of this -  

```
eth0    Link encap:Ethernet  HWaddr b8:27:eb:fb:3a:5b   
          inet addr:192.168.1.224  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25920 errors:0 dropped:0 overruns:0 frame:0
          TX packets:7377 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:4716330 (4.4 MiB)  TX bytes:3498622 (3.3 MiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:2805 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2805 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:2790624 (2.6 MiB)  TX bytes:2790624 (2.6 MiB)
```

All we need to gather from this output is the inet addr- which is your Pi's IP address. So write town that snippet down on paper or engrain it in your noggin because we shall need that number in the steps to come. 

So at this point we can leave the Pi alone, we enabled SSH and successfully retrieved the IP address pointing to the Pi, at this time open up your Mac and on the search bar (Top right hand corner) search for X11-  which is a fancier terminal window which will help us finish up this SSH business for good.   

In order for us to connect to the Raspberry Pi via SSH we must first generate a key, to do this insert this command within your terminal -

` ssh-keygen -R xxx.xxx.x.xxx  <- insert your Pi IP addr here. `

Now that the key is generated to the Rasp Pi type into the terminal ssh -X [[yourPIname@ipaddress]].

` ssh -X pi@xxx.xxx.x.xxx`

You will now be prompted to enter the password associated with the Pi that you created during the initial boot up.

Congratulations! You now are SSH'ed into your Raspberry Pi's terminal via your Computer! To enter the GUI environment simply enter

`lxsession`
