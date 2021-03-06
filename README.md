winboxHunter
============
#Prerequisites:
```
- Python2.7
- Impacket (svn checkout http://impacket.googlecode.com/svn/trunk/ impacket-read-only)
- Ruby
- Veil Evasion (git clone https://github.com/Veil-Framework/Veil-Evasion.git)
```

#Description:
If you are working on a penetration test remotely, its sometimes hard to determine when the users start work or connect their laptops to the network.

winboxHunter is useful if you have managed to capture and cracked a bunch of NTLM credentails and want to run Metasploit against these windows boxes as and when they are connected to the network.

winboxHunter listens for NBNS broadcast packets so that when a new winBox is connected to the network, it will use the Impacket scripts (psexec.py and wmiexec.py) to push an executable onto the winBox and runs it.

In the background, winboxHunter runs Metasploit with payload handler (multi/handler) and listens for incoming connections from the winboxes.

You might want to modify autorunCmd.rc to specify the Metasploit commands you want to run on the pwned winbox upon connecting back to Metasploit.


```
See meterpreter.rc and autorunCmd.rc for more details.
```
If a host changes its IP address due to DHCP lease expiration, it will not attempt to exploit the winbox twice.


#Format of password.txt
```
domain/username password
```

#Instructions:
Meterpreter executable 
- You only need to use one of the below 2 options
```
- You can either use your own meterpreter payload executable  using the -e or --exe argument (payload=windows/meterpreter/reverse_https, rport=8443) or
- You can use the -n or --enableVeil argument to generate a meterpreter payload executable using Veil Evasion
```

You can run winboxHunter using the below sample command
![alt tag](https://raw.githubusercontent.com/milo2012/winboxHunter/master/screenshot.png)
```
ruby winboxHunter.rb -n -f password.txt -v
```

When you run winboxHunter, a linux screen with the name "msfscreen" will be created and msfconsole will be executed. You can connect to the screen via the below command
```
screen -dr msfscreen
```


