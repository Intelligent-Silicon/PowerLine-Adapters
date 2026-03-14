# plctool -i7 hub wireshark packet capture overlay


### Packet 1

```
Frame 5: Packet, 60 bytes on wire (480 bits), 60 bytes captured (480 bits) on interface \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}, id 1
    Section number: 1
    Interface id: 1 (\Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2})
        Interface name: \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}
        Interface description: Ethernet 2
    Encapsulation type: Ethernet (1)
    Arrival Time: Mar 11, 2026 23:26:16.952229800 GMT Standard Time
    UTC Arrival Time: Mar 11, 2026 23:26:16.952229800 UTC
    Epoch Arrival Time: 1773271576.952229800
    [Time shift for this packet: 0.000000000 seconds]
    [Time delta from previous captured frame: 681.170300 milliseconds]
    [Time since reference or first frame: 2.681372800 seconds]
    Frame Number: 5
    Frame Length: 60 bytes (480 bits)
    Capture Length: 60 bytes (480 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: eth:ethertype:homeplug-av]
    Character encoding: ASCII (0)
Ethernet II, Src: Ethernet2_00:00:02 (02:00:00:00:00:02), Dst: 00:00:00_00:00:aa (00:00:00:00:00:aa)
    Destination: 00:00:00_00:00:aa (00:00:00:00:00:aa)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: Ethernet2_00:00:02 (02:00:00:00:00:02)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: Homeplug AV (0x88e1)
    [Stream index: 2]
HomePlug AV protocol
    MAC Management Header
        .... ...0 = Version: 1.0 (0)
        Type: GET_SW.REQ (Get Device/SW Version Request) (0xa000)
            .... ..00 = LSB: Request (0x0)
            101. .... = MSB: Vendor Specific (0x5)
    Vendor MME
        OUI: Qualcomm Atheros (0x00b052)
```


### Packet 2

```
Frame 6: Packet, 297 bytes on wire (2376 bits), 297 bytes captured (2376 bits) on interface \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}, id 1
    Section number: 1
    Interface id: 1 (\Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2})
        Interface name: \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}
        Interface description: Ethernet 2
    Encapsulation type: Ethernet (1)
    Arrival Time: Mar 11, 2026 23:26:16.954866100 GMT Standard Time
    UTC Arrival Time: Mar 11, 2026 23:26:16.954866100 UTC
    Epoch Arrival Time: 1773271576.954866100
    [Time shift for this packet: 0.000000000 seconds]
    [Time delta from previous captured frame: 2.636300 milliseconds]
    [Time delta from previous displayed frame: 2.636300 milliseconds]
    [Time since reference or first frame: 2.684009100 seconds]
    Frame Number: 6
    Frame Length: 297 bytes (2376 bits)
    Capture Length: 297 bytes (2376 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: eth:ethertype:homeplug-av]
    Character encoding: ASCII (0)
Ethernet II, Src: 00:00:00_00:00:aa (00:00:00:00:00:aa), Dst: Ethernet2_00:00:02 (02:00:00:00:00:02)
    Destination: Ethernet2_00:00:02 (02:00:00:00:00:02)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: 00:00:00_00:00:aa (00:00:00:00:00:aa)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: Homeplug AV (0x88e1)
    [Stream index: 2]
HomePlug AV protocol
    MAC Management Header
        .... ...0 = Version: 1.0 (0)
        Type: GET_SW.CNF (Get Device/SW Version Confirmation) (0xa001)
            .... ..01 = LSB: Confirm (0x1)
            101. .... = MSB: Vendor Specific (0x5)
    Vendor MME
        OUI: Qualcomm Atheros (0x00b052)
    Get Device/SW Version
        Status: 0
        Device ID: QCA7450/QCA7420 (0x20)
        Version length: 38
        Version: MAC-QCA7420-1.2.0.1580-02-20150902-CS
            [Expert Info (Warning/Undecoded): Trailing stray characters]
                [Trailing stray characters]
                [Severity level: Warning]
                [Group: Undecoded]
        Upgradable: False
```

### Packet 3

