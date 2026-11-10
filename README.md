# 🧪 Active Directory Homelab: Home-Brewed Enterprise Chaos
Welcome to my local domain lab—where Active Directory policies are strict, virtual machines run rampant, and RAM usage is a constant cause of existential dread.

This repository documents the creation of *lab.local*, a fully isolated Windows Enterprise domain built from scratch inside Oracle VirtualBox. Built as a hands-on playground to master domain infrastructure, identity management, and upcoming security monitoring, this setup simulates real-world enterprise environments without the risk of accidentally taking down a real company's production network.

## 🏗️ The Architecture (The "Who's Who" of My RAM)
| Node | Role | OS | Purpose |
| --- | --- | --- | --- |
| DC01 | Domain Controller | Windows Server 2022 | The Brain: DNS, AD DS, and enforcer of domain law. |
| USR02Pro | Workstation | Windows 11 Pro | Standard user client domain-joined for daily operational noise. |
| User01Ent | Workstation | Windows 11 Enterprise | Premium target endpoint ready for enterprise policy testing. |

<img width="915" height="463" alt="image" src="https://github.com/user-attachments/assets/eb257d0b-7c1d-405c-8f87-20b2083dd30d" />

## 📂 Organizational Units & Group Policy (GPO) Structure
To keep lab.local running smoothly without absolute entropy, the domain is split into four isolated Organizational Units (OUs), each tailored with its own set of Group Policy Objects:

- 💼 Sales: Locked-down policies to keep users from clicking every suspicious link in sight.

- 🧮 Accounting: Tight network perimeter settings—because nobody messes with payroll.

- 👔 Executive: Elevated domain access, heavily audited (and prayed for).

- 🛡️ IT: Full administrative control, custom diagnostic tooling, and zero restriction settings.

## ⚡ Key Highlights
- Zero to Domain Controller: Standard Windows Server deployment escalated to a functional AD DS root forest.

- Custom Organizational Design: Fully segmented user groups, OU structures, and GPO enforcement.

- Multi-Tier Endpoints: Seamless domain integration across both Windows 11 Pro and Enterprise client builds.

- Controlled Isolation: Internal virtual networking configured so traffic stays inside the lab boundary.

## 🚀 What’s Next? (Future Cyber Mayhem)
This isn't just a static Active Directory setup—it's a launchpad for offensive and defensive cybersecurity experimentation:

- 🦝 SIEM Integration (Wazuh): Deploying host-based agents across all nodes for real-time log telemetry and threat detection.

- 🔍 Vulnerability Assessment: Running automated scans (Nessus/OpenVAS) to find and document misconfigurations.

- 🎯 Attack Surface Testing: Turning lab.local into a target environment to simulate Kerberoasting, privilege escalation, and lateral movement defenses.
