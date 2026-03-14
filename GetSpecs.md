# Getting your Adapter specs

If you can communicate with the powerline adapter plugged directly into your Windows box, these are the commands to get their specs.

This is a useful step to ensure you can communicate directly with the powerline adapter from your Windows box.

### Getting the Powerline Adapter Specifications

Using the command below, swapping over each powerline adapter one by one we should see the information below.

```
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i[Number] -t[timeout milliseconds] -I[Device Identity with options, a displays the device attributes, r displays the firmware revision, m displays the network Membership]
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Iarm 
```

The Powerline adapters hardware specs for Firmware version 1.0.0.351-06-20120608.
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Iarm 
nic4 00:B0:52:00:00:03 Request Version Information
nic4 00:00:00:00:00:02 QCA7420 MAC-QCA7420-1.0.0.351-06-20120608-FINAL
nic4 00:B0:52:00:00:03 Fetch Device Attributes
nic4 00:00:00:00:00:02 QCA7420-MAC-QCA7420-1.0.0.351-06-20120608-FINAL (1mb)
        PIB 0-0 8080 bytes
        MAC 00:00:00:00:00:02
        DAK 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00 (none/secret)
        NMK 50:D3:E4:93:3F:85:5B:70:40:78:4D:F8:15:AA:8D:B7 (HomePlugAV)
        NID AE:A9:CD:0E:7C:82:00
        Security level 0
        NET TPL406EA1_FW101b01
        MFG A*AT1*N01000*P0104*F0101*H1A*D2CH*CTPL406EA1_FW101b01
        USR TPL406EA1_PIB104CEB_WM
        CCo Auto
        MDU N/A
nic4 00:00:00:00:00:02 Fetch Network Information
nic4 00:00:00:00:00:02 Found 0 Network(s)

source address = 00:00:00:00:00:02

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

These 3 lines from the output tells us the firmware installed on the powerline Adapter.
```
nic4 00:00:00:00:00:02 QCA7420 MAC-QCA7420-1.0.0.351-06-20120608-FINAL
nic4 00:00:00:00:00:02 QCA7420-MAC-QCA7420-1.0.0.351-06-20120608-FINAL (1mb)
USR TPL406EA1_PIB104CEB_WM
```

The rest of the settings from this command will be explained in more detail later on.