```
Frame 7: Packet, 60 bytes on wire (480 bits), 60 bytes captured (480 bits) on interface \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}, id 1
    Section number: 1
    Interface id: 1 (\Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2})
        Interface name: \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}
        Interface description: Ethernet 2
    Encapsulation type: Ethernet (1)
    Arrival Time: Mar 11, 2026 23:26:17.589893600 GMT Standard Time
    UTC Arrival Time: Mar 11, 2026 23:26:17.589893600 UTC
    Epoch Arrival Time: 1773271577.589893600
    [Time shift for this packet: 0.000000000 seconds]
    [Time delta from previous captured frame: 635.027500 milliseconds]
    [Time delta from previous displayed frame: 635.027500 milliseconds]
    [Time since reference or first frame: 3.319036600 seconds]
    Frame Number: 7
    Frame Length: 60 bytes (480 bits)
    Capture Length: 60 bytes (480 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: eth:ethertype:homeplug-av]
    Character encoding: ASCII (0)
Ethernet II, Src: Ethernet2_00:00:02 (02:00:00:00:00:02), Dst: 00:00:00_00:00:aa (00:00:00:00:00:aa)
    Destination: 00:00:00_00:00:aa (00:00:00:00:00:aa)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: Ethernet2_00:00:02 (02:00:00:00:00:02)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: Homeplug AV (0x88e1)
    [Stream index: 2]
HomePlug AV protocol
    MAC Management Header
        .... ...0 = Version: 1.0 (0)
        Type: OP_ATTR.REQ (Get Device Attributes Request) (0xa068)
            .... ..00 = LSB: Request (0x0)
            101. .... = MSB: Vendor Specific (0x5)
    Vendor MME
        OUI: Qualcomm Atheros (0x00b052)
    Get Device Attributes Request
        Cookie: 2018915346
        Report Type: Binary (0x00)
```

### Packet 4

```
Frame 8: Packet, 1053 bytes on wire (8424 bits), 1053 bytes captured (8424 bits) on interface \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}, id 1
    Section number: 1
    Interface id: 1 (\Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2})
        Interface name: \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}
        Interface description: Ethernet 2
    Encapsulation type: Ethernet (1)
    Arrival Time: Mar 11, 2026 23:26:17.594029000 GMT Standard Time
    UTC Arrival Time: Mar 11, 2026 23:26:17.594029000 UTC
    Epoch Arrival Time: 1773271577.594029000
    [Time shift for this packet: 0.000000000 seconds]
    [Time delta from previous captured frame: 4.135400 milliseconds]
    [Time delta from previous displayed frame: 4.135400 milliseconds]
    [Time since reference or first frame: 3.323172000 seconds]
    Frame Number: 8
    Frame Length: 1053 bytes (8424 bits)
    Capture Length: 1053 bytes (8424 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: eth:ethertype:homeplug-av]
    Character encoding: ASCII (0)
Ethernet II, Src: 00:00:00_00:00:aa (00:00:00:00:00:aa), Dst: Ethernet2_00:00:02 (02:00:00:00:00:02)
    Destination: Ethernet2_00:00:02 (02:00:00:00:00:02)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: 00:00:00_00:00:aa (00:00:00:00:00:aa)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: Homeplug AV (0x88e1)
    [Stream index: 2]
HomePlug AV protocol
    MAC Management Header
        .... ...0 = Version: 1.0 (0)
        Type: OP_ATTR.CNF (Get Device Attributes Confirmation) (0xa069)
            .... ..01 = LSB: Confirm (0x1)
            101. .... = MSB: Vendor Specific (0x5)
    Vendor MME
        OUI: Qualcomm Atheros (0x00b052)
    Get Device Attributes Confirmation
        .... .... .... ..00 = Status: Success (0x0)
        Cookie: 2018915346
        Report Type: Binary (0x00)
        Size: 118
        Data
            Hardware platform: QCA7420
            Software platform: MAC
            Major version: 1
            Minor version: 2
            Software/PIB version: 0
            Software build number: 2
            Reserved
            Build date: 20150902
            Release type: CS
            SDRAM type: 88
            Reserved
            .... ..01 = Line frequency (Hz): 50Hz (1)
            .... 01.. = Zero-crossing: Detected (1)
            SDRAM size (Mbytes): 1
            Authorization mode: 137
```

### Packet 5

