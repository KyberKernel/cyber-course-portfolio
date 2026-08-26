Part 1: Setting Up the Network Topology
First, I opened Cisco Packet Tracer and added three generic PCs to the workspace. I used PC0, PC1, and PC2.

Next, I connected each PC to an Ethernet port on the wireless router. I used straight-through Ethernet cables for all three connections.

I waited for the connection lights to change from amber to green. Once all of the lights were green, the PCs were connected correctly to the router.

Part 2: Observing the Default DHCP Settings
I started by checking the DHCP settings on PC0.

I clicked PC0.
I selected the Desktop tab.
I opened IP Configuration.
I selected DHCP.
PC0 automatically received an IP address from the router. I checked the default gateway and recorded it as:

Default Gateway: 192.168.0.1

I then closed the IP Configuration window.

Next, I opened the Web Browser on PC0. I entered 192.168.0.1 into the address bar.

The router asked me for a username and password. I entered:

Username: admin
Password: admin
After logging in, I looked through the Basic Setup page. I noticed that DHCP was enabled by default. I also saw the starting IP address for the DHCP range and the number of addresses that could be assigned to clients.

Part 3: Changing the Router IP Address
Next, I changed the IP address of the wireless router.

I went to the Router IP Settings section.
I changed the router IP address from the default network to:
192.168.5.1

I scrolled to the bottom of the page.
I clicked Save Settings.
After saving the settings, the web page displayed an error message. This was expected because I had changed the router's IP address.

I closed the web browser.

I then renewed the IP address on PC0:

I opened IP Configuration.
I selected Static.
I selected DHCP again.
This allowed PC0 to request new IP information from the router using the new network.

I opened the web browser again and entered the new router address:

192.168.5.1

When prompted, I entered:

Username: admin
Password: admin
I was able to access the router's configuration page again.

Part 4: Changing the DHCP Address Range
After changing the router's IP address, I checked the DHCP settings again.

I noticed that the DHCP Server Start IP Address had automatically changed to the new network, which was the 192.168.5.x network.

I then changed the DHCP settings.

The starting IP address was changed from:

192.168.5.100

to:

192.168.5.126

I also changed the Maximum Number of Users to:

75

I scrolled to the bottom of the page and clicked Save Settings.

I then closed the web browser.

To make PC0 request a new address, I opened IP Configuration, selected Static, and then selected DHCP again.

After that, I opened the Command Prompt and entered:

ipconfig

The IP address assigned to PC0 was:

PC0 IP Address: 192.168.5.126

This showed that the router was correctly assigning addresses from the new DHCP range.

Part 5: Enabling DHCP on the Other PCs
Next, I configured PC1 to receive its IP address automatically.

I clicked PC1.
I selected the Desktop tab.
I opened IP Configuration.
I clicked DHCP.
PC1 automatically received an IP address from the router.

The IP address assigned to PC1 was:

PC1 IP Address: 192.168.5.127

I closed the configuration window.

I then repeated the same process for PC2. I opened PC2, selected the Desktop tab, opened IP Configuration, and selected DHCP.

PC2 successfully received an IP address from the router.

Part 6: Verifying Connectivity
Finally, I tested the network to make sure all of the devices could communicate.

I clicked PC2, opened the Desktop tab, and selected Command Prompt.

First, I entered:

ipconfig

This allowed me to check the IP configuration assigned to PC2.

I then tested the connection to the wireless router by entering:

ping 192.168.5.1

The ping was successful.

Next, I tested the connection to PC0 by entering:

ping 192.168.5.126

This ping was also successful.

Finally, I tested the connection to PC1 by entering:

ping 192.168.5.127

The ping was successful as well.

Results
The network was configured successfully. The wireless router was changed to the 192.168.5.1 network, and the DHCP range was changed to start at 192.168.5.126 with a maximum of 75 users.

The IP addresses I recorded were:

Device	IP Address
Router	192.168.5.1
PC0	192.168.5.126
PC1	192.168.5.127
PC2	Obtained automatically through DHCP

The successful ping tests showed that the PCs could communicate with the router and with each other.
