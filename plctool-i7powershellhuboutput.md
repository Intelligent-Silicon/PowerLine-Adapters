# plctool -i7 hub output


```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i7 -t500 -Iarm 00:00:00:00:00:AA
nic7 00:00:00:00:00:AA Request Version Information
nic7 00:00:00:00:00:AA QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
nic7 00:00:00:00:00:AA Fetch Device Attributes
nic7 00:00:00:00:00:AA QCA7420-MAC-QCA7420-1.2.0.1580-02-20150902-CS (1mb)
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
nic7 00:00:00:00:00:AA Fetch Network Information
nic7 00:00:00:00:00:AA Found 1 Network(s)

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

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```