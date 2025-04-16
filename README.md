<h1 align="center">
  <img src="https://readme-typing-svg.herokuapp.com?size=22&duration=4000&pause=800&color=32CD32&center=true&vCenter=true&width=900&height=60&lines=🧪+Deploying+a+Homelab+for+Simulated+ATT%26CK+Scenarios" alt="Typing animation title">
</h1>

Cybersecurity is a continuous battle between attackers (Red Team) and defenders (Blue Team). To better understand this dynamic, I built a homelab featuring Active Directory (AD) to simulate **MITRE ATT&CK** scenarios in a controlled environment. The goal was to **capture attack logs using Splunk** and gain hands-on experience with detecting and mitigating threats in real time.

⸻

# 🛠️ Project Overview

This project demonstrates the interplay between offensive and defensive cybersecurity operations by:
	
 •	**Deploying a Windows Active Directory Environment**: Setting up a domain controller, user accounts, and security policies.

	
 •	**Simulating Attacks**: Conducting controlled adversarial attacks using techniques mapped to the MITRE ATT&CK framework.

	
 •	**Capturing & Analyzing Logs with Splunk**: Collecting and visualizing security logs to develop real-time detection capabilities.


⸻

# 🏗️ Homelab Setup

Virtualized using VMware/VirtualBox, isolated for safety.

💻 **Virtual Machines**

Target Machine	    -  Windows 10 Pro

Domain Controller	  -  Windows Server 2022

Attacker Machine	  -  Kali Linux

Log Server	        -  Ubuntu (Splunk)



⸻

