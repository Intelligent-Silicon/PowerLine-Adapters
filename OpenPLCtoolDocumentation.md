# Open PLC Util Documentation & The Basics

To find the documentation that accompanies this repo, using File Explorer, navigate to the folder where you downloaded the repo to and then look for the folder called ```DocBook```.

Alternatively copy and paste the following path into your web browser's search box (omni box) : ```file:///C:/Users/[Your Username]/source/repos/open-plc-utils/docbook/index.html```

This will show the full documentation for the Open PLC Utils repo including program code explanations, program explanations, and Linux scripting examples.

The Web browser locations use forward slashes ```/```, everything else like File Explorer, Terminal and Powershell use back slashes ```\```.

## Common Powerline Adapter Commands

You can skip over this section, as detailed instructions are in the later steps.

There's only 2 programs from the Toolkit that are needed to flash firmware on the Trendnet TPL-406e. You can confirm this by looking in the Programs Files where the manufacturers own firmware utility installs to.

Look in ```C:\Program Files (x86)\TRENDnet\TRENDnet Powerline Utility``` if using a 64bit Windows OS, which is Windows XP through to 11, or in ```C:\Program Files\TRENDnet\TRENDnet Powerline Utility``` if using a 32bit Windows OS, which is [Windows 95](https://dl.acm.org/doi/fullHtml/10.1145/238386.238611) through to Windows 10. Windows 11 is only supplied as a 64bit OS.

### plcinit.exe

This program used to exist in the Toolkit, but its functionality is now included in ```plctool```. It was used to flash firmware files to the device. References to this program still exist in the Toolkit documentation and is shipped by Trendnet in their utility programs suggesting the manufacturer is using an older version of the Toolkit and not the latest release seen at https://github.com/qca/open-plc-utils.

### modpib.exe

Changes the device identity parameters in a PIB file and update the checksum.

Device identity parameters are the MAC, DAK, NMK and the Manufacturer, Network and User HFID. Collectively, they establish the device network identity.

When flashing firmware, always make sure the PIB file contains the MAC ID of the device that is to be flashed, otherwise when using the Force Flash (-FF) switch/flag, all the powerline adapters that are flashed with the same PIB file will end up with the same MAC ID and thats not allowed.


### plctool.exe

This version of the Qualcomm Atheros Powerline Device Manager performs basic operations on powerline devices using vendor-specific management messages.

It can be used to interrogate and control devices or upgrade firmware if on-board NVRAM is present, which it is with the Trendnet TPL-406e powerline adapter. Most modern powerline adapters will have NVRAM, but some older powerline adapters may not.

It supports chipsets QCA6410, QCA7000 and QCA7420 and is the proper tool for upgrading panther/lynx chipset series devices.

It is important to reset panther/lynx devices after updating, because reset after update is not automatic anymore.

Also, everything takes longer because part of the memory is erased before being written.

Some operations may take 20 to 40 seconds so be patient.

This program version is identical to legacy program int6k except for option -m which uses version 1 of the Qualcomm Atheros VS_NW_INFO vendor-specific message.
Older firmware versions may not recognize this message version.

### Windows Defender interception

Programs using version 1 of the VS_NW_INFO vendor-specific message like int6k[xyz] and amp[xyz] programs will almost certainly trigger Windows Defender, in which case, either try plc[xyz] program files or disable Windows Defender. 

This is an example of Windows Defender blocking the int6K program called from Powershell despite running with elevated Administrator permissions. If running the programs in other ways, like from another program as in Trendnets case, you may not see the notification messages, because of the way the [toast notifications](https://learn.microsoft.com/en-us/windows/apps/develop/notifications/app-notifications/toast-notifications-overview) work and the inability to view historical notifications easily.

```
PS C:\Users\admin1\Documents\GitHub\open-plc-utils\VisualStudioNET\Programs> .\int6k  -i1 -n "C:\Users\admin1\Documents\Powerline Adapters\Original Firmware\3.nvm" 00:00:00:00:00:02
Program 'int6k.exe' failed to run: An Application Control policy has blocked this fileAt line:1 char:1
+ .\int6k  -i1 -n "C:\Users\admin1\Documents\Powerline Adapters\Origina ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~.
At line:1 char:1
+ .\int6k  -i1 -n "C:\Users\admin1\Documents\Powerline Adapters\Origina ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ResourceUnavailable: (:) [], ApplicationFailedException
    + FullyQualifiedErrorId : NativeCommandFailed
```

If you totally disable Windows Defender you can then get the correct output. 
```
PS C:\Users\admin1\Documents\GitHub\open-plc-utils\VisualStudioNET\Programs> .\int6k  -i1 -n "C:\Users\admin1\Documents\Powerline Adapters\Original Firmware\3.nvm" 00:00:00:00:00:02
nic1 00:00:00:00:00:02 Read Firmware from Device
int6k.exe: ReadFirmware1: Read timeout or network error
PS C:\Users\admin1\Documents\GitHub\open-plc-utils\VisualStudioNET\Programs>
```

### Get Help

If you are unsure what command switches/flags can be used with any of the programs simply use
```
--Help
```

### Command line switchs/flags

Do pay attention to the difference between upper case and lower case, they can make things go wrong very quickly. Whilst Windows is not case sensitive in general, Windows can be made to be case sensitive when accessing files or folders across all hard disks and individual folders and subfolders used by [WSL2 Linux distro's](https://learn.microsoft.com/en-us/windows/wsl/case-sensitivity).

The command line switches/flags used with plctool can mostly be used with other programs, but some exceptions to this rule do exist, so be careful.

For example ```-i [Ethernet name or number/Interface name]``` switch/flag is universal across all programs, the ```plctool``` ```-M``` switch/flag sets the NMK on the device, but in ```modpib``` ```-M``` sets the MAC ID in the PIB file.


Whilst the order you place individual switches/flags on the command line doesnt matter, the program will process them in the correct order for its own use.


```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\modpib --help

 program: modify selected PIB parameters and update checksum

 command: modpib.exe [options] file [file] [...]

 options: [C:D:L:M:N:S:T:U:v!?]

 -C n   CCo Selection is n
 -D x   DAK as xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx
 -L n   security level is n
 -M x   MAC as xx:xx:xx:xx:xx:xx
 -N x   NMK as xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx
 -S s   MFG string is s
 -T s   NET string is s
 -U s   USR string is s
 -v     verbose messages
 -!     version information
 -?     help summary

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool --help

 program: Qualcomm Atheros Panther/Lynx Powerline Device Manager

 command: plctool.exe [options] device [device] [...]

 options: [abB:d:D:efFHi:IJ:K:l:LmMn:N:p:P:QqrRS:t:Tvw:x!?]

 -a     read Device Attributes using VS_OP_ATTRIBUTES
 -B n   perform pushbutton action (n) using MS_PB_ENC [1|2|3|'join'|'leave'|'status']
 -d f   dump and clear watchdog report to file (f) using VS_WD_RPT
 -D x   Device Access Key (DAK) is (x) [689F074B8B0275A2710B0B5779AD1630]
 -e     redirect stderr to stdout
 -f     read NVRAM Configuration using VS_GET_NVM
 -F[F]  flash [force] parameters and/or firmware using VS_MODULE_OPERATION
 -H     stop host action requests using VS_HOST_ACTION.IND
 -i n   host interface is (n) [2]
 -I     read device identity using VS_MODULE_OPERATION
 -J x   set NMK on remote device (x) via local device using VS_SET_KEY (see -K)
 -K x   Network Membership Key (NMK) is (x) [50D3E4933F855B7040784DF815AA8DB7]
 -l n   loop (n) times [1]
 -L     display link status
 -m     read network membership information using VS_NW_INFO
 -M     set NMK on local device using VS_SET_KEY (see -K)
 -n f   read NVM from SDRAM to file (f) using VS_MODULE_OPERATION
 -N f   write firmware file (f) to flash memory using VS_MODULE_OPERATION
 -p f   read PIB from SDRAM to file (f) using VS_MODULE_OPERATION
 -P f   write parameter file (f) to flash memory using VS_MODULE_OPERATION
 -q     quiet mode
 -Q     quick flash (return immediately)
 -r     read hardware and firmware revision using VS_SW_VER
 -R     reset device using VS_RS_DEV
 -S f   write softloader file (f) to flash memory using VS_MODULE_OPERATION
 -t n   read timeout is (n) milliseconds [200]
 -T     restore factory defaults using VS_FAC_DEFAULTS
 -v     verbose mode
 -w n   pause (n) seconds [0]
 -x     exit on error
 -!     version information
 -?     help summary

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Encapsulating Spaces

