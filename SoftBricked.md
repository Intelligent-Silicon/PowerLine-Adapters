# Soft Bricked Powerline Adapters

### Establish if a device is soft bricked.

We need to establish if each powerline adapter is soft bricked or not, so by having the powerline adapter plugged directly into the windows box and not having to use a MAC ID we can see what output it gives us. Even if the device is soft bricked it will still communicate. 


The command and switches to get the device status, attributes, revision and network membership.
```
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i[Number] -t[timeout milliseconds] -I[a = attributes, r = revision, m = network membership]
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Iarm
```

The Mac ID returned on the second line determines the powerline adapter status, as explained in [Special Status Ethernet MAC Addresses](SpecialStatusMACs.md)

Toolkit programs will generally always send a command to the local aka Local Management Address (LMA) address and the resulting output with a MAC ID tells you the status of the device. In this example the DAK is also showing the HomePlugAV MAC ID suggesting a default PIB was used when it should use the DAK from the powerline adapter. 

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Iarm
nic4 00:B0:52:00:00:01 Request Version Information
nic4 00:B0:52:00:00:03 QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
nic4 00:B0:52:00:00:01 Fetch Device Attributes
nic4 00:B0:52:00:00:03 QCA7420-MAC-QCA7420-1.2.0.1580-02-20150902-CS (1mb)
        PIB 0-0 8080 bytes
        MAC 00:B0:52:00:00:03
        DAK 68:9F:07:4B:8B:02:75:A2:71:0B:0B:57:79:AD:16:30 (HomePlugAV)
        NMK 50:D3:E4:93:3F:85:5B:70:40:78:4D:F8:15:AA:8D:B7 (HomePlugAV)
        NID B0:F2:E6:95:66:6B:03
        Security level 0
        NET Qualcomm Atheros Enabled Network
        MFG Qualcomm Atheros HomePlug AV Device
        USR Qualcomm Atheros Enabled Product
        CCo Never
        MDU N/A
nic4 00:B0:52:00:00:01 Fetch Network Information
nic4 00:B0:52:00:00:03 Found 0 Network(s)

source address = 00:B0:52:00:00:03

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

The PIB file should always match the version of the NVM firmware file, when it doesnt, the firmware flash will abort showing the below message, except when the Force Flash (-FF) switch/flag is used, then you get no error messages and the flash takes place causing you more work!

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm" -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib" -F
nic4 00:B0:52:00:00:01 Start Module Write Session
nic4 00:00:00:00:00:02 Can't Lock Flash Memory (0x23): Device refused request
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```


