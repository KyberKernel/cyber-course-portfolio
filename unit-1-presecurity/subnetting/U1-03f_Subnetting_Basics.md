U1-03f Subnetting Basics
Task 1 - Binary ↔ Decimal for a Single Octet
1.1 - Decimal to Binary
Decimal	Binary
10	00001010
210	11010010
168	10101000
16	00010000
255	11111111
128	10000000
192	11000000
248	11111000
0	00000000

Work shown:

210 = 128 + 64 + 16 + 2 = 11010010
168 = 128 + 32 + 8 = 10101000
248 = 128 + 64 + 32 + 16 + 8 = 11111000
1.2 - Binary to Decimal
Binary	Decimal
11000000	192
11111111	255
10101000	168
00010000	16
11111000	248
11010010	210

Work shown:

11111111 = 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255
10101000 = 128 + 32 + 8 = 168
11010010 = 128 + 64 + 16 + 2 = 210
1.3 - Full-Address Conversion
Decimal → Binary
IPv4 Address	Binary
10.210.168.16	00001010.11010010.10101000.00010000
192.168.0.1	11000000.10101000.00000000.00000001
172.16.5.100	10101100.00010000.00000101.01100100
Binary → Dotted-Decimal
Binary	IPv4 Address
11000000.10101000.00000001.00000001	192.168.1.1
00001010.00001010.00000000.01001011	10.10.0.75
Task 2 - Recognize the Class and CIDR
2.1 - What Class Is It?
Address	Class	Default Mask (Dotted)	Default Mask (CIDR)
10.0.0.5	A	255.0.0.0	/8
192.168.1.1	C	255.255.255.0	/24
172.16.4.20	B	255.255.0.0	/16
8.8.8.8	A	255.0.0.0	/8
200.100.50.25	C	255.255.255.0	/24

Class ranges:

Class A: 1–126
Class B: 128–191
Class C: 192–223
2.2 - Mask ↔ CIDR ↔ Binary
Dotted-Decimal	CIDR	Binary (32 bits)
255.255.255.0	/24	11111111.11111111.11111111.00000000
255.255.0.0	/16	11111111.11111111.00000000.00000000
255.0.0.0	/8	11111111.00000000.00000000.00000000
255.255.255.192	/26	11111111.11111111.11111111.11000000
255.255.248.0	/21	11111111.11111111.11111000.00000000
255.255.255.128	/25	11111111.11111111.11111111.10000000
2.3 - Networks and Hosts per Class
Class	Default CIDR	Number of Possible Networks	Number of Hosts per Network
A	/8	128 nets	16,777,214 hosts
B	/16	16,384 nets	65,534 hosts
C	/24	2,097,152 nets	254 hosts
Task 3 - The Five Key Values
3.1 - 172.16.0.0/16
subnet mask:       255.255.0.0
network address:   172.16.0.0
default gateway:   172.16.0.1
host range start:  172.16.0.2
host range end:    172.16.255.254
broadcast:         172.16.255.255

3.2 - 10.10.0.0/26

A /26 has 6 host bits.

Total addresses: 2^6 = 64
Usable hosts: 64 - 2 = 62
Block size: 64
subnet mask:       255.255.255.192
network address:   10.10.0.0
default gateway:   10.10.0.1
host range start:  10.10.0.2
host range end:    10.10.0.62
broadcast:         10.10.0.63

3.3 - 192.168.5.0/28

A /28 has 4 host bits.

Total addresses: 2^4 = 16
Usable hosts: 16 - 2 = 14
Block size: 16
subnet mask:       255.255.255.240
network address:   192.168.5.0
default gateway:   192.168.5.1
host range start:  192.168.5.2
host range end:    192.168.5.14
broadcast:         192.168.5.15

3.4 - 10.0.0.0/30

A /30 has 2 host bits.

Total addresses: 2^2 = 4
Usable hosts: 4 - 2 = 2
Block size: 4
subnet mask:       255.255.255.252
network address:   10.0.0.0
default gateway:   10.0.0.1
host range start:  10.0.0.2
host range end:    10.0.0.2
broadcast:         10.0.0.3


A /30 is commonly used for point-to-point links because it provides exactly two usable host addresses.

3.5 - 192.168.100.128/25

A /25 has 7 host bits.

Total addresses: 2^7 = 128
Usable hosts: 128 - 2 = 126
Block size: 128
Network starts at .128
Broadcast is .255
subnet mask:       255.255.255.128
network address:   192.168.100.128
default gateway:   192.168.100.129
host range start:  192.168.100.130
host range end:    192.168.100.254
broadcast:         192.168.100.255