```
Frame 10: Packet, 60 bytes on wire (480 bits), 60 bytes captured (480 bits) on interface \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}, id 1
    Section number: 1
    Interface id: 1 (\Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2})
        Interface name: \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}
        Interface description: Ethernet 2
    Encapsulation type: Ethernet (1)
    Arrival Time: Mar 11, 2026 23:26:18.206483200 GMT Standard Time
    UTC Arrival Time: Mar 11, 2026 23:26:18.206483200 UTC
    Epoch Arrival Time: 1773271578.206483200
    [Time shift for this packet: 0.000000000 seconds]
    [Time delta from previous captured frame: -64.876700 milliseconds]
    [Time delta from previous displayed frame: 612.454200 milliseconds]
    [Time since reference or first frame: 3.935626200 seconds]
    Frame Number: 10
    Frame Length: 60 bytes (480 bits)
    Capture Length: 60 bytes (480 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: eth:ethertype:homeplug-av]
    Character encoding: ASCII (0)
Ethernet II, Src: Ethernet2_00:00:02 (02:00:00:00:00:02), Dst: 00:00:00_00:00:aa (00:00:00:00:00:aa)
    Destination: 00:00:00_00:00:aa (00:00:00:00:00:aa)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: Ethernet2_00:00:02 (02:00:00:00:00:02)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: Homeplug AV (0x88e1)
    [Stream index: 2]
HomePlug AV protocol
    MAC Management Header
        .... ...0 = Version: 1.0 (0)
        Type: Unknown (0xa0b0)
            .... ..00 = LSB: Request (0x0)
            101. .... = MSB: Vendor Specific (0x5)
    Vendor MME
        OUI: Qualcomm Atheros (0x00b052)
```

### Packet 6

```
Frame 12: Packet, 1447 bytes on wire (11576 bits), 1447 bytes captured (11576 bits) on interface \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}, id 1
    Section number: 1
    Interface id: 1 (\Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2})
        Interface name: \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}
        Interface description: Ethernet 2
    Encapsulation type: Ethernet (1)
    Arrival Time: Mar 11, 2026 23:26:18.210747600 GMT Standard Time
    UTC Arrival Time: Mar 11, 2026 23:26:18.210747600 UTC
    Epoch Arrival Time: 1773271578.210747600
    [Time shift for this packet: 0.000000000 seconds]
    [Time delta from previous captured frame: -60.644900 milliseconds]
    [Time delta from previous displayed frame: 4.264400 milliseconds]
    [Time since reference or first frame: 3.939890600 seconds]
    Frame Number: 12
    Frame Length: 1447 bytes (11576 bits)
    Capture Length: 1447 bytes (11576 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: eth:ethertype:homeplug-av]
    Character encoding: ASCII (0)
Ethernet II, Src: 00:00:00_00:00:aa (00:00:00:00:00:aa), Dst: Ethernet2_00:00:02 (02:00:00:00:00:02)
    Destination: Ethernet2_00:00:02 (02:00:00:00:00:02)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: 00:00:00_00:00:aa (00:00:00:00:00:aa)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: Homeplug AV (0x88e1)
    [Stream index: 2]
HomePlug AV protocol
    MAC Management Header
        .... ...0 = Version: 1.0 (0)
        Type: Unknown (0xa0b1)
            .... ..01 = LSB: Confirm (0x1)
            101. .... = MSB: Vendor Specific (0x5)
    Vendor MME
        OUI: Qualcomm Atheros (0x00b052)
```

### Packet 7

```
Frame 13: Packet, 60 bytes on wire (480 bits), 60 bytes captured (480 bits) on interface \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}, id 1
    Section number: 1
    Interface id: 1 (\Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2})
        Interface name: \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}
        Interface description: Ethernet 2
    Encapsulation type: Ethernet (1)
    Arrival Time: Mar 11, 2026 23:26:18.217162300 GMT Standard Time
    UTC Arrival Time: Mar 11, 2026 23:26:18.217162300 UTC
    Epoch Arrival Time: 1773271578.217162300
    [Time shift for this packet: 0.000000000 seconds]
    [Time delta from previous captured frame: 6.414700 milliseconds]
    [Time delta from previous displayed frame: 6.414700 milliseconds]
    [Time since reference or first frame: 3.946305300 seconds]
    Frame Number: 13
    Frame Length: 60 bytes (480 bits)
    Capture Length: 60 bytes (480 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: eth:ethertype:homeplug-av]
    Character encoding: ASCII (0)
Ethernet II, Src: Ethernet2_00:00:02 (02:00:00:00:00:02), Dst: 00:00:00_00:00:aa (00:00:00:00:00:aa)
    Destination: 00:00:00_00:00:aa (00:00:00:00:00:aa)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: Ethernet2_00:00:02 (02:00:00:00:00:02)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: Homeplug AV (0x88e1)
    [Stream index: 2]
HomePlug AV protocol
    MAC Management Header
        .... ...1 = Version: 1.1 (1)
        Type: NW_INFO.REQ (Network Info Request) (0xa038)
            .... ..00 = LSB: Request (0x0)
            101. .... = MSB: Vendor Specific (0x5)
        Fragmentation Info: 0x0000
            0000 .... = Fragment count: 0
            .... 0000 = Fragment index: 0
            Fragment Sequence number: 0
    Vendor MME
        OUI: Qualcomm Atheros (0x00b052)
```

