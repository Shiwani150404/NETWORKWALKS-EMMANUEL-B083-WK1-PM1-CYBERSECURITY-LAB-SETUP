# Cybersecurity Lab Environment Setup

Building an isolated virtual lab for penetration testing and ethical hacking practice.

## Project Overview

This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

## Objectives

- Install and configure VirtualBox
- Install/import Kali Linux as a virtual machine
- Create a private NAT Network for the cybersecurity lab
- Configure network connectivity for Kali Linux
- Assign a consistent IP address to the Kali VM
- Verify network connectivity and DNS resolution
- Take a clean VM snapshot for recovery
- Document the complete setup process
- Prepare the environment for future cybersecurity projects

## Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing. It will be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

**Important:** This laboratory will only be used for systems that I own or have explicit permission to test. I will not use the lab or its tools to attack unauthorized systems.

## Lab Configuration

| Component | Configuration |
|---|---|
| Host Machine | LENOVO |
| Host OS | Windows 11 |
| Host RAM | 8GB |
| Processor | Intel Core i3 |
| Hypervisor | VirtualBox 7.2.6 |
| Security OS | Kali 2026.2 |
| Kali RAM | 2048 MB |
| Virtual Network | NAT Network |
| Network Address | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |
| Future VM Range | 10.0.0.3–10.0.0.99 |

## Lab Setup Procedure

### Step 1. Install 7-Zip
7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a `.7z` archive.

### Step 2. Install VirtualBox
VirtualBox was installed as the hypervisor.

### Step 3. Create the NAT Network
A dedicated NAT Network was created in VirtualBox.

**Configuration:**
- Network Name: `NatNetwork`
- IPv4 Prefix: `[10.0.0.0/24]`
- DHCP: Enabled
- IPv6: Disabled

A NAT Network was chosen because multiple VMs connected to the same NAT Network can communicate with one another while also having outbound network connectivity — allowing future attacker and target VMs to communicate within the lab.

### Step 4. Import Kali Linux
The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

**Network adapter configuration:**
- Adapter 1 attached to: NAT Network
- Network: `NatNetwork`
- Adapter Type: Intel PRO/1000 MT Desktop

**VM resources allocated:**
- RAM: 2048 MB
- Processors: 2
- Video Memory: 128 MB

A shared folder was also configured for transferring files between the host OS and the Kali VM.

### Step 5. Configure the Kali Linux Network
The Kali Linux network configuration was checked and set to a consistent IPv4 address.

**Example configuration:**
- IP Address: `[10.0.0.2]`
- Subnet Mask: `255.255.255.0`
- Gateway: `[10.0.0.1]`
- DNS: `[8.8.8.8]`

Network configuration was confirmed via the terminal.

### Step 6. Create a Clean VM Snapshot
After completing the initial configuration, a VirtualBox snapshot was created.

This snapshot represents the clean baseline of the lab — if a future exercise changes or damages the VM, it can be restored to this state.

### Step 7. Configure 'Drag-and-Drop' and 'Shared Clipboard'
To enable file transfer between host and VM, and a shared clipboard, these features were enabled in VirtualBox VM settings, and the VBox Guest Additions image was installed inside the Kali VM.

## Lab Verification

| Test | Command | Expected Result |
|---|---|---|
| Check IP address | `ip a` | Correct Kali IP displayed |
| Test gateway | `ping [10.0.0.1]` | Successful replies |
| Test Internet connectivity | `ping 8.8.8.8` | Successful replies |
| Test DNS resolution | `nslookup networkwalks.com` | Domain resolves |
| Verify Nmap | `nmap --version` | Nmap version displayed |
| Verify snapshot | Restore snapshot and run `ip a` | Baseline configuration restored |

## What I Learned

**1. NAT vs NAT Network**
Before this project I assumed "NAT" was just one setting in VirtualBox. I learned there's a real difference between a plain NAT adapter (which only lets a VM reach the outside world, isolated from other VMs) and a NAT Network (which lets multiple VMs talk to each other *and* reach the internet). That distinction matters a lot once you start adding target machines alongside the attacker VM.

**2. How Virtual Networking Actually Behaves**
Setting up the adapter taught me that a virtual network isn't just a checkbox — the adapter type, the network it's attached to, and the DHCP settings all interact, and getting one wrong quietly breaks connectivity without an obvious error message.

**3. Static IP Configuration**
Assigning a fixed IP to the Kali VM, instead of relying on DHCP, made me actually understand what an IP address, subnet mask, gateway, and DNS server each do — rather than just typing them in because a guide said so.

**4. Snapshots Are a Safety Net, Not an Afterthought**
Taking a clean snapshot right after the initial setup meant I could experiment with configurations later without worrying about breaking the whole lab. It changed how I think about testing in general — always have a known-good state to fall back to.

**5. Documentation Is Part of the Work, Not an Extra Step**
Writing down each step, the exact commands I ran, and the problems I hit (not just the final working config) turned this from "a VM I set up once" into something I can actually repeat, explain to someone else, or reuse as a reference for future projects.

## Security & Ethical Use

This laboratory is intended strictly for educational purposes only.

## Tools & Resources

- 7-Zip: https://7-zip.org/download.html
- VirtualBox: https://virtualbox.org/wiki/Downloads
- Kali Linux: https://kali.org/get-kali

## Author

**[Shiwani Dodke]**
[Cybersecurity Professional B083]

## Project Information

Program Name: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity & Pentesting Lab Setup | Repository: GitHub

