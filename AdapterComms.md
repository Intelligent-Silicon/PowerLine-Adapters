# Communicating with your Powerline Adapter reliably

There's two main issue's which affect your ability to communicate with your powerline adapters. 

The first is the network card in your windows box and the second is how your powerline adapter connects to the network.

The best way to avoid any doubt when trying to communicate directly with a powerline adapter, is to plug the ethernet cable from your Windows box to the power line adapter, obviously the powerline adapter needs to be plugged into a main's socket in order to power it on.

This repo work's on this basis, so to communicate with multiple powerline adapter's it involves alot of unplugging and plugging in of different powerline adapters before making changes or reviewing information from the device.

In the Qualcomm document, this is referred to as a ```local``` connection which is also the [LMA](https://github.com/Intelligent-Silicon/PowerLine-Adapters/blob/main/SpecialStatusMACs.md#00b052000001). In the absence of a MAC ID, you may see ```local``` being used in the documention instead or nothing at all. 

The main reason for working like this is because the powerline adapter could go to sleep if the device eg TV, Printer, thats plugged into it goes into a deep sleep and stops transmitting network data and some power supplies kill power when the main device has been switched off to save power, but can be a nuisance when trying to access devices like a powerline adapter. Hacker's dont like the tech, it restricts their window of opportunity. 

The transmission of TCP/IP network data using the HomePlug1.0 or HomePlugAV(2) protocols wakes these powerline adapter wake up. If the powerline adapter is not in a network group because its NMK passphrase is different, you will find it hard to communication with the device, so plugging them directly in to the windows box is highly recommended.

Life is just much easier if its plugged directly into your windows box.


### Windows box network card

IF your windows box only has one Ethernet network card, no Bluetooth, no Wi-Fi, and not running any virtualisation software, like [MS Hyper-V](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/overview) (possibly for WSL2) or [VMware](https://www.vmware.com/) programs, then your Ethernet connection will almost certainly be interface number 1.

However to be sure, run the ```pcapsdev``` program to find out what Ethernet cards you have in your computer.

```
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\pcapdevs
 1 01:00:00:00:00:01 \Device\NPF_{A0C14E52-9811-4363-A3E4-6E8C3F1E353F} (Ethernet 1)
 2 00:50:56:C0:00:08 \Device\NPF_{A01B79E9-77ED-40C5-AA5A-A8249909CD6F} (VMware Virtual Ethernet Adapter)
 3 00:50:56:C0:00:01 \Device\NPF_{A3E64511-4B4E-4846-B8DB-ED87C1CE41FB} (VMware Virtual Ethernet Adapter)
 4 02:00:00:00:00:02 \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2} (Ethernet 2)
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

Here we can see there are two physical Ethernet cards and two virtual one's. If you are using Hyper-V it would appear in the list above.

For this repo, the Ethernet card in 4th place will be used.

The command line switch/flag used to identify the network card with Open PLC Util programs will always be ```-i[number]``` eg ```-i4```. If we were to use the Intel Ethernet card then the number would be 1 eg ```-i1```, in other situations like using Linux you might see ```-i Eth0```.

For more information see in your web browser: ```file:///C:/Users/[Your Username]/source/repos/open-plc-utils/docbook/ch05s03.html``` 

### Ethernet card IP Address

As you will be plugging the ethernet cable from the powerline adapter straight into the window's box, if you only have one ethernet connection which is normally connected to the router or you have a spare ethernet card as in this case which has not been assigned an IP address setting, you will need to set these manually for the open PLC utils programs to work properly and reset the windows ethernet card back to whatever it was after using the Open PLC Utils programs.

To get the name of the ethernet card, in MS Terminal or MS Powershell running with elevated permissions as Administrator, use this command:
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> ipconfig

Windows IP Configuration


Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : myLAN.name
   Link-local IPv6 Address . . . . . : fe80::7e56:65bf:bf79:648b%14
   IPv4 Address. . . . . . . . . . . : 192.168.100.47
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.100.1

Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::f365:d170:778c:a2ea%2
   Default Gateway . . . . . . . . . :

Ethernet adapter VMware Network Adapter VMnet1:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::1173:9112:ba8e:21b1%15
   IPv4 Address. . . . . . . . . . . : 192.168.40.1
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . :

Ethernet adapter VMware Network Adapter VMnet8:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::6a26:62b4:c93b:5054%13
   IPv4 Address. . . . . . . . . . . : 192.168.253.1
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . :
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>

```

Ethernet 2 is what corresponds to Interface 4 from the pcapsdev output and we will be using this network card in the windows box to plug an ethernet cable directly into the powerline adapters, which are plugged into an extension lead socket on the desk.

To set IP address settings, make sure Terminal or Powershell is running elevated as Administrator.

```
PS C:\WINDOWS\system32> netsh interface ip set address name="Ethernet 2" static 192.168.50.10 255.255.255.0 192.168.50.1 

```

```
PS C:\WINDOWS\system32> ipconfig

Windows IP Configuration


Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : myLAN.name
   Link-local IPv6 Address . . . . . : fe80::7e56:65bf:bf79:648b%14
   IPv4 Address. . . . . . . . . . . : 192.168.178.47
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.178.1

Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::f365:d170:778c:a2ea%2
   IPv4 Address. . . . . . . . . . . : 192.168.50.10
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.50.1

Ethernet adapter VMware Network Adapter VMnet1:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::1173:9112:ba8e:21b1%15
   IPv4 Address. . . . . . . . . . . : 192.168.40.1
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . :

Ethernet adapter VMware Network Adapter VMnet8:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::6a26:62b4:c93b:5054%13
   IPv4 Address. . . . . . . . . . . : 192.168.253.1
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . :
PS C:\WINDOWS\system32>
```

Note that Powershell is running as Administrator and we can tell this from the path that's displayed ```PS C:\WINDOWS\system32>```.

Thats it, the ethernet card is now setup with a fixed ip configuration ready to work with the powerline adapters.

To reset the ethernet card back to its previous settings after you have finished working on the powerline adapters, use the following if it obtained the IP address from the router using DHCP, if DHCP wasnt used, use the above fixed ip configuration method to set it back to what it was previously.

```
PS C:\WINDOWS\system32> netsh interface ip set address "Ethernet 2" dhcp

PS C:\WINDOWS\system32>
```

