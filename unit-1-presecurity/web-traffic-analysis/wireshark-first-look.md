Wireshark First Look: Cleartext vs. Encrypted Traffic
Assignment: U1-03a Wireshark – Cleartext vs Encrypted Traffic

Introduction
This lab compared two packet captures of the same fictional login: one sent over ordinary HTTP and the other sent over HTTPS. The comparison shows why encryption is important: HTTP exposes application data directly to anyone monitoring the network, while HTTPS protects the contents of the conversation with TLS encryption.

Important note: The credentials and personal information below come from the fictional, isolated lab capture supplied for this assignment. They should not be treated as real user information.

Part A -  HTTP Capture
1. What username and password were sent?
The username was anna.virtanen, and the password was Summer2026!. Both values were visible in the HTTP request because the login form was transmitted without encryption.

The relevant lines from the Follow HTTP Stream output were:

POST /login HTTP/1.1
Content-Type: application/x-www-form-urlencoded

username=anna.virtanen&password=Summer2026!

2. Which HTTP method submitted the login form?
The login form used the POST method. The request line POST /login HTTP/1.1 shows that the credentials were placed in the request body rather than in the URL. However, POST by itself does not provide confidentiality; because this request used HTTP, the body was still readable in the packet capture.

3. What was the SESSIONID cookie, and why is it dangerous if exposed?
The value of the session cookie was:

SESSIONID=a3f9c2e7b81d4f60a5e2c9d10f4b7e88

The server sent it in this response header:

Set-Cookie: SESSIONID=a3f9c2e7b81d4f60a5e2c9d10f4b7e88; Path=/; HttpOnly

An attacker who obtains this cookie may be able to reuse the active session, a situation commonly called session hijacking. In that case, the attacker might access the dashboard as the already-authenticated user without knowing the password. The HttpOnly attribute helps prevent JavaScript from reading the cookie, but it cannot protect the cookie from being observed directly on an unencrypted HTTP connection.

4. What two sensitive pieces of information were visible on the dashboard?
The dashboard exposed several personal or security-relevant details. Two examples are:

1	The user’s role was Finance Administrator.
2	The user’s email address was anna.virtanen@pohjola-logistics.local.

The dashboard also revealed the user’s name, Anna Virtanen, and the last login address, 10.10.10.50. The relevant response body was:

<!DOCTYPE html><html><head><title>Dashboard</title></head><body><h1>Welcome back, Anna Virtanen</h1><p>Role: Finance Administrator</p><p>Email: anna.virtanen@pohjola-logistics.local</p><p>Last login from 10.10.10.50</p></body></html>

Part B - HTTPS Capture
5. Could the username and password be found in the HTTPS capture? Why or why not?
No. The username and password could not be found as readable values in the HTTPS capture because the login request and server responses were carried inside an encrypted TLS session. Wireshark could still identify the TLS handshake and encrypted application-data records, but without the appropriate decryption keys it could not display the form fields, cookie, or dashboard content in plaintext.

This is the key difference between the two captures: the HTTP stream reconstructs the conversation as readable text, while the HTTPS stream shows encrypted bytes and packet metadata instead of the actual application content.

6. What server name was visible in the first TLS Client Hello?
The Server Name Indication (SNI) in the Client Hello was:

lab-portal.local

This means that the destination hostname was visible during the TLS setup, even though the login details and page contents were encrypted.

7. What can an eavesdropper still learn from the HTTPS capture?
An eavesdropper could still learn some metadata, including the communicating IP addresses, the destination port, the timing of packets, and the approximate size and direction of the exchanged records. In this capture, the client was 10.10.10.50, the server was 10.10.10.10, and the server was contacted on TCP port 443.

This metadata does not reveal the password or the dashboard text, but it can still provide useful information about who is communicating, when communication occurs, and how much data is exchanged. The hostname lab-portal.local was also visible through SNI in this TLS 1.2 capture.

Part C - Making Sense of It
8. Why does the protocol choice matter for confidentiality?
HTTP sends application data in plaintext, whereas HTTPS uses TLS to encrypt the conversation so that network observers cannot normally read credentials, cookies, or page contents.

9. Where might you use an untrusted network, and what would be protected or exposed?
One everyday example is logging in to an online banking or email account while connected to public Wi-Fi at an airport or cafe. HTTPS protects the login credentials, session data, and page contents from ordinary network eavesdropping, but some metadata—such as the device’s network connection, the destination address or hostname in some circumstances, the timing of the traffic, and the approximate amount of data—may still be visible. A VPN can provide an additional layer of protection by encrypting traffic between the device and the VPN server, although the VPN provider can then observe some connection information.

Reflection
What surprised me most was how much information was exposed by the HTTP capture. The username, password, session cookie, personal details, and user role were all readable by simply following the stream. In contrast, the HTTPS capture still revealed connection metadata and the server name, but the actual login and dashboard contents appeared as encrypted data rather than readable text.
