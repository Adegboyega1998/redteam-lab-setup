# Red Team Lab Setup


Isolated multi-VM lab for penetration testing practice.  

Includes Kali (attacker), Metasploitable2 (Linux target), and Windows 10 (Windows target) on a VirtualBox Host-Only network, plus NAT internet for Kali.


## Topology


![Lab Network](network-diagram/lab_network_diagram.png)

- **VirtualBox Host-Only:** `vboxnet0` → `192.168.56.0/24` (DHCP on)

- **NAT:** Kali only (tool updates), targets remain isolated

**VMs & IPs**

- **Kali Linux (attacker):** `192.168.56.106` (Host-Only) + NAT  
- **Metasploitable2 (target):** `192.168.56.107` (Host-Only)  
- **Windows 10 (target):** `192.168.56.102` (Host-Only)

> Evidence screenshots are in `/screenshots`. Raw Nmap outputs go in `/scans`.

## What this project covers

- VirtualBox install & VM imports (Kali, Metasploitable2, existing Win10)
- Host-Only + NAT network configuration
- Connectivity verification with `ping`
- Baseline reconnaissance with **Nmap**: quick scan, full TCP, service/version, OS detect
- Windows Firewall effect on scans (temporarily disabled for learning, then re-enabled)

## Skills demonstrated

- Linux basics (Kali updates, terminal)
- Virtualization & network isolation (Host-Only vs NAT)
- Network discovery & enumeration (ICMP, Nmap)
- Interpreting scan results to plan attacks

## Tools

- **VirtualBox**
- **Kali Linux** (nmap, tcpdump/wireshark available)
- **Metasploitable2**
- **Windows 10 Evaluation**
- **Nmap**

## Repo structure

redteam-lab-setup/
├─ README.md
├─ setup.md # step-by-step with commands \& explanations
├─ network-diagram/
│ └─ lab\_network\_diagram.png
├─ scans/
│ ├─ metasploitable/ # nmap outputs (txt)
│ └─ windows/ # nmap outputs (txt)
└─ screenshots/ # evidence shots (01..25\_\*.png)

## Key evidence (sample)

- `01_virtualbox_installed.png` – VirtualBox installed  
- `02_kali_vm_imported.png`, `03_kali_first_boot.png`, `15_kali_apt_update.png` – Kali ready  
- `04_metasploitable_imported.png`, `05_metasploitable_login_screen.png` – Metasploitable ready  
- `06_windows10_vm_settings.png`, `09_windows10_first_boot.png` – Windows ready  
- `10_host_only_network.png` – Host-Only adapter set  
- `11_…`, `12_…`, `13_…` – VM network settings  
- `14_kali_ping_targets.png` – Connectivity confirmed  
- `16_…`–`20_…` – Nmap installed & scans  
- `21_…`–`25_…` – Windows firewall off → scan → back on

## How to reproduce (short)

1. Install VirtualBox (+ Extension Pack).  
2. Import **Kali** (prebuilt OVA) and update:
- sudo apt update && sudo apt -y full-upgrade
3. Create Metasploitable2 VM using its Metasploitable.vmdk.
4. Use an existing Windows 10 VM (or install from ISO).
5. Create Host-Only network (vboxnet0), enable DHCP.
6. Set adapters:
* Kali: NAT + Host-Only
* Metasploitable2: Host-Only
* Windows: Host-Only
7. Verify with ping from Kali → both targets.
8. Run Nmap scans (quick, full TCP, -sV, -O) and save outputs to /scans.

## Notes

Windows Firewall was disabled temporarily to demonstrate how it affects port visibility, then re-enabled.

All testing occurs on an isolated Host-Only network. Do not scan systems you don’t own or have permission to test.





