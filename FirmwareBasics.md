# Firmware Basics

The QCA7420 chipset has some basic functionality built into the chip and firmware (chip code) which can be altered using a method called flashing. The chip comes with configurations for SPI, UART, and Ethernet interfaces.

Firmware for the Trendnet TPL-406E v1 adapters is found at https://downloads.trendnet.com/TPL-406E/firmware.

The firmware versions ending WW stands for World Wide, NA stands for North America, and IDA stands for Indonesia.

Different manufacturers using the QCA7420 chipset can supply the firmware in different formats.

### ```.bin``` ```.image``` Firmware files 

These are generally used for updating the Wi-Fi component of an extender (e.g., TP-Link TL-WPA4220) via the web interface, and can also contain the NVM and PIB files in one file. Analysing the file using a [Hex Editor](https://mh-nexus.de/en/hxd/) will show this. Trendnet currently do not supply a BIN file for the TPL-406e powerline adapter but do with other Trendnet devices.


### ```.nvm``` Firmware file 

An NVM (Non-Volatile Memory) firmware binary file is a raw data file containing instructions and configurations for hardware components—such as NICs, controllers, or microcontrollers—that persists even when power is removed. It is used to update or patch device behavior, typically loaded into flash or EEPROM memory.

These contain the firmware for the QCA7420 chipset itself (the part that handles data over electrical wires), and is provided by Qualcomm to manufacturers like Trendnet or TP-Link. More complicated devices like computers can have multiple chips built into a platform like a motherboard which requires NVM firmware to be updated. When this occurs, the [DTMF](https://www.dmtf.org) [Platform Level Data Model(PLDM)](https://www.dmtf.org/sites/default/files/standards/documents/DSP0240_1.2.0.pdf) is generally adhered to, in order to update individual chips. In the case of powerline adapters, the PLDM isnt generally necessary as the QCA7420 is directly monitoring the communication via the Ethernet port and the mains pins.

The QCA7420 firmware is based on a series of applets which could be likened to small programs or a series of procedures or Object Orientated Programming (OOP) class methods, that can be called by address or value in different orders to perform different functions. 


### ```.pib``` (Parameter Information Block) Firmware file  

 These contain the configuration settings for the Powerline chipset, such as region-specific data, MAC addresses, and security keys, typically configured by the powerline adapter manufacturer so QCA7420 works with the physical hardware like the mains pins and the electrical supply of the country the device is designed for. The PIB file comes in different versions which is dependant on the PLC chip in use.

| Firmware Type | Compatible PIB |
| ------------- | -------------- |
| AR7400 legacy | PIB v3         |
| QCA7420       | PIB v4         |
| QCA7500       | PIB v5+        |

PIB files are not to be confused with Microsoft Power Bi files, which sometimes appear in search engine results!

### Key Contents of a PIB v4 File

    Device Identity & Configuration: Information identifying the chipset, manufacturer, and hardware version.
    Network Membership Key (NMK): The master key for the powerline network, essential for encryption and security.
    Default Authorization Key (DAK): A key used to authorize new devices to join the network.
    MAC Address: The unique Ethernet hardware address of the PLC device.
    Prescalers & Tone Masks (RF Management): Detailed data used to control powerline signal amplitude across frequencies (1.8 MHz to 30 MHz) to comply with electromagnetic emission standards.
    SLAC Settings (Signal Level Attenuation Characterization): Settings that determine whether a device acts as a vehicle or an Electric Vehicle Supply Equipment (EVSE/charger) during Electric Vehicle charging handshakes.
    Host Interface Settings: Configurations for SPI, UART, or Ethernet interfaces.
    Checksum: A value at the end of the file used to verify data integrity.
	
### PIB v4 Structure and Technical Details

    Object-Driven Structure: The file is organized into data objects, each with specific offsets, lengths, and types (integers, arrays, or structures).
    Proprietary Format: The exact mapping of the bytes is proprietary to Qualcomm Atheros, and the structure can change between firmware revisions.
    Manipulation: Tools like open-plc-utils (specifically getpib, setpib, modpib, and xml2pib) are used to read or modify these files.
    Prescaler Format: Prescalers often appear in a two-column ASCII format, representing index and amplitude attenuation values (00-FF)
	
The TPL-406E powerline adapters do not have any WiFi functionality so the ```.bin``` file is not needed, but other homeplug models have wifi built in enabling the creation of mesh networks. This also suggests the firmware is shared with device's that may may still be supported years later making it possible to extract the NVM and PIB file from the .bin file and bring the powerline adapaters firmware up to date.

The TP-Link TL-PWPA4220 which uses Wifi uses the same QCA7240 chip as the Trendnet TPL-406E for example.




