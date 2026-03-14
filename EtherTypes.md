# Ether Types

Ether Types are a 2 byte (16bit) value found in the Ethernet 2 Packet Frame Headers which are used to identify the type of data being sent. In other words Ethertypes identify the Network Layer Protocol eg IPv4, IPv6, Arp, Vlan, & HomePlug that is encapsulated in the payload.

A full list for all registered applications of the Ethertypes can be found at https://standards-oui.ieee.org/ethertype/eth.txt

| EtherType | Name| Comment | 
|-----------|-----|---------|
| 0x8878 | HomePlug 1.0 | US based Lucent : No Longer Used |
| 0x88e1 | HomePlug AV | US based  HomePlug Powerline Alliance, Inc. : Current |
| 0x8100 | Vlan | Customer VLAN Tag (C-TAG) as defined in IEEE Std 802.1Q |
| 0x88a8 | Vlan | Service VLAN Tag (S-TAG) or Backbone VLAN Tag (B-TAG) as defined in IEEE Std 802.1Q |
| 0x88F5 | Vlan | Multiple VLAN Registration Protocol (MVRP) defined in IEEE Std 802.1Q |
| 0x8912 | Fritz Box | Barcelona based : MediaXtream a proprietary powerline communication (PLC) technology developed by Gigle Networks |


The Ether Types are used in WireShark Protocol capture filters which is described here [WireShark Packet Capturing](Wireshark.md#wireshark-capture-filters)