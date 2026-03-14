# Editing the PIB file

The PIB file supplied with the NVM by the manufacturer work together and have to match. 

The PIB file structure and content is proprietary to Qualcomm Atheros, Ocala FL USA so public information is not available.

When it comes to using a PIB file with a different NVM file, the revision numbers must at least match, and any new features included in the NVM firmware file may require configuration settings that are not found in older PIB firmware files.

You cant edit a PIB file using a hex editor unless you correctly update the checksums that are also stored in the PIB file. 

```ChkPIB``` and ```ChkNVM``` are the programs which can display the firmware files manifest. The manifest shows things like the version numbers to help you make sure they match each other.

```SetPIB``` is the program which edits the PIB file and updates the checksums automatically. https://github.com/qca/open-plc-utils/blob/master/pib/setpib.1

```GetPIB``` is the partner program which fetches the data from the PIB file. https://github.com/qca/open-plc-utils/blob/master/pib/getpib.1

```Pib2XML``` and ```XML2Pib``` are the programs which will help you edit the PIB file using an XML editor.

### NVM and PIB Manifests


```ChkPIB``` and ```ChkNVM``` are the programs which can display the version numbers from their manifest. The manifest for the PIB and NVM must match otherwise the ```plctool``` will reject any attempt to flash the firmware.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\ChkNVM -m "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm"
------- C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm (0) -------
        Signature: 1234ABCD
        Hardware Compatibility: QCA7420
        Chain Major Version: 1
        Chain Minor Version: 4
        Chain Type: Firmware
        Build Major Version: 1
        Build Minor Version: 2
        Build Major Subversion: 0
        Build Sustaining Release: 2
        Build Type: CS
        Manifest Version: 1
        Build Number: 1580
        Build Date: 20150902
        Build Time: 173123
        Device Type: 7420
        Build Hostname: TOR-SW-BUILD01
        Build Username: buildbot
        Build Description: QCA7420/6410/7000 MAC SW v1.2.0 Rev:02 CS
        Build Version String: FW-QCA7420-1.2.0.1580-02-CS-20150902:173123-buildbot:TOR-SW-BUILD01-1-1.4
        Generic Identifier 0: 0
        Generic Identifier 1: 0
        Softloader Major Version: 0
        Softloader Minor Version: 1
        Manifest Free Space: 140/768 bytes
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```
``` 
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\chkpib -m "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib"
------- C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib (0) -------
        Signature: 1234ABCD
        Hardware Compatibility: QCA7420
        Chain Major Version: 1
        Chain Minor Version: 4
        Chain Type: Parameter Block
        Build Major Version: 1
        Build Minor Version: 2
        Build Major Subversion: 0
        Build Sustaining Release: 2
        Build Type: CS
        Manifest Version: 1
        Build Number: 1580
        Build Date: 20150902
        Build Time: 173123
        Device Type: 7420
        Build Hostname: TOR-SW-BUILD01
        Build Username: buildbot
        Build Description: QCA7420/6410/7000 MAC SW v1.2.0 Rev:02 CS
        Build Version String: PIB-QCA7420-1.2.0.1580-02-CS-20150902:173123-buildbot:TOR-SW-BUILD01-1-1.4
        Generic Identifier 0: 0
        Generic Identifier 1: 0
        Softloader Major Version: 0
        Softloader Minor Version: 1
        Manifest Free Space: 140/768 bytes
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

This is the manifest from the PIB file for a previous firmware version. As you can see they dont match the NVM file manifest shown above so would be rejected if any attempt to flash a device with firmware files that dont match.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\chkpib -m "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib"
------- C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib (0) -------
        Signature: 1234ABCD
        Hardware Compatibility: QCA7420
        Chain Major Version: 1
        Chain Minor Version: 2
        Chain Type: Parameter Block
        Build Major Version: 1
        Build Minor Version: 0
        Build Major Subversion: 0
        Build Sustaining Release: 1
        Build Type: FINAL
        Manifest Version: 1
        Build Number: 337
        Build Date: 20120309
        Build Time: 224652
        Device Type: 7420
        Build Hostname: TOR-SW-BUILD02
        Build Username: buildbot
        Build Description: QCA7420/6410/7000 MAC SW v1.0.0 Rev:01 FINAL
        Build Version String: PIB-QCA7420-1.0.0.337-01-FINAL-20120309:224652-buildbot:TOR-SW-BUILD02-1-1.2
        Generic Identifier 0: 0
        Generic Identifier 1: 0
        Softloader Major Version: 0
        Softloader Minor Version: 1
        Manifest Free Space: 140/768 bytes
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```
This is the error message which will be shown when the NVM and PIB file manifests dont match.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm" -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib" -F
nic4 00:B0:52:00:00:01 Start Module Write Session
nic4 00:B0:52:00:00:01 Flash C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib

	<Snip>

nic4 00:B0:52:00:00:01 Close Session
nic4 00:00:00:00:00:02 Minor Version Mismatch (0x48): Device refused request
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```
### Editing the PIB File.

