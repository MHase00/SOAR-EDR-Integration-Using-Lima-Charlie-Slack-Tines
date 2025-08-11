# **SOAR-EDR Integration Using LimaCharlie, Slack & Tines** 🚀

[![Security Automation](https://img.shields.io/badge/Security-Automation-blue)](#) [![EDR](https://img.shields.io/badge/EDR-LimaCharlie-orange)](#) [![Workflow](https://img.shields.io/badge/Workflow-Tines-green)](#)

---

## **Introduction**

This project showcases an **end-to-end Security Orchestration, Automation, and Response (SOAR)** setup that integrates:

- **LimaCharlie EDR** for real-time threat detection  
- **Tines** for automated workflow orchestration  
- **Slack** for incident alerts and analyst decision-making  
- **Email** for detailed incident notifications  

### Key Features:
- **Real-time detection** of malicious activity  
- **Automated Slack & Email alerts** with incident details  
- **Interactive analyst prompts** for isolation decisions  
- **Automated endpoint isolation** via LimaCharlie  


---

## **Architecture**

![Architecture Diagram](https://github.com/user-attachments/assets/80f7352e-32f3-4221-87bb-13cab51e981c)

---

## **Descriptive Workflow**

1. LimaCharlie detects a hacktool execution  
2. Detection details sent to **Tines** via webhook  
3. **Tines** sends:
   - Slack alert to `#alerts` channel
   - Email notification with incident details  
4. **Tines** prompts analyst: *Isolate the machine?* (**Y/N**)  
   - **Yes** → LimaCharlie isolates endpoint & sends Slack confirmation  
   - **No** → No isolation action taken  

---

## **Step-by-Step Implementation**

### **Step 1 – Create LimaCharlie Account & Install Agent**
- Deploy a Windows VM  
- Install LimaCharlie agent  
- Verify endpoint appears in LC **Sensors** list  

![Step 1](https://github.com/user-attachments/assets/d5767b83-9b7c-4346-84af-2e324b94effe)  
![Step 1b](https://github.com/user-attachments/assets/e1d85c0c-ccf5-484d-91ba-829a27b05365)  

---

### **Step 2 – Generate Telemetry for Detection**
- Disable Microsoft Defender (lab-only)  
- Download & execute **LaZagne** from GitHub  
- Confirm LC captures telemetry  

![Step 2](https://github.com/user-attachments/assets/a0119f65-26c2-48b7-8d9b-04f88074b5df)  
![Step 2b](https://github.com/user-attachments/assets/0b9d87f0-75c9-4d9a-8a06-5602db81bebe)  

---

### **Step 3 – Create Detection Rule in LimaCharlie**
- Define rule matching hacktool execution  
- Test rule using captured event data  

![Step 3](https://github.com/user-attachments/assets/82b77dc4-0c32-462c-b8b9-cad8c38d7bc8)  
![Step 3 Test](https://github.com/user-attachments/assets/8f25218b-41db-4c58-bc1e-7f5d2ebd665a)  

---

### **Step 4 – Validate Detection**
- Rerun LaZagne  
- Confirm detection triggers in LC within minutes  

![Step 4](https://github.com/user-attachments/assets/24532da1-9213-4bda-b570-f185af7d5a75)  

---

### **Step 5 – Setup Slack and Tines Accounts**
- Create Slack workspace & channel `#alerts`  
- Create Tines account  

![Step 5](https://github.com/user-attachments/assets/5b28e898-d763-47e7-af11-0dd3e88bef44)  

---

### **Step 6 – Connect LimaCharlie to Tines**
- Generate webhook in Tines (“Retrieve LC Detection”)  
- Add webhook in LC Outputs → Detections  

![Step 6](https://github.com/user-attachments/assets/a19bd68e-6d73-43a0-b697-1c633ff683ef)  
![Step 6b](https://github.com/user-attachments/assets/cad421bf-c58a-4c6b-a815-f81fe12fa0ce)  

---

### **Step 7 – Test LC → Tines Integration**
- Run LaZagne again  
- Verify detection in both LC and Tines  

![Step 7](https://github.com/user-attachments/assets/86362e70-507d-489e-8a1a-d9671e57c46b)  

---

### **Step 8 – Configure Slack Integration in Tines**
- Add Slack credentials in Tines  
- Install Tines app in Slack  
- Use Channel ID for `#alerts`  

![Step 8](https://github.com/user-attachments/assets/68bae88b-d228-40c7-aa6a-594bdcc1cce3)  
![Step 8b](https://github.com/user-attachments/assets/6eac5931-7fb4-406a-b867-6bf3de8b3516)  
![Step 8c](https://github.com/user-attachments/assets/16fdda8e-2931-49a5-9154-583a07d6b0a4)  

---

### **Step 9 – Verify Slack Alerts**
- Send test detection  
- Confirm message appears in `#alerts`  

![Step 9](https://github.com/user-attachments/assets/9d87b111-5e37-435c-85f6-f3f9125161a7)  

---

### **Step 10 – Configure Email Notifications**
- Add email credentials in Tines (temp email for testing)  
- Send test detection  
- Verify email received  

![Step 10](https://github.com/user-attachments/assets/ef30aa25-eda6-4c7d-938a-86de70601db9)  
![Step 10b](https://github.com/user-attachments/assets/bb161bf1-c9b6-41b1-b60a-b1c395190e14)  

---

### **Step 11 – Create User Prompt Page in Tines**
- Add page with “Isolate Machine? (Yes/No)”  
- Display detection parameters: Time, Source IP, Hostname, Command Line, File Path  

![Step 11](https://github.com/user-attachments/assets/700a0b53-b630-4b6b-97c6-3248aee01043)  
![Step 11b](https://github.com/user-attachments/assets/3c071f68-3e77-40c1-9ff9-f3b5194b5f22)  
![Step 11c](https://github.com/user-attachments/assets/c92cb125-fefc-4856-bf42-dbc55c0e1e32)  
![Step 11d](https://github.com/user-attachments/assets/8665c3ee-1764-432b-bd15-d2b894671c7b)  

---

### **Step 12 – Add Conditional Workflow Logic**
- If **Yes** → Execute LC isolation template  
- If **No** → End workflow  

![Step 12](https://github.com/user-attachments/assets/c5caa4f8-3946-4f68-892b-ea8786fd9fb6)  
![Step 12b](https://github.com/user-attachments/assets/8457430a-a66d-46cc-8d57-d74e0f407a16)  

---

### **Step 13 – Connect LC Isolation Action**
- Use `routing.sid` from detection event  
- Test isolation on lab endpoint  

![Step 13](https://github.com/user-attachments/assets/4f36a514-e3ec-42af-98d5-abaa5f898495)  
![Step 13b](https://github.com/user-attachments/assets/342b95fe-4519-4c5d-bf1a-ae4620cd4416)  
![Step 13c](https://github.com/user-attachments/assets/9cd77709-beee-4a85-81ed-8116ecc050f7)  

---

### **Step 14 – Important Note**
> **True** and **False** values are case-sensitive in Tines workflows.

![Step 14](https://github.com/user-attachments/assets/e6be5929-d2fb-4a90-85aa-a3b4f4df2e13)  

---

### **Step 15 – Final Working Workflow**
- End-to-end automation from detection → alert → decision → isolation  

![Step 15](https://github.com/user-attachments/assets/0d7dc255-3dcf-45e6-9b4d-ab9b09ba9e6d)  

---

## **Conclusion**
You have now built a complete **SOAR EDR pipeline** integrating **LimaCharlie**, **Tines**, **Slack**, and **Email**.  
This demonstrates capabilities in:
- Threat detection  
- Incident automation  
- Workflow orchestration  
- Endpoint response  
