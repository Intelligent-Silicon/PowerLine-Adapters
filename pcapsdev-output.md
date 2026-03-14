# pcapsdev

The powershell output showing the order of the network interface cards in the window box. 

This info is needed before we can use plctool to direct commands to the powerline adapters 2 and 3.

Interface 4 (Ethernet 3) is plugged into the Fritz!box router

Interface 7 (Ethernet 2) is plugged into Powerline Adapter 3

Interface 8 (Ethernet 1) is plugged into Powerline Adapter 2

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\pcapdevs
 1 01:00:00:00:4E:F9 \Device\NPF_{9F7F9DE8-C99D-47D0-AB66-EC41A50DB12E} (WAN Miniport (Network Monitor))
 2 01:00:00:00:4E:F9 \Device\NPF_{45802C87-F407-4C83-A031-A781B1399BC1} (WAN Miniport (IPv6))
 3 01:00:00:00:4E:F9 \Device\NPF_{49449FE2-7602-46FD-A967-F537717BB69B} (WAN Miniport (IP))
 4 03:00:00:00:00:03 \Device\NPF_{FCD238FE-BD4A-415B-A66D-B1807428B915} (Ethernet 3)
 5 00:50:56:C0:00:08 \Device\NPF_{A01B79E9-77ED-40C5-AA5A-A8249909CD6F} (VMware Virtual Ethernet Adapter for VMnet8)
 6 00:50:56:C0:00:01 \Device\NPF_{A3E64511-4B4E-4846-B8DB-ED87C1CE41FB} (VMware Virtual Ethernet Adapter for VMnet1)
 7 02:00:00:00:00:02 \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2} (Ethernet 2)
 8 01:00:00:00:00:01 \Device\NPF_{A0C14E52-9811-4363-A3E4-6E8C3F1E353F} (Ethernet 1)
 9 00:00:00:00:00:00 \Device\NPF_Loopback       (Adapter for loopback traffic capture)
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

Back to HUB [Packet Analysis](HubCapture.md)