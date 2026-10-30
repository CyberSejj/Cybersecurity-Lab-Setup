🛡️ Cybersecurity Lab Setup

A personal cybersecurity lab built using Oracle VirtualBox and Kali Linux to explore networking, Linux administration, network troubleshooting, and practical cybersecurity fundamentals.

This project documents my lab setup process, system configuration, connectivity testing, and real troubleshooting experience.

🎯 Project Objectives

- Set up a virtual cybersecurity environment.
- Install and configure Kali Linux.
- Understand virtual network interfaces and IP addressing.
- Test network and internet connectivity.
- Identify and resolve DNS configuration issues.
- Document practical commands, results, and troubleshooting steps.

💻 Host System Specifications

Component| Specification
Laptop| ASUS TUF F15
Processor| Intel Core i7-12700H
RAM| 16 GB DDR4
Graphics| NVIDIA GeForce RTX 3050 (4 GB)
Integrated GPU| Intel Iris Xe
Storage| NVMe SSD
Operating System| Windows 11
Virtualization| Enabled

⚙️ Lab Environment

Component| Details
Virtualization Software| Oracle VirtualBox
Guest Operating System| Kali Linux
Kali Version| 2026.2
Network Configuration| Two active network interfaces

🌐 Network Configuration

The Kali Linux virtual machine has two active network interfaces.

Interface| IP Address| Subnet
eth0| 10.0.0.2| 10.0.0.0/24
eth1| 192.168.56.101| 192.168.56.0/24
lo| 127.0.0.1| Loopback

Default Gateway

"10.0.0.1"

DNS Configuration

After troubleshooting, the DNS servers were configured as:

- Primary DNS: "1.1.1.1"
- Secondary DNS: "1.0.0.1"

🧪 Practical Testing

The following commands were used to inspect and test the lab environment.

1. Check IP addresses

ip -br -4 addr

2. View routing information

ip route

3. Check memory

free -h

4. Check available CPU count

nproc

5. Test gateway connectivity

ping -c 4 10.0.0.1

6. Test internet connectivity

ping -c 4 1.1.1.1

7. Test domain name resolution

ping -c 4 google.com

🔍 DNS Troubleshooting

During the initial connectivity tests, the virtual machine could successfully reach the gateway and an external IP address. However, domain name resolution was failing.

Issue Identified

The initial DNS configuration used "10.0.0.1" as its nameserver, but DNS queries to that server were being refused.

Investigation

The following commands were used:

cat /etc/resolv.conf

nslookup google.com

A direct DNS query to Cloudflare was then tested:

nslookup google.com 1.1.1.1

The direct query succeeded, indicating that an alternative DNS resolver was reachable.

Solution Implemented

The DNS configuration was updated using NetworkManager:

sudo nmcli connection modify "Wired connection 1" ipv4.dns "1.1.1.1 1.0.0.1" ipv4.ignore-auto-dns yes

The connection was reactivated:

sudo nmcli connection up "Wired connection 1"

The final DNS configuration was verified:

cat /etc/resolv.conf

Finally, domain connectivity was tested again:

ping -c 4 google.com

Result

<details>
<summary>View troubleshooting outcome</summary>- Gateway connectivity: Successful
- External IP connectivity: Successful
- Initial DNS resolution: Failed
- Direct query to Cloudflare DNS: Successful
- DNS configuration updated: Successful
- Final domain resolution test: Successful

</details>📚 What I Learned

Through this lab setup, I gained practical experience with:

- Kali Linux environment setup.
- Virtual machine networking.
- IP addressing and routing.
- Linux terminal commands.
- DNS resolution and troubleshooting.
- NetworkManager configuration.
- Connectivity verification and basic diagnostics.

📁 Project Documentation

Detailed lab documentation and supporting screenshots will be maintained in the ""docs"" (docs/lab-setup.md) folder.


## 🎥 Setup Demonstration

[**Watch the Kali Linux Setup Preview (MP4)**](./cybersecurity-lab-setup-demo.mp4)

This short video shows the VirtualBox and Kali Linux startup process. It is a setup preview and does not demonstrate the network connectivity tests or DNS troubleshooting.

## 📌 Project Status

- Virtual lab environment configured.
- Network interfaces and routing information inspected.
- DNS resolution issue identified and resolved.
- Setup screenshots and preview video uploaded.
- Lab configuration and troubleshooting documented.
- 

⚠️ Disclaimer

This is a personal educational lab created for learning and practicing cybersecurity fundamentals. All testing is conducted within my own virtual lab environment or against systems for which I have authorization.

---

Project: Cybersecurity Lab Setup
Author: Sejal Devi
Tools: Kali Linux | Oracle VirtualBox | NetworkManager | Linux Terminal
