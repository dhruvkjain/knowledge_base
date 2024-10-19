## Ethical Hacking

<details>
<summary>Types</summary>
<br>

> ### **`Types`** :
[What Are The Five Steps Of Ethical Hacking? - DEV Community](https://dev.to/sudip_sg/what-are-the-five-steps-of-ethical-hacking-4hfe)
1) Social engineering : exploit human psychology, rather than technical security gaps to gain access to data and applications. They trick legitimate users into submitting their passwords or installing malicious software that grants them access to network machines and services.

2) Web application hacking : 
     Vulnerabilities that manipulate the application :
     - [Cross-Site Scripting](https://crashtest-security.com/cross-site-scripting-xss/)
     - [Cross-Site Request Forgery](https://crashtest-security.com/cross-site-request-forgery-csrf/)
     - [Insecure configuration](https://crashtest-security.com/disable-ssl-insecure-algorithm/)
     - [Injection attacks](https://crashtest-security.com/what-are-the-different-types-of-injection-attacks/)

3) Hacking wireless networks 

4) System hacking (hacking personal computer and servers)

 [Crashtest Security](https://crashtest-security.com/) offers a comprehensive suite of testing tools that help you identify threats within your application.

</details>

<details>
<summary>Methods</summary>
<br>

> ### **`Methods`** :
Reference ==> [Ethical hacking techniques - DEV Community](https://dev.to/snyk/ethical-hacking-techniques-3anh)
1) predictive analytics models is one of the main uses of AI and ML in cybersecurity. These models look for trends and abnormalities that can point to a potential security problem by analyzing data from a range of sources, including network traffic, user behaviour, and system logs.
2) Internet of Things testing's objective is to identify any security flaws in IoT hardware, communication protocols, and the networks they use by network mapping, device identification, firmware analysis, penetration testing, and vulnerability scanning.
3) Social engineering attacks, such as phishing and pretexting
4) Red teaming involves simulating a real-world attack scenario to identify potential vulnerabilities and test an organization's incident response capabilities.
5) Bug bounty programs allow organizations to incentivize ethical hackers to identify potential vulnerabilities in their systems and report them in exchange for a reward.

</details>

<details>
<summary>Steps</summary>
<br>

> ### **`Steps`** :
1) Reconnaissance : hacker documents the organization’s request, finds valuable configuration and login information of the system, and probes the networks.
    Informations such as :
    - Naming conventions
    - Services on the network
    - Servers handling workloads in the network
    - IP Addresses
    - Names and Login credentials of users connected to the network
    - Physical location of target machine
    
2) Penetration testing : 
    - Network Mapping : This involves discovering the network topology, including host information, servers, routers, and firewalls within the host network. Once mapped, white hat hackers can visualize and strategize the next steps of the ethical hacking process.
    - Port Scanning : Ethical hackers use automated tools to identify any open ports on the network. This makes it an efficient mechanism to enumerate the services and live systems in a network, and how to establish a connection with these components.
    - Vulnerability Scanning : The use of automated tools to detect weaknesses that can be exploited to orchestrate attacks.
       Tools for scanning : 
       - SNMP Sweepers
       - Ping sweeps
       - Network mappers
       - Vulnerability scanners
       
