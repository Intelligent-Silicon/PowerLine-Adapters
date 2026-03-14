# Flashing the firmware files

This step is to flash the required NVM firmware file and a configured PIB firmware file unique to each powerline adapter using Open PLC Utils. 

### Things to consider

These instructions are based on the powerline adapter being plugged directly into the Windows box.

When flashing firmware using ```plctool```, the device will NOT automatically factory reset after the firmware is uploaded to the powerline adapter. 

[Because parts of the firmware now involves erasing, processes can reportedly take between 20-40 seconds but its unclear which operations!](https://github.com/qca/open-plc-utils/blob/46c3506453c15b873fd6ed3e76c9872cea5e143a/plc/plctool.1#L20)

When a problem occurs, always try factory resetting the powerline adapter first using the command below.
```
.\plctool -i4 -t500 -T
```

If it takes any longer than a few minutes for the firmware process to complete uploading onto the powerline adapter or you dont get to see any of the output seen [here](TypicalFirmwareFlashing.md), making sure Powershell or Terminal has focus, press CTRL + C to cancel the action and get the Powershell or Terminal prompt back, then factory reset the adapter, wait a moment and then try to flash the firmware again.

In most cases, you only need to use the Flash switch (-F), however if problems occur with flashing and everything else has been double checked and ruled out, then trying the Force Flash (-FF) can be used.

If you see a ```Device refused request``` like the one shown below, try factory resetting the powerline adapter before trying again.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm" -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\Hub.pib" -FF
nic4 00:B0:52:00:00:01 Start Module Write Session
nic4 00:00:00:00:00:02 Can't Lock Flash Memory (0x23): Device refused request
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

If factory resetting the adapter and even trying to flash the default v2 ```firmware FW_TPL-406Ev2.nvm``` and ```FW_TPL-406Ev2.pib``` doesnt work, check you Windows box network adapter settings using ```ipconfig```.

Once the Windows box network settings have been double checked, try flashing the FINAL version of the firmware ```MAC-QCA7420-v1.0.0-06-X-FINAL.nvm``` and ```TPL406EA1_PIB104CEB_WM.pib```

If none of that works, disable Windows Defender and try again.


### Flash Firmware

This is the command and switches/flags which will flash the firmware onto the powerline adapters. 

If you have copied the firmware files to the repo's Programs folder you can use the command on the 2nd line below.

If you have the firmware files in a different folder to the Programs folder, you should include the file paths as seen on the 3rd, 4th & 5th lines below. 

Dont forget to encapsulate long paths and files names in double quotes to handle the space character properly as seen on the 3rd, 4th & 5th lines below.

Dont forget to configure the PIB file but you can configure the powerline adapter after uploading the default NVM and PIB (see previous steps).

If after flashing the new firmware and configuration settings, waiting a moment, and the new updates seem partially completed, you can always reset the powerline adapater to the default latest firmware on line 6, or the last Final release on line 7, before attempting the firmware upgrade again.

```
.\plctool -i[Number] -t[timeout milliseconds] -N [path\and\name\of\adapters\Firmwarefile.NVM] -P [path\and\name\of\adapters\Firmwarefile.PIB] -F[F forcibly flash firmware]
.\plctool -i4 -t500 -N FW_TPL-406Ev2.nvm -P FW_TPL-406Ev2.pib -F F
.\plctool -i4 -t500 -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm" -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\Hub.pib" -F
.\plctool -i4 -t500 -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm" -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA2.pib" -F
.\plctool -i4 -t500 -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm" -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA3.pib" -F
.\plctool -i4 -t500 -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm" -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib" -FF
.\plctool -i4 -t500 -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\MAC-QCA7420-v1.0.0-06-X-FINAL.nvm" -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib" -FF
```



### Typical firmware flashing output

Below is a link to a webpage which shows the typical output seen during a firmware flashing process.

[Typical firmware flashing output](TypicalFirmwareFlashing.md) you will see during the firmware flashing process.

### Checking the settings

Its a good idea to check the powerline adapter settings after flashing new firmware.

The powerline adapters button has been disabled on all devices, so when the button is pushed in and held in for at least 30 seconds, the LED lights never go out suggesting the button has been disabled and the line ```Security level 1``` should be seen in all the revision output shown below.


The way to tell if the firmware has been successfully installed is by checking the MAC ID's shown.

This example shows the ```00:B0:52:00:00:01``` LMA MAC ID and then the ```00:00:00:00:00:AA``` powerline adapters unique MAC ID. The firmware successfully installed. 
```
nic4 00:B0:52:00:00:01 Request Version Information
nic4 00:00:00:00:00:AA QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
```

This example show the ```00:B0:52:00:00:01``` LMA MAC ID and then the ```00:B0:52:00:00:03``` powerline adapters unique MAC ID. The firmware successfully installed, but the manufacturers default PIB was used so communication is deactivated. 
```
nic4 00:B0:52:00:00:01 Request Version Information
nic4 00:B0:52:00:00:03 QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS
```



