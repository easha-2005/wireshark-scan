# wireshark-scan
🔍 Wireshark Network Traffic Analysis Report
🎯 Objective: To capture live packets using Wireshark, identify at least three network protocols, and analyze the communication patterns to develop protocol awareness and network troubleshooting skills.

📁 Captured File
File Name: scan results.pcapng
Capture Tool: Wireshark
Device: AzureWaveTec_8f:aa:ab (192.168.31.89)

📡 Summary of Observed Protocols
Protocol	Description	Use Case
TCP	Transmission Control Protocol	Used for reliable communication, connection-oriented, majorly observed in HTTPS, HTTP
HTTP	Hypertext Transfer Protocol	Used for fetching resources such as web pages
DNS	Domain Name System	Used for resolving domain names into IP addresses
ARP	Address Resolution Protocol	Resolves IP to MAC addresses in a local network
TLSv1.2	Transport Layer Security	Secures communication over the internet (HTTPS)

🧪 Detailed Packet Analysis
🔸 1. HTTP Traffic:
Observation: HTTP GET request to Microsoft Update server:

bash
Copy
Edit
GET /pr/492350f6.../Office/Data/16.0.18827.20128/a640_exp.cab
Host: f.c2r.ts.cdn.office.net
Port Used: 80 (Standard HTTP)

Tool Insight: This is a plain text transfer of files from Microsoft servers – likely an update.

Security Concern: HTTP is unencrypted, which means data could be sniffed or manipulated.

🔸 2. DNS Queries:
Examples of Queries:

kotlin
Copy
Edit
settings-win.data.microsoft.com
metadata.google.internal
v10.events.data.microsoft.com
Port Used: 53 (UDP)

Purpose: Resolving names like settings-win.data.microsoft.com to corresponding IP addresses.

Security Note: Basic DNS is unencrypted (can be intercepted).

🔸 3. TCP Handshakes:
Multiple packets show:

SYN, SYN-ACK, ACK sequences indicating connection establishment.

Example:

yaml
Copy
Edit
Src Port: 443, Dst Port: 50591, SYN, ACK=1, Seq=0
Significance: Forms the backbone for HTTP/S, TLS, FTP and other reliable protocols.

🔸 4. TLSv1.2 (HTTPS):
TLS sessions over port 443 to domains like:

settings-win.data.microsoft.com

Shows exchange of:

Server Hello

Client Hello

Certificate

Purpose: Secure encrypted session establishment.

Security Benefit: Prevents eavesdropping and tampering.

🔸 5. ARP Requests:
Example:

nginx
Copy
Edit
Who has 169.254.169.254? Tell 192.168.31.89
Use: Maps IP to MAC within local network.

Device Role: Helps in IP-MAC resolution for local communications.

🔐 Security Observation Summary
Risk	Explanation	Suggestion
Unencrypted HTTP	Files requested via HTTP (like .cab update files) can be intercepted	Use HTTPS wherever possible
Plain DNS	Domains resolved via unencrypted DNS	Prefer DoH (DNS over HTTPS)
Open TCP ports	Various ephemeral ports are used for outgoing connections	Monitor open ports for unexpected traffic

✅ Protocols Identified
Protocol	Application Layer	Transport Layer
HTTP	✔️	TCP
DNS	✔️	UDP
ARP	❌ (Data Link Layer)	N/A
TLS	✔️ (Encryption)	TCP
TCP	❌ (Transport Layer)	TCP
