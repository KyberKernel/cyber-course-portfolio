Assignment: Map Your Network
Connect the networking concepts from this section — IP addresses, MAC addresses, subnets, gateways, DNS, and ports — to the real machine in front of you.
By the end you'll have produced a "network profile" of your own computer and the network it sits on, using the same command-line tools security professionals reach for every day.
Part 1 — Your machine's identity

1. What are your computer's IPv4 and MAC addresses?
- IPv4 address is 192.168.1.37 and my MAC address is a4:83:e7:1b:2c:xx.

2. What is the difference between a private IP and a public IP, and why does a router use private IPs?
-private IP is used inside a local network, while a public IP is used on the internet.
The home router uses private IP addresses for the devices in the local network so they can share the same internet connection on one public IP address.

3. What is the difference between an IP address and a MAC address? Which can change, which is mostly fixed, and which OSI layers do they use?
An IP address is like a logical address that identifies my device on the network.
The MAC address is a physical address connected to hardware and is mostly fixed.
IP addresses work at OSI Layer (Network), while MAC addresses work at OSI (Data Link).

4. How many addresses are in a /24 subnet? How many are usable? What are the network and broadcast addresses for 192.168.1.37/24?
/24 subnet has 256 addresses in total and 254 usable addresses.
The network address is 192.168.1.0 and the broadcast address is 192.168.1.255.

Part 2 — Reaching the internet

1. What is your default gateway, and is it on the same subnet?
The default gateway is 192.168.1.1 and it is on the same subnet because my computer is 192.168.1.37/24 (255.255.255.0) and both addresses are in the 192.168.1.0/24 network.

2. What are the average ping times to your gateway and 1.1.1.1? Why are they different?
The average ping to my gateway was 2ms and the average ping to 1.1.1.1 was 18ms.
The gateway is faster because it is on my local network, while 1.1.1.1 is located on the internet.

3. What service lets you use example.com instead of its IP address?
The DNS lets me use example.com instead of its IP address. It translates the domain name into an IP address.

Part 3 — DNS
1. Which DNS server is your computer using?
My computer is using 192.168.1.1 as its DNS server. This is also my router.

2. What IP addresses do example.com and two other websites resolve to? Why can websites have multiple IP addresses?
example.com ----- 93.184.216.34
google.com ---- 142.250.74.14, 142.250.74.46
cloudflare.com ---- 104.16.132.229, 104.16.133.229
Some websites have multiple IP addresses because they use multiple servers.
This helps them handle more traffic and keep the website available if one server has a problem or heavy load.

3. What could someone learn from watching your DNS queries?
They could see which domain names I was looking up.
They would not see the actual HTTPS content, but they could still get an idea of which websites or services I was using.

Part 4 — Traceroute
1. How many hops are there to example.com, and what is the first hop?
There were 11 hops to example.com. The first hop was 192.168.1.1, which is my default gateway.

2. What do * * * entries mean in traceroute?
It usually means that a router did not respond to the traceroute request.

Part 5 — Listening ports
1. List the ports your machine is listening on. For each, note whether it's listening on 127.0.0.1/localhost ?
Port	Protocol	Interface
135	TCP	All interfaces
139	TCP	All interfaces
445	TCP	All interfaces
5357	TCP	All interfaces
49664	TCP	Localhost
49665	TCP	Localhost
The ports on 127.0.0.1 are only available on my own computer.
The ports on 0.0.0.0 can potentially be reached by other devices on the network.

2. What are two of these ports used for, and why does the interface matter for security?
Port 445 is commonly used for SMB file sharing and port 135 is used for Windows RPC.
A port listening only on localhost is harder for another device to reach, while a port listening on all interfaces can be accessed from the network.

3. Is your computer exposing more or fewer network-facing services than expected?
My computer has fewer network-facing services than total listening ports because some of the ports are only listening on localhost.
I was a little surprised that ports 135, 139, 445 and 5357 were network-facing, so I would check if I actually need all of them.
Network Profile
IPv4 address: 192.168.1.37
Subnet mask / CIDR: 255.255.255.0 / /24
MAC address: a4:83:e7:1b:2c:xx
Network address: 192.168.1.0
Broadcast address: 192.168.1.255
Gateway and reachability
Default gateway: 192.168.1.1
Ping to gateway: 2ms
Ping to 1.1.1.1: 18ms
DNS server: 192.168.1.1
example.com: 93.184.216.34
Path to the internet
Hops to example.com: 11
First hop: 192.168.1.1
Listening ports
Port	Protocol	Interface	Common use
135	TCP	All	Windows RPC
139	TCP	All	NetBIOS
445	TCP	All	SMB/file sharing
5357	TCP	All	Web Services for Devices
49664	TCP	Localhost	Windows service
49665	TCP	Localhost	Windows service
Reflection

The main thing that surprised me was how many services can be running on a computer without me really noticing them.
I usually just think about my computer having an IP address and connecting to the router, but there are actually a lot of things happening in the background.
The command I found most useful was ipconfig because it shows a lot of the basic network information in one place.
I can see my IP address, subnet, gateway and DNS settings, so it makes it easier to understand how my computer is connected to the internet.

Thanks for reading and giving us part of your time and have a good rest of the day :)
