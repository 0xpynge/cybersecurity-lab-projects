## Types of Network Threats:
- Viruses: Malicious code that attaches to programs/files and spreads when executed.
- Worms: Self-replicating malware that spreads across networks without human action.
- Trojans: Malicious programs disguised as legitimate software; create backdoors for attackers.
- Phishing Attacks: Deceptive emails or messages tricking users into revealing sensitive data.

## Basic Security Concepts:
- Firewalls: Hardware/software that filters incoming and outgoing network traffic based on rules.
- Encryption: Process of converting data into unreadable form to protect confidentiality during storage or transmission.
- Secure Network Configurations: 
    - Use strong passwords and authentication.
    - Keep systems patched and updated.
    - Disable unnecessary services/ports.
    - Implement least privilege access.

2. Implement Basic Security Measures
- Open Start and search for Windows Security.
- Select Firewall and network protection.
- Confirm Domain network, Private network, and Public network all show On.
<img width="675" height="650" alt="image" src="https://github.com/user-attachments/assets/a986d14c-5183-455b-801c-45635c00c2dc" />

Figure 1. Windows Security showing firewall on for all profiles.

Create an inbound rule to block Telnet (port 23)
Open Start and search for Windows Defender Firewall with Advanced Security. 
 Select Inbound Rules on the left.
In Actions, click New Rule.
Choose Port, then Next.
Select TCP. Choose Specific local ports and enter 23. Click Next.
Choose Block the connection. Click Next.
Check Domain, Private, and Public. Click Next.
Name the rule Telnet Block and click Finish. Verify the rule appears in the list.

<img width="870" height="360" alt="image" src="https://github.com/user-attachments/assets/e280cf5e-938a-4eac-a636-a1477bf598b4" />

Figure 2. Inbound Rules view.

<img width="870" height="456" alt="image" src="https://github.com/user-attachments/assets/14f672bd-d58b-43ce-9357-c5918d856adf" />

Figure 3. New Inbound Rule: select Port.

<img width="870" height="391" alt="image" src="https://github.com/user-attachments/assets/753871a9-12a3-42f0-bba7-67452a3d4d26" />

Figure 4. Specify TCP port 23 for Telnet.

<img width="870" height="407" alt="image" src="https://github.com/user-attachments/assets/cdb210ea-19f1-4af0-935f-f3c44b2f778a" />

Figure 5. Select Block the connection.

<img width="870" height="210" alt="image" src="https://github.com/user-attachments/assets/09a679b6-764a-4c3b-a19a-ab7f442ff51b" />

Figure 6. Telnet Block rule listed under Inbound Rules.

## Secure your Wi‑Fi on the router
1. Log in to the router’s admin page in a browser. The address is often 192.168.0.1 or 192.168.1.1.
2. Change the default admin password to a strong, unique one and save.
3. Open Wireless or Wi‑Fi settings.
4. Set Authentication/Mode to WPA2‑PSK or WPA2/WPA3‑Personal. Avoid WEP or None.
5. Set Encryption to AES if available. If the only option is TKIP & AES, use that but prefer AES‑only when possible.
6. Enter a strong Wi‑Fi passphrase (12–16+ characters, mix of letters, numbers, and symbols). Save changes.
7. Reconnect devices using the new Wi‑Fi password.

<img width="870" height="826" alt="image" src="https://github.com/user-attachments/assets/f71b27d1-65e6-45ca-9d91-0a18ac8c6fe8" />

Figure 7. Choose WPA2‑PSK or WPA/WPA2‑PSK (avoid WEP/None).

<img width="870" height="449" alt="image" src="https://github.com/user-attachments/assets/5032c2e4-53dc-43ce-864f-a2e3b4ccdde5" />

Figure 8. Set encryption and enter a strong passphrase.

## Additional hardening (recommended)
1. Disable WPS and remote administration unless you need them.
2. Turn off unused services and ports on the router and devices.
3. Update router firmware and operating systems regularly.
4. Use a unique SSID that does not reveal personal information.
5. Back up the router configuration after you secure it.

## Monitor Network Traffic
1. Capturing TCP Traffic (Handshake)
The first screenshot shows TCP traffic between the local machine (192.168.50.240) and a remote server (34.223.124.45). Wireshark filters were applied (tcp.port == 80) to isolate HTTP traffic over TCP.

Key observations:
- SYN, SYN-ACK, and ACK packets establish the TCP three-way handshake.
- Retransmissions and RST packets indicate possible connection issues.
- Unusual retransmissions or resets could mean packet loss, instability, or scanning attempts.
<img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/aeb03971-fca8-4486-804a-462614301adf" />

Figure 1. TCP traffic including handshake, retransmissions, and resets.

2. Identifying HTTP Traffic
The second screenshot captures HTTP traffic on port 80. The display filter 'http' was applied to show only HTTP requests and responses.

Key observations:
- The client sends an HTTP GET request to neverssl.com.
- Server responses include 200 OK and 301 Moved Permanently messages.
- By examining the request and response headers, analysts can see the requested URI, user agent, and response content type.
- Suspicious HTTP traffic might include unexpected hosts, unencrypted sensitive data, or abnormal request patterns.
  <img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/667974db-d811-40c1-908a-414983c6908e" />
  
Figure 2. HTTP GET request and server responses captured in Wireshark.

3. Analyzing DNS Queries
The third screenshot displays DNS queries and responses, filtered with 'dns'. The local system queries multiple domain names (e.g., chatgpt.com, gvt2.com) to resolve them into IP addresses.

Key observations:
- Standard queries (type A) request IPv4 addresses for domain names.
- Responses include authoritative answers with resolved IP addresses.
- Repeated DNS queries, failed lookups, or suspicious domain names may indicate malware activity or command-and-control communication.
<img width="975" height="461" alt="image" src="https://github.com/user-attachments/assets/bcafcdfc-5e45-4fc7-a3db-bd05aec08c38" />

Figure 3. DNS queries and responses showing domain resolution.

4. Spotting Unusual or Suspicious Traffic
When analyzing captures, some signs of suspicious traffic include:
- Excessive retransmissions or RST packets (may indicate scanning or unstable connections).
- HTTP traffic to unknown or suspicious hosts.
- DNS queries to unusual domains, especially with random strings.
- Unexpected protocols or ports in use.

By combining protocol analysis with security knowledge, Wireshark helps analysts detect potential threats.

## Additional Security Measures for Larger Networks
- Deploy IDS/IPS to detect and block suspicious activity.
- Use network segmentation to limit access between systems.
- Enforce access controls with multi-factor authentication (MFA).
- Implement centralized logging and SIEM for anomaly detection.
- Perform regular vulnerability scans and patch management.
- Protect endpoints with antivirus/EDR solutions.
- Encrypt sensitive communications (VPNs, TLS).

## Educating Others on Network Security
- Explain risks in everyday terms (e.g., identity theft, financial loss).
- Promote strong, unique passwords and password managers.
- Encourage two-factor authentication on accounts.
- Teach caution against phishing emails and suspicious links.
- Stress importance of software and system updates.
- Compare network security to locking doors at home for familiarity.