# ⚙️ Infrastructure Setup
	
 •	**Domain Controller**: Configured with Static IP, promoted to DC 


 ![win server ip](https://github.com/user-attachments/assets/a7b66966-d581-419c-8eaf-fd2ea9baf38e)


 
 •	**User Accounts**: Created with varying privileges


![User Accounts ](https://github.com/user-attachments/assets/0d012af3-5877-4dc5-99a8-cb2fb6b2bb9e)


 
 •	**Windows 10 Endpoint**: Installed Splunk Universal Forwarder + Sysmon

![Target IP](https://github.com/user-attachments/assets/c8c2b1de-27bd-4a13-8f25-63536193b743)



![Universal Forwarder](https://github.com/user-attachments/assets/1e98c158-b7c0-4ba0-b412-ee4f6488b906)



![Sysmon Install](https://github.com/user-attachments/assets/f48ce9f8-49f2-4b72-a52f-3435bc9bbe05)


 
 •	**Kali Linux**: Configured for offensive simulations


![Kali Ip](https://github.com/user-attachments/assets/68c7c1c2-527e-4027-978d-73e4e83e4e98)

	
 •	**Splunk Server (Ubuntu)**: Aggregates logs from all sources


 ![Splunk IP](https://github.com/user-attachments/assets/3f31c17f-bd78-4a5e-a063-b8437c5fc629)



 
 ![Splunk Server ](https://github.com/user-attachments/assets/49d00cce-5c13-4bc2-b46d-a40961c2a5b4)


⸻

# 🧰 Tools Used
	
 •	**Red Team**: Windows PowerShell, Crowbar (Brute-force)

 •	**Blue Team**: Splunk, Sysmon, Windows Event Logs

 •	**Virtualization**: VMware or VirtualBox

⸻

# 🖼️ Architecture Diagram


![AD-Project](https://github.com/user-attachments/assets/bd7621b4-7ea7-4e52-b73c-a761aebab758)

 
 •	Windows Server DC managing Active Directory
 
 •	Windows 10 endpoints joined to domain
 
 •	Kali Linux for simulating adversary actions
 
 •	Splunk to collect logs from all machines
 
 •	**Data Flow:** Logs ➡️ Splunk ➡️ Analysis/Alerting

⸻

# 🔥 Simulated ATT&CK Scenarios

**1. Brute-Force Login with Crowbar (T1110.001)**
	
 •	**Attack:** SSH/RDP brute force using weak credentials 


![crowbar rdp](https://github.com/user-attachments/assets/1504f1e4-66dc-454a-96a7-3506179b4aaf)

  •	**Detection:** Event logs + Splunk dashboard

 
![Logs of Brute force from Kali 1](https://github.com/user-attachments/assets/1352af88-2cda-40e1-bd72-e42c8a6f2caf)


![Logs of Brute force from Kali 2](https://github.com/user-attachments/assets/311c49cd-91b3-4182-b740-75c39e2bd1da)


**Mitigations:**
    
• Enforce strong password policies to prevent weak credentials.

• Implement multi-factor authentication (MFA) for remote access.

• Use account lockout policies to block repeated failed login attempts.

• Monitor login attempts with SIEM tools like Splunk.

⸻

**2. Privilege Escalation via PowerShell (T1136.001)**
	
 •	**Attack:** Created a local user and added to Admin group


![ART 1](https://github.com/user-attachments/assets/59ba97a9-a736-4a1f-b1ea-d2fd170d7e36)


  •	**Detection:** Monitored for new user creation + script execution	


![ART 1 Log 4720](https://github.com/user-attachments/assets/20f2dae9-3358-48df-9410-00decb82bf7c)


![ART 1 logs](https://github.com/user-attachments/assets/b2055942-ba19-47fb-a955-be9f01864386)



**Mitigations:**
  
•	Restrict PowerShell execution policies to prevent unauthorized script execution.

•	Implement privileged access management (PAM) to limit admin account usage.

•	Enable Windows Defender Application Control (WDAC) to prevent unauthorized changes.

•	Monitor user creation events and log privilege escalation attempts in Splunk.

⸻

**3. Execution via Scripting (T1059.001)**
	
 •	**Attack:** Malicious PowerShell script execution


![ART 2](https://github.com/user-attachments/assets/a1dcdf8e-3c69-414d-b88e-125c27e30598)


  
  •	**Detection:** Captured with Sysmon and Event Logs


  ![ART 2 log](https://github.com/user-attachments/assets/047e6525-54fc-43e4-8136-2369b510e8a1)


**Mitigations:**

•	Implement application allowlisting to prevent execution of unapproved scripts.

•	Enable logging and script block logging in Windows to monitor suspicious activity.

•	Use endpoint detection & response (EDR) solutions to detect abnormal script execution.
	  

⸻

**4. Service Stop Attack (T1489)**
	
 •	**Attack:** Disabled critical Windows services


![ART 3](https://github.com/user-attachments/assets/ecba80c4-7cfa-494a-9e69-2afc2fe08686)


  
  •	**Detection:** Logged service shutdown attempts


![ART 3 log](https://github.com/user-attachments/assets/ea91526e-3f18-4454-80c5-5e2689815598)



**Mitigations:**

•	Enforce tamper protection to prevent unauthorized service modifications.

•	Use group policies (GPO) to restrict service control access.

•	Monitor and log all service stop attempts with Splunk alerts.

•	Implement automatic restart policies for critical security services.

⸻

**5. Remote Code Execution via WMI (T1047)**
	
 •	**Attack:** WMI used to execute remote commands


![ART 4](https://github.com/user-attachments/assets/90b8d6d6-6f44-406f-8f39-e7b58477e3ed)



  •	**Detection:** Logged via Sysmon + Event Logs


![ART 4 log](https://github.com/user-attachments/assets/6908f9e2-173e-4308-a063-22862edc88ee)


**Mitigations:**

•	Restrict WMI access to only trusted administrators.

•	Implement host-based firewall rules to block unauthorized remote execution.

•	Use endpoint protection solutions to detect and block abnormal WMI activity.

•	Monitor WMI events in Splunk for early threat detection.

⸻

# 📊 Log Analysis with Splunk

**Collected logs from:**
	
 •	Windows Event Logs (Security, System, Application)
	
 •	Sysmon for advanced visibility
	
 •	Network traffic monitoring

**Key Capabilities**
	
 •	Real-time attack pattern identification
	
 •	Visual dashboards for adversary movement
	
 •	Alerts for malicious behaviors

⸻

# 🎯 Key Takeaways

 
 •	Hands-on ATT&CK simulation boosts Red & Blue Team skills
 
 •	AD monitoring is essential for enterprise defense
 
 •	Splunk enables proactive detection	
 
 •	Simulated adversary actions sharpen incident response

⸻

# ✅ Conclusion

This project demonstrates how to safely simulate Red Team tactics and leverage Blue Team tools like Splunk to detect and mitigate threats in real time. Regular simulation and monitoring are key to staying ahead of evolving cybersecurity challenges.
