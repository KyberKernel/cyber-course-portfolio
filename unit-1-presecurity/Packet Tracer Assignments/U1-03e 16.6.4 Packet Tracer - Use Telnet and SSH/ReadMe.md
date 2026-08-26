Part 1 – Verify Connectivity
Step 1: Verify the IP Address on PC0
I selected PC0 from the Packet Tracer topology.

I opened the Desktop tab and selected Command Prompt.

I used the following command to check the IP configuration:

C:\> ipconfig

PC0 displayed the following network information:

IPv4 Address:    192.168.1.12
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.1.1

This confirmed that PC0 successfully received an IPv4 address from DHCP.

Command Used
ipconfig

The ipconfig command allowed me to verify the IPv4 address, subnet mask, and default gateway assigned to PC0.

Step 2: Verify Connectivity to the HQ Router
Next, I tested the connection between PC0 and the HQ router.

The IP address of the HQ router is:

64.100.1.1

From the PC0 Command Prompt, I entered:

C:\> ping 64.100.1.1

The ping was successful.

This confirmed that PC0 could communicate with the HQ router and that the network connection was working correctly.

Part 2 – Access the Remote Device
Step 1: Attempt to Connect Using Telnet
After verifying connectivity from PC0, I attempted to access the HQ router using Telnet.

I entered:

C:\> telnet 64.100.1.1

The connection initially opened, but the HQ router immediately closed the connection.

The result was:

Trying 64.100.1.1 ...Open

[Connection to 64.100.1.1 closed by foreign host]

Was the Telnet connection successful?
No.

The Telnet connection was not successful because the HQ router was configured not to allow Telnet access.

Telnet is considered insecure because it does not encrypt the information sent between the computer and the network device.

Part 3 – Connect Using SSH
Step 1: Start an SSH Connection
Because Telnet was not allowed, I used SSH to securely access the HQ router.

From PC0, I entered:

C:\> ssh -l admin 64.100.1.1

The -l admin option specifies that I was connecting with the username admin.

Step 2: Enter the Password
The router asked me for the password.

I entered:

class

The login was successful.

Step 3: Verify the Router Prompt
After successfully connecting to the router, the command prompt changed to:

HQ#

The HQ# prompt confirmed that I was successfully connected to the HQ router using SSH.

4. Commands Used
Command	Purpose
ipconfig	Checks the IP configuration of PC0
ping 64.100.1.1	Tests connectivity to the HQ router
telnet 64.100.1.1	Attempts remote access using Telnet
ssh -l admin 64.100.1.1	Connects securely to the router using SSH
class	Password used for the SSH login

5. Results
The lab was completed using PC0.

PC0 successfully received an IP address through DHCP.
PC0 successfully pinged the HQ router at 64.100.1.1.
Telnet access was unsuccessful because the router did not allow Telnet.
SSH access was successful.
The final router prompt was HQ#.
6. What I Learned
In this lab, I learned how to verify a computer's IP configuration and establish remote access to a router.

I first used PC0 and the ipconfig command to verify that it received an IPv4 address through DHCP. I then used ping to make sure PC0 could reach the HQ router.

After confirming connectivity, I tried Telnet. The connection was closed by the router because Telnet was disabled for security reasons.

I then used SSH:

ssh -l admin 64.100.1.1

After entering the password class, I successfully accessed the router and received the HQ# prompt.

This showed me that SSH should be used instead of Telnet when secure remote management is required.
