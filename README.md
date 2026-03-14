# PowerLine Adapters

[HomePlugs](https://en.wikipedia.org/wiki/HomePlug) a type of [Powerline communication (PLC) module](https://en.wikipedia.org/wiki/Power-line_communication) convert existing main's AC electrical wiring (but can work on DC wiring for EV chargers) into a stable, high-speed Ethernet network, ideal for extending the local area network into rooms with weak Wi-Fi or for other compact forms of wired communication. Homeplugs are typically sold in pairs, a four pack or an eight pack, one connects to the mains socket next to a router or switch with an ethernet cable leading from the homeplug into the router and then other homeplugs to the mains socket around the property providing wired ethernet connection to nearby devices and a reliable plug-and-play solution for various network related tasks.

Powerline Communication is not be confused with Programmable Logic Controllers (PLC) that control industrial automation processes.

This repo is dedicated to the ways the firmware can be updated, how to unbrick powerline adapters, using the Trendnet TPL-406E, but the techniques may also work with other powerline adapter's from different manufacturers using the same or similar chipsets.

For those curious about the [Power-Line communication](https://en.wikipedia.org/wiki/Power-line_communication) technology, may be surprised to learn its the same technology found in EV's and EV chargers, eg DC faster chargers (CCS) and smart AC charging to help them communicate for features like Plug & Charge, automated billing and Vehicle to Grid (V2G). This also explains why some EV charger's have problems communicating with vehicles and vice versa and then subsequently fail to charge. Other major applications include Advanced Metering Infrastructure (AMI/Smart Meters), smart street lighting control, home/building automation (HVAC, security), and solar panel monitoring/inverters.

There are potential security risks with using these HomePlug devices unless you live in a farm or mansion house on a country estate with no neighbours where the signals cant be detected passing over the mains cables.

Like all technology, there may also be other attack vectors not mentioned here.


### Wifi or PowerLine Adapters ?


Building materials that significantly block or weaken Wi-Fi signals include dense, metallic, or water-dense materials, most notably metal (steel, aluminium), concrete, brick, stone, and low-emissivity (Low-E) glass. These materials absorb, reflect, or disperse radio waves, causing high attenuation, often creating dead zones in homes or offices. 

Powerline adapters simply need reasonably sound mains electrical wiring. If used in new build houses on dense housing estates like those seen in the UK, or living in apartment blocks, the wiring can be so good with short cable runs (distances) that you can detect your neighbours powerline adapter's potentially giving yourself access to their internet connection, network and devices. [This is a potential hacking security risk](https://en.wikipedia.org/wiki/HomePlug#Security).

Off grid electrical generators will affect the powerline adapter because they introduce high electrical noise, unstable voltage and frequency variations in the building's main's wiring, so they may not work so well if at all, where as Wifi devices have power supplies which help them handled minor fluctuations in the electrical supply. The UK Telephone network also has its own independant power so in the event of a power cut, its possible to have a router running on a UPS battery backup communicating with the internet providing wifi access where as the powerline adapters will not work due to the power cut.

Generally speaking AC generates more EMI than DC, higher currents generates more EMI than higher voltages, but high voltage can still generate high amounts of EMI. The higher the Wattage, the higher the EMI and the wattage is calculated by Voltage x Amps.

This means yours mains electricity supply and electrical devices can generate the most amount of EMI, compared to Ethernet cables and copper based telephone wires. Using a typical UK Kettle which boils water rapidly compared to other countries which have kettles that boil more slowly, generates a large amount of EMI.


| Electrical Cable	    | Current Type | Voltage | Current 		| Watts  |
|-----------------------|---------|---------|---------------|--------| 
| UK Mains Electricity	| AC 	  |	240	    | 13A 			| 3000W  |
| Ethernet ([PoE++](https://en.wikipedia.org/wiki/Power_over_Ethernet))		| DC	  | 48	    | 960mA (0.96A) | 46.08W |
| Ethernet 				| DC      |	2.5		| 960mA (0.96A) | 2.4W   |
| UK telephone			| DC	  |	48		| 50mA (0.05A)  | 2.4W   |


Powerline adapters can also interfere with unshielded Ethernet and unshielded telephone cables because they emit EMI from the mains electricity cables they are plugged into. Wifi transmits at a lower power so doesnt affect unshielded ADSL telephone and ethernet cables. 

EMI can turn a 100Mbps ADSL telephone internet connection into a 20Mbps ADSL telephone internet connection, which is a significant performance drop giving you typical internet speeds last seen back in the UK in the early 00's. Likewise it can also cause devices using unshielded ethernet cables to disconnect from the LAN and throw up messages saying the device is unplugged from the LAN. [LG's TV's](https://en.wikipedia.org/wiki/WebOS) connected to the net will fail to stream content from the internet and will report the ethernet cable has been disconnected.

This can be avoided if the mains cable's they are plugged into do not run parallel within 30cm of each other with unshielded ethernet and telephone cables. Obviously [trunking](https://en.wikipedia.org/wiki/Electrical_conduit) doesnt allow cables to run parallel at least 30cm apart when mains, telephone and ethernet cables are contained inside a single trunk, which is why using shielded cables are important, but metal trunking naturally provides shielding especially when mains cable is contained in its own seperate trunks, something that is seen in state buildings built in the 50's, 60's and 70's, and older commercial buildings repurposed into industrial look apartments.

Shielded cables can typically have a foil wrapped around the cores inside the cable, or a single foil wrapped around the outer most sheath of all the cores. A cheap DIY form of shielding can be performed by wrapping kitchen baking/roasting foil around the unshielded cables where they run parallel with other unshielded cables. 

The application and budget the cable was designed for will indicate the properties of the cable, eg voltage and current seen passing over the cable and less so the electricity type (AC or DC). Other properties like the chemical composition of the cable sheaths ie Low Smoke Zero Halogen (LSOH) are regularity requirements to produce minimal, non-toxic and low visibility smoke in public building fires to help firefighters navigate around buildings on fire, colour for identification purposes and core types eg single solid copper cores where the cable is only expected to be bent or flexed into shape once or twice as its laid around building as in the case of mains electrical wiring, or small multi strand copper cores making up the equivalent diameter surface area in high flex, high bend applications like headphone cables. The reason for lots of strands in repeated high flex or high bend situations is simply because if an individual strand breaks, its lying next to another strand which may or may not be broken and so the electricity can jump the strand next to it and still travel along the length of the strands to the other end, completing the circuit.

The need to update firmware is also a necessity because bugs in firmware or configuration settings that have made it out the development lab, need addressing and new developments or improvements that need new firmware because of operational changes, like simply reducing timeout periods between different functions. The developments and improvements are often built into later revised models as this is a form of planned obsolescence especially when new global standards are agreed and rolled out. Whilst new standards are being negotiated, manufacturers will be looking at their product, trying to make sure their product meets these new standards.

People exposed to high levels of Zinc over a short period of time can feel wifi and mobile phone signals transmissions from their smart phones, tablets and other smart devices, mains electricity through cables and walls with embedded mains cables, so the use of powerline adapters can relieve that pain, whilst numerous NHS GP's ignore the condition.

### Getting Started

If you have experienced problems which have not been resolved by using the latest manufacturer's updates and tools, or its not been possible to update to the latest version shown below using the manufacturers own software, then the following will provide an alternative route which may resolve the problem(s) being experienced.

These actions were performed using a Windows 11 Pro (25H2) box to communicate with the Trendnet TPL-406e powerline adapters to update the firmware from ```1.0.0.351-06-20120608-FINAL (1.0.0-06)``` Release Date Feb 2013 to ```1.2.0.1580-02-20150902-CS (v2)``` Release Data circa Sept 2015.


[Trendnet TPL-406E Background](TrendnetTPL406E.md)

[HomePlug standards](HomePlugStandards.md)

[Firmware Basics](FirmwareBasics.md)

[Qualcomm Atheros Open Powerline Toolkit](Toolkit.md)

[Special Status Ethernet MAC Addresses](SpecialStatusMACs.md)

[Ether Types](EtherTypes.md)

### Steps to Flash Firmware using Windows

This process can take as little as ten minutes to perform, longer with a slower windows computer and/or slow internet access.

1. [Download & install Visual Studio 2026 Community edition](DownloadVisualStudio.md)

2. [Download Open PLC Utils and Build (Compile)](DownloadPLCtool.md)

3. [Open PLC Tool Documentation & The Basics](OpenPLCtoolDocumentation.md)

4. [Communicating with your Powerline Adapter reliably](AdapterComms.md)

5. [Establishing if your Adapter is soft bricked](SoftBricked.md)

6. [Getting your Adapter specs](GetSpecs.md)

7. [Backing up existing Firmware](BackupFirmware.md)

8. [Factory Reset the adapter](FactoryReset.md)

9. [Downloading the firmware](DownloadingFirmware.md)

10. [Setting the DAK and NMK with hpavkey](SetDakNMK.md)

11. [Setting the firmware PIB File with modpib](PIBFileSettings.md)

12. [Configure the firmware PIB files](ConfigurePIBfile.md)

12. [Flashing the firmware files](FlashingFirmware.md)

13. [Correct Powerline Adapter settings after Flashing](FlashedFirmware.md)


### Other areas of Interest

[JTAG, SPI and UART](JTAGspiUART.md)

[Editing the PIB file](EditingPIB.MD)

[Deciphering the .PIB file](DecipherPIBfile.md)

[Reverse Engineering the Firmware](ReverseEngineerFirmware.md)

[WireShark Network Packet Capturing](Wireshark.md)

[HUB Packet Analysis](HubCapture.md)

[Fritz Box 7530 Router & Powerline Adapters](FritzBox.md)
