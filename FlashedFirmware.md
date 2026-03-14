# Correct Powerline Adapter settings after Flashing

### Correct Hub Powerline Adapter settings
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Ir
nic4 00:B0:52:00:00:01 Request Version Information
nic4 00:00:00:00:00:AA QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
        PIB 0-0 8660 bytes
        MAC 00:00:00:00:00:AA
        DAK DB:F4:0B:77:21:02:DE:DA:70:E1:4D:58:D4:F5:C0:93
        NMK 0E:EA:12:28:14:16:1D:C9:97:AE:B1:F2:77:A3:9D:C1
        NID 5D:3A:2F:2B:7E:5C:11
        Security level 1
        NET [NET]
        MFG [MFG]
        USR [USR]
        CCo Auto
        MDU N/A
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Correct Powerline Adapter 2 settings
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Ir
nic4 00:B0:52:00:00:01 Request Version Information
nic4 00:00:00:00:00:02 QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
        PIB 0-0 8660 bytes
        MAC 00:00:00:00:00:02
        DAK 47:C4:A0:54:D9:05:01:7F:2F:DD:EF:AD:AF:CA:1B:A5
        NMK 0E:EA:12:28:14:16:1D:C9:97:AE:B1:F2:77:A3:9D:C1
        NID 5D:3A:2F:2B:7E:5C:11
        Security level 1
        NET [NET]
        MFG [MFG]
        USR [USR]
        CCo Auto
        MDU N/A
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Correct Powerline Adapter 3 settings
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Ir
nic4 00:B0:52:00:00:01 Request Version Information
nic4 00:00:00:00:00:03 QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
        PIB 0-0 8660 bytes
        MAC 00:00:00:00:00:03
        DAK C8:4F:4A:CA:99:B5:33:AD:8F:B3:B5:9D:0D:21:5C:A2
        NMK 0E:EA:12:28:14:16:1D:C9:97:AE:B1:F2:77:A3:9D:C1
        NID 5D:3A:2F:2B:7E:5C:11
        Security level 1
        NET [NET]
        MFG [MFG]
        USR [USR]
        CCo Auto
        MDU N/A
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Powerline Adapters in a Powerline Network Group

The ```-Im``` switch/flag shows all the devices plugged into the mains communicating with each other, albeit with reportedly very slow network speeds of just 9Mbps which is the idle speed!
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Im
        PIB 0-0 8660 bytes
        MAC 00:00:00:00:00:AA
        DAK DB:F4:0B:77:21:02:DE:DA:70:E1:4D:58:D4:F5:C0:93
        NMK 0E:EA:12:28:14:16:1D:C9:97:AE:B1:F2:77:A3:9D:C1
        NID 5D:3A:2F:2B:7E:5C:11
        Security level 1
        NET [NET]
        MFG [MFG]
        USR [USR]
        CCo Auto
        MDU N/A
nic4 00:B0:52:00:00:01 Fetch Network Information
nic4 00:00:00:00:00:AA Found 1 Network(s)

source address = 00:00:00:00:00:AA

        network->NID = 5D:3A:2F:2B:7E:5C:11
        network->SNID = 5
        network->TEI = 1
        network->ROLE = 0x02 (CCO)
        network->CCO_DA = 00:00:00:00:00:AA
        network->CCO_TEI = 1
        network->STATIONS = 2

                station->MAC = 00:00:00:00:00:02
                station->TEI = 2
                station->BDA = FF:FF:FF:FF:FF:FF
                station->AvgPHYDR_TX = 009 mbps Primary
                station->AvgPHYDR_RX = 009 mbps Primary

                station->MAC = 00:00:00:00:00:03
                station->TEI = 3
                station->BDA = FF:FF:FF:FF:FF:FF
                station->AvgPHYDR_TX = 009 mbps Primary
                station->AvgPHYDR_RX = 009 mbps Primary

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

Here you can see the speed increase with one adapter thats in use, and the other adapter is just idling.
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Im
        PIB 0-0 8660 bytes
        MAC 00:00:00:00:00:02
        DAK 47:C4:A0:54:D9:05:01:7F:2F:DD:EF:AD:AF:CA:1B:A5
        NMK 0E:EA:12:28:14:16:1D:C9:97:AE:B1:F2:77:A3:9D:C1
        NID 5D:3A:2F:2B:7E:5C:11
        Security level 1
        NET [NET]
        MFG [MFG]
        USR [USR]
        CCo Auto
        MDU N/A
nic1 00:B0:52:00:00:01 Fetch Network Information
nic1 00:00:00:00:00:02 Found 1 Network(s)

source address = 00:00:00:00:00:02

        network->NID = 5D:3A:2F:2B:7E:5C:11
        network->SNID = 11
        network->TEI = 1
        network->ROLE = 0x02 (CCO)
        network->CCO_DA = 00:00:00:00:00:02
        network->CCO_TEI = 1
        network->STATIONS = 2

                station->MAC = 00:00:00:00:00:AA
                station->TEI = 2
                station->BDA = 2C:91:AB:54:2E:2B
                station->AvgPHYDR_TX = 113 mbps Primary
                station->AvgPHYDR_RX = 086 mbps Primary

                station->MAC = 00:00:00:00:00:03
                station->TEI = 3
                station->BDA = FF:FF:FF:FF:FF:FF
                station->AvgPHYDR_TX = 009 mbps Primary
                station->AvgPHYDR_RX = 009 mbps Primary

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```