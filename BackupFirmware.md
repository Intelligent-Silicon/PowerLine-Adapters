# Backup Firmware

Backing up the firmware from the powerline adapters, should be one of the first tasks to carry out if you want to analyse the firmware, this way you can capture any malicious firmware that may have been installed on the device.

In practice, the Open PLC Util tools cant down the NVM file, only the PIB configuration files, so this step is largely a waste of time!

### Recovering Firmware

To recover the firmware, and assuming you can communicate with the powerline adapter having it plugged into the Windows box, use the following commands

To recover the .pib file
```
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i[Number] -t[timeout milliseconds] -p[path\and\name\of\adapters\file.pib] 
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -p "C:\Users\admin1\Documents\Powerline Adapters\Recovered Firmware\AdapterHub.pib" 
```

To recover the .NVM file
```
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i[Number] -t[timeout milliseconds] -n [path\and\name\of\adapters\file.NVM] 
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -n "C:\Users\admin1\Documents\Powerline Adapters\Recovered Firmware\AdapterHub.NVM" 
```

Here the powerline adapter has refused to give up the NVM firmware so this is what is displayed.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -n "C:\Users\admin1\Documents\Powerline Adapters\Recovered Firmware\AdapterHub.NVM" 
nic4 00:00:00:00:00:02 Read Module from Memory
nic4 00:00:00:00:00:02 Module not available in NVM or Memory (0x32): Device refused request
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

This make's it impossible to recover any faulty firmware for later analysis using this method. This isnt helpful by any means, but using JTAG or SPI mentioned later on could help give up the firmware, or some other clues that the firmware may not be stock.