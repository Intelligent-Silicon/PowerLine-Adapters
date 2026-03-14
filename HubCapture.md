# HUB Packet Analysis

In this configuration, the Windows 11 (25H2) Pro box has three Network Interface Cards (NIC)'s, two plugged into a TPL-406E powerline adapter (PA2 & PA3), and one plugged directly into the Fritz box router. The 3rd Powerline adapter (Hub) is plugged into a network cable thats plugged into an AVM Fritz!Box router. The Fritz!box router works like an unmanaged switch so packets are directed to the correct port and are not broadcasted to all ports except the broadcast specific packets.

Wireshark is capturing all three NIC's with Promiscuous mode enabled using the Capture Filter created to capture the HomePlug 1.0 and HomePlugAV protocols. Ignoring the HomePlugAV packets sent from the Fritz Box because AVM supply their own powerline adapters which work with their router to make a [mesh network](https://en.wikipedia.org/wiki/Mesh_networking).



These are commands which will be sent to the powerline adapters, with WireShark capturing the communication on all three NIC's. Only the first plctool command will be analysed.
```
.\pcapdevs
.\plctool -i7 -t500 -Iarm 00:00:00:00:00:AA
.\plctool -i8 -t500 -Iarm 00:00:00:00:00:AA
.\plctool -i7 -t500 -Iarm 00:00:00:00:00:02
.\plctool -i8 -t500 -Iarm 00:00:00:00:00:02
.\plctool -i7 -t500 -Iarm 00:00:00:00:00:03
.\plctool -i8 -t500 -Iarm 00:00:00:00:00:03
```


### pcapdevs

The powershell output showing the order of the network interface cards in the window box. This info is needed before we can use plctool to direct commands to the powerline adapters 2 and 3.

[.\pcapdevs Output](pcapsdev-output.md)



## Powershell Command .\plctool -i7 -t500 -Iarm 00:00:00:00:00:AA & Output 

The powershell output and Wireshark packet captures showing the data from the Hub powerline adapter.

[plctool -i7 hub powershell output](plctool-i7powershellhuboutput.md)

[plctool -i7 hub wireshark raw packet capture](plctool-i7hubwiresharkrawpacketcapture.md)

[plctool -i7 hub wireshark packet capture overlay](plctool-i7hubwiresharkpacketcaptureoverlay.md)




### Analysis

```
.\plctool -i7 -t500 -Iarm 00:00:00:00:00:AA
```

This command sends a series of packets from the Windows box Ethernet 2 NIC (-i7) to Powerline Adapter 3 thats directly plugged into it. 

PA3 processes the command and forwards it on the HUB powerline adapter.

The HUB powerline adapter is plugged into the router, so has no direct ethernet cable connection with the Window box. Because of this, the resulting HUB DAK is shown as ```DAK 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00 (none/secret)``` because the HUB powerline adapter firmware treats a request originating from another powerline adapter as remote and will not give away the DAK, so its classed as Secret and not None.

The command is asking the Hub powerline adapter ```00:00:00:00:00:AA``` for the following information ```a``` which is powerline adapter attributes, ```r``` which is software revision and ```m``` which is the network membership topology.

plctool will process the ```arm``` switches/flags in the order ```r```, then ```a``` and then ```m```.

Wireshark is listening on all 3 nics in order to capture any duplicate packets. As it happens no duplicated packets are captured suggesting tw things. First the Fritz!box is operating like an unmanaged switch directing each packet to the corresponding port and the powerline adapters are also processing and routing packets accordingly.

In practice, the data received by a powerline adapter needs to be broadcast across the mains electricity cable. The data is encrypted, something only the powerline adapters in the same NMK group can decrypt, and possibly encrypted so it can only be decrypted by the powerline adapter the data is intended for. At this stage its impossible to verify exactly how the data is transmitted, the former is possible, but the latter is best.


Below is a summary of the packets transmitted and received to get the data thats shown in the [powershell output](plctool-i7powershellhuboutput.md).

| No. | Time | Source | Destination | Protocol | Length | Info |
|-----|------|--------|-------------|----------|--------|------|
| 1 | 0.000000000 | Ethernet2_00:00:02 | 00:00:00_00:00:aa |	HomePlug AV	| 60 | Qualcomm Atheros, GET_SW.REQ (Get Device/SW Version Request) |
| 2	| 0.002589700 | 00:00:00_00:00:aa | Ethernet2_00:00:02 | HomePlug AV	| 297 | Qualcomm Atheros, GET_SW.CNF (Get Device/SW Version Confirmation) |
| 3	| 0.617425400 | Ethernet2_00:00:02 | 00:00:00_00:00:aa | HomePlug AV	| 60 | Qualcomm Atheros, OP_ATTR.REQ (Get Device Attributes Request) |
| 4	| 0.622216000 | 00:00:00_00:00:aa | Ethernet2_00:00:02 | HomePlug AV	| 1053 | Qualcomm Atheros, OP_ATTR.CNF (Get Device Attributes Confirmation) |
| 5	| 1.243149100 | Ethernet2_00:00:02 | 00:00:00_00:00:aa | HomePlug AV	| 60 | Qualcomm Atheros, Unknown 0xa0b0 |
| 6	| 1.248530600 | 00:00:00_00:00:aa | Ethernet2_00:00:02 | HomePlug AV	| 1447 | Qualcomm Atheros, Unknown 0xa0b1 |
| 7	| 1.252603300 | Ethernet2_00:00:02 | 00:00:00_00:00:aa | HomePlug AV	| 60 | Qualcomm Atheros, NW_INFO.REQ (Network Info Request) |
| 8	| 1.255674600 | 00:00:00_00:00:aa | Ethernet2_00:00:02 | HomePlug AV	| 108 | Qualcomm Atheros, NW_INFO.CNF (Network Info Confirmation) |



