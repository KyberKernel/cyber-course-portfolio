Part 1 – Verify Connectivity to the Web Server
Step 1: Open the Command Prompt

I selected the External Client in the Packet Tracer topology.

I opened the Desktop tab and then opened the Command Prompt.

Step 2: Ping the web server

I entered the following command:

ping ciscolearn.web.com


The ping successfully reached the web server.

I noticed that the ping output displayed an IP address for ciscolearn.web.com.

This showed me that the domain name was resolved to an IP address by the DNS service before the traffic was sent.

The network uses source and destination IP addresses to deliver traffic between devices.

Step 3: Close the Command Prompt

After confirming connectivity, I closed the Command Prompt.

I left the External Client desktop window open because I needed it for the next part of the activity.

Part 2 – Connect to the Web Server
Step 1: Open the Web Browser

From the External Client's Desktop tab, I opened the Web Browser.

Step 2: Enter the website address

I entered:

ciscolearn.web.com


into the URL field.

The web page loaded successfully.

I read the information displayed on the page and left the web page open.

Step 3: Minimize the External Client

I minimized the External Client window without closing it.

This allowed me to access the server configuration while keeping the client available for comparison.

Part 3 – View the HTML Code
Step 1: Open the web server

From the Logical topology, I selected the ciscolearn.web.com server.

I opened the server window and selected the Services tab.

Step 2: Open the HTTP service

I selected the HTTP tab.

I located the index.html file and selected the edit option.

This displayed the HTML code stored on the web server.

Step 3: Compare the HTML with the web page

I compared the HTML markup in the index.html file with the web page displayed in the External Client's browser.

I could see that the HTML code on the server was responsible for creating the content and layout displayed by the web browser.

This helped me understand that a web browser requests the HTML document from the server and then interprets the HTML to display the web page.

Step 4: Close the windows

After comparing the HTML code and the web page, I closed both the External Client and web server windows.

Part 4 – Observe Traffic Between the Client and Web Server
Step 1: Enter Simulation Mode

I clicked the Simulation tab in the lower-right corner of Packet Tracer.

This allowed me to observe the packets as they traveled through the network.

Step 2: Open the Simulation Panel

I double-clicked the Simulation Panel to unlock it from the Packet Tracer window.

This allowed me to move the Simulation Panel and see the entire network topology at the same time.

Step 3: Configure the Simulation Filters

I selected Edit Filters from the Simulation Panel.

I opened the Misc tab.

I checked that only:

TCP
HTTP

were selected.

This allowed me to focus on the traffic related to the web request.

Step 4: Create a Complex PDU

I selected the open envelope above the Simulation Mode icon to create a Complex PDU.

I then clicked the External Client to make it the source device.

The Create Complex PDU window appeared.

Step 5: Configure the Complex PDU

I changed the settings as required.

For the application, I selected:

HTTP

I then clicked the ciscolearn.web.com server to make it the destination.

The server's IP address appeared in the destination field.

For the starting source port, I entered:

1000


For the simulation settings, I selected Periodic Interval and entered:

120 seconds

Step 6: Create the PDU

I clicked Create PDU.

The PDU was then added to the simulation.

Step 7: Observe the traffic

I clicked Play in the Simulation Panel.

The animation showed the packets traveling from the External Client toward the web server and back.

I increased the animation speed using the play control slider so that I could observe the traffic more efficiently.

When the Buffer Full window appeared, I selected View Previous Events.

Step 8: Examine the Event List

I scrolled through the Event List and observed the packets generated during the web request.

I noticed that there were several packets traveling between the client and server.

This happened because HTTP uses TCP for communication. Before HTTP data can be exchanged, TCP establishes a connection between the client and server. TCP also uses acknowledgements to confirm that packets have been received.

Therefore, a simple web request produces more network traffic than just the actual HTTP data.

3. What I Learned

During this lab, I learned that accessing a website involves several network processes.

First, the domain name ciscolearn.web.com must be resolved to an IP address using DNS. The client can then communicate with the server using its IP address.

I also learned that the web page displayed by the browser comes from HTML code stored on the web server. The browser interprets this HTML and displays the resulting page.

Finally, using Simulation Mode helped me see that HTTP traffic uses TCP. TCP establishes a connection and uses acknowledgements, which creates additional packets and network overhead.
