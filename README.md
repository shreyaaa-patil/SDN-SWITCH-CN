# SDN-SWITCH-CN
This repository consists of the code and observations for CN orange problem submission of assigned topic 

1) SDN learning switch controller

To implement a controller that mimics a learning switch by dynamically learning MAC addresses and installing forwarding rules.
Demonstrates MAC address learning logic, Dynamic flow rule installation, Packet forwarding validation, Flow table inspection

Implementation:

Hosts (2 hosts in this case) are connected to the Switch. Initially, the switch does not know the destination mac address when a host sends a packet, so the switch forwards the packet to the Ryu controller. The controller processes the packet, learns the source MAC address, and instructs the switch to either flood the packet or install a flow rule for future packets. During the first communication between hosts, ARP broadcast and flooding are seen, indicating that the switch is learning the network and MAC addresses. After the controller installs the appropriate flow rules, subsequent communications are handled directly by the switch, resulting in efficient forwarding with reduced overhead.