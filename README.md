# 🚀 SOAR-EDR Automation

## 🔍 Project Overview
This project automates threat detection and response using **Tines** as the SOAR platform and **Lima Charlie** as the EDR solution. When a suspicious activity (e.g., password recovery tool execution) is detected, an alert is triggered in **Tines**, which sends notifications to **Slack and Email**. The user is then prompted to decide whether to isolate the affected machine.

## 🛠 Features
✅ **Automated Threat Detection** – Detects suspicious activity on a Windows Server 2022 VM.  
✅ **Real-Time Alerting** – Sends Slack and Email notifications containing event details.  
✅ **User-Triggered Response** – Prompts the user to decide if the affected machine should be isolated.  
✅ **Automated Machine Isolation** – If confirmed, Lima Charlie isolates the infected machine.  
✅ **Comprehensive Logging** – Logs detection events and response actions.

## 📌 Architecture Diagram
![SOAR-EDR Workflow](https://github.com/user-attachments/assets/c81de9e0-f78e-4b27-8018-c4cef2012d78)

## 🔧 Prerequisites
Make sure you have the following:
- 🖥 **Windows Server 2022** (VM on VMware/VirtualBox)
- 🔍 **Lima Charlie Account** (for endpoint detection and response)
- 🤖 **Tines Account** (for automation workflows)
- 📩 **Slack Account** (for receiving alerts)
- 📧 **Email Service (SquareX)** (for email notifications)

## 🚀 Step-by-Step Implementation

### 1️⃣ Setting Up Windows Server 2022 on VMware
1️. Download **Windows Server 2022 ISO** from Microsoft's official website.  
2️. Create a new VM in **VMware Workstation**.  
3️. Assign **4GB RAM, 2 CPUs, 60GB disk space**.  
4️. Mount the ISO and complete the installation.  
5️. Install **VMware Tools** for better performance.
![Windows Server 2022](https://github.com/user-attachments/assets/8a19edcc-bad9-4d5e-9276-f735be44c02a)

### 2️⃣ Deploying Lima Charlie
#### 🔹 Installing Lima Charlie Agent on Windows Server 2022
1️. Log into **Lima Charlie** and create an **organization**.  
2️. Generate an **installation key**.  
3️. Download the **Lima Charlie Windows 64-bit sensor**.  
4️. Open **PowerShell as Administrator** and run:  
   ```powershell
   cd Downloads
   ./hcp_win_x64_release_4.29.0.exe -i <paste_installation_key>
   ```
5️. Verify the agent is running in Windows Services.
![LimaCharlie-Installation](https://github.com/user-attachments/assets/0700bcf4-b283-41f2-bf13-0acdcb896b7b)

### 3️⃣ Generating Telemetry Data
🔹 **Download & Execute LaZagne**

1️. Download **LaZagne** from GitHub: [Alessandroz/LaZagne](https://github.com/Alessandroz/LaZagne).  
2️. Disable **Windows Defender** (so it doesn't block LaZagne).  
3️. Run **LaZagne** in PowerShell:
   ```powershell
   ./lazagne.exe
   ```
4️. Confirm that Lima Charlie captures the event in logs.

### 4️⃣ Creating Detection & Response Rules
📌 **Define a rule in Lima Charlie to detect LaZagne execution**:
🔗 [`lima_charlie_D&R_rule`](https://github.com/xAHIINX00/SOAR-EDR-Automation/blob/main/Rules/lima_charlie_D%26R_rule.json)

### 5️⃣ Setting Up Slack & Email Notifications
🔹 **Slack Setup**: Create an channel in Slack, generate a bot token, and add it to your workspace.  
🔹 **Email Setup**: Use **SquareX** for sending alerts.

### 6️⃣ Automation - Connecting Lima Charlie & Tines
🤖 **Integrate Lima Charlie & Tines Workflow**:

1️. Create an **output in Lima Charlie** to send logs to Tines.  
2️. Configure **Tines credentials** to interact with Slack and Lima Charlie.  
3️. Setup workflow in **Tines**:
   - 📩 Send alerts to Slack & Email.
   - 🔄 Prompt user for machine isolation.
   - 🛡 If confirmed, trigger Lima Charlie to isolate the machine.
     
4️. JSON playbook file: [`tines_playbook`](https://github.com/xAHIINX00/SOAR-EDR-Automation/blob/main/playbook/tines_playbook.json)
![Tines-Automation](https://github.com/user-attachments/assets/4bb227bb-f7cc-4e5f-b3d5-d4f1d1e7cc23)

### 7️⃣ Testing the Workflow
✅ Execute **LaZagne** again.  
✅ Verify **Lima Charlie** detects it.  
✅ Check if **Slack & Email notifications** are received.  
✅ Respond to **Tines prompt** to isolate the machine.  
✅ Confirm **Lima Charlie successfully isolates** the system.

## 📷 Output Screenshots
✅ [LaZagne Execution Detection](https://github.com/xAHIINX00/SOAR-EDR-Automation/blob/main/Output/Detection.png)  
✅ Slack & Email Alerts.  
✅ User Prompt for Isolation.  
✅ Machine Isolation Confirmation.  

## 🔥 Future Improvements
🔹 **VirusTotal Integration** – For automatic hash lookups.  
🔹 **Threat Intelligence Enrichment** – Fetch additional threat context.  
🔹 **Multi-EDR Support** – Extend beyond Lima Charlie.

## 🤝 Contributions & Contact
🚀 **Feel free to contribute or reach out**:  
🔗 **GitHub**: [xAHIINX00](https://github.com/xAHIINX00)  
📧 **Email**: (ahinsunil.m@gmail.com)  
💼 **LinkedIn**: [Ahin Sunil M](www.linkedin.com/in/ahinsunil-m) 

---
🚀 **Built with ❤️ by Ahin Sunil M**
