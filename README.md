# SDN-SWITCH-CN
This repository consists of the code and observations for CN orange problem submission of assigned topic 

1) SDN learning switch controller

To implement a controller that mimics a learning switch by dynamically learning MAC addresses and installing forwarding rules.
Demonstrates MAC address learning logic, Dynamic flow rule installation, Packet forwarding validation, Flow table inspection

Implementation:

Hosts (2 hosts in this case) are connected to the Switch. Initially, the switch does not know the destination mac address when a host sends a packet, so the switch forwards the packet to the Ryu controller. The controller processes the packet, learns the source MAC address, and instructs the switch to either flood the packet or install a flow rule for future packets. During the first communication between hosts, ARP broadcast and flooding are seen, indicating that the switch is learning the network and MAC addresses. After the controller installs the appropriate flow rules, subsequent communications are handled directly by the switch, resulting in efficient forwarding with reduced overhead.

Steps to Run the Project:

### 1. System Preparation

On terminal run, (to upgrade)

```bash
sudo apt update
sudo apt upgrade -y
```

---

### 2. Install Required Tools

Install Mininet

```bash
sudo apt install mininet -y
```

Install Open vSwitch

```bash
sudo apt install openvswitch-switch -y
```

Install Python dependencies

```bash
sudo apt install python3-pip -y
pip3 install --user ryu
pip3 install eventlet==0.30.2
```

---

### 3. Clean Previous Mininet State

Clear old configurations

```bash
sudo mn -c
```

---

### 4. Start the Ryu Controller

Run the learning switch controller

```bash
python3 -m ryu.cmd.manager sdnswitch.py
```

---

### 5. Start Mininet Topology

Open a new terminal and run

```bash
sudo mn --controller=remote --switch=ovsk --topo=single,3
```

This creates:

* 1 switch (s1)
* 3 hosts (h1, h2, h3)

---

### 6. Verify Connectivity

Inside the Mininet CLI

```bash
h1 ping h2
```

---

### 7. Observe Learning Behavior

Run the ping command twice

```bash
h1 ping h2
```
Observations:
* First run: ARP broadcast and flooding
* Second run: Direct forwarding using installed flow rules

---

### 8. View Flow Table

In a new terminal while Mininet is running

```bash
sudo ovs-ofctl dump-flows s1
```

---

### 9. Measure Performance

Inside Mininet

```bash
iperf
```

---
On wireshark we see:

* ARP packets during first communication
* ICMP packets after flow rules are installed

---

### 12. Exit Mininet

```bash
exit
```
Results:



