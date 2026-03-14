# Downloading Firmware

We want to download the latest version of the firmware which is ```FW_TPL-406Ev2.zip```.

Found on the website https://downloads.trendnet.com/TPL-406E/firmware/.

This ```FW_TPL-406Ev2.zip``` firmware version file only contains firmware files (.bin, .nvm & .pib), the earlier firmware version zip files also contains Trendnet's Windows Utility program to upload the firmware to the powerline adapters. 

So the rest of this webpage is not relevant to Open PLC Utils which is what we are using, but if you are using Trendnet's Utility program to upload firmware carry on reading below.

### Install .NET Framework 3.5

The Trendnet_Setup programs needs .NET 3.5 Framework installed. If its not installed on your computer, the installation will attempt to install it for you, generally this works, but sometimes it doesnt and then that causes problems. 

So we check if its installed and if its not, we install & reboot the Windows box before installing the Trendnet_Setup program to avoid problems.

In the Windows 11 taskbar search box, type in "turn Windows Features on or off" and open the program. Alternatively press Window Key + R, and in the drop down list box that appears in the popup Run window, type "OptionalFeatures.exe" and then click the OK button.

When the Windows Features window appears, see if the .NET Framework 3.5 has a blue box, if it is, then .NET 3.5 Framework is installed. If its not installed tick the checkbox next to .NET Framework 3.5 (includes .NET2.0 and 3.0). If you expand the tree node, you will see the child options are also ticked, they do not need to be installed so you can untick them if you want.

Once .NET 3.5 Framework is installed its safer to progress onto installing the TrendNet_Setup program.


### Optional Powershell file hash command

If you download all the firmware files, you might want to use this command in powershell to hash a file and see if any of the files have got a matching hash with other versions of the firmware. This is for curiosity to see if any of the firmware files are identical.

```
Command																																											MD5 HASH
Get-FileHash "[path\and\name\of\adapters\Firmwarefile.Ext]" -Algorithm [MD5|SHA1|SHA256|SHA384|SHA512] | Format-List
Get-FileHash "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\FW_TPL406E_v1.0R(1.0.0.37-01)-WW\MAC-QCA7420-v1.0.0-01-X-FINAL.nvm" -Algorithm MD5 | Format-List	5C6496B84520522AF08240B2AA984E76
Get-FileHash "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\FW_TPL406E_v1.0R(1.0.0.37-01)-WW\TPL406EA1_PIB103CEB_WM.pib" -Algorithm MD5 | Format-List			571685B911D18D7E1A7FA44A41C1CA76
Get-FileHash "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\MAC-QCA7420-v1.0.0-06-X-FINAL.nvm" -Algorithm MD5 | Format-List		9CBAFF723B180885325E329F8AF72E7C
Get-FileHash "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406e_v1.0r(1.0.0-06)-ww\TPL406EA1_PIB104CEB_WM.pib" -Algorithm MD5 | Format-List			7D296C392F4E98A7AA0B1346607D34B0
Get-FileHash "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.nvm" -Algorithm MD5 | Format-List										68D9211E0CD82E51B69AFE3971F8F987
Get-FileHash "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib" -Algorithm MD5 | Format-List										1C16AD85D8D310C2502DAF00245B3F7F
```
As you can see, the firmware files are all unique.

## Files and Download Source

TrendNet TPL-406E webpage   : https://www.trendnet.com/support/support-detail.asp?prod=125_TPL-406E

Programs and firmware available from the above link.

```
File 									Version												Release Date
utility_powerline(v7.1.0101).zip		v7.1 Build 0101										9/2013
FW_TPL-406E_v1.0R(1.0.0-06)-WW.zip		QCA7420 MAC-QCA7420-1.0.0.351-06-20120608-FINAL		2/2013
```


TrendNet TPL-406E firmware  : https://downloads.trendnet.com/TPL-406E/firmware/

Programs and firmware available from the above link.

```
File 									Version												Release Date
FW_TPL-406Ev2.zip						QCA7420 MAC-QCA7420-1.2.0.1580-02-20150902-CS		9/2015
FW_TPL-406E_v1.0R(1.0.0-06)-WW.zip		QCA7420 MAC-QCA7420-1.0.0.351-06-20120608-FINAL		2/2013
FW_TPL406E_v1.0R(1.0.0.37-01)-WW.zip	QCA7420 MAC-QCA7420-1.0.0.337-01-20120309-FINAL		6/2012
```


### utility_powerline(v7.1.0101).zip

Windows Defender will report a threat has been found in this file. This is likely due to the reported bug where WinPCap 4.1.3 suffer's from DLL Injection. Microsoft will also report tools that could be used for hacking/penetration testingare a threat, so there may be nothing in this report other the DLL injection vulnerability in WinPCap.

More information can be found here: https://www.winpcap.org/


### FW_TPL-406Ev2.zip 
```
File Contents										MD5 HASH
FW_TPL-406Ev2.bin									
FW_TPL-406Ev2.nvm									68D9211E0CD82E51B69AFE3971F8F987
FW_TPL-406Ev2.pib									1C16AD85D8D310C2502DAF00245B3F7F
```

### FW_TPL-406E_v1.0R(1.0.0-06)-WW.zip
```
File Contents										MD5 Hash
Firmware Upgrade Procedure.pdf
FW_TPL-406E_v1.0R(1.0.0-06)-Release_Notes.txt
MAC-QCA7420-v1.0.0-06-X-FINAL.nvm					9CBAFF723B180885325E329F8AF72E7C
TPL406EA1_PIB104CEB_WM.pib							7D296C392F4E98A7AA0B1346607D34B0
Trendnet_setup.exe
```
If you have previously installed and uninstalled the Trendnet_Setup program and WinPCap setup program, this version of the Trendnet_Setup program detects a leftover registry entry for WinPCap but DOES NOT offer to "forcibly" install WinPCap 4.1.3.

It should install WinPCap 4.1.3.


### FW_TPL406E_v1.0R(1.0.0.37-01)-WW.zip
```
File Contents										MD5 Hash
Firmware Upgrade Procedure.pdf
FW_TPL-406E_v1.0R(1.0.0.37-01)-Release_Notes.txt
MAC-QCA7420-v1.0.0-01-X-FINAL.nvm					5C6496B84520522AF08240B2AA984E76
TPL406EA1_PIB103CEB_WM.pib							571685B911D18D7E1A7FA44A41C1CA76
Trendnet_setup.exe
```

If you have previously installed and uninstalled the Trendnet_Setup program and WinPCap setup program, this version of the Trendnet_Setup program detects a leftover registry entry for WinPCap and does offer to "forcibly" install WinPCap 4.1.2.

It should install WinPCap 4.1.2.


