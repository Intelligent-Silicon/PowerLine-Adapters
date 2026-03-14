# Deciphering the .PIB file

In most standard Qualcomm Atheros (QCA) PIBs (like those for the QCA7000, QCA7420, or QCA6410), country-specific behaviour is governed by a combination of a Country Code byte and a Tone Mask.

The firmware available on the Trendnet website https://downloads.trendnet.com/TPL-406E/firmware/ comes in three regional variations:

The filename ends in either WW, NA or IDA which means:

WW = World Wide

NA = North America

IDA = Indonesia

Be sure to download the correct version for your country unless you are looking for regional differences.


### 1. The Country Code Byte
The literal "Country Code" is typically located at offset 0x0024 in the PIB, but for reasons outlined here https://github.com/qca/open-plc-utils/pull/33#issuecomment-94879769, the PIB structure now changes for each chip, so the offset address shouldnt be relied upon from Ai with access to older documentation or older devices, but when dealing with tech, you can treat this as an almost certain constant, that the United States will always try to be first, as seen in the list below as well in things like international telephone country codes. 

With things like that in mind, you may be able to decipher the PIB file, but its layout does change between chips. Identifying the objects from within is key. Likewise don’t just look at Trendnet documents and tools, look at others manufacturers that use the Qualcomm chips, like TP-Link. Many manufacturers and support staff will leak pertinent information, often faster than a leaky sieve because they are NOT used to dealing with secrets let along national secrets! Hence the saying Need to know basis.

```
    Location: 0x0024 (1 byte)
    Common Values:
        0x00: North America (FCC)
        0x01: Europe (CE/ETSI)
        0x02: Japan
        0x03: United Kingdom
```

You can check this value using the getpib utility:

```
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\getpib "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\FW_TPL-406Ev2.pib" 0024 byte
84
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

In this example for the QCA7420, it appears the offset address is perhaps not accurate or maybe it is, if you read on...

### 2. The Tone Mask (Frequency Control)

This information maybe relevant to PIB file intended for a chip that is not the QCA7420, but gives you an idea of what sorts of things to look for.

Simply changing the country code byte often isn't enough to make a device compliant. The device also uses a Tone Mask, which defines which sub-carrier frequencies are "notched out" (muted) to prevent interference with local amateur radio or emergency bands.

    Standard Location: Offsets starting around 0x0084.
    Structure: This is a Long datatype (4 bytes) bitmask. If a bit is set to 0, the device will not transmit on that specific frequency.
	
### 3. Prescalers (Power Levels)

The "Regulatory Power Level" is controlled by Prescalers. These are maps that tell the chip how much power to output for each frequency band and could be useful for reducing power to reduce interference or increase power for long cable runs.

    Location: These are usually stored in a large block starting at offset 0x0438 (though this varies significantly between firmware versions).

    Management: Use the psin and psout utilities to extract these as text files, modify them, and re-insert them.

How to change it safely

If you have a known-good PIB file for your target region (e.g., europe.pib), the safest way to "convert" a device is to use the chkpib utility to verify your current one, then use setpib to modify the offset:

```
Set country code to Europe (0x01) at offset 0x0024
setpib filename.pib 0024 byte 01
```
Warning: If you set a country code that doesn't match the internal Tone Mask or Prescalers already in the file, the firmware might reject the PIB as "corrupt" or "invalid" during the boot process.
