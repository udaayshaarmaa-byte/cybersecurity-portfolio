1\. Star Topology

A network where all devices are connected to a central device such as a switch or hub.

Working: Data is sent from a device to the central device, which forwards it to the destination.

&#x20;Advantages: Scalable, reliable, easy to add devices

&#x20;Disadvantages: Expensive, high maintenance, central device failure affects entire network

2\. Bus Topology

A network that uses a single backbone cable to connect all devices.

Working: Data travels along the backbone and is received by all devices.

&#x20;Advantages: Low cost, easy setup

&#x20;Disadvantages: Bottlenecks, difficult troubleshooting, single point of failure

3\. Ring Topology

Devices are connected in a circular loop where each device connects to two others.

Working: Data travels in one direction and passes through devices until it reaches its destination.

&#x20;Advantages: Less congestion, easier fault detection

&#x20;Disadvantages: Slow, entire network fails if one device/cable breaks

4\. Switch

A device that connects multiple devices in a network and forwards data only to the intended recipient.

&#x20;Uses ports to connect devices

&#x20;Tracks device locations (MAC addresses)

&#x20;Reduces network traffic compared to hubs

5\. Router

A device that connects different networks and directs data between them.

Routing: Process of determining the best path for data between networks.

6\. Subnetting

The process of dividing a large network into smaller sub-networks.

Benefits: Efficiency, security, better control

IP Address Components

* &#x20;Network Address: Identifies the network (e.g., 192.168.1.0)
* &#x20;Host Address: Identifies a device (e.g., 192.168.1.100)
* &#x20;Default Gateway: Connects to other networks (e.g., 192.168.1.254)

Example: A company may divide its network into departments such as HR, Finance, and Accounting

using subnetting.

7. Address Resolution Protocol (ARP)

ARP is used to map an IP address to a MAC address within a network.

Purpose: Allows devices to identify each other physically using MAC addresses.

&#x20;Each device maintains an ARP cache (table of IP-MAC mappings)

&#x20;Used when a device wants to communicate within the same network

How ARP Works

* &#x20;ARP Request: Broadcast asking 'Who has this IP address?'
* &#x20;ARP Reply: Device with that IP responds with its MAC address
* &#x20;Mapping is stored in ARP cache for future communication

8\. Dynamic Host Configuration Protocol (DHCP)

DHCP automatically assigns IP addresses to devices on a network.

DHCP Process (DORA)

* &#x20;Discover: Device searches for DHCP server
* &#x20;Offer: Server offers an IP address
* &#x20;Request: Device requests the offered IP
* &#x20;Acknowledge (ACK): Server confirms assignment

If DHCP is not used, IP addresses must be assigned manually.

