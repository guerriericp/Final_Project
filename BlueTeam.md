# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology


The following machines were identified on the network:
- Kali
  - **Operating System**: Debian Kali 5.4.0
  - **Purpose**: The Attacking machine
  - **IP Address**: 192.168.1.90
- ELK
  - **Operating System**: Ubuntu 18.04
  - **Purpose**: Elastic search and kibana
  - **IP Address**: 192.168.1.100
- Target 1
  - **Operating System**: Linux 8
  - **Purpose**: The WordPRess Host
  - **IP Address**: 192.168.1.110
- Capstone
  - **Operating System**: Ubuntu 18.04
  - **Purpose**: The Vulnerable Web Server
  - **IP Address**: 192.168.1.105

### Description of Targets
_TODO: Answer the questions below._

The target of this attack was: `Target 1: 192.168.1.110`

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Name of CPU Usage Monitor

Alert 1 is implemented as follows:
  - **Metric**: WHEN max() OF system.process.cpu.total.pct OVER all documents IS ABOVE 0.5 FOR THE LAST 5 minutes
  - **Threshold**: IS ABOVE 0.5
  - **Vulnerability Mitigated**: Programs taking up an excessive amount of resources, Malicious software
  - **Reliability**: This alert is highly reliable. It might give a couple false positives but overall it will help with CPU usage even if there isn't a malicious software running.
![CPU Usage Monitor alert logs](https://github.com/guerriericp/Final_Project/blob/main/Images/CPU_usage.png "CPU Usage Monitor alert logs")
#### Name of HTTP Request Size Monitor
Alert 2 is implemented as follows:
  - **Metric**: WHEN sum() of http.request.bytes OVER all documents IS ABOVE 3500 FOR THE LAST 1 minute
  - **Threshold**: IS ABOVE 3500
  - **Vulnerability Mitigated**: Could potententially catch DDOS attacks and code injection.
  - **Reliability**: This is a medium reliability alert since it is possible to just have high HTTP traffic. 
![HTTP Request size Monitor](https://github.com/guerriericp/Final_Project/blob/main/Images/HTTP_request_size_blue_team.png "HTTP Request Size Monitor logs")
#### Name of Excessive HTTP Errors
Alert 3 is implemented as follows:
  - **Metric**: WHEN count() GROUPED OVER top 5 'http.response.status_code' IS ABOVE 400 FOR THE LAST 5 minutes
  - **Threshold**: IS ABOVE 400
  - **Vulnerability Mitigated**: Enumeration and Brute Force.
  - **Reliability**: The Alert is highly reliable. It is tracking errors codes that goes beyond 400 and this filters out all the successful responses. If this errors codes are going off in a high amount something is for sure going on.
![Excessive HTTP Errors](https://github.com/guerriericp/Final_Project/blob/main/Images/Excessive_HTTP_Errors.png "Excessive HTTP error logs")
### Suggestions for Going Further (Optional)
_TODO_: 
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 2
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 3
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