When using long paths, filenames or pass phrases, if there is a space character in the content, then the content needs to be encapsulated or wrapped in double quotes.

For example
```
-T "Qualcomm Atheros Enabled Network"
-S "Qualcomm Atheros HomePlug AV Device"
-U "Qualcomm Atheros Enabled Product"
-N "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm"
-P "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib"
-N "My New NMK Passphrase"
```


### Check Powerline adapter status

Below are examples of the type of output to expect when a powerline adapter is functional or soft bricked. As this is plugged directly into the Windows box, no MAC ID is specified on the command line.

Note how the request is sent to the Local Management Address (LMA) MAC ID 00:B0:52:00:00:01.

The device will respond using its normal MAC ID which indicates its functional as we can see below and see it communicating with another power line adapter.
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -Iarm
nic4 00:B0:52:00:00:01 Request Version Information
nic4 00:00:00:00:00:02 QCA7420-MAC-QCA7420-1.0.0.351-06-20120608-FINAL
nic4 00:B0:52:00:00:01 Fetch Device Attributes
nic4 00:00:00:00:00:02 QCA7420-MAC-QCA7420-1.0.0.351-06-20120608-FINAL (1mb)
        PIB 0-0 8080 bytes
        MAC D8:EB:97:C1:15:62
        DAK 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00 (none/secret)
        NMK 50:D3:E4:93:3F:85:5B:70:40:78:4D:F8:15:AA:8D:B7 (HomePlugAV)
        NID AE:A9:CD:0E:7C:82:00
        Security level 0
        NET Qualcomm Atheros Enabled Network
        MFG Qualcomm Atheros HomePlug AV Device
        USR Qualcomm Atheros Enabled Product
        CCo Auto
        MDU N/A
nic4 00:B0:52:00:00:01 Fetch Network Information
nic4 00:00:00:00:00:02 Found 1 Network(s)

source address = 00:00:00:00:00:02

        network->NID = AE:A9:CD:0E:7C:82:00
        network->SNID = 12
        network->TEI = 3
        network->ROLE = 0x00 (STA)
        network->CCO_DA = 00:00:00:00:00:03
        network->CCO_TEI = 1
        network->STATIONS = 1

                station->MAC = 00:00:00:00:00:03
                station->TEI = 1
                station->BDA = 04:02:1F:38:9D:3A
                station->AvgPHYDR_TX = 009 mbps Primary
                station->AvgPHYDR_RX = 009 mbps Primary

PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Abbreviations

```
BDA			= Bridged Destination Address
CCO			= Central Coordinator
CCO_DA 		= Central Coordinator Destination Address
CCO_TEI 	= Central Coordinator Terminal Equipment Identifier
DAK   		= Device Access Key
MDU   		= Multiple Dwelling Unit
NID 		= Network Identifier
NMK   		= Network Membership Key
PIB   		= Parameter Information Block
SNID 		= Short Network Identifier
STA			= Station
TEI 		= Terminal Equipment Identifier
```

### Factory Reset powerline adapter

This is the command to use to factory reset a powerline adapter. You will need to use this option if the device doesnt automatically reset after a firmware update which happens with the v1.2.0 firmware.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\plctool -i4 -T
nic4 00:B0:52:00:00:01 Restore Factory Defaults
nic4 00:00:00:00:00:02 Restoring ...
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Timeout 

The default timeout period built into the program is 50 milliseconds. In some situations, like when the powerline adapter has gone to sleep because the device thats plugged into is switched off or in a deep sleep, it can take longer for the powerline adapter to wake up. Increasing the timeout period can resolve the problem where you get a slightly misleading response.

