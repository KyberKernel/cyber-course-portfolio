Part 1: Local Network Communication
Step 1: Open the Command Prompt

I selected the host with the IP address 172.16.31.3 and opened the Command Prompt.

I entered:

ping 172.16.31.2


This sent ICMP echo request packets from 172.16.31.3 to 172.16.31.2.

Because both devices are on the same network, the communication did not need to go through a router or default gateway.

Step 2: Switch to Simulation Mode

I switched Packet Tracer from Realtime Mode to Simulation Mode.

I ran the ping command again:

ping 172.16.31.2


An envelope appeared next to the source device. The envelope represented the PDU that was being sent through the network.

Step 3: Examine the First PDU

I clicked the PDU and looked at the OSI Model and Outbound PDU Details tabs.

The information was:

Device: 172.16.31.3
Source MAC: 0060.7036.2849
Destination MAC: 000C:85CC:1DA7
Source IPv4: 172.16.31.3
Destination IPv4: 172.16.31.2

This showed me that the Ethernet frame was being sent directly from the source host to the destination host because both devices were on the same local network.

Step 4: Follow the PDU

I clicked Capture / Forward to move the PDU through the network.

I recorded the information at each step.

Device	Source MAC	Destination MAC	Source IPv4	Destination IPv4
172.16.31.3	0060.7036.2849	000C:85CC:1DA7	172.16.31.3	172.16.31.2
Switch 2	0060.7036.2849	000C:85CC:1DA7	N/A	N/A
172.16.31.2 (in)	000C:85CC:1DA7	000C:85CC:1DA7	172.16.31.3	172.16.31.2
172.16.31.2 (out)	0060.7036.2849	0060.7036.2849	172.16.31.2	172.16.31.3
Step 5: Examine the Echo Reply

When the destination received the ping, it sent an ICMP echo-reply back to 172.16.31.3.

I noticed that the source and destination addresses were reversed.

The reason is that 172.16.31.2 is now the sender, while 172.16.31.3 is now the receiver.

Therefore, the source and destination addresses change for the reply.

Part 2: Remote Network Communication
Step 1: Return to the Command Prompt

I returned to the Command Prompt on host 172.16.31.3.

This time, I entered:

ping 10.10.10.2


This was different from Part 1 because 10.10.10.2 is on a different network.

The source is on:

172.16.31.0/24

The destination is on:

10.10.10.0/24

Therefore, a router was required.

Step 2: Switch to Simulation Mode

I switched back to Simulation Mode and ran the ping again.

An envelope appeared next to 172.16.31.3.

I clicked the PDU and examined the addressing information.

The PDU contained:

Source MAC: 0060.7036.2849
Destination MAC: 00D0:BA8E:741A
Source IPv4: 172.16.31.3
Destination IPv4: 10.10.10.2
Step 3: Identify the Destination MAC Address

I checked the router's interface information.

The destination MAC address 00D0:BA8E:741A belongs to the router's FastEthernet1/0 interface.

This made sense because the destination was on a remote network. Instead of sending the Ethernet frame directly to 10.10.10.2, the computer sent it to its default gateway, which was the router.

Step 4: Follow the PDU to the Router

I repeatedly clicked Capture / Forward and watched the PDU move through the network.

I recorded the information at each point.

Device	Source MAC	Destination MAC	Source IPv4	Destination IPv4
172.16.31.3	0060.7036.2849	00D0:BA8E:741A	172.16.31.3	10.10.10.2
Switch 2	0060.7036.2849	00D0:BA8E:741A	N/A	N/A
Router (in)	0060.7036.2849	00D0:BA8E:741A	172.16.31.3	10.10.10.2
Router (out)	00D0:588C:2401	0060:2F84:4AB6	172.16.31.3	10.10.10.2
Switch 1	00D0:588C:2401	0060:2F84:4AB6	N/A	N/A
Access Point	N/A	N/A	N/A	N/A
10.10.10.2	0060:2F84:4AB6	00D0:588C:2401	10.10.10.2	172.16.31.5
Step 5: Observe What Happened at the Router