Task 4 - Which Subnet Does This Host Belong To?
4.1 - 10.10.0.75/26

A /26 has blocks of 64 addresses:

0–63
64–127
128–191
192–255


75 falls into the 64–127 block.

Network address:   10.10.0.64
Broadcast:         10.10.0.127


Valid host: Yes.

10.10.0.75 is between the network address 10.10.0.64 and broadcast address 10.10.0.127, so it is a usable host address.

4.2 - 192.168.1.200/26

A /26 has blocks of 64 addresses:

0–63
64–127
128–191
192–255


200 falls into the 192–255 block.

Network address:   192.168.1.192
Broadcast:         192.168.1.255


Valid host: Yes.

192.168.1.200 is neither the network address nor the broadcast address.

4.3 - 172.16.5.130/25

A /25 has two blocks:

0–127
128–255


130 falls into the 128–255 block.

Network address:   172.16.5.128
Broadcast:         172.16.5.255


Valid host: Yes.

172.16.5.130 is between the network and broadcast addresses.

4.4 - 10.0.0.0/30

A /30 has blocks of four addresses:

0–3
4–7
8–11
...


Therefore:

Network address:   10.0.0.0
Broadcast:         10.0.0.3


Valid host: No.

10.0.0.0 is the network address, not a usable host address.

The two usable host addresses are:

10.0.0.1
10.0.0.2

Task 5 - Slicing Up a /24

Given network:

192.168.10.0/24


A /24 contains 256 addresses.

Dividing it into four equal /26 subnets gives four blocks of 64 addresses each.

5.1 - Four Equal /26 Subnets
Subnet 1 - 192.168.10.0/26
Network address:   192.168.10.0
Default gateway:   192.168.10.1
Host range:        192.168.10.2 – 192.168.10.62
Broadcast:         192.168.10.63

Subnet 2 - 192.168.10.64/26
Network address:   192.168.10.64
Default gateway:   192.168.10.65
Host range:        192.168.10.66 – 192.168.10.126
Broadcast:         192.168.10.127

Subnet 3 - 192.168.10.128/26
Network address:   192.168.10.128
Default gateway:   192.168.10.129
Host range:        192.168.10.130 – 192.168.10.190
Broadcast:         192.168.10.191

Subnet 4 - 192.168.10.192/26
Network address:   192.168.10.192
Default gateway:   192.168.10.193
Host range:        192.168.10.194 – 192.168.10.254
Broadcast:         192.168.10.255

5.2 - Enough Hosts?
CIDR	Total Addresses	Usable Hosts
/24	256	254
/25	128	126
/26	64	62
/27	32	30
/28	16	14
/29	8	6
/30	4	2

A /26 provides 62 usable hosts, so it can fit all four departments. However, it wastes address space for the smaller departments.

Department	Required Hosts	Recommended CIDR	Usable Hosts
Department A	50	/26	62
Department B	25	/27	30
Department C	10	/28	14
Department D	2	/30	2

Justification:

Department A: /26 is required because /27 only provides 30 usable hosts.
Department B: /27 is sufficient because it provides 30 usable hosts.
Department C: /28 is sufficient because it provides 14 usable hosts.
Department D: /30 provides exactly 2 usable hosts and is suitable for a point-to-point link.
Task 6 - IPv6, Briefly
6.1 - Hex ↔ Decimal ↔ Binary Refresher
Hex	Decimal	Binary (4 bits)
0	0	0000
5	5	0101
a	10	1010
f	15	1111
6.2 - Compress These IPv6 Addresses
Address 1

Original:

2001:0df8:23f2:0000:0000:0000:0000:0f11


Compressed:

2001:df8:23f2::f11

Address 2

Original:

2001:0000:00d0:00f2:0000:0000:0000:0f11


After removing leading zeroes:

2001:0:d0:f2:0:0:0:f11


Compressed:

2001:0:d0:f2::f11

Address 3

Original:

fe80:0000:0000:0000:0000:0000:0000:0001


Compressed:

fe80::1


The :: notation can replace one consecutive run of zero groups in an IPv6 address. It can only be used once per address because using it more than once would make the original address ambiguous.

6.3 - Why Do We Need IPv6?

We need IPv6 because IPv4 has a limited number of available addresses, and the growth of the Internet has made IPv4 address exhaustion a major problem. IPv6 uses 128-bit addresses, providing a vastly larger address space so that many more devices can have unique IP addresses.
