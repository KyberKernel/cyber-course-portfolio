Wireshark Cleartext vs Encrypted Traffic

Part 1 HTTP Capture

1- Find the login submission. What username and password were sent? Paste the line from the stream where you found them.
The username and password are not shown in the packet list we have. The login was sent using the HTTP login request.
POST /login HTTP/1.1


2- The login form was submitted using which HTTP method GET or POST?
It was submitted using POST.

3- What is the value of the SESSIONID cookie? Why might an attacker who sees this cookie be dangerous, even without the password?
The exact SESSIONID value is not shown in the packet data we have.
If someone got the session cookie, they could potentially access the users logged in session without knowing the password.

4- The dashboard page reveals personal details about the user. List two pieces of sensitive information visible there.
The two personal details are not shown in the packet list we have. The capture does show that the dashboard was successfully opened.
HTTP/1.1 200 OK  (text/html)

Part 2 HTTPS Capture

1- Can you find the username and password anywhere in this capture? Why or why not?
No. The username and password are encrypted by TLS, so we cannot read them from the HTTPS traffic.

2- What is the server name shown in the Client Hello?
The server name is lab-portal.local.
Client Hello (SNI=lab-portal.local)


3- Even though the contents are encrypted, name one thing an eavesdropper can still learn from the HTTPS capture.
An eavesdropper can still see the IP addresses of the client and server.
They can also see when the connection happens and the size of the packets.

Part 3 Making Sense of It

1- In one sentence: why does the protocol choice (HTTP vs HTTPS) matter for confidentiality?
HTTPS encrypts the data, while HTTP sends it openly, so HTTPS makes it much harder for someone watching the network to read private information.

2- Name one situation in your daily life where you might be sending traffic over an untrusted network. What protects you, and what would still be exposed?
One example is using public WiFi in the cafe. HTTPS protects the information we send,
such as passwords, but someone on the network could still see some information like the destination, timing, and traffic size.

What surprised me most was how much easier it is to read information from HTTP traffic. With HTTPS, the actual login information is hidden, even though some connection details are still visible.
