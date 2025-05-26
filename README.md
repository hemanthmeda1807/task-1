# Cyber Security Internship – Task 1

**Internship Provider:** Elevate Labs  
**Intern Name:** Meda Venkata Naga Hemanth Kumar  
**Operating System Used:** Ubuntu

---

## 🔍 Task 1: Scan Your Local Network for Open Ports

### 🎯 Objective
Learn to discover open ports on devices in your local network to understand network exposure.

---

## 🛠️ Tools Used
- **Nmap** – for network and port scanning
- **Wireshark** – for analyzing captured packets
- **tcpdump** – to capture traffic in `.pcap` format for Wireshark

---

## ⚙️ Task Implementation

### 1. Install Nmap
Comand : sudo snap install nmap
![nmap-install](https://github.com/user-attachments/assets/f264fe71-f1e0-4b6d-8f22-473fca2677a5)

### 2. Verify Nmap Installation
Command : nmap --version

### 3. Find Local IP Address and Range
Command : ip a
![ip](https://github.com/user-attachments/assets/8cd55192-e67c-4bdd-bed7-02abe37e4ad1)
here my local IP range is 192.168.43.34/24

### 4. Scan Network for Live Hosts
Command : nmap -sn 192.168.43.0/24
![live-hosts](https://github.com/user-attachments/assets/cf3de050-3c56-4435-9bc0-3ca9aaf60012)
**only two active hosts on my network found:**
- **one is Wi-Fi router gateway: 192.168.43.1**
- **other is my laptop: 192.168.43.34**

### 5. Scan for open ports using a TCP SYN Scan
Command : sudo nmap -sS 192.168.43.0/24
![open-ports](https://github.com/user-attachments/assets/50bb3d65-563b-4c02-8079-63cd7340d3eb)
**open ports found :**
- **port – 53/tcp**
- **state – open**
- **service – domain(DNS)**
#### **Indicates router is running a DNS server.**

### 6. Capture Traffic with tcpdump for Wireshark Analysis
#### Wireshark accepts .pcap files but nmap can’t generate directly these files so here I have used another tool called **tcpdump**
#### Command: sudo tcpdump -i wlo1 -w ~/nmap_scan_capture.pcap
#### start it and open another terminal to run nmap script
#### Command:sudo nmap -sS 192.168.43.0/24
#### start it and after completion of nmap scan stop the tcpdump scan also by typing ^c then
#### open the capture file with Wireshark.
![wireshark-1](https://github.com/user-attachments/assets/c1320211-948a-4319-9f24-c23a2a1838f8)
![wireshark-analyze](https://github.com/user-attachments/assets/8f5c916e-ecb0-407b-ac79-c3de59194b8d)

### 7. Common services running on ports
port 53/tcp → domain(DNS) → DNS(Domain Name System) services translates domain names to IP addresses. Usually runs on routers for dedicated DNS servers.
### 🌐 Common Ports and Services
| Port    | Protocol | Service Description                       |
| ------- | -------- | ----------------------------------------- |
| 53/tcp  | TCP      | DNS – Domain Name System                  |
| 80/tcp  | TCP      | HTTP – Web Servers                        |
| 443/tcp | TCP      | HTTPS – Secure Web Servers                |
| 22/tcp  | TCP      | SSH – Secure Shell for Remote Access      |
| 25/tcp  | TCP      | SMTP – Mail Transfer                      |
| 53/udp  | UDP      | DNS – UDP variant for fast, stateless DNS |
| 21/tcp  | TCP      | FTP – File Transfer Protocol              |
| 445/tcp | TCP      | SMB – Windows File Sharing                |
| 23/tcp  | TCP      | Telnet – Unencrypted Remote Login         |

### 8. Potential security risks from open ports.
#### 1) Port 53/tcp (DNS):
- **if exposed externally or misconfigured, can be exploited fro DNS amplification/ reflection attacks(DDoS).**
- **Can leak network infrastructure information if zone transfers are allowed without restrictions.**
- **Internal exposure is usually less risky but still worth monitoring.**
No other open ports found with the this IP.

### 9. Scanning results as text files
Command: nmap -oN scan_results.txt 192.168.43.0/24
![results-txt](https://github.com/user-attachments/assets/7931b2b6-b908-4508-afc2-f0b4ad1effc7)

### 10. Scanning results in HTML format
Command: nmap -oN scan_results.html 192.168.43.0/24
![results-html](https://github.com/user-attachments/assets/f5517ccb-7cf7-4513-ad58-904884a4c503)


