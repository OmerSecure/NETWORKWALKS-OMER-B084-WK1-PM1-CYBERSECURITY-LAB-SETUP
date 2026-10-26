<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Waqas%20Karim%20CCIE-C00000?style=flat-square" />
</p>

---

## 📌 Project Overview

This project documents the setup of a **virtual cybersecurity and penetration-testing laboratory** using VirtualBox and Kali Linux. 

The goal was to create a controlled, isolated environment where security tools, network scanning, and vulnerability assessment can be practiced safely. The lab is built on a private virtual network, allowing for the addition of target machines in future exercises.

---

## 🎯 Objectives

The main objectives of this project were to:

- Install and configure VirtualBox.
- Import and configure Kali Linux as a virtual machine.
- Create a private **NAT Network** (`10.0.0.0/24`) for the lab.
- Assign a static IP address (`10.0.0.2/24`) to the Kali VM.
- Enable clipboard sharing and file drag-and-drop.
- Set up a shared folder (`/downloads`) between the host and Kali.
- Verify network connectivity and DNS resolution.
- Take a clean VM snapshot for recovery.
- Document the entire process with screenshots and explanations.

---

## 🛡️ Purpose of the Lab

The lab provides an isolated environment for cybersecurity learning and authorized security testing. It can be used for activities such as:

- Network reconnaissance
- Port scanning (e.g., with Nmap)
- Vulnerability assessment
- Packet analysis (e.g., with Wireshark)
- Web security testing
- Exploitation practice (e.g., with Metasploit)

⚠️ **Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Unauthorized access is illegal.

---

## 🏗️ Lab Architecture

![](1-screenshot-title-image.png)

The lab is built on a **NAT Network** (`10.0.0.0/24`). The Kali Linux VM is assigned `10.0.0.2`. Additional target machines (Windows, Android, etc.) can be added later to the same network.

---

## ⚙️ Lab Configuration

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | ------------------ |
| 🖥️ Host OS         | Windows 11         |
| 🧠 Host RAM        | 16 GB              |
| ⚡ Processor       | Intel Core i7      |
| 🧰 Hypervisor      | VirtualBox 7.2     |
| 🐉 Security OS     | Kali Linux 2026.2  |
| 🧠 Kali RAM        | 2048 MB            |
| 🌐 Virtual Network | NAT Network        |
| 📡 Network Address | `10.0.0.0/24`      |
| 🐧 Kali IP Address | `10.0.0.2/24`      |
| 🚪 Default Gateway | `10.0.0.1`         |
| 🌍 DNS Server      | `8.8.8.8`          |
| 🔮 Future VM Range | `10.0.0.3–10.0.0.99` |

---

# 🪜 Lab Setup Procedure

## Step 1. Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual-machine package.

## Step 2. Install VirtualBox

VirtualBox was installed as the hypervisor.

## Step 3. Create the NAT Network

A dedicated NAT Network was created with the following settings:

```text
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled
https://2-screenshot-network-settings-1.png/

A NAT Network was chosen because it allows multiple VMs to communicate with each other while also having outbound internet access.

Step 4. Import Kali Linux
The Kali Linux VM was downloaded and imported into VirtualBox. The network adapter was configured as follows:

text
Adapter 1
Attached to: NAT Network
Network:     NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
https://3-screenshot-kali-linux.png/

A shared folder was also configured to transfer files between the host and the Kali VM.

Step 5. Configure the Kali Linux Network
A static IP address was configured for Kali Linux:

text
IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway: 10.0.0.1
DNS: 8.8.8.8
https://4-screenshot-kali-network-settings.png/

Step 6. Create a Clean VM Snapshot
After completing the setup, a snapshot was created with the name Clean Kali - Network Setup. This serves as a baseline for future exercises.

🔎 Lab Verification
✅ Test	🧾 Command	🎯 Expected Result
🌐 Check IP address	ip a	10.0.0.2/24 displayed
📡 Test gateway	ping 10.0.0.1	Successful replies
🌍 Test Internet connectivity	ping 8.8.8.8	Successful replies
🔎 Test DNS resolution	nslookup networkwalks.com	Domain resolves
🧰 Verify Nmap	nmap --version	Nmap version displayed
🔄 Verify snapshot	Restore snapshot and run ip a	Baseline configuration restored
Example Results:

text
IP Address: 10.0.0.2/24
Gateway:    10.0.0.1
DNS:        8.8.8.8
🐞 Problems Encountered & Solutions
Problem 1: Internet Connectivity Issue in Kali Linux
After setting the static IP, Kali Linux lost its internet connection. This is a known issue with VirtualBox v7 and Kali Linux 2026.1 or newer.

Solution:

The following commands were used to fix the issue:

bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
Note: The connection name may vary. I identified my active connection using nmcli connection show before running the commands.

Problem 2: VirtualBox VT-x / Virtualization Error
The VM failed to start initially because hardware virtualization was disabled in the BIOS.

Solution:

Restarted the computer and entered the BIOS/UEFI settings.

Enabled Intel VT-x / Hardware Virtualization.

Saved the changes and restarted.

The VM started successfully.

💡 What I Learned
This project gave me hands-on experience in building a virtual lab from scratch. Key takeaways include:

NAT Network vs. NAT: A NAT Network allows multiple VMs to communicate with each other, which is essential for a multi-machine lab.

Static IP Configuration: I learned how to configure and verify IPv4 settings in Kali Linux.

VM Snapshots: Creating a clean snapshot before any risky activity is crucial for easy recovery.

Troubleshooting: I encountered real-world networking issues and learned how to resolve them using nmcli and BIOS settings.

Documentation: Writing clear, structured documentation is a vital professional skill.

🔐 Security & Ethical Use
This laboratory is intended strictly for educational purposes.

🔗 Tools & Resources
7-Zip: https://7-zip.org/download.html

VirtualBox: https://virtualbox.org/wiki/Downloads

Kali Linux: https://kali.org/get-kali

👤 Author
Omer Bawazir
Cybersecurity Graduate | B084

LinkedIn: https://www.linkedin.com/in/OmerSecure

📌 Project Information
Program Name: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity & Pentesting Lab Setup | Repository: GitHub

text

---

### 📸 خطوات مهمة لإكمال المستودع

1. **أضف الصور:** يجب أن ترفع الصور التالية إلى نفس المستودع (بجانب ملف `README.md`):
   - `1-screenshot-title-image.png` (صورة عامة للمختبر أو شاشة VirtualBox).
   - `2-screenshot-network-settings-1.png` (صورة إعدادات NAT Network في VirtualBox).
   - `3-screenshot-kali-linux.png` (صورة لشاشة Kali Linux تعمل).
   - `4-screenshot-kali-network-settings.png` (صورة لمخرجات أمر `ip a` أو إعدادات الشبكة في Kali).
   *تأكد من أن أسماء الصور مطابقة تماماً لما هو مكتوب في ملف `README.md` لكي تظهر تلقائياً.*

2. **تحقق من الروابط:** تأكد من أن رابط LinkedIn الخاص بك صحيح، وأن اسم المستودع مطابق للصيغة المعتمدة.

3. **التسليم:** بعد رفع كل شيء، اذهب إلى [https://networkwalks.com/submission/](https://networkwalks.com/submission/) واملأ النموذج قبل **الجمعة 11:59 مساءً بتوقيت دبي**.

بالتوفيق في الأسبوع الأول! إذا احتجت مساعدة في صياغة منشور LinkedIn الخاص بهذا المشروع، أخبرني.
