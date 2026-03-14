# Fritz Box 7530 Router & Powerline Adapters

The Fritz!box 7530 router and probably other routers detects powerline adapters.

Unfortunately it does incorrectly report a powerline adapter is interfering with the telephone DSL cable. 

Error messages which could be seen in the Fritz!Box event log (http://fritz.box/#/log) include:
```
Impaired quality of the signal on the DSL line was detected due to incorrect cabling. Please
make sure that your line does not include any branching or multi-distributors. The branch is
11 meters long. It is impairing the transmission rate by around 22534 kbit/s.
```

```
The DSL signal may have been distorted by powerline.
```

```
The internet connection (DSL) was cleared. Interference may have been caused by
powerline.
```

Whilst powerline adapters can interfere with telephone DSL cables, especially if the cable is not shielded, it is a bit of a shame the Fritz!box cites powerline adapters as a possible cause when they are simply not plugged in and have been unplugged for hours and days!

This may be in part due to the router firmware, or even the Broadcomm (not Huawei) green street cabinets detecting powerline adapter interference and reporting back to the router. In this case, the green street cabinet is well within range of these powerline adapters. 

Problem is, that doesnt added up when the powerline adapters are simply not plugged in. Whilst its possible for the right equipment to detect signals/interference from a distance, well beyond the range of usability, its unknown at this stage if the Broadcomm green cabinets have that capability built in.

However AVM do provide various powerline adapters, and the equivalent model using the QCA 7420 chipset found in the Trendnet TPL406e is called a Fritz 510E powerline adapter. 

The firmware for this model can be downloaded from https://download.avm.de/fritzpowerline/ website.

There are two image files:

https://download.avm.de/fritzpowerline/fritzpowerline-510e-a/other/recover/fritz.powerline_510E_A_120_01_14.image

https://download.avm.de/fritzpowerline/fritzpowerline-510e-a/other/fritz.os/fritz.powerline_510E_A_150_02_24.image

The last link is what is of interest. Version 1.5.0.1-24 released 20200416. This is a more modern version and the numbering is similar to what Trendnet use, suggesting the firmware is actually designed and written by Qualcomm and then manufacturers like Trendnet & AVM simply brand and configuring the firmware, or some "engineers" have a very limited imagination when it comes to version numbering. Dont rule out the latter when it comes to tech engineers!

When viewing the image file in a hex editor, it appears to be an unencrypted file containing both the PIB and NVM firmware. 

This means, it should be possible to extract a range of bytes from the ```fritz.powerline_510E_A_150_02_24.image``` file into a file with the ```.PIB``` file extension and then a different range of bytes for a file with the ```.nvm``` file extension.

The potentially difficult part will be identify the correct range of bytes for each file because checksums are used, but the code for the location of the checksums exists in the github repo open plc utils code, specifically the source code for chkpib and chknvm. 

If successful it should then be possible to use plctool to flash the Trendnet TPL-406e powerline adapters with the Fritz firmware. That should then at least keep the Fritz!box router happy especially if their firmware allows the Fritz!box router to communicate and control their own brand powerline adapters.

There could be other pitfulls, but these wont become apparent until the firmware flash is attempted.

ChatGPT reckons the PIB file offsets are 0x00 to 0x04000 in the image file, citing a website boxmatrix.info as its source, but that website could be Ai prompt poisoning. Google claims the boxmatrix.info website is a fitness app, but its not accessible using a webbrowser, so does seem a little suspicious to say the least!

Anyway, once a byte range has been decided on for the PIB file, save the range into a file with the PIB file extension and then use chkPIB to authenticate it. 

Work out the byte range for the NVM firmware to copy into a file with the NVM file extension and use chknvm to authenticate the NVM file. 

If both check out, try to flash these firmware files using plctool, then try to access them from the fritzbox router software.

The ISP, in this case Zen Internet were of little use for offering up the real reason why the unplugged Trendnet TPL-406e powerline adapters were purportedly affecting the internet connection!

When it comes to tech, rule nothing out simply because the powers that be for centuries have been trying to control people and lie over many things! Cynical but true sadly!

