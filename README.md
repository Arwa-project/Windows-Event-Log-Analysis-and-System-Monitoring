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



![PowerShell Screenshot 1](powershell1.jpg)




















![PowerShell Screenshot 2](Powershell-screenshot2.jpg)





## Non-.evtx Log Files

### Identified Log Files
The non-.evtx log files identified in the output are as follows:

- **setupact.log**: Located in `C:\$WINDOWS.~BT\Sources\Panther`
- **setuperr.log**: Located in `C:\$WINDOWS.~BT\Sources\Panther`
- **COPYING.LGPLv2.1.txt**: Located in `C:\Program Files\Adobe\Acrobat DC\Acrobat\AcroCEF`
- **LICENSE.txt**: Located in `C:\Program Files\Adobe\Acrobat DC\Acrobat\AcroCEF`
- **commit.txt**: Located in `C:\Program Files\Adobe\Acrobat DC\Acrobat\WebResources\Resource0\app1`
- **version.txt**: Located in `C:\Program Files\Adobe\Acrobat DC\Acrobat\WebResources\Resource0\OWP\default`
- Other `.txt` files related to Adobe Acrobat (e.g., `symbol.txt`, `zdingbat.txt`) and various language files (`.txt`) in the `C:\Program Files\Autopsy-4.21.0\autopsy\7-Zip\Lang` directory.
- **TableTextServiceYi.txt**: Likely contains text data related to a specific service or process.
- **about_BeforeEach_AfterEach.help.txt**: Appears to be a help document, providing information or instructions regarding certain functions or commands.



### Error Messages in the Files
To assess whether there are any error messages in the log files, it is necessary to open and review the contents of `setupact.log`, `setuperr.log`, and other pertinent log files:

- **setuperr.log**: could include error messages related to problems encountered during Windows installation or updates.
- **setupact.log**:is likely to offer a comprehensive record of the actions executed during the setup, along with any warnings or errors that may have occurred. 

According to the output, setuperr.log has a size of 0 bytes, suggesting that it contains no
messages. In contrast, setupact.log has data (6825 bytes), indicating that it should be examined
for any possible error messages or warnings.

Although there are no apparent errors in the identified text files, further scrutiny of `setupact.log` is necessary to ensure no critical issues are missed.


### How do these logs compare to the .evtx files in terms of detail and structure?

#### Detail:
- **.evtx Files**: these files offer comprehensive information, including timestamps, event IDs, sources, and detailed descriptions of events, which aids in thorough diagnostics and analysis of system behavior.
- **Non-.evtx Files**: the identified non-.evtx logs, such as `setupact.log`, `setuperr.log`, and various `.txt` files (e.g., `LICENSE.txt`, `commit.txt`), generally provide less detailed information.  
  For example:
  - `setupact.log` and `setuperr.log` might contain setup-related information, but `setuperr.log` has a size of 0 bytes, indicating it does not contain any messages.
  - The `.txt` files, like `LICENSE.txt` and `about_BeforeEach_AfterEach.help.txt`, often contain instructions or help content rather than critical system logs.

#### Structure:
- **.evtx Files**: these logs are stored in a binary format designed for the Windows Event Viewer, enabling users to filter, search, and analyze logs based on structured data points.
- **Non-.evtx Files**: the non-.evtx files, such as `setupact.log`, are typically text-based and may lack the structured format found in `.evtx` files.  
  For example:
  - `setupact.log` and `setuperr.log` might contain setup-related information, but `setuperr.log` has a size of 0 bytes, indicating it does not contain any messages.

- The `setupact.log` may have some structure as a log file, but the text files (like `LICENSE.txt` and others) are usually unstructured plain text, making it more difficult to analyze quickly.

In summary, non-.evtx log files offer less detail and organization than `.evtx` files. Their simpler plain text format makes them more accessible, but this can restrict their effectiveness for in-depth troubleshooting tasks.

---

### Part 3: Summarize the Presence or Absence of Event Log Indicators
 












