# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

```bash
$ nmap -sV 192.168.1.110
```
![NMAP scan](https://github.com/guerriericp/Final_Project/blob/main/Images/nmap_scan_final_project.png "NMAP scan")

This scan identifies the services below as potential points of entry:
- Target 1
 1. Port 22/TCP 	    Open 	SSH
 2. Port 80/TCP 	    Open 	HTTP
 3. Port 111/TCP 	Open 	rcpbind
 4. Port 139/TCP 	Open 	netbios-ssn
 5. Port 445/TCP 	Open 	netbios-ssn


The following vulnerabilities were identified on each target:
- Target 1
 1. User Enumeration
 2. Weak user password
 3. Misconfiguration of User Priviledges 

### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: b9bbcb33ellb80be759c4e844862482d
    - **Exploit Used**
      - WPScan to enumerate users of the targeted WordPress site
      - `$ wpscan --url http://192.168.1.110 --enumerate u`
    - User 'Michael' is our target
  - `flag2.txt`: _TODO: Insert `flag2.txt` hash value_
    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Include the command run_
