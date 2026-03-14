# Special Status Ethernet MAC Addresses

When using the Toolkit, various programs will show their output and special MAC ID's or MAC Addresses will be shown in this output.

These MAC ID's are built into the firmware so cant be changed so they can differentiate commands that can be sent to foreign (not within a Network Membership Key (NMK) group, remote (within a NMK group) or local (ethernet cable plugged direct into a Windows or Linux computer) and they can indicate the state the device. 


### [Your Device Mac ID]

Functioning properly but you could have still misconfigured it like NOT sharing the NMK to participating powerline adapters to form a group. This device MAC ID is whats normally found on the label stuck to the back of the device, unless its been changed by a PIB file using the Force Flash (-FF) method.

### local

see 00:B0:52:00:00:01 - "local" is a synonym for the Qualcomm Atheros (vendor specific) Local Management Address (LMA). All local (plugged in directly) Atheros devices will respond to this address but remote and foreign devices will not.

### 00:B0:52:00:00:01

The Local Management Address (LMA) also know as the Default Bootloader Device Address for sending commands direct to the QCA7420 when the device is plugged in directly to the computer, but remote and foreign devices will not respond.
 
Output coming from this MAC ID can also mean no PIB was stored in NVRAM so the generic Atheros PIB was, or you downloaded and flashed the generic Atheros PIB without changing the MAC address to the device MAC ID beforehand. 


### 00:B0:52:00:00:03

Output from this MAC ID indicates the Default PIB is used when no other PIB is available or stored in NVRAM. The Default PIB disables communication over powerline. Use MODPIB to change the Network Membership Key (NMK), Device Access Key (DAK) and set the MAC ID in the PIB file to the powerline adapters MAC ID. You can examine the PIB file in a Hex Editor to see these before and after changes.

### 00:B0:52:00:00:06

Output has been seen coming from this MAC ID but no explanation can be found online, other than its appeared in examples when force flashing firmware, which could suggest the MAC ID is specified in the PIB used.