Default timeout period 50
```
-T [Milli Seconds]
-T 50 
```
500 milli seconds (0.5 second) which works well when the devices are networked. 
```
-T 500
```

1000 milli seconds (1 second) timeout.
```
-T 1000
```

### Change Passphrase Key (NMK)

In order to join powerline adapters together into a group, they all need to share the same passphrase, and because these can be variable in length, its converted into a fixed length key.

A blank passphrase can be set using the below switch/flag.
```
-N 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
```

The default Powerline Adapter NMK which is seen as (HomePlugAV).
```
-N 68:9F:07:4B:8B:02:75:A2:71:0B:0B:57:79:AD:16:30
```

The program called hpavkey can be used to generate a new NMK. If you want to use spaces in the phrase encapsulate it in double quotes.
```
.\hpavkey -M [variable length passphrase]
.\hpavkey -M "My New password"
```
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey "My New Password"
ECAD59E4C274C29BBADFCDCB7C7020FAC40E91D829A31AC2D641EBC55A9F8B95
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

If you dont encapsulate the pass phrase in quotes, each word is seen as a new password and generates 3 keys.
```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey My
8ED6791BDF3D61A1E6EDCBB253979B0A6BEF7F3D99DDA0FB49CFFE96923514B6
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey My New
8ED6791BDF3D61A1E6EDCBB253979B0A6BEF7F3D99DDA0FB49CFFE96923514B6
18FDD549B2ED367AC0C74CBEC1214644728515B30EDBCB78E7D322757A7C8359
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey My New Password
8ED6791BDF3D61A1E6EDCBB253979B0A6BEF7F3D99DDA0FB49CFFE96923514B6
18FDD549B2ED367AC0C74CBEC1214644728515B30EDBCB78E7D322757A7C8359
E7CF3EF4F17C3999A94F2C6F612E8A888E5B1026878E4E19398B23BD38EC221A
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

```-e``` Enforce Homeplug AV length and content rules.

The passphrase needs to be between 12 and 64 characters.

The passphrase must consist of 7-bit ASCII characters in the range 0x20 Hex aka 32 Decimal aka the space characters through to 0x7F Hex aka 127 Decimal aka the Delete character.
```
-e 
```
An ASCII table can be seen here https://commons.wikimedia.org/wiki/File:ASCII-Table-wide.svg


### Central Coordinator Selection Mode.

When the powerline adapters are in a group and have formed a network, one of the devices needs to be in-charge or a Central Coordinator (CCo).

The default option (0) is for any powerline adapter to be a CCo but this can sometimes cause problems with devices so a manual override can be specified.

To make these changes involves modifying the unique PIB file for each device in the network group, so one PIB states ```2``` and all other's state ```1```. If two or more devices are set to be CCo, this could cause constant wrestling between the devices, having the effect of slowing up the network group communication speed.

The options available are:
```
0	Auto, the station may act either as a CCo or STA of an AVLN
1	Never, the station will never become the CCo of an AVLN
2	Always, the station will not join other AVLNs as a STA
3	User, the user assign how the station act either as CCo or STA of an AVLN
```

The command for this is
```
.\modpib -C [0-4]
```

## Curious Fingers

### Disabling the push button aka Set Security Level

If you have kids, they like to push buttons and the powerline adapters typically have at least one button they can press. This can cause problems pairing and resetting devices so to avoid the inconvenience its generally recommended this is disabled but you will have to create a PIB file for each device when flashing the firmware.

The default is for the button to be enabled and then you can then pair (3 second hold) or factory reset (10-20 second hold) the powerline adapter. Disabling the button disables both pairing and factory reseting which then requires the device to plugged into the computer direct.

You can enable and disable the button using these commands:

Enable powerline adapter button
```
.\modpid -L 1 [PIB file]
```
Disable powerline adapter button
```
.\modpid -L 0 [PIB file]
```

Whilst Qualcomms own documentation suggests the button can be toggled using hpavkey, in practice this is not possible. It might have been possible in the past, its certainly not today though!

Enable powerline adapter button - This does not work
```
.\hpavkey -L 0
```
Disable powerline adapter button - This does not work
```
.\hpavkey -L 1
```