### Packet 8

```
Frame 14: Packet, 108 bytes on wire (864 bits), 108 bytes captured (864 bits) on interface \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}, id 1
    Section number: 1
    Interface id: 1 (\Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2})
        Interface name: \Device\NPF_{0156D633-7701-466B-AEC4-039E8870D1F2}
        Interface description: Ethernet 2
    Encapsulation type: Ethernet (1)
    Arrival Time: Mar 11, 2026 23:26:18.219828700 GMT Standard Time
    UTC Arrival Time: Mar 11, 2026 23:26:18.219828700 UTC
    Epoch Arrival Time: 1773271578.219828700
    [Time shift for this packet: 0.000000000 seconds]
    [Time delta from previous captured frame: 2.666400 milliseconds]
    [Time delta from previous displayed frame: 2.666400 milliseconds]
    [Time since reference or first frame: 3.948971700 seconds]
    Frame Number: 14
    Frame Length: 108 bytes (864 bits)
    Capture Length: 108 bytes (864 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: eth:ethertype:homeplug-av]
    Character encoding: ASCII (0)
Ethernet II, Src: 00:00:00_00:00:aa (00:00:00:00:00:aa), Dst: Ethernet2_00:00:02 (02:00:00:00:00:02)
    Destination: Ethernet2_00:00:02 (02:00:00:00:00:02)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: 00:00:00_00:00:aa (00:00:00:00:00:aa)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: Homeplug AV (0x88e1)
    [Stream index: 2]
HomePlug AV protocol
    MAC Management Header
        .... ...1 = Version: 1.1 (1)
        Type: NW_INFO.CNF (Network Info Confirmation) (0xa039)
            .... ..01 = LSB: Confirm (0x1)
            101. .... = MSB: Vendor Specific (0x5)
        Fragmentation Info: 0x0000
            0000 .... = Fragment count: 0
            .... 0000 = Fragment index: 0
            Fragment Sequence number: 0
    Vendor MME
        OUI: Qualcomm Atheros (0x00b052)
    Network Info Confirmation
        Reserved
        Number of AV Logical Networks: 1
        Networks informations
            Network ID: 5d3a2f2b7e5c11
            Reserved
            Short Network ID: 0x0e
            Terminal Equipment Identifier: 7
            Reserved
            .... ..10 = Station Role: Central coordinator (0x2)
            CCo MAC Address: 00:00:00_00:00:aa (00:00:00:00:00:aa)
            CCo Terminal Equipment Identifier: 7
            Reserved
        Number of AV Stations: 2
        Reserved
        Stations Informations
            Station MAC Address: 00:00:00_00:00:03 (00:00:00:00:00:03)
            Station Terminal Equipment Identifier: 5
            Reserved
            MAC Address of first Node Bridged by Station: Ethernet2_00:00:02 (02:00:00:00:00:02)
            Average PHY Tx data Rate (Mbits/sec): 84
            .... 0000 = PHY Tx Coupling: Primary (0)
            0000 .... = PHY Rx Coupling: Primary (0)
            Reserved
            Average PHY Rx data Rate (Mbits/sec): 103
            Reserved
        Stations Informations
            Station MAC Address: 00:00:00_00:00:02 (00:00:00:00:00:02)
            Station Terminal Equipment Identifier: 9
            Reserved
            MAC Address of first Node Bridged by Station: Dell_01:01:01 (a4:bb:6d:01:01:01)
            Average PHY Tx data Rate (Mbits/sec): 128
            .... 0000 = PHY Tx Coupling: Primary (0)
            0000 .... = PHY Rx Coupling: Primary (0)
            Reserved
            Average PHY Rx data Rate (Mbits/sec): 120
            Reserved
```