The most important thing I noticed was that the MAC addresses changed at the router.

Before the router, the frame used:

Source MAC: 0060.7036.2849
Destination MAC: 00D0:BA8E:741A

After the router, the frame used:

Source MAC: 00D0:588C:2401
Destination MAC: 0060:2F84:4AB6

The IPv4 addresses remained the same during the request.

This showed me that routers remove the old Layer 2 frame and create a new Layer 2 frame for the next network.

Step 6: Follow the Echo Reply

I then followed the echo-reply from 10.10.10.2 back toward 172.16.31.3.

The reply contained:

Device	Source MAC	Destination MAC	Source IPv4	Destination IPv4
10.10.10.2	0060:2F84:4AB6	00D0:588C:2401	10.10.10.2	172.16.31.3
Access Point	N/A	N/A	N/A	N/A
Switch 1	0060:2F84:4AB6	00D0:588C:2401	N/A	N/A
Router (in)	0060:2F84:4AB6	00D0:588C:2401	10.10.10.2	172.16.31.3
Router (out)	00D0:BA8E:741A	0060:7036.2849	10.10.10.2	172.16.31.3
Switch 2	00D0:BA8E:741A	0060.7036.2849	N/A	N/A

I noticed that the IPv4 source and destination addresses were reversed because 10.10.10.2 was now sending the reply to 172.16.31.3.

The MAC addresses also changed again when the reply passed through the router.

Reflection Questions
What different types of cables/media were used?

I observed copper, fiber, and wireless connections in the topology.

Did the cables change the handling of the PDU?

No. The type of cable did not change the addressing or the basic handling of the PDU.

Did the wireless Access Point do anything to the PDUs?

Yes. The access point repackaged the data into wireless 802.11 frames.

Was PDU addressing changed by the Access Point?

No. The addressing information was not changed by the access point.

What was the highest OSI layer that the Access Point used?

The highest layer observed for the access point was Layer 1, the Physical layer.

At what OSI layer do cables and access points operate?

They operate at Layer 1, the Physical layer.

Which MAC address appeared first in the PDU Details tab?

The destination MAC address appeared first.

What do the red Xs and green check marks mean?

The red X means that the device did not accept the PDU because the destination MAC address did not match the device's MAC address.

The green check mark means that the PDU was accepted by the device.

Where did the MAC addresses change?

The MAC addresses changed when the PDU passed through the router.

Which device uses MAC addresses beginning with 00D0:BA?

The router uses the MAC addresses beginning with 00D0:BA.

What did the other MAC addresses belong to?

The other MAC addresses belonged to the sending and receiving devices and their interfaces.

Did the IPv4 addresses change?

No. The source and destination IPv4 addresses stayed the same while the original packet traveled through the network.

What happens to the source and destination addresses in the ping reply?

They switch because the device that originally received the ping becomes the source of the reply.

Why are the router interfaces part of two different IP networks?

The router connects two different IP networks. Therefore, each router interface needs to belong to a different network so that it can communicate with both networks and forward traffic between them.

Which IP networks are connected by the router?

The router connects:

172.16.31.0/24
10.10.10.0/24
Conclusion

After completing the Packet Tracer simulation, I learned how MAC addresses and IPv4 addresses work together when data travels through a network.

For the local communication, 172.16.31.3 communicated directly with 172.16.31.2 because both devices were on the same network. The frame was addressed directly to the destination device's MAC address, so a router was not required.

For the remote communication, 172.16.31.3 needed to communicate with 10.10.10.2, which was on another network. In this case, the source device sent the frame to the router's MAC address. When the router received the frame, it created a new frame for the next network. This caused the MAC addresses to change, while the IPv4 addresses remained the same.

When the destination sent the ping reply, the source and destination IPv4 addresses were reversed. The MAC addresses were also changed again when the reply passed through the router.

Overall, this activity helped me understand that MAC addresses are used for communication on the local network segment, while IPv4 addresses identify the source and destination networks across the entire communication path