3) Gaining Access : Attempting to send a malicious payload to the application through the network, an adjacent subnetwork, or physically using a connected computer.
    Tools to simulate attempted unauthorized access,
    - Buffer overflows
    - Phishing  
    - [Injection attacks](https://crashtest-security.com/what-are-the-different-types-of-injection-attacks/)
    - [XML External Entity processing](https://crashtest-security.com/xxe-processing/)
    - Using components with known vulnerabilities.
    
    If the attacks are successful, the hacker has control of the whole or part of the system and may simulate further attacks such as data [breaches](https://crashtest-security.com/prevent-breach-attacks/) and Distributed Denial of Service (DDoS).
    
4) Maintaining Access :  involves processes used to ensure the hacker can access the application for future use. A white-hat hacker continuously exploits the system for further vulnerabilities and [escalates privileges](https://crashtest-security.com/privilege-escalation-guide/) to understand how much control attackers can gain once they get past security clearance. Some attackers may also try to hide their identity by removing any evidence of an attack and installing a backdoor for future access.
    
5) Clearing Tracks : To avoid any evidence that leads back to their malicious activity, hackers perform tasks that erase all traces of their actions.
    This includes : 
    - Uninstalling scripts/applications used to carry out attacks
    - Modifying registry values
    - Clearing logs
    - Deleting folders created during the attack
    For those hackers looking to maintain undetected access, they tend to hide their identity using techniques such as :
    - Tunneling
    - Stenography

</details>
<details>
<summary>Tools/website to learn</summary>
<br>

- Shodan is a search engine for internet-connected devices, providing information about their vulnerabilities. Features include device search, banner parsing, and an API for developers.
- [TryHackMe (for learning) ](https://tryhackme.com/)
- [HACKSPLAINING (for learning) ](https://www.hacksplaining.com/)
- Nmap (Network Scanner) Tool 
- Burp Suite (Bug Bounty) Tool 
- Wpscan (WordPress Scanner) Tool 
- Sqlmap (Database Scanning & Exploiting) Tool 
- Metasploit (Exploit generator & Development) Tool 
- Aircrack-Ng (Wi-Fi Hacking) Tool 
- Ghidra (Reverse Engineering) Tool 
- John The Ripper (Password Cracker) Tool 
- Wireshark (Packet Capture) Tool 
- Hashcat (Hash Decrypter)


</details>

<details>
<summary>Top 44 Ports (Basics)</summary>
<br>

🕵‍♀

Top 44 Ports (Basics)
1. FTP - Port 21
2. SSH - Port 22
3. Telnet - Port 23
4. SMTP | Port 25 and Submission Port 587
5. DNS - Port 53
6. Finger - Port 79
7. HTTP - Port 80
8. Kerberos - Port 88
9. POP3 - Port 110
10. RPCInfo - Port 111
11. Ident - Port 113
12. SNMP - Port 161
13. Check Point FireWall-1 Topology - Port 264
14. LDAP - Port 389
15. SMB - Port 445
16. Rexec - Port 512
17. Rlogin - Port 513
18. RSH - port 514
19. AFP - Apple Filing Protocol - Port 548
20. Microsoft Windows RPC Services | Port 135 and Microsoft RPC Services over HTTP | Port 593
21. HTTPS - Port 443 and 8443
22. RTSP - Port 554 and 8554
23. Rsync - Port 873
24. Java RMI - Port 1099
25. MS-SQL | Port 1433
26. Oracle - Port 1521
27. NFS - Port 2049
28. ISCSI - Port 3260
29. SAP Router | Port 3299
30. MySQL | Port 3306
31. Postgresql - Port 5432
3️2. HPDataProtector RCE - Port 5555
3️3. VNC - Port 5900
3️4. CouchDB - Port 5984
3️5. Redis - Port 6379
3️6. AJP Apache JServ Protocol - Port 8009
3️7. PJL - Port 9100
3️8. Apache Cassandra - Port 9160
3️9. Network Data Management Protocol (ndmp) - Port 10000
4️0. Memcache - Port 11211
4️1. MongoDB - Port 27017 and Port 27018
4️2. EthernetIP-TCP-UDP - Port 44818
4️3. UDP BACNet - Port 47808


</details>
<details>
<summary>100 web vulnerabilities, categorized into various types:</summary>
<br>

Injection Vulnerabilities:
1. SQL Injection (SQLi)
2. Cross-Site Scripting (XSS)
3. Cross-Site Request Forgery (CSRF)
4. Remote Code Execution (RCE)
5. Command Injection
6. XML Injection
7. LDAP Injection
8. XPath Injection
9. HTML Injection
10. Server-Side Includes (SSI) Injection
11. OS Command Injection
12. Blind SQL Injection
13. Server-Side Template Injection (SSTI)
Broken Authentication and Session Management:
14. Session Fixation
15. Brute Force Attack
16. Session Hijacking
17. Password Cracking
18. Weak Password Storage
19. Insecure Authentication
20. Cookie Theft
21. Credential Reuse
Sensitive Data Exposure:
22. Inadequate Encryption
23. Insecure Direct Object References (IDOR)
24. Data Leakage
25. Unencrypted Data Storage
26. Missing Security Headers
27. Insecure File Handling
Security Misconfiguration:
28. Default Passwords
29. Directory Listing
30. Unprotected API Endpoints
31. Open Ports and Services
32. Improper Access Controls
33. Information Disclosure
34. Unpatched Software
35. Misconfigured CORS
36. HTTP Security Headers Misconfiguration
XML-Related Vulnerabilities:
37. XML External Entity (XXE) Injection
38. XML Entity Expansion (XEE)
39. XML Bomb
Broken Access Control:
40. Inadequate Authorization
41. Privilege Escalation
42. Insecure Direct Object References
43. Forceful Browsing
44. Missing Function-Level Access Control
Insecure Deserialization:
45. Remote Code Execution via Deserialization
46. Data Tampering
47. Object Injection
API Security Issues:
48. Insecure API Endpoints
49. API Key Exposure
50. Lack of Rate Limiting
51. Inadequate Input Validation
Insecure Communication:
52. Man-in-the-Middle (MITM) Attack
53. Insufficient Transport Layer Security
54. Insecure SSL/TLS Configuration
55. Insecure Communication Protocols
Client-Side Vulnerabilities:
56. DOM-based XSS
57. Insecure Cross-Origin Communication
58. Browser Cache Poisoning
59. Clickjacking
60. HTML5 Security Issues
Denial of Service (DoS):
61. Distributed Denial of Service (DDoS)
62. Application Layer DoS
63. Resource Exhaustion
64. Slowloris Attack
65. XML Denial of Service
Other Web Vulnerabilities:
66. Server-Side Request Forgery (SSRF)

What is SSRF? 
Server-side request forgery (also known as SSRF) is a web security vulnerability that allows an attacker to induce the server-side application to make HTTP requests to an arbitrary domain of the attacker's choosing. 
In a typical SSRF attack, the attacker might cause the server to make a connection to internal-only services within the organization's infrastructure. In other cases, they may be able to force the server to connect to arbitrary external systems, potentially leaking sensitive data such as authorization credentials.

67. HTTP Parameter Pollution (HPP)
68. Insecure Redirects and Forwards
69. File Inclusion Vulnerabilities
70. Security Header Bypass
71. Clickjacking
72. Inadequate Session Timeout
73. Insufficient Logging and Monitoring
74. Business Logic Vulnerabilities
75. API Abuse
Mobile Web Vulnerabilities:
76. Insecure Data Storage on Mobile Devices
77. Insecure Data Transmission on Mobile Devices
78. Insecure Mobile API Endpoints
79. Mobile App Reverse Engineering
IoT Web Vulnerabilities:
80. Insecure IoT Device Management
81. Weak Authentication on IoT Devices
82. IoT Device Vulnerabilities
Web of Things (WoT) Vulnerabilities:
83. Unauthorized Access to Smart Homes
84. IoT Data Privacy Issues
Authentication Bypass:
85. Insecure "Remember Me" Functionality
86. CAPTCHA Bypass
Server-Side Request Forgery (SSRF):
87. Blind SSRF
88. Time-Based Blind SSRF
Content Spoofing:
89. MIME Sniffing
90. X-Content-Type-Options Bypass
91. Content Security Policy (CSP) Bypass
Business Logic Flaws:
92. Inconsistent Validation
93. Race Conditions
94. Order Processing Vulnerabilities
95. Price Manipulation
96. Account Enumeration
97. User-Based Flaws
Zero-Day Vulnerabilities:
98. Unknown Vulnerabilities
99. Unpatched Vulnerabilities
100. Day-Zero Exploits


</details>