Using a Hex Editor (like https://mh-nexus.de/en/hxd/ - Donate ware), and changing the bytes at address 0xD4 to 0xDF from ```0x43,0x53,0x00,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF,0xFF``` to ```0x46,0x49,0x4E,0x41,0x41,0x4C,0x00,0xCC,0xCC,0xCC,0xCC,0xCC,0xCC```, saving the file with a new name, we can see this has changed the Build Type from ```CS``` to ```FINAL``` but its not updated the checksums obviously and chkpib doesnt correct the checksums it seems. 

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\chkpib -m "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2 -CS-To-Final.pib"
------- C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2 -CS-To-Final.pib (0) -------
        Signature: 1234ABCD
        Hardware Compatibility: QCA7420
        Chain Major Version: 1
        Chain Minor Version: 4
        Chain Type: Parameter Block
        Build Major Version: 1
        Build Minor Version: 2
        Build Major Subversion: 0
        Build Sustaining Release: 2
        Build Type: FINAL
        Manifest Version: 1
        Build Number: 1580
        Build Date: 20150902
        Build Time: 173123
        Device Type: 7420
        Build Hostname: TOR-SW-BUILD01
        Build Username: buildbot
        Build Description: QCA7420/6410/7000 MAC SW v1.2.0 Rev:02 CS
        Build Version String: PIB-QCA7420-1.2.0.1580-02-CS-20150902:173123-buildbot:TOR-SW-BUILD01-1-1.4
        Generic Identifier 0: 0
        Generic Identifier 1: 0
        Softloader Major Version: 0
        Softloader Minor Version: 1
        Manifest Free Space: 140/768 bytes
chkpib.exe: pibchain2 found bad image checksum in C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2 -CS-To-Final.pib module 0
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Update PIB File checksums

Using the example above where the Build Types has been changed from ```CS``` to ```FINAL```, SetPIB reports it can be used to repair the check sum...

However the call to ```nvmseek2``` would suggest a coding error where the PIB file is being checked first before it can be repaired and because its got a checksum error, ```nvmseek2``` is aborting before it can be repaired.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\setpib -x "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2-CS-To-Final.pib"
setpib.exe: nvmseek2 found bad image checksum in C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2-CS-To-Final.pib module 0: operation canceled
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

So one way of updating the PIB file is to develop a script which can be done using Powershell, to extract data by cycling through all data types from an offset address and then using Regular Expressions to try to identify the data, before moving onto a new address. Its slow, its potentially tedious if its not automated with a script, but its one way of getting offset addresses that match data types. The regular expressions would need to be crafted to recognise the type of data to expect, easier with string data, than bytes, short's and longs, which could be a value or a bitmask. But using GetPib can build up a layout picture semi automatically before its edited with SetPib, with the added advantage Setpib can update checksums in the PIB file automatically.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\getpib "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib" 01F7 byte
0
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\setpib -v "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib" 01F7 byte 1
000001D0                      00 00 00 00 00 00 00 00 00        .........
000001E0 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ................
000001F0 00 00 00 00 00 00 00 01 00 00 00 00 00 00 00 00 ................
00000200 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ................
00000210 00 00 00 00 00 00 00 00                         ........

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\getpib "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib" 01F7 byte
1
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

More information can be elucidated from reading https://github.com/qca/open-plc-utils/blob/master/pib/setpib.1 but some of the challenges can be read here : https://github.com/qca/open-plc-utils/pull/33#issuecomment-94879769


### Prescalers 

```psIn``` and ```psOut``` will get the prescaler data in and out, and that data will take up a sizeable part of the PIB file.


### XML

Two other commands which have not been looked at in any detail are ```Pib2XML``` and ```XML2Pib```. 

Purportedly they will output the PIB file into an XML format file with ```PIB2XML``` being capable of outputting the default XSD schema, but documentation says the use of an object definition file is mandatory in order to get the data out into an XML file. Without the object definition file, ```Pib2XML``` wont export the data. 

Now it could be useful to view the source code here, but its suspected the object definition file is little more than a mask or template which is used to pull data from offsets into an xml format. In effect an automated version of whats suggested above but without the need for Regular Expressions to deduce the data and data type.

Anyway as this is beyond the remit of the repo, little more will happen here, but you have some ideas of what approaches might work.