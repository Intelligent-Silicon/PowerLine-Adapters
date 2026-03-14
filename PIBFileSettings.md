# Setting the firmware PIB File with modpib

ModPib is the program to use to modify the firmware PIB file before flashing it to the powerline adapter.


If you flash firmware (.nvm & .pib) files, you need to make sure the PIB file has the powerline adapaters unique MAC ID & DAK of the device in it. 

The PIB file supplied by the manufacturer will be a generic PIB file designed for the accompanying NVM firmware file only.

The manufacturer supplied PIB file comes with generic DAK and MAC ID's which need to be changed. 

If the DAK and MAC ID are not changed and the manufacturer supplied PIB file is used to flash multiple powerline adapters using the command example below, then problems can occur, namely all the powerline adapters end up with the same NID, NMK, DAK and [00:B0:52:00:00:03](SpecialStatusMACs.md#00b052000003) MAC ID and the CCo is set to never, so the powerline will not work properly. Your only resolution is to change the PIB file and reflash to get the powerline adapter working.

```
.\plctool -i4 -t500 -F -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib" -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm"
```

If you want to check the Manifest of the PIB & NVM files, use the commands ```chkpib``` and ```chknvm``` seen below to see the version numbers of the NVM & PIB files, making sure the versions numbers match.
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\chkpib -m "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA2.pib"
------- C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA2.pib (0) -------
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
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\chknvm -m "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm"
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

If you attempt to flash firmware where the NVM and PIB dont have at least matching version numbers, then below is an example of the error you will see, even if you use the Force Flash (-FF) option. There are other configuration settings in the PIB file which cant be altered using modpib that also control how the NVM firmware works. These include [Signal Level Attenuation Characterization (SLAC)](https://github.com/qca/open-plc-utils/blob/46c3506453c15b873fd6ed3e76c9872cea5e143a/slac/pev.1#L13) settings and Attenuation Calibration Data (sometimes called "[prescalers](https://github.com/qca/open-plc-utils/blob/46c3506453c15b873fd6ed3e76c9872cea5e143a/pib/psin.1#L4)" or [amplitude maps](https://github.com/qca/open-plc-utils/blob/46c3506453c15b873fd6ed3e76c9872cea5e143a/pib/psin.1#L13)). This is why you should use the matching NVM and PIB files when flashing the firmware incase new features in the NVM firmware exist and there is no corresponding configuration or vice versa. 

Likewise if there are firmware files for your region of the world, you should use that to make sure the devices work properly and comply with legislation.

This repo might go into the other configuration settings at a later date but is beyond the remit of this repo currently.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -F -P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib" -N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW-QCA7420-1.5.0.0026-02-CS-20200114.nvm"
nic4 00:B0:52:00:00:01 Start Module Write Session
nic4 00:B0:52:00:00:01 Flash C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib
RESERVED 0x00000000

 <snip>
 
nic4 00:B0:52:00:00:01 Close Session
nic4 00:B0:52:00:00:03 Minor Version Mismatch (0x48): Device refused request
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### The Minimum Required Changes

Because each powerline adapter needs a PIB which has the device's DAK and MAC ID in it, you need to make the minimum of 3 changes to the PIB file before it can be flashed.

The manufacturers own firmware utility software will get the DAK and MAC ID from the powerline adapter, change the PIB file and then flash the original NVM and modified PIB file. We do the same using Open PLC Utils but manually, command by command.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -t500 -Ir
nic4 00:B0:52:00:00:01 Request Version Information
nic4 00:00:00:00:00:02 QCA7420 MAC-QCA7420-1.0.0.351-06-20120608-FINAL
        PIB 0-0 8080 bytes
        MAC 00:00:00:00:00:02
        DAK 68:9F:07:4B:8B:02:75:A2:71:0B:0B:57:79:AD:16:30 (HomePlugAV)
        NMK 50:D3:E4:93:3F:85:5B:70:40:78:4D:F8:15:AA:8D:B7 (HomePlugAV)
        NID B0:F2:E6:95:66:6B:03
        Security level 0
        NET TPL406EA1_FW101b01
        MFG A*AT1*N01000*P0104*F0101*H1A*D2CH*CTPL406EA1_FW101b01
        USR TPL406EA1_PIB104CEB_WM
        CCo Auto
        MDU N/A
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### modpib commandline switches/flags

Dont forget the ```---help``` attribute will show you the modpib switches/flags.

```
.\modpib --help
```


The format for using the modpib command is as follows
```
.\modpib -[[Modpib switches/flags and their settings] recurring ] [path\and\name\of\adapters\Firmwarefile.PIB]
```
You can have multiple modpib swtches/flags on a single command line, hence the recurring. You can also run modpib over the firmware PIB file as many times you are like, so you can run the modpib command with one switch/flag and then run another modpib command with another swtch/flag and so on and so on. Modpib will update checksums accordingly.

### Central Coordinator

Sets the Central Coordinator status for the powerline adapter in the PIB file. This has to be unique to each powerline adapter if one device is to be the CCo and all other stations, otherwise all the same if set to Auto.

The Central Coordinator is where you can designate via the PIB file the powerline adapter can be in charge of the powerline network group or just a station in the powerline network group. Generally speaking its best to leave these all on ```0 Auto, the station may act either as a CCo or STA of an AVLN (
Audio Video LAN)``` unless you have a pressing need to nominate one as the Central Coordinator and the other's as Stations in the powerline adapter network group.

```
.\modpib -C [Central Coordinator Mode, 0 is Auto, the station may act either as a CCo or Station of a powerline network group, 1 is Never, the station will never become the CCo, 2 is Always, the station will not join other powerline network groups as a Station, 3 is User, the user assign how the station act either as CCo or STA of an AVLN] [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -C 0 [path\and\name\of\adapters\Firmwarefile.PIB]
```


### Device Access Key (DAK)

Sets the 16 hexadecimal number DAK of the powerline adapter in the PIB file. This has to be unique to each powerline adapter.

There is no documentation from Trendnet or Qualcomm stating if the Device Password (DPW) thats on the stick on label found on the back of the powerline adapter is the DAK and if it is, how its supposed to be used with hpavkey or modpib. 

Should the DPW used with hpavkey use the alphanumerics and hypens verbatim as seen in the 3rd example below, or just the alphanumerics without the hyphens seen in the 4th example below?

The 3rd and 4th line both generate different output. So if you know the answer, drop us a message please.

```
.\hpavkey -D [Convert Unique password to DAK format]
.\hpavkey -D "Unique Device Access Key"
.\hpavkey -D "FDSQ-PKRP-CPSK-YPFZ"
.\hpavkey -D "FDSQPKRPCPSKYPFZ"
```

The resulting output from ```hpavkey -D``` is used with modpib to set the DAK which is a 16 characters Hexadecimal number. The use of colon seperators is optional.

```
.\modpib -D [DAK in format xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx (16) ] [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -D A3AA7A439C9FC1CFB99FBC2B9F5B9AB0 [path\and\name\of\adapters\Firmwarefile.PIB]
```
If you are going to Force Flash (-FF) the powerline adapter, you can change the DAK and MAC ID from whats on the stick on label. So you dont have to ensure each PIB file has the correct MAC and DAK hexadecimal number but you still need to make sure the DAK and MAC ID is unique to the powerline adapter.

### Security Level ( Toggle Push button Pairing)

The powerline adapters come with a button which performs one of two different functions depending on how long its pressed in and held in for.

To pair a device with other devices, press and hold the button for 3 seconds. The powerline adapter goes into pairing mode for 2 minutes. Perform the same function on the other powerline adapters you want to pair it with, all within the 2 minute window of the first powerline adapter put into pairing mode.

To factory reset the device, press and hold the button for 10 to 20 seconds until the LED lights switch off. When the LED lights have switched off, release the button and the powerline adapter will be started up in a factory reset state, thats the equivalent of using ```.\plctool -i4 -t500 -T```.

If you disable the button, and lose all your settings, just plug the powerline adapter directly into the windows box like you are doing now and you can reset things that way.
```
.\modpib -L [Security Level (button pairing & Reset), 0 is enabled, 1 is disabled] [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -L1 [path\and\name\of\adapters\Firmwarefile.PIB]
```

### MAC ID (medium access control id or media access control id)

Sets the 12 hexadecimal number MAC ID of the powerline adapter in the PIB file. This has to be unique to each powerline adapter.

```
.\modpib -M [MAC ID in the format xx:xx:xx:xx:xx:xx ] [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -M 00:00:00:00:00:01 [path\and\name\of\adapters\Firmwarefile.PIB]
```

If you are going to Force Flash (-FF) the powerline adapter, you can change the DAK and MAC ID from whats on the stick on label. So you dont have to ensure each PIB file has the correct MAC and DAK hexadecimal number but you still need to make sure the DAK and MAC ID is unique to the powerline adapter.

The Organisationally Unique Identifier (OUI) in a MAC address is the first 6 hexadecimal numbers aka three octets aka 24 bits of the 12 hexadecimal number, which identify the manufacturer. Purchased from the IEEE, this prefix allows for the identification of network hardware vendors. For example, in 00:1A:2B:3C:4D:5E, the OUI is 00:1A:2B. You can look this up in a number of websites like https://www.macvendorlookup.com/ and https://www.wireshark.org/tools/oui-lookup.html .

As this can typically identify the manufacturer, like any device with a MAC ID, it provides hackers with knowledge of what the device is, which could prove useful in gaining access to the device and potentially the ability to load malware (malicious program code) into the firmware in order to gain persistence. Persistence is where a hacker can keep their malware in the device for future requirements like remotely control a device for their own means when ever they like with minimal effort. 

So there is some argument in changing the MAC ID that might or might not slow up hackers.


### Network Membership Key (Network passphrase group)

Sets the 16 hexadecimal number NMK of the powerline adapter in the PIB file. This has to be shared with each powerline adapter in a powerline network group.

hpavkey is the program which creates the required output for use as a NMK.

It takes a variable length password or pass phrase and converts it into a 16 digit Hex Key.
If the option ```-e``` is used, the password or passphrase has to meet the following criteria:

The passphrase needs to be between 12 and 64 characters.

The passphrase must consist of 7-bit ASCII characters in the range 0x20 Hex aka 32 Decimal aka the space characters through to 0x7F Hex aka 127 Decimal aka the Delete character.

An ASCII table can be seen here https://commons.wikimedia.org/wiki/File:ASCII-Table-wide.svg

```
.\hpavkey --help
```
```
.\hpavkey -e[Enforces the HomePlug AV password rules. No additional option] -M[Convert Unique password to NMK format]
.\hpavkey -e -M "Unique Shared Network Membership Key"
.\hpavkey -M "HomePlugAV"
```

The resulting output from hpavkey is used here to set the NMK.
```
.\modpib -N [NMK in format xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx (16) ] [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -N 39B5BBF7CC7FF76069257425BF25C80B [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -N 50D3E4933F855B7040784DF815AA8DB7 [path\and\name\of\adapters\Firmwarefile.PIB]
```
For more information, [see the NMK section in the previous step](SetDakNMK.md#network-membership-key-nmk).
## Data Strings

The following 63 character data strings dont service any functional purpose to the powerline adapter but can be used for identification purposes besides providing the Manufacturer, Network and User details. To change the data strings use the modpib switches/flags shown below.

This can be useful for storing Asset ID's or other (unique) identifiers on the device where businesses need to keep track of the devices in their IT fleet, groups or families who want to record their details in case of theft or mix up's where multiple powerline adapters may be used in a location. In practice, most entities stick a label sometimes with a unique identifier on the device so that specialist equipment doesnt need to be used to identify the device, like when it last passed its electrical safety test.

### Manufacturers (MFG) String

Maximum length 63 Characters.

```
.\modpib -S [Manufacturers String encapsulated in double quotes ] [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -S "Manufacturers Name Goes Here" [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -S "Qualcomm Atheros HomePlug AV Device" [path\and\name\of\adapters\Firmwarefile.PIB]
```

### Network (NET) String

Maximum length 63 Characters.

```
.\modpib -T[Timeout in Milliseconds] -T [User String encapsulated in double quotes ] [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -T "Network String Goes Here" [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -T "Qualcomm Atheros Enabled Network" [path\and\name\of\adapters\Firmwarefile.PIB]
```

### User (USR) String

Maximum length 63 Characters.

```
.\modpib -U [User String encapsulated in double quotes ] [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -U "User String Goes Here" [path\and\name\of\adapters\Firmwarefile.PIB]
.\modpib -U "Qualcomm Atheros Enabled Product" [path\and\name\of\adapters\Firmwarefile.PIB]
```


### PIB Settings  

3 PIB files for 3 powerline adapters.

All powerline adapters will be set to Auto for the CCo.

The NMK is shared.

The button is disabled on all powerline adapters.

The String data (Net, Mfg & Usr) is set to generic Qualcomm firmware strings 
```
.\hpavkey -e -M "2nd Longer Password!"
77D92B19F8AF73F8672547A6FD76ECCC
.\modpib -L1 -C0 -N 77D92B19F8AF73F8672547A6FD76ECCC -S "Qualcomm Atheros HomePlug AV Device" -T "Qualcomm Atheros Enabled Network" -U "Qualcomm Atheros Enabled Product" "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\Hub.pib"
.\modpib -L1 -C0 -N 77D92B19F8AF73F8672547A6FD76ECCC -S "Qualcomm Atheros HomePlug AV Device" -T "Qualcomm Atheros Enabled Network" -U "Qualcomm Atheros Enabled Product" "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA2.pib"
.\modpib -L1 -C0 -N 77D92B19F8AF73F8672547A6FD76ECCC -S "Qualcomm Atheros HomePlug AV Device" -T "Qualcomm Atheros Enabled Network" -U "Qualcomm Atheros Enabled Product" "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA3.pib"
```

### Hub

This command contains the unique data for the Hub's pib file.

Unique DAK

Unique MAC ID
```
.\hpavkey -e -D "1st Long Password! Hub" 
D7FECE12C7041284FD316F08074C1395
.\modpib -D D7FECE12C7041284FD316F08074C1395  -M 00:00:00:00:00:01  "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\Hub.pib"
```

### Powerline Adapter 2

This command contains the unique data for the Powerline Adapter #1's pib file.

Unique DAK

Unique MAC ID
```
.\hpavkey -e -D "1st Long Password! PA2" 
247A9BA19DC6B1C0F39E4838FC3E6529
.\modpib -D 247A9BA19DC6B1C0F39E4838FC3E6529  -M 00:00:00:00:00:02  "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA2.pib"
```

### Powerline Adapter 2

This command contains the unique data for the Powerline Adapter #2's pib file.

Unique DAK

Unique MAC ID
```
.\hpavkey -e -D "1st Long Password! PA3" 
FAA623481B16BD659852880AA5CA4AC9
.\modpib -D FAA623481B16BD659852880AA5CA4AC9  -M 00:00:00:00:00:03  "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA2.pib"
```