### Packet 1 

This packet sent from the windows box Ethernet 2 to PA3 requests the HUB powerline adapter ```00:00:00:00:00:AA``` to send back its current firmware version aka revision.
 
Powershell Output
```
Line 1: nic7 00:00:00:00:00:AA Request Version Information
```

[The Packet data sent to the Hub powerline adapter.](plctool-i7hubwiresharkrawpacketcapture.md#packet-1)

[The Wireshark overlay for Packet 1](plctool-i7hubwiresharkpacketcaptureoverlay.md#packet-1)

In the Wireshark overlay, in the HomePlug AV Protocol section, the TYPE is visible with ```GET_SW.REQ (Get Device/SW Version Request) (0xa000)```


### Packet 2

This is the packet of data sent from the HUB powerline adapter back to the windows box. 

Powershell Output
```
Line 2: nic7 00:00:00:00:00:AA QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
```

[The Packet data sent from the Hub powerline adapter.](plctool-i7hubwiresharkrawpacketcapture.md#packet-2)

[The Wireshark overlay for Packet 2](plctool-i7hubwiresharkpacketcaptureoverlay.md#packet-2)

In the packet data, the version is clearly seen, and its interpreted by wireshark when looking at the overlay and plctool in the powershell output.

### Packet 3

This packet sent from the windows box Ethernet 2 to PA3 requests the HUB powerline adapter 00:00:00:00:00:AA to send back its current hardware configuration aka attributes.

Powershell Output
```
nic7 00:00:00:00:00:AA Fetch Device Attributes
```

[The Packet data sent from the Hub powerline adapter.](plctool-i7hubwiresharkrawpacketcapture.md#packet-3)

[The Wireshark overlay for Packet 3](plctool-i7hubwiresharkpacketcaptureoverlay.md#packet-3)

In the Wireshark overlay, in the HomePlug AV Protocol section, the TYPE is visible with ```Type: 4 bytes: 68 a0 - Type: OP_ATTR.REQ (Get Device Attributes Request) (0xa068)```

### Packet 4

This is the packet of data sent from the HUB powerline adapter back to the windows box. 

Powershell Output
```
Line 4:	nic7 00:00:00:00:00:AA QCA7420-MAC-QCA7420-1.2.0.1580-02-20150902-CS (1mb)
```

[The Packet data sent from the Hub powerline adapter.](plctool-i7hubwiresharkrawpacketcapture.md#packet-4)

[The Wireshark overlay for Packet 4](plctool-i7hubwiresharkpacketcaptureoverlay.md#packet-4)

The packet of data is largely empty, containing the version number again. This may be the result of some of the firmware updates, whilst older applets still exist.

Wireshark shows some information which is not going to appear using plctool, but will appear if using the command amptool.
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\amptool -i6 -Iar 00:00:00:00:00:aa
nic7 00:00:00:00:00:AA Request Version Information
nic7 00:00:00:00:00:AA QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
nic7 00:00:00:00:00:AA Fetch Device Attributes
nic7 00:00:00:00:00:AA QCA7420-MAC-1-2-0000-02-1580-20150902-CS-X (1mb) (0xF5) "50Hz" "Detected"  0x89
nic7 00:00:00:00:00:AA Device Identity
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

Here you can see there is ```(0xF5) "50Hz" "Detected"  0x89``` which can be seen in the packet data and wireshark overlay. This relates to the electricity frequency (50Hz) seen in the UK. Other countries use 60Hz. As its showing "Detected", and knowing the Trendnet download website has different firmware versions for different countries, do the non World Wide firmware versions suggest the mains electricity supply is being used for data transfer or signalling at the municipal or neighbourhood level, perhaps to control streets lights or for other purposes like billing?  Later versions of the firmware dont have seperate regional versions, indicating the firmware is capable of working with the regional requirements automatically. It also shows when looking at the date the firmware is available, that updating firmware is not a quick process. Lets hope it doesnt have any bugs then!

### Packet 5

This packet sent from the windows box Ethernet 2 to PA3 requests the HUB powerline adapter 00:00:00:00:00:AA to send back its current hardware configuration aka attributes.

There is no corresponding Powershell Output for this packet, but its almost certainly the second stage of getting the powerline adapters configuration which was started in packets 3 and 4. 

[The Packet data sent from the Hub powerline adapter.](plctool-i7hubwiresharkrawpacketcapture.md#packet-5)

[The Wireshark overlay for Packet 5](plctool-i7hubwiresharkpacketcaptureoverlay.md#packet-5)

Now this is where Wireshark doesnt recognise the HomePlug AV TYPE, like it does in earlier packets. Its probably because its not been updated to handle the changes in the firmware using the HomePlug AV protocol. 

### Packet 6 

This is the packet of data sent from the HUB powerline adapter back to the windows box.

Powershell Output
```
        PIB 0-0 8660 bytes
        MAC 00:00:00:00:00:AA
        DAK 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00 (none/secret)
        NMK 0E:EA:12:28:14:16:1D:C9:97:AE:B1:F2:77:A3:9D:C1
        NID 5D:3A:2F:2B:7E:5C:11
        Security level 1
        NET [NET]
        MFG [MFG]
        USR [USR]
        CCo Auto
        MDU N/A
```

[The Packet data sent from the Hub powerline adapter.](plctool-i7hubwiresharkrawpacketcapture.md#packet-6)

[The Wireshark overlay for Packet 6](plctool-i7hubwiresharkpacketcaptureoverlay.md#packet-6)

The Wireshark overlay doesnt recognise the data sent back in response to the TYPE request seen in packet 5, but the layout of the packet is very similar to what is seen in the PIB file when the PIB file is viewed in the HEX editor. 

### Packet 7

This packet sent from the windows box Ethernet 2 to PA3 requests the HUB powerline adapter 00:00:00:00:00:AA to send back its current hardware configuration aka attributes.

Powershell Output.
```
Line 5: nic7 00:00:00:00:00:AA Fetch Network Information
```

[The Packet data sent to the Hub powerline adapter.](plctool-i7hubwiresharkrawpacketcapture.md#packet-7)

[The Wireshark overlay for Packet 7](plctool-i7hubwiresharkpacketcaptureoverlay.md#packet-7)

In this packet Wireshark recognises the TYPE as seen with the ```Type: NW_INFO.REQ (Network Info Request) (0xa038)```, so the next packet should be recognised by Wireshark.

Note also the MAC Management Header has also changed to ```.... ...1 = Version: 1.1 (1)``` from ```.... ...0 = Version: 1.0 (0)``` seen in earlier packets.
Secret information can be conveyed in plain sight for all to see and watch, if only those in on it knows its true meaning.

### Packet 8

This is the packet of data sent from the HUB powerline adapter back to the windows box.

Powershell Output
```
Line 6: nic7 00:00:00:00:00:AA Found 1 Network(s)

		source address = 00:00:00:00:00:AA

			network->NID = 5D:3A:2F:2B:7E:5C:11
			network->SNID = 14
			network->TEI = 7
			network->ROLE = 0x02 (CCO)
			network->CCO_DA = 00:00:00:00:00:AA
			network->CCO_TEI = 7
			network->STATIONS = 2

					station->MAC = 00:00:00:00:00:03
					station->TEI = 5
					station->BDA = 84:16:F9:02:D4:8C
					station->AvgPHYDR_TX = 084 mbps Primary
					station->AvgPHYDR_RX = 103 mbps Primary

					station->MAC = 00:00:00:00:00:02
					station->TEI = 9
					station->BDA = A4:BB:6D:D1:0F:93
					station->AvgPHYDR_TX = 128 mbps Primary
					station->AvgPHYDR_RX = 120 mbps Primary
```

[The Packet data sent from the Hub powerline adapter.](plctool-i7hubwiresharkrawpacketcapture.md#packet-8)

[The Wireshark overlay for Packet 8](plctool-i7hubwiresharkpacketcaptureoverlay.md#packet-8)

This packet is fairly straight forward with much of the information displayed in the powershell output, contained in a serial format within the packet data.


### Summary

There is still no NMK found in plain sight in any of the packets, so it may be hidden in plain sight with individual bytes spread across the packet data. Examining the program code will give up that secret.

But thats all there is to capturing ethernet packet data and examining its contents. 

Anyone who can read the program code found in the github repo will be able to see the code for plctool, and see what each byte of packet data means, but for those who dont program, Wireshark is a quick handy tool to get an overview of the packets of data being sent between a powerline adapter the plctool.

Those who know that ethernet cables only have a maximum cable length of 100 metres and wonder why powerline adaptors have a range of 300 metres, thats because of the different types of electricity used (voltage and current) and the frequencies, like a radio frequency, thats sent down the wire. This is why powerline adapters can interfere with telephone cables and unshielded ethernet cables. 


