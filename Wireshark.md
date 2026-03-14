# WireShark Network Packet Capturing

Wireshark is a tool which captures the data sent over Ethernet cables, USB cables, Wifi & Bluetooth.


### Wireshark Capture Filters

In order to capture the data sent to or from the Powerline Adapters using Wireshark, its advisable to create a Capture Filter. As the name suggests, when capturing network traffic, selecting a Capture Filter, will filter out all the other network packet communications that not necessary, and there's a lot of network traffic.

The Ether Type protocols are described here [Ether Types](EtherTypes.md)

Wireshark -> Capture -> "Capture filter for selected interfaces" -> + button to add a new Capture Filter

Filter Name: ```PowerLine Comms```

Filter Expression: ```ether proto 0x8878 or ether proto 0x88e1```

The Filter Expression changes its background from a maroon to a green colour when the filter expression is correct. If it remains maroon coloured, there is a problem with the filter expression.

Click the OK button to save and close the window.

Because some powerline adapters can work with Vlans including these TPL-406E's, the Vlan Ether Types 0x88a8 can be included in the Filter Expression (see below) if Vlans are being used over the devices.

Filter Expression with Vlan: ```ether proto 0x8878 or ether proto 0x88e1 or ether proto 0x8100 or ether proto 0x88a8 or ether proto 0x88F5```

### WireShark Packet Captures

Wireshark -> Capture -> Options

The Capture Window shows all the interfaces that data can captured on. 

Input Tab.

Select the Ethernet adapters that are directly plugged into the powerline adapter(s), in this case Ethernet and Ethernet 2.

When selecting an interface, click the green ribbon button thats next to the drop down listbox prompt: Capture filter for selected interfaces. 

Select the entry: ```PowerLine Comms: ether proto 0x8878 or ether proto 0x88e1```

If at any time you want to unselect the filter, do not use the option: ```Remove this filter``` at the top of this drop down list because it will delete this capture filter and you will need to create it again, instead use the X button on the right of the drop down list box to clear it.

If the Checkbox titled: ```Enable Promiscuous mode on all interfaces``` is enabled, its preferable to click this option so its ticked.

Promiscuous mode enables a network interface card (NIC) to capture all data packets passing through a network segment, rather than just those addressed to the specific NIC. In other words, Promiscuous mode lets you be a bystander observing all passing (network) traffic on a "road" instead of just seeing what comes in or out of a building door (network interface card). As always, sometimes you can see the content of the network traffic, like passengers on a bus (unencrypted data), and sometimes you cant see the contents inside a lorry (encrypted data)l or when observing people going in and out of a building door, encrypted data is like not being able to see the contents of an opaque bag, and unencrypted data is like being able to see whats in a transparent bag. 

Promiscuous mode has its limitations though, because it only really works if the network is a using a hub or router which sends all network packets down all network cables. Hub's and routers which work like this are generally the cheapest to buy, because it requires virtually no effort to configure the network in the firmware, its just plug and play. 

An Unmanaged switch and more expensive routers, whilst a little more expensive also requires no effort to configure, still effectively plug and play, but it does identify the network traffic data and directs it down the correct cable instead of broadcasting the packet data to all ports. Therefore Promiscuous mode wont capture any passing network traffic destined for other locations. 

A Managed Switch also directs network traffic down the correct network cable, and its default configuration is that of an unmanaged switch but provides an web and/or command line interface that allows more network routing configurations to be set up. Again Promiscuous mode wont capture any passing network traffic destined for other locations but a Managed switch usually offers the facility to capture all network data passing to or from the Managed switch and output the data on a dedicated network cable which is what Wireshark and other packet capture software can capture for later analysis. Some switches will also capture the packets internally for short bursts. A managed switch outputting all packets from all ports to a single port will almost certainly see some performance degradation when under load, just like 3 lanes of motorway into one lane of motorway see's traffic flows slow down.

Once you have setup the Capture Filter on each NIC (Ethernet and Ethernet 2), with Promiscuous mode ticked for both, click the start button. 

Run the commands you want to examine the packets for like ```.\plctool -i6 -t500 -Iarm 00:00:00:00:00:AA```.

We can stop the capture any time we like by clicking the Red Square in the top left of the toolbar.

After stopping the capture, you can save the captured data to a file for later analysis. 

Use WireShak -> File -> Save As -> [Year][Month][Day] [Hour][Mins] [Brief Description of type of Capture]

Then click the Save button.

This saves the packet capture for later analysis.










