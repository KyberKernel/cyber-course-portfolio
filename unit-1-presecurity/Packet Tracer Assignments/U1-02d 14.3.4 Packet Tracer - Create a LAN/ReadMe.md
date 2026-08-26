Part 1 – Connect Network Devices and Hosts
Step 1: Power on the devices

I opened the Physical tab for the end devices and the Office Router.

I turned on the devices using the power switch. I checked that the green power LED appeared.

The switch did not have a power switch, so no power button was required for it.

Step 2: Connect the network devices

I selected the Copper Straight-Through cable and connected the devices according to the required connections.

I made the following connections:

Device	Port	Connected To	Port
Office Router	G0/0	ISP1	G0/0
Office Router	G0/1	Switch	G0/1
Admin PC	F0	Switch	F0/1
Manager PC	F0	Switch	F0/2
Printer	F0	Switch	F0/24

After connecting the devices, I waited for the links to initialize. The connection indicators changed to green, confirming that the physical connections were working.

Part 2 – Configure Devices with IPv4 Addressing
Step 1: Configure the Admin PC

I opened the Admin PC and selected:

Desktop → IP Configuration

I selected DHCP.

The PC automatically received its IPv4 configuration from the network.

Step 2: Configure the Manager PC

I opened the Manager PC and went to:

Desktop → IP Configuration

I also selected DHCP.

The Manager PC automatically received its IPv4 configuration.

Step 3: Configure the Printer

I opened the Printer and selected:

Config → FastEthernet0

I manually entered:

IP Address: 192.168.1.100
Subnet Mask: 255.255.255.0

I used a static IP address for the printer because a printer should normally have a predictable address so that other devices can easily reach it.

Addressing Table
Device	Interface	IPv4 Address	Subnet Mask
Admin PC	NIC	DHCP	—
Manager PC	NIC	DHCP	—
Printer	NIC	192.168.1.100	255.255.255.0
www.cisco.pt	NIC	209.165.200.225	—
Discussion Question 1
Why are the IPv4 addresses of the two PCs different, while their subnet mask and default gateway are the same?

The two PCs have different IPv4 addresses because every device on the network needs a unique IP address.

The subnet mask is the same because both PCs are connected to the same LAN. The default gateway is also the same because both PCs use the same router to communicate with devices outside their local network.

Discussion Question 2
The printer does not need a default gateway since it is only accessed locally. If one were required, what value would be used?

The default gateway would be the IP address of the LAN interface of the Office Router.

I could determine this address by checking the default gateway that the PCs received through DHCP. Since the devices are on the same LAN, they use the router's LAN interface as their gateway.

Part 3 – Verify End Device Configuration and Connectivity
Step 1: Check the PC configurations

I checked the IP configuration of both PCs.

Both PCs received IPv4 addresses from the 192.168.1.0/24 network through DHCP.

They also received the required default gateway and DNS information.

This confirmed that DHCP was working correctly.

Step 2: Test connectivity to the printer

From the Admin PC, I opened the Command Prompt and entered:

ping 192.168.1.100


The ping was successful.

I then repeated the same test from the Manager PC:

ping 192.168.1.100


The ping was also successful.

This confirmed that the PCs could communicate with the printer over the local network.

Step 3: Test the web server using its IP address

I opened the web browser on the Admin PC and entered the IP address of the web server.

The server was reachable.

I repeated the test from the Manager PC, and the server was also reachable.

Step 4: Test the web server using its URL

I entered the web server's URL into the browser.

The web page loaded successfully.

This showed that the network had both connectivity to the remote server and working DNS resolution.

Discussion Question 3
If the server is reachable by IP address but not by URL, what is the likely cause?

The likely cause is a DNS problem.

DNS translates a website name or URL into an IP address. If the IP address works but the URL does not, the DNS server may be unreachable or the computer may have an incorrect DNS server configuration.

Part 4 – Use Networking Commands to View Host Information
Step 1: Use the ipconfig command

I opened the Command Prompt on a PC and entered:

ipconfig


The command displayed the basic IPv4 configuration of the PC.

The information included:

IPv4 address
Subnet mask
Default gateway

This allowed me to verify the network configuration from the command line.

Step 2: Use the ipconfig /all command

I then entered:

ipconfig /all


This command displayed more detailed information about the network adapter.

The information included:

IPv4 address
Subnet mask
Default gateway
MAC address
DHCP server
DNS server

This command was useful for viewing the complete network configuration of the PC.

Step 3: Use the tracert command

I used the tracert command to determine the path from the PC to the remote web server.

The command showed the routers that the traffic passed through before reaching the destination.

Question: How many routers were passed, and how were they identified?

I found that two routers were passed.

They were identified by the IP addresses of the router interfaces that received the incoming traffic.

Question: Where is the second router located?

The second router is located inside the Internet cloud.

7. Reflection
What is the biggest facilities challenge when setting up a LAN in a new office?

In my opinion, the biggest challenge is the physical cabling infrastructure.

The office needs network outlets in convenient locations for computers, printers, and other devices. These outlets then need to be connected back to a central location where the switch and router are installed.

Installing network cables can take a lot of time and may require cables to be routed through walls, ceilings, or other parts of the building. Therefore, planning the physical network before the office opens is very important.

8. Conclusion

In this lab, I created a small branch-office LAN step by step.

First, I powered on the network devices and connected the Office Router, ISP1, switch, Admin PC, Manager PC, and Printer using copper straight-through cables.

Next, I configured the Admin PC and Manager PC to obtain their IPv4 addresses automatically using DHCP. I configured the Printer manually with the static IP address 192.168.1.100 and subnet mask 255.255.255.0.

After configuring the devices, I tested connectivity using the ping command. Both PCs were able to successfully communicate with the printer.

I then tested the remote web server using both its IP address and URL. Finally, I used ipconfig, ipconfig /all, and tracert to examine the network configuration and the path to the remote server.

From this lab, I learned how DHCP, IPv4 addressing, subnet masks, default gateways, DNS, switches, routers, and network troubleshooting commands work together to create and verify a functioning LAN.
