# Trendnet TPL-406E Background

Trendnet is a US based company not to be confused with the the Chinese company TP-Link who also make networking products and frequently appear in search engine results when using the ```TPL``` part of the powerline adapter's model number.

The TPL-406E powerline adapter uses a Powerline Communication (PLC) System-on-Chip (SoC) with AR7420 etched on the chip.

AR stands for Atheros who were specialists in networking chipsets, and were later acquired/bought by Qualcomm a specialist in mobile phone chipsets who wanted to expand their portfolio of products. 

As a result in some documentation and software the CPU chip may be refereed to as an AR7420, AR7000 series, AR7400 series, QCA7420, QCA7000 series or Panther series chip. 

The Panther series encompasses the QCA6410, QCA7000 and QCA7240 chips.

TheTPL-406E works with the [HomePlug 1.0](https://en.wikipedia.org/wiki/HomePlug#HomePlug_1.0) & [HomePlug AV](https://en.wikipedia.org/wiki/HomePlug#HomePlug_AV) standards but not the latest [HomePlugAV2](https://en.wikipedia.org/wiki/HomePlug#HomePlug_AV2), [HomePlug Green PHY (CCS EV charging)](https://en.wikipedia.org/wiki/HomePlug#HomePlug_Green_PHY) standards and the [HomePlug Access BPL](https://en.wikipedia.org/wiki/HomePlug#HomePlug_Access_BPL) isnt really relevant for this device.

[HomePlug 1.0](https://en.wikipedia.org/wiki/HomePlug#HomePlug_1.0) is based on [IEEE-802.3](https://en.wikipedia.org/wiki/IEEE_802.3), has [ethertype](https://en.wikipedia.org/wiki/EtherType) [0x887B](https://github.com/qca/open-plc-utils/blob/46c3506453c15b873fd6ed3e76c9872cea5e143a/VisualStudioNET/include/net/ethernet.h#L64) and uses special message formats.

[HomePlug AV](https://en.wikipedia.org/wiki/HomePlug#HomePlug_AV) is based on [IEEE-802.3](https://en.wikipedia.org/wiki/IEEE_802.3), has [ethertype](https://en.wikipedia.org/wiki/EtherType) [0x88E1](https://github.com/qca/open-plc-utils/blob/46c3506453c15b873fd6ed3e76c9872cea5e143a/VisualStudioNET/include/net/ethernet.h#L65) and special message formats. A subset of those message formats are left unspecified so that chipset vendors can define message formats for their own products.

Power Line range up to 300 meters for IP access.

Twisted Pair range up to 600 meters for IP access.

Full specifications can be found at https://www.qualcomm.com/networking-infrastructure/products/ar7420


Although maximum throughput is often quoted, these apply to lab conditions in other words ideal or perfect conditions. The speeds seen with powerline adapters in a property will change constantly to reflect if they are idling or sending/receiving data. Electrical noise is caused by other indoor and outdoor electrical devices like vacuum cleaners, hair dryers, washing machines, fridges, air conditioning units, electrical pressure washers and so on, regardless of if the cable is shielded or not.

These powerline adapters will form a network group with no more than 8 devices in the group. The connections between the devices are reportedly bridges, but they wont show up in network routing tables. Its quite likely the firmware has some sort of internal network switching designed specifically for powerline adapters when restrictions like 8 devices in a network group exist, because 8 is a common number of ports (ethernet cable sockets) seen in hubs and switches.

For this repo, the chip will be interchangeably referred to as the QCA7240 or chipset, the manufacturer Qualcomm, the powerline adapter TPL-406E will be interchangeably referred as the Device, Powerline Adapter or TPL-406E.

Much of the work the device does is handled by the Qualcomm chipset, and the periphery ie mainboard, case, LED's and mains electricity components for use in different parts of the world is handled by Trendnet.

Chipsets are developed more slowly, but mainboard development occur more quickly due to components not living up to spec, better component pricing from new manufacturers or new manufacturing processes and to compensate for factors in local markets and regulation changes.

Manufacturer Specifications: https://www.trendnet.com/products/powerline-500/TPL-406E#specifications
 
Support appears to have been discontinued around 2017 so you may be able to pick up some cheap one's on Ebay to see what you learn, bring back to life and can hack.






