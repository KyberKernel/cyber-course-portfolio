Subnetting Basics
|Decimal|Binary|Calculation Notes|
|-|-|-|
|10|`00001010`|Direct conversion|
|210|`11010010`|128 + 64 + 16 + 2|
|168|`10101000`|168 − 128 = 40 → 40 − 32 = 8 → 8 − 8 = 0|
|16|`00010000`|Direct conversion|
|255|`11111111`|All bits set|
|128|`10000000`|Direct conversion|
|192|`11000000`|128 + 64|
|248|`11111000`|Direct conversion|
|0|`00000000`|All bits zero|

### Binary to Decimal Breakdown

|Binary|Decimal|Math Breakdown|
|-|-|-|
|`11000000`|192|Direct conversion|
|`11111111`|255|Direct conversion|
|`10101000`|168|128 + 32 + 8|
|`00010000`|16|Direct conversion|
|`11111000`|248|128 + 64 + 32 + 16 + 8|
|`11010010`|210|128 + 64 + 16 + 2|

### Full Address Translations

* `10.210.168.16` → `00001010.11010010.10101000.00010000`
* `192.168.0.1` → `11000000.10101000.00000000.00000001`
* `172.16.5.100` → `10101100.00010000.00000101.01100100`
* `11000000.10101000.00000001.00000001` → `192.168.1.1`
* `00001010.00001010.00000000.01001011` → `10.10.0.75`

\---

## SECTION 2: Classful Addressing \& Subnet Masks

### Class Identification Matrix

|Target IP|Class|Dotted Mask|Prefix|
|-|-|-|-|
|10.0.0.5|A|255.0.0.0|/8|
|192.168.1.1|C|255.255.255.0|/24|
|172.16.4.20|B|255.255.0.0|/16|
|8.8.8.8|A|255.0.0.0|/8|
|200.100.50.25|C|255.255.255.0|/24|

### Subnet Mask Conversion

|Dotted-Decimal|CIDR Prefix|Binary Equivalent|
|-|-|-|
|255.255.255.0|/24|`11111111.11111111.11111111.00000000`|
|255.255.0.0|/16|`11111111.11111111.00000000.00000000`|
|255.0.0.0|/8|`11111111.00000000.00000000.00000000`|
|255.255.255.192|/26|`11111111.11111111.11111111.11000000`|
|255.255.248.0|/21|`11111111.11111111.11111000.00000000`|
|255.255.255.128|/25|`11111111.11111111.11111111.10000000`|

### Class Capacity Overview

|Class|Prefix|Possible Networks|Usable Hosts / Network|
|-|-|-|-|
|Class A|/8|128 nets|16,777,214 hosts|
|Class B|/16|16,384 nets|65,534 hosts|
|Class C|/24|2,097,152 nets|254 hosts|

\---

## SECTION 3: Network Parameter Summaries

**172.16.0.0 /16**

* Subnet Mask: `255.255.0.0`
* Network ID: `172.16.0.0`
* Default Gateway: `172.16.0.1`
* Host Address Range: `172.16.0.2` – `172.16.255.254`
* Broadcast Address: `172.16.255.255`

**10.10.0.0 /26**

* Subnet Mask: `255.255.255.192`
* Network ID: `10.10.0.0`
* Default Gateway: `10.10.0.1`
* Host Address Range: `10.10.0.2` – `10.10.0.62`
* Broadcast Address: `10.10.0.63`

**192.168.5.0 /28**

* Subnet Mask: `255.255.255.240`
* Network ID: `192.168.5.0`
* Default Gateway: `192.168.5.1`
* Host Address Range: `192.168.5.2` – `192.168.5.14`
* Broadcast Address: `192.168.5.15`

**10.0.0.0 /30**

* Subnet Mask: `255.255.255.252`
* Network ID: `10.0.0.0`
* Default Gateway: `10.0.0.1`
* Host Address Range: `10.0.0.2` – `10.0.0.2`
* Broadcast Address: `10.0.0.3`

**192.168.100.128 /25**

* Subnet Mask: `255.255.255.128`
* Network ID: `192.168.100.128`
* Default Gateway: `192.168.100.129`
* Host Address Range: `192.168.100.130` – `192.168.100.254`
* Broadcast Address: `192.168.100.255`

\---

## SECTION 4: Host Verification Audit

**Target Host: `10.10.0.75/26`**

* Network: `10.10.0.64` | Broadcast: `10.10.0.127`
* Verification: **VALID HOST**. Falls inside the `.64` subnet range (`.65` through `.126`).

**Target Host: `192.168.1.200/26`**

* Network: `192.168.1.192` | Broadcast: `192.168.1.255`
* Verification: **VALID HOST**. Sits between Network ID (`.192`) and Broadcast (`.255`).

**Target Host: `172.16.5.130/25`**

* Network: `172.16.5.128` | Broadcast: `172.16.5.255`
* Verification: **VALID HOST**. Upper-half IP inside the `/25` split block.

**Target Host: `10.0.0.0/30`**

* Network: `10.0.0.0` | Broadcast: `10.0.0.3`
* Verification: **INVALID HOST**. Represents the Network ID itself and cannot be assigned to an interface.

\---

## SECTION 5: Network Allocation \& Subnetting

### Equal Four-Way Split of `192.168.10.0/24` into `/26` Subnets

* **Subnet 1**: Network `192.168.10.0` | GW `192.168.10.1` | Range `192.168.10.2` – `192.168.10.62` | Broadcast `192.168.10.63`
* **Subnet 2**: Network `192.168.10.64` | GW `192.168.10.65` | Range `192.168.10.66` – `192.168.10.126` | Broadcast `192.168.10.127`
* **Subnet 3**: Network `192.168.10.128` | GW `192.168.10.129` | Range `192.168.10.130` – `192.168.10.190` | Broadcast `192.168.10.191`
* **Subnet 4**: Network `192.168.10.192` | GW `192.168.10.193` | Range `192.168.10.194` – `192.168.10.254` | Broadcast `192.168.10.255`

### Subnet Capacity Chart

|CIDR|Total Addresses|Usable Host Capacity|
|-|-|-|
|/24|256|254|
|/25|128|126|
|/26|64|62|
|/27|32|30|
|/28|16|14|
|/29|8|6|
|/30|4|2|

> \*\*Allocation Strategy Note:\*\* While uniform `/26` subnets accommodate all departments, variable sizing avoids address space waste:
> - \*\*Department A (50 hosts):\*\* Assign `/26` (Provides 62 usable)
> - \*\*Department B (25 hosts):\*\* Assign `/27` (Provides 30 usable)
> - \*\*Department C (10 hosts):\*\* Assign `/28` (Provides 14 usable)
> - \*\*Department D (2 hosts):\*\* Assign `/30` (Provides 2 usable)

\---

## SECTION 6: IPv6 Fundamentals

### Hexadecimal Quick Table

|Hex|Decimal|Binary|
|-|-|-|
|`0`|0|`0000`|
|`5`|5|`0101`|
|`a`|10|`1010`|
|`f`|15|`1111`|

### IPv6 Address Compression

* `2001:0df8:23f2:0000:0000:0000:0000:0f11` → `2001:df8:23f2::f11`
* `2001:0000:00d0:00f2:0000:0000:0000:0f11` → `2001:0:d0:f2::f11`
* `fe80:0000:0000:0000:0000:0000:0000:0001` → `fe80::1`

### Transition Motivation

IPv6 is necessary because IPv4 address pool depletion cannot support the global volume of connected devices. Its 128-bit structure delivers a virtually unlimited pool of unique addresses, granting devices globally routable IPs and eliminating dependence on NAT.

