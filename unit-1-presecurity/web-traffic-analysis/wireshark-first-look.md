Wireshark First Look: Cleartext vs. Encrypted Traffic

Assignment: U1-03a Wireshark – Cleartext vs. Encrypted Traffic

Introduction

This lab compared two packet captures of the same fictional login: one sent over ordinary HTTP and the other sent over HTTPS. The comparison demonstrates why encryption is important. HTTP sends application data without encryption, allowing someone monitoring the network to read sensitive information. HTTPS uses TLS encryption to protect the contents of the communication.

Important note: The credentials and personal information below come from the fictional, isolated lab capture supplied for this assignment. They should not be treated as real user information.

Part 1 HTTP Capture
1. What username and password were sent?

The username was anna.virtanen, and the password was Summer2026!. Both values were visible in plain text because the login form was transmitted over HTTP without encryption.

The relevant HTTP request was:

POST /login HTTP/1.1
Host: lab-portal.local
Content-Type: application/x-www-form-urlencoded
Content-Length: 55

username=anna.virtanen&password=Summer2026!&remember=on


Therefore:

Username: anna.virtanen
Password: Summer2026!

The fact that the request used POST does not make the information secure. Because the connection was ordinary HTTP, the request body could still be read in the packet capture.

2. Which HTTP method was used to submit the login form?

The login form used the POST method.

The request line was:

POST /login HTTP/1.1


POST places the form data in the request body rather than directly in the URL. However, POST itself does not provide encryption or confidentiality. Since this request used HTTP, the username and password were still visible to someone monitoring the traffic.

3. What is the SESSIONID cookie, and why is it dangerous if exposed?

The session cookie was:

SESSIONID=a3f9c2e7b81d4f60a5e2c9d10f4b7e88


The server sent it in the response header:

HTTP/1.1 302 Found
Set-Cookie: SESSIONID=a3f9c2e7b81d4f60a5e2c9d10f4b7e88; Path=/; HttpOnly
Location: /dashboard


The SESSIONID identifies the user's authenticated session. If an attacker obtains a valid session cookie, they may be able to reuse it to access the user's active session without knowing the password. This is commonly known as session hijacking.

The HttpOnly attribute helps prevent JavaScript from reading the cookie through the browser, but it does not protect the cookie from being observed while it is transmitted over an unencrypted HTTP connection.

4. What two pieces of sensitive information were visible on the dashboard?

Two examples of sensitive information visible on the dashboard were:

User's role: Finance Administrator
User's email: anna.virtanen@pohjola-logistics.local

The dashboard also exposed the user's full name and last-login IP address.

The relevant dashboard content was:

<!DOCTYPE html><html><head><title>Dashboard</title></head><body>
<h1>Welcome back, Anna Virtanen</h1>
<p>Role: Finance Administrator</p>
<p>Email: anna.virtanen@pohjola-logistics.local</p>
<p>Last login from 10.10.10.50</p>
</body></html>


This demonstrates that HTTP can expose not only login credentials but also information contained in authenticated web pages.

Part 2 HTTPS Capture
5. Could the username and password be found in the HTTPS capture? Why or why not?

No. The username and password could not be found as readable values in the HTTPS capture.

HTTPS uses TLS (Transport Layer Security) to encrypt the application data exchanged between the client and server. Wireshark can still identify the TLS handshake and encrypted application-data records, but without the appropriate decryption keys it cannot display the username, password, cookie, or dashboard contents as readable plaintext.

This is the main difference between the two captures:

HTTP: Application data is visible in plaintext.
HTTPS: Application data is encrypted and appears as encrypted TLS records.
6. What server name was visible in the first TLS Client Hello?

The server name was:

lab-portal.local


This hostname was visible through the Server Name Indication (SNI) field in the TLS Client Hello.

SNI can reveal the hostname a client is attempting to connect to, even though the actual application data, such as login credentials and page contents, is encrypted.

7. What can an eavesdropper still learn from the HTTPS capture?

An eavesdropper can still observe certain network metadata even when HTTPS is used.

In this capture, the observer could see information such as:

Client IP address: 10.10.10.50
Server IP address: 10.10.10.10
Destination port: 443
Packet timing
Approximate packet or record sizes
Direction of the communication
The server hostname lab-portal.local through SNI

This metadata does not reveal the password or dashboard contents. However, it can still provide information about who is communicating, when communication occurs, and approximately how much data is being exchanged.

Part 3 — Making Sense of It
8. Why does the protocol choice matter for confidentiality?

The protocol choice matters because HTTP does not encrypt application data, while HTTPS uses TLS encryption.

With HTTP, someone monitoring the network may be able to read usernames, passwords, session cookies, and information displayed on web pages.

With HTTPS, the application data is encrypted, so ordinary network observers cannot normally read the credentials, cookies, messages, or page contents.

Therefore, HTTPS provides much stronger confidentiality than HTTP.

9. Where might you use an untrusted network, and what would be protected or exposed?

One example is using public Wi-Fi at a coffee shop, airport, hotel, or other public location.

If I log in to an online banking or email account over HTTPS, TLS protects sensitive information such as:

Usernames and passwords
Session information
Messages
Web page contents
Other application data

However, HTTPS does not necessarily hide all network metadata. Depending on the circumstances, an observer may still see information such as IP addresses, connection timing, traffic size, and possibly the destination hostname.

A VPN can provide an additional layer of protection by encrypting traffic between the device and the VPN server. However, the VPN provider can then observe certain connection information.

Reflection

What surprised me most was how easy it was to read the HTTP traffic. The username, password, session cookie, personal information, and user role were all visible by following the HTTP stream in Wireshark.

In contrast, the HTTPS capture still revealed some connection metadata, such as IP addresses and the server name, but the actual login credentials and dashboard contents appeared as encrypted TLS data rather than readable text.

This lab showed me why HTTPS is important. Simply using a POST request does not make a login secure. The important difference is whether the communication is protected by encryption. HTTP can expose sensitive information to network observers, while HTTPS uses TLS to protect the contents of the communication.
