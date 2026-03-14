# Factory Reset Powerline Adapters

This is the command to Factory Reset the powerline adapters after uploading the firmware to the powerline adapter or when the powerline adapters are no longer communicating with each other and you need to take things back to Factory reset configuration.

This step is largely unnecessary, but there's no harm in putting the adapter's in a factory reset state to make sure any changes that need a reboot are actioned. 

### Factory Reset Command

```
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i[Number] -t[timeout milliseconds] -T[Factory Reset back to defaults]
PS C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -T 
```

If the Factory Reset has worked properly, this is the output you will see.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -T 
nic4 00:B0:52:00:00:01 Restore Factory Defaults
nic4 00:00:00:00:00:02 Restoring ...
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

If the Factory Reset has not worked properly, this is the output you will see.
Note how its missing a line informing us its Restoring...
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -T
nic4 00:00:00:00:00:02 Restore Factory Defaults
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```





