# Windows-Event-Log-Analysis-and-System-Monitoring
# Event Log Analysis and Insights

# Lab: Analyzing Windows Event Logs

## Objectives
This lab will guide you through the process of:
1. Examining existing event logs.
2. Locating and examining event logs that are not in `.evtx` format.
3. Summarizing the presence or absence of event log indicators on your system.

By the end of this exercise, you will gain hands-on experience in analyzing Windows event logs for system and security monitoring.

---

## Pre-requisites
To successfully complete this lab, you should have:
- Basic knowledge of the Windows operating system.
- Familiarity with using the Command Prompt or PowerShell.
- Access to a Windows computer with administrative privileges.

---

## Materials Needed
- **A Windows computer** (Windows 10 or later is preferred).
- **Notebook or text editor** for taking notes and documenting observations.




## Part 1: Event Log Observations and Analysis

#### 1. Which event types (Error, Warning, Information) are most frequent?
**Warnings:**
- The most frequent event type is **Warning**.  
Warnings were frequent from these sources:
  - **DistributedCOM (Event ID: 10016)** – occurred multiple times.
  - **LsaSrv (LSA)**  
  - **Kernel-PnP (Event ID: 219)**  
  - **Win32k**


![Event Logs Screenshot](Eventlogs-screenshot1.jpg)












- Warning from **DistributedCOM** occurred on 10/3/2024 at 10:38 AM (Event ID: 10016).  
- Warning from **VMnetDHCP** occurred on 10/2/2024 at 4:24 PM (Event ID: 1).  
- Warning from **VMnetDHCP (Event ID: 1)** was repeated more than 7 times.  
- Frequent warning sources include:  
  - **Win32k (Event ID unknown)**  
  - **LsaSrv (LSA)**  
  - **Kernel-PnP (Event ID: 219)**  




![Event Logs Screenshot 2](Eventlogs-screenshot2.jpg)






**Errors:**
- Frequent Errors were seen from:  
  - **DistributedCOM (Event ID: 10016)** – appeared more than 10 times.  
  - **SurfaceTconDriver (Event ID: 13)** – occurred more than 10 times.  
  - **Service Control Manager** (Event ID unknown).  

**Critical:**
- Critical events from **Kernel-Power** appeared 3 times.




![Event Logs Screenshot 3](Eventlogs-screenshot3.jpg)





---

#### 2. What are some common Event IDs that you observed?
The following Event IDs were frequently observed:
- **10016** – DistributedCOM  
- **219** – Kernel-PnP  
- **6155** – LSA (LsaSrv)  
- **10317** – Source unknown  
- **13** – SurfaceTconDriver  
- **1** – VMnetDHCP  
- **8265** – EnhancedPhishingProtection  
- **700, 701** – Win32k  

---

#### 3. Did you notice any recurring issues or patterns?
- **DistributedCOM warnings and errors (Event ID: 10016)** were highly frequent, indicating potential permission-related issues.  
- **VMnetDHCP warnings (Event ID: 1)** were repeated often, pointing to possible issues with virtual network services like VMware or VirtualBox.  
- **Kernel-PnP warnings (Event ID: 219)** and **Kernel-Power critical errors** may indicate device connectivity or power management problems.  
- **LsaSrv (LSA)** warnings suggest potential issues with the Local Security Authority Subsystem.  
- Recurring **SurfaceTconDriver errors (Event ID: 13)** may point to hardware or driver-related issues involving display or communication drivers.  
- Multiple warnings and errors from sources such as **Win32k**, **LsaSrv**, and **Service Control Manager** indicate potential system instability involving key services or drivers.

--- 


## Part 2: Locate and Examine Event Logs That Are Not `.evtx` Files

### 1. What types of logs did you find that weren’t .evtx files?
The following command was executed to locate non-.evtx files:  
```powershell
Get-ChildItem -Path C:\ -Recurse -Include *.log, *.txt, *.csv -ErrorAction SilentlyContinue 

The output is displayed in the screenshot below:



![PowerShell Screenshot 1](Powershell-screenshot1.jpg)






![PowerShell Screenshot 2](Powershell-screenshot2.jpg)











