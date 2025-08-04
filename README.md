First of all I opened my Kali linux machine and typed ifconfig command on root terminal through that I got my IP address as 10.104.247.36/24. Then I performed nmap TCP SYN Scan by the command nmap -sS 10.104.247.36/24
and performed a network scan using wireshark for same IP address.Through that I got to know the following result for the following hosts:-
Host 10.104.247.21
Port 53/tcp open 
MAC Address: F6:89:15:93:38:37 
Host 10.104.247.243
All scanned ports in ignored states 
Host 10.104.247.36
No open ports, all scanned ports closed
Research: Common Services Running on Open Ports
Port 53/tcp (DNS)
Service: Domain Name System (DNS) is used to translate domain names to IP addresses. It’s an essential network service.
Port usage: While DNS runs primarily over UDP port 53, it also uses TCP port 53 for zone transfers, large queries/responses, or DNSSEC.
Security Risks of Open Port 53
DDoS Attacks: DNS servers on port 53 are frequent targets for Distributed Denial of Service (DDoS) attacks. 
DNS Spoofing & Cache Poisoning: Attackers can exploit improperly secured DNS to redirect users to malicious sites or inject bad cache records. This is known as DNS spoofing or cache poisoning.
Unrestricted Queries: If your DNS server on port 53 is accessible to the public or broader network, it may be abused for unauthorized queries, used by attackers for exfiltration (DNS tunneling), or as part of botnet operations.
Sensitive Data Exposure: DNS logs and queries can reveal network activity patterns, which could be of interest to attackers if not adequately protected.
What to do:-
Restrict Access: Limit access to port 53 to only trusted internal IP addresses. Block external/public access unless absolutely necessary for authoritative or recursive DNS.
Monitoring: Continuously monitor DNS query logs for signs of abnormal or malicious activity.
Harden the Server: Disable recursion for external queries, patch your DNS server software regularly, and use DNS-specific firewalls.
Network Segmentation: Ensure DNS is isolated from other critical services and has the least privilege necessary.
What You Should DoIf you do NOT intend this host to provide DNS resolution for your network, close port 53 or disable the DNS service on 10.104.247.21.
If the DNS service is required, make sure it is not accessible publicly and is properly configured and hardened according to security standards.
Regularly run vulnerability scans and keep your DNS server updated.

Summary of Service and Security Risks
Host IP	Open Port	Service	Security Risks	Mitigation
10.104.247.21	53/tcp	DNS	DDoS, spoofing, abuse	Restrict access, monitor logs, patch
10.104.247.243	None	
10.104.247.36	None	
