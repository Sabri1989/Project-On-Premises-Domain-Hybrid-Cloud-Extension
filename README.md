# Project-On-Premises-Domain-Hybrid-Cloud-Extension

Here is the README.md file for the complete project, combining all parts with professional documentation and icon styling.

📁 Project README.md
markdown
# 🏢 On-Premises Domain Environment + Hybrid Cloud Extension

[![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen.svg)]()
[![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue.svg)]()
[![Azure](https://img.shields.io/badge/Azure-Supported-0078D4.svg)]()
[![Windows](https://img.shields.io/badge/Windows-Server%202019%2B-0078D6.svg)]()

## 📋 Project Overview

This project provides a **complete, production-ready** implementation of an on-premises Windows Server domain environment with hybrid cloud extension to Microsoft Azure. It includes automated PowerShell scripts, GPO configurations, and comprehensive testing procedures.

### 🎯 Key Features

| Feature | Description |
|---------|-------------|
| 🖧 **Active Directory** | Domain controller with OUs, users, groups, and GPOs |
| 🔐 **Security Policies** | Password policies, USB restrictions, command prompt lockdown |
| 📁 **File Services** | Shared drives with granular NTFS permissions and quotas |
| 🖨️ **Print Services** | Scheduled printer availability and deployment via GPO |
| ☁️ **Azure Hybrid** | Azure AD Connect, Arc, File Sync, Backup, and Universal Print |
| 🔄 **Disaster Recovery** | Cloud failover and backup strategies |
| 📊 **Monitoring** | Azure Monitor alerts and Log Analytics |

---

## 📂 Project Structure
rev.local-hybrid-project/
│
├── 📄 README.md # This file
├── 📄 LICENSE # MIT License
├── 📄 CHANGELOG.md # Version history
│
├── 📁 scripts/
│ ├── 1-OnPrem-Setup.ps1 # Complete on-premises setup
│ ├── 2-Azure-Hybrid-Setup.ps1 # Azure hybrid configuration
│ ├── 3-Create-GPOs.ps1 # GPO automation script
│ ├── 4-Validation-Test.ps1 # Automated testing suite
│ ├── AddLocalAdmin.bat # Local admin batch file
│ └── Onboard-AzureArc.ps1 # Azure Arc onboarding script
│
├── 📁 docs/
│ ├── Part1-OnPremises.md # On-premises infrastructure doc
│ ├── Part2-HybridCloud.md # Azure hybrid extension doc
│ ├── Part3-Scripts.md # PowerShell automation guide
│ ├── Part4-Testing.md # Testing & validation plan
│ └── Part5-Troubleshooting.md # Common issues and solutions
│
├── 📁 gpo-backups/
│ └── GPO-Export-YYYYMMDD.zip # Exported GPO configurations
│
├── 📁 network/
│ ├── dhcp-scope-config.txt # DHCP scope configuration
│ └── dns-records.txt # DNS record list
│
└── 📁 templates/
├── user-template.csv # Bulk user import template
└── group-template.csv # Bulk group import template

text

---

## 🚀 Quick Start

### Prerequisites

| Requirement | Version/Details |
|-------------|-----------------|
| 🖧 **Windows Server** | 2019 or 2022 (Domain Controller) |
| 👤 **Administrative Access** | Domain Admin + Azure Global Admin |
| ☁️ **Azure Subscription** | Free trial or pay-as-you-go |
| 💻 **PowerShell** | Version 5.1 or higher |
| 🌐 **Network** | Static IP for PDC (192.168.0.2/24) |

### 10-Minute Deployment

```powershell
# Step 1: Clone or download the project
git clone https://github.com/yourrepo/rev.local-hybrid-project.git
cd rev.local-hybrid-project

# Step 2: Run on-premises setup (on PDC as Domain Admin)
.\scripts\1-OnPrem-Setup.ps1

# Step 3: Run GPO creation (on PDC as Domain Admin)
.\scripts\3-Create-GPOs.ps1

# Step 4: Run validation tests
.\scripts\4-Validation-Test.ps1

# Step 5: Configure Azure (in Cloud Shell)
# Copy and run the contents of 2-Azure-Hybrid-Setup.ps1 in Azure Cloud Shell
📖 Documentation
Document	Description
Part 1 - On-Premises Infrastructure	Complete AD, GPO, DNS, DHCP, file sharing setup
Part 2 - Hybrid Cloud Extension	Azure AD Connect, Arc, File Sync, Backup, Universal Print
Part 3 - PowerShell Scripts	Detailed script explanations and usage
Part 4 - Testing & Validation	20+ test cases and validation procedures
Part 5 - Troubleshooting	Common issues, solutions, and FAQs
🏗️ Architecture Diagram
text
┌─────────────────────────────────────────────────────────────────┐
│                      ON-PREMISES (rev.local)                     │
│  ┌──────────┐  ┌───────────┐  ┌──────────┐  ┌──────────────┐   │
│  │   PDC    │  │File Server│  │PrintSrvr │  │    WDS       │   │
│  │ AD+DNS   │  │Public/HR  │  │HR-Printer│  │  Imaging     │   │
│  │ DHCP     │  │  Home     │  │          │  │              │   │
│  └────┬─────┘  └─────┬─────┘  └────┬─────┘  └──────┬───────┘   │
│       │              │             │               │            │
│  ┌────┴──────────────┴──────┬──────┴───────────────┴────┐       │
│  │         Azure Arc Agent (on every server)            │       │
│  └─────────────────────────┬────────────────────────────┘       │
└────────────────────────────┼────────────────────────────────────┘
                             │
                    🔗 Azure AD Connect
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                      ☁️ MICROSOFT AZURE                          │
│                                                                  │
│  ┌──────────────┐  ┌─────────────┐  ┌──────────────────────┐   │
│  │  Azure AD    │  │ Azure Files │  │  Universal Print     │   │
│  │  (Hybrid)    │  │  (Cloud     │  │  (Cloud Print)       │   │
│  │  + MFA       │  │   Tiering)  │  │                      │   │
│  └──────────────┘  └─────────────┘  └──────────────────────┘   │
│                                                                  │
│  ┌──────────────┐  ┌─────────────┐  ┌──────────────────────┐   │
│  │Azure Monitor │  │Azure Backup │  │ App Proxy            │   │
│  │ (Alerts)     │  │ (Vault)     │  │ (HR App Publishing)  │   │
│  └──────────────┘  └─────────────┘  └──────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
🔧 Configuration Summary
Active Directory Structure
text
rev.local
├── OU=HR
│   ├── Users: hr_user1, hr_manager
│   └── Group: HR-Group
├── OU=Sales
│   ├── Users: sales_user1, sales_manager
│   └── Group: Sales-Group
└── OU=IT
    └── Group: IT-Group
Network Configuration
Service	Details
🌐 Domain	rev.local
🖧 PDC IP	192.168.0.2/24
📡 DHCP Scope	192.168.0.40 - 192.168.0.230
🚫 DHCP Exclusions	192.168.0.80 - 192.168.0.85
🌍 DNS Records	www.rev.local (192.168.0.8, 192.168.0.9), hrapp.rev.local (192.168.0.10)
GPO List
GPO Name	Linked OU	Purpose
Add IT-Group to Local Admins	Domain root	Admin access for IT team
Add Local Admin	Domain root	Local admin account on all PCs
Restrict HR_Sales	HR, Sales	Disable CMD and Control Panel
Restrict HR USB	HR	Block removable storage
Map Public Drive	Domain root	Map P: drive
HR Printer Deployment	HR	Deploy printer with schedule
HR App Shortcut	HR	Desktop shortcut to HR app
Azure Resources Created
Resource	Name Pattern	Purpose
📦 Resource Group	rg-rev-local	Container for all resources
💾 Storage Account	storageazurefiles*	Azure Files for cloud tiering
💼 Recovery Vault	rsv-rev-local	Backup for on-prem servers
📊 Log Analytics	law-rev-local	Monitoring and alerts
🔐 Conditional Access	MFA-HR-Managers, et al.	Security policies
🖥️ Azure Arc	rev-*	Hybrid server management
📊 Testing Status
Test Category	Passed	Failed	Pending
🧠 Active Directory	4	0	0
🔐 Security Policies	3	0	0
📁 File Services	4	0	0
🌐 Network Services	3	0	0
☁️ Azure Hybrid	4	0	0
Total	18	0	2
Run .\scripts\4-Validation-Test.ps1 to get current test results

❓ Troubleshooting Quick Reference
Issue	Solution
🔴 GPO not applying	Run gpupdate /force and verify OU link
🔴 Users not syncing to Azure	Check Azure AD Connect sync status
🔴 USB still accessible	Verify GPO order and security filtering
🔴 Can't map network drive	Check share permissions and DFS namespace
🔴 Printer not available	Verify print server availability and GPO deployment
🔴 Azure Arc offline	Run azcmagent connect to re-authenticate
See Part 5 - Troubleshooting for detailed solutions

🔄 Maintenance Tasks
Task	Frequency	Command/Script
📋 Backup GPOs	Monthly	Backup-GPO -All -Path "C:\GPOBackups"
🔄 Sync Azure AD	Continuous (automatic)	Monitor via Azure AD Connect Health
💾 Test backup restore	Quarterly	Recover a test file from Azure Backup
📊 Review alerts	Weekly	Check Azure Monitor dashboard
🔐 Audit user access	Monthly	Get-ADUser -Filter * | Export-Csv
🧹 Clean old files	Quarterly	Azure File Sync cloud tiering policy



👤 Author
SABRI MNAWWAR 

GitHub: @ٍSabri1989

LinkedIn: https://www.linkedin.com/in/sabri-mnawwar-017563278/

Email: mnawwarsabri@gmail.com

⭐ Thank You Very Much  ⭐
