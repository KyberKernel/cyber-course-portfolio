Wireshark Cleartext vs Encrypted Traffic
Part 1- HTTP Capture
1. What username and password were sent?
The login used a POST request. The username and password were visible in plain text.
POST /login HTTP/1.1
Host: lab-portal.local
Content-Type: application/x-www-form-urlencoded
Content-Length: 55
username=anna.virtanen&password=Summer2026!&remember=on
Username: anna.virtanen
Password: Summer2026!
2. Which HTTP method was used?
The login form used the POST method.
3. What is the SESSIONID cookie? Why is it dangerous?
The server sent this response:
HTTP/1.1 302 Found
Set-Cookie: SESSIONID=a3f9c2e7b81d4f60a5e2c9d10f4b7e88; Path=/; HttpOnly
Location: /dashboard
SESSIONID: a3f9c2e7b81d4f60a5e2c9d10f4b7e88
If an attacker gets this cookie, they may be able to log in as the user without knowing the password. This is called session hijacking. The HttpOnly setting helps stop JavaScript from reading the cookie, but it does not stop someone from seeing it when it is sent over normal HTTP.
4. List two pieces of sensitive information.
Two pieces of sensitive information on the dashboard are:
Full name: Anna Virtanen
Email: anna.virtanen@pohjola-logistics.local
The dashboard also shows the user's role as Finance Administrator and the last-login IP address.
Part 2- HTTPS Capture
5. Can you find the username and password?
No. The username and password cannot be seen in plain text in the HTTPS capture.
HTTPS uses TLS to encrypt the data. When following the TCP stream, the login information is encrypted and cannot be read.
6. What is the server name in the Client Hello?
The server name is:
lab-portal.local
It can be found in the SNI (Server Name Indication) field of the TLS Client Hello.
7. What can an eavesdropper still learn?
An eavesdropper can still see some network information, such as IP addresses, connection times, and packet sizes.
In this capture:
Client: 10.10.10.50
Server: 10.10.10.10
The SNI hostname may also be visible.
Part 3- Making Sense of It
8. Why does HTTP vs HTTPS matter for confidentiality?
HTTP sends data in plain text, so someone watching the network can read it. HTTPS encrypts the data with TLS, so sensitive information such as passwords and cookies cannot normally be read by the observer.
9. Give one example of using an untrusted network.
One example is using public Wi-Fi in a coffee shop. HTTPS protects passwords, messages, and other private information from being read by people watching the network. However, some information, such as IP addresses, connection times, and possibly the server name, can still be visible.
Reflection
What surprised me most was how easy it was to read the HTTP traffic.
The username, password, cookie, and personal information were all visible. With HTTPS, this information was encrypted and could not be read. This showed me why HTTPS is important for keeping information safe.
