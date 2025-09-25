# azure-sentinel-honeypot
Azure Sentinel honeypot and SOC detection lab simulating real-world attacksazure
This repository documents my hands-on lab project where I deployed a **honeypot environment in Azure** and integrated it with **Microsoft Sentinel (SIEM)** to detect and visualize attacks.

Inspired by: [joshmadakor1/Sentinel-Lab](https://github.com/joshmadakor1/Sentinel-Lab), but extended with my own detections, workbooks, and SOC-style analysis.

---

##  Project Overview
- Deployed **Windows & Linux honeypot VMs** in Microsoft Azure.  
- Configured **Data Collection Rules (DCR)** and **AMA agents** to stream logs into **Log Analytics Workspace**.  
- Integrated with **Microsoft Sentinel** to monitor, detect, and respond to threats.  
- Built **custom analytics rules** in KQL to detect:
  - Brute Force Attempts (Windows & Linux)
  - Privilege Escalation & Role Assignments (Azure AD / Entra ID)
  - Firewall Tampering
  - Malware Detection Events
  - Triggered **incidents & alerts** mapped to MITRE ATT&CK tactics (Credential Access, Privilege Escalation, etc.).  

---

## Architecture
- **Virtual Network (VNet)** – Isolated network to host resources.  
- **Network Security Group (NSG)** – Initially allowed inbound traffic for honeypot exposure.  
- **Virtual Machines** – 2 Windows servers + 1 Linux server for attack surface.  
- **Log Analytics Workspace** – Central log ingestion and storage.  
- **Azure Key Vault** – Target resource for privilege escalation attempts.  
- **Azure Storage Account** – Used for telemetry and attack logging.  
- **Microsoft Sentinel** – SIEM/SOAR solution for detections and incidents.
  
<img width="837" height="531" alt="topology" src="https://github.com/user-attachments/assets/d354cbbd-7304-4616-a745-3109b609c22d" />

  ---
## Provisioning & Resource Setup
- Deployed **2 Windows VMs** and **1 Linux VM** inside a single VNet.  
- Configured **Network Security Groups (NSGs)** with intentionally open inbound rules to simulate insecure conditions.  
- Provisioned **Azure Key Vault** for secret management.  
- Created **Storage Account & Containers** to archive and centralize logs.
![NSG Open Rule](https://github.com/user-attachments/assets/0b5ac6d9-8104-467d-b734-cd213ec6b48f)  
![VMs Deployed](https://github.com/user-attachments/assets/f312a7b1-8e9d-401e-b80b-afaa38e5a119)
![Key Vault Created](https://github.com/user-attachments/assets/86bc2b32-00da-436c-8a90-821ec89011cd)  
*Provisioned Azure Key Vault for generating and managing access keys.*  
![Storage Account Setup](https://github.com/user-attachments/assets/511c76e1-a3bc-48fe-821d-3de381db6d98)  
*Storage account created to capture and export log data.*  


### 2. Connecting to Sentinel
- Created a **Log Analytics Workspace**.  
- Connected resources and ingested logs into Sentinel.  
![Sentinel Integration](https://github.com/user-attachments/assets/295bc4c4-49d8-4bd1-9cba-088517f99fff)  


### 3. Enabling Data Collection
- Set up **Data Collection Rules (DCRs)** to forward logs.  
- Verified logs were successfully ingested.  
![DCR Setup](https://github.com/user-attachments/assets/d8ca361a-1bc5-4832-8a0f-ab14808b0079)  
![Logs Flowing](https://github.com/user-attachments/assets/94388f92-52e6-4186-b9ed-55edf49907ba)

---
## 🎯 Simulated Attacks

To generate realistic activity:
- Performed **brute force login attempts** from attacker VM.  
- Executed malicious commands on the Linux VM.
- Check logs for malicious activity.
![Failed Logins](https://github.com/user-attachments/assets/c77c171d-b286-4973-83e2-3c5f724c448a)  
![Linux Attack](https://github.com/user-attachments/assets/f4134c79-5c18-48bd-9f29-32c32bb007d9)  
![Auth Logs](https://github.com/user-attachments/assets/67ac4c40-a449-48cc-a839-21af2bbfad73)  
![Auth Logs](https://github.com/user-attachments/assets/37882817-d6c0-467e-ae3c-095723396dca)  

---

## 📊 Sentinel Analytics & Workbooks  
- Queried logs with **KQL** to track brute-force attempts and event volume.  
- Created and enabled **analytics rules** for suspicious activity.  
- Built **workbooks** for real-time visualization.    
![Log Volume Query (~54k Events)](https://github.com/user-attachments/assets/bdd4be60-35f2-4317-9cad-dcdb0bfaaf11)    
![Analytics Rules Enabled](https://github.com/user-attachments/assets/d3daf0c7-5069-4703-9d95-d5117c400386)    
![Workbook Dashboard](https://github.com/user-attachments/assets/47ca99c1-1a16-4a52-a96e-8ebb397d7fc9)    


## 🚨 Incidents & Detection
- Sentinel successfully triggered **incidents** from simulated attacks.  
- Detected brute-force attempts and enriched them with attacker information.  

![Incident Detected](https://github.com/user-attachments/assets/65ad8fc9-3f5e-4125-a9ce-eb3411006cdf)  
![Attack Visualization](https://github.com/user-attachments/assets/31560cb9-df7f-4078-9c05-f94be56498b7)  
![Attacker Info](https://github.com/user-attachments/assets/c488b34b-c62d-4241-9f15-0702ebec0526)  

---
