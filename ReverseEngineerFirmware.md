# Reverse Engineer Firmware

You may want to reverse the engineer the firmware to look for security holes. Here in Europe this a perfectly legal activity and legislation override's contracts.

Steps to Reverse Engineer a data file like a bin, nvm or pib file.

### 1. Initial Analysis & Setup
    
        Acquire the File: Obtain the binary NVM dump, often extracted from device firmware or via a hardware interface like UART.
        Use a Hex Editor: Open the file in a hex editor (e.g., [HxD](https://mh-nexus.de/en/hxd/)) to view raw bytes.
        String Search: Use the strings command or built-in search functions to identify ASCII strings, which may reveal function names, settings labels, or configuration data.

### 2. Structuring and Parsing
        Structure: Define a "grammar" or map the binary file, color-coding different regions (headers, data blocks).
        Identify Patterns: Look for repeating patterns, such as checksums, pointers, or fixed-length data fields, as described by CyberGibbons: https://cybergibbons.com/alarms-2/signalling-devices/reverse-engineering-a-csl-dualcom-gprs-part-7-board-startup

### 3. Interpretation and Modification
        Data Mapping: Correlate specific values in the data file with known device behaviours (e.g., changing a setting in the software and observing which bytes change in the NVM dump).
        Patching/Modifying: Modify specific bytes to alter behaviour, keeping in mind that checksums or CRC values may need to be recalculated for the file to be accepted by the device.
        Document findings: Create a detailed map of the file structure for future reference
		

### Clues, Hints and Esoteric Knowledge

When looking for clues et al to help decipher whats going in binary files, its worth looking through public interactions and forums (where they exist) such as the one's shown below 

https://github.com/qca/open-plc-utils/issues 

https://community.tp-link.com/en/home/forum/topic/90763


Social media and general purpose technical forums are also a good source for getting hints or clues as to how a device may work or how it might affect other devices. Likewise techniques shown in different domains, like software hacking can cross over into hardware hacking, so gain a broad understanding of the task in hand whilst looking for parallels.

Blogs:

https://arcanenibble.github.io/dumping-lego-nxt-firmware-off-of-an-existing-brick.html

Youtube:

https://www.youtube.com/watch?v=KsiuA5gOl1o

https://www.youtube.com/@mediacccde

https://www.youtube.com/@DEFCONConference

https://www.youtube.com/@hackaday

https://www.youtube.com/watch?v=cf3zxHuSM2Y

https://www.youtube.com/results?search_query=stuxnet

https://www.youtube.com/watch?v=zBjmm48zwQU


Reddit: 

https://www.reddit.com/r/rfelectronics/comments/qnvmo2/any_rf_specialist_in_here_will_a_powerline/

https://www.reddit.com/r/cordcutters/comments/zj5jtj/trendnet_powerline_adapters/

Stack Exchange: 

https://ham.stackexchange.com/questions/2032/do-ethernet-over-power-adapters-interfere-with-radios


Its also worth reading through blogs on the subject because you don’t know what (private) communication the blogger has had with the manufacturer or other technical person, that’s been passed on and then given out on the blog.

https://fitzcarraldoblog.wordpress.com/2020/07/22/updating-the-powerline-adapters-in-my-home-network/

And all sources of documentation like man pages for linux distro's could also provide information because of when they were created and last updated.

https://manpages.ubuntu.com/manpages/noble/man1/plctool.1.html

Failing that use some of the archive tools like the one's shown below, they could give out information from sources which is later retracted.

[Wayback Machine](https://web.archive.org/)

[Archive.is](https://archive.is/)


BBS systems which have moved to the web. In the early days of computing, before the internet and at the start of the internet, Bulletin Board Systems (BBS) existed for sharing information. Some of these BBS's were quite technical in nature, check out those sources to see what you can find. 

What is important, is knowing what the instructions are in the chipset's instruction set. You will be able to marry up some of the chipset instructions with the code in the firmware mainly because its communicating directly with the hardware, unlike normal program where you will be using the API's provided by the middle man aka the Operating System. So blogs and websites like these could also be useful for deciphering firmware.
https://news.ycombinator.com/item?id=47028803

https://zyedidia.github.io/blog/posts/6-arm64/

And if you cant get your hands on the instruction set from the chipset manufacturer, then activities like this can help you decode the chipset instruction set.

https://www.righto.com/2026/02/8087-instruction-decoding.html

At which point your country's security service's may be taking an interest in you and your abilities... for the Lulz.


You may have gathered by now, that some tasks like reverse engineering firmware, is not a five minute job. Having knowledge of the chip, its memory and experience with writing firmware can all help to figure out what the lines of code are, and if you can get the instruction set for the chip, this can also help you decipher whats going on, because firmware is an area Anti-Virus programs can rarely check, which makes devices ideal targets for hackers.

Some of the techniques used to hide malicous code in programs can also be applied to firmware, some of those methods can be learnt here:

Mikko Hypponen: Fighting viruses, defending the net : https://www.youtube.com/watch?v=cf3zxHuSM2Y

Langner's Stuxnet Deep Dive: https://www.youtube.com/watch?v=zBjmm48zwQU

### Latest NVM Firmware

There is a post on the TP-Link website (https://community.tp-link.com/us/home/forum/topic/204238) which has a link to a later version of the QCA7420 firmware found at this address (https://community.tp-link.com/us/home/forum/topic/204238) which is purportedly ```FW-QCA7420-1.5.0.0026-02-CS-20200114.nvm```.

1st point, its not got its accompanying PIB file which is needed so that configuration settings in the PIB configure the NVM firmware and tell the NVM firmware how to work. 

2nd point, the Toolkit wont let you flash this latest version unless you have a PIB file whose manifest matches.

3rd point, the electrical components used on the Trendnet TPL-406E may not be suitable for this more modern NVM firmware. 

So find a suitable PIB and then you could give it a go, and breath new life and new functionality in the Trendnet TPL-406E powerline adapters, keeping them from being just more e-waste.

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\chknvm -m "C:\Users\admin1\Documents\Powerline Adapters\FW-QCA7420-1.5.0.0026-02-CS-20200114\FW-QCA7420-1.5.0.0026-02-CS-20200114.nvm"
------- C:\Users\admin1\Documents\Powerline Adapters\FW-QCA7420-1.5.0.0026-02-CS-20200114\FW-QCA7420-1.5.0.0026-02-CS-20200114.nvm (0) -------
        Signature: 1234ABCD
        Hardware Compatibility: QCA7420
        Chain Major Version: 1
        Chain Minor Version: 5
        Chain Type: Firmware
        Build Major Version: 1
        Build Minor Version: 5
        Build Major Subversion: 0
        Build Sustaining Release: 2
        Build Type: CS
        Manifest Version: 1
        Build Number: 26
        Build Date: 20200114
        Build Time: 141834
        Device Type: 7420
        Build Hostname: Custom
        Build Username: Custom
        Build Description: QCA7420-1.5.0 REV:02 CS 0026
        Build Version String: FW-QCA7420-1.5.0.0026-02-CS-20200114:141834-Custom:Custom-1-1.5
        Generic Identifier 0: 0
        Generic Identifier 1: 0
        Softloader Major Version: 0
        Softloader Minor Version: 1
        Manifest Free Space: 140/768 bytes
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```
