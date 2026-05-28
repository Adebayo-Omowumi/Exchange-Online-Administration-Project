# Exchange-Online-Administration-Project

---

# Project Overview
This project demonstrates the implementation and administration of a secure and properly configured Exchange Online environment for Harford Property Management after migrating from on-premises Exchange to Microsoft 365.

---

# The project covers:
Shared mailbox administration

Distribution list management

Mail flow configuration

Anti-spam protection

Room and equipment mailbox configuration

Exchange Online security hardening

Leaver mailbox access governance

Documentation and troubleshooting 

---

# Business Scenario
Harford Property Management recently migrated from on-premises Exchange Server to Exchange Online. The environment lacked proper mailbox delegation, shared mailboxes, mail flow controls, anti-spam protection, and governance processes.

---

# Technologies Used
| Technology | Purpose |
|:----:|:----:|
| Microsoft 365 | Cloud productivity platform |
| Exchange Online | Email and mailbox administration |
| Microsoft Entra ID | Identity and authentication |
| Exchange Admin Center | Exchange administration
| Microsoft Defender for Office 365 | Anti-spam and mail security |
| PowerShell | Advanced Exchange configuration |
| GitHub | Documentation repository |

---

# Environment Configuration
| Configuration Item | Value |
|:----:|:----:|
| Tenant Type | Microsoft 365 Business |
| Email Platform | Exchange Online |
| Authentication | Modern Authentication |
| Mailbox Types | User, Shared, Room, Equipment |
| Security Controls | Mail flow rules, Anti-sperm polies |

---
# Exchange-Online-Administration-Project/
│
├── README.md
│
├── Design-Documents/
│   ├── mailbox-architecture.md
│   ├── shared-mailbox-design.md
│   ├── mail-flow-rules.md
│   ├── anti-spam-configuration.md
│   └── mobile-access-policy.md
│
├── Runbooks/
│   ├── create-shared-mailbox.md
│   ├── create-distribution-list.md
│   ├── grant-mailbox-permissions.md
│   ├── create-room-mailbox.md
│   ├── create-equipment-mailbox.md
│   ├── create-transport-rule.md
│   └── access-leaver-mailbox.md
│
├── Change-Records/
│   └── exchange-online-initial-build.md
│
└── Troubleshooting/
    ├── send-as-delay.md
    ├── mail-flow-rule-conflicts.md
    ├── room-mailbox-booking-conflicts.md
    └── shared-mailbox-send-as-failure.md






---





---


---












---



---




---





---

# create-distribution-list.md

# Objective

Create a distribution list for departmental communication.

# Steps

1. Open Exchange Admin Center

2. Navigate to Recipients > Groups

3. Create Distribution List

4. Add group members

5. Enable authenticated senders only

6. Save configuration

# Validation

# Emails delivered successfully

External senders blocked



---

# grant-mailbox-permissions.md

# Objective

Grant mailbox delegation permissions.

# Steps

1. Open mailbox properties

2. Navigate to Mailbox Delegation

3. Add Full Access permission

4. Add Send As permission

5. Save configuration

6. Wait for propagation



# Important Note

Send As permissions may take up to 60 minutes to propagate.


---

# create-room-mailbox.md

3 Objective

Create a room mailbox for meeting scheduling.

Steps

1. Open Exchange Admin Center

2. Navigate to Recipients > Resources

3. Create Room Mailbox

4. Configure room capacity

5. Enable Auto Accept

6. Configure conflict prevention



# PowerShell Configuration

```Powershell Set-CalendarProcessing "Boardroom" -AllowConflicts $false```


---

# create-equipment-mailbox.md

# Objective

Create an equipment mailbox.

Steps

1. Open Exchange Admin Center

2. Navigate to Recipients > Resources

3. Create Equipment Mailbox

4. Configure booking settings

5. Save configuration




---

# create-transport-rule.md

# Objective

Create Exchange Online mail flow rules.

# Steps

1. Open Exchange Admin Center

2. Navigate to Mail Flow > Rules

3. Create new rule

4. Configure conditions

5. Configure actions

6. Set rule priority

7. Test functionality



# Validation

Rule triggers correctly

Internal mail unaffected

External mail processed successfully



---

# access-leaver-mailbox.md

# Objective

Grant temporary access to a former employee mailbox.

# Approval Requirements

HR approval

Legal approval

Management approval


#Steps

1. Verify approval documentation

2. Open mailbox properties

3. Navigate to Mailbox Delegation

4. Grant Full Access permission

5. Document access period

6. Review and remove access later



# Security Considerations

Access must be temporary

Access must be documented

Activity should be auditable



---



---




---

# mail-flow-rule-conflicts.md

# Problem

Mail flow rules process emails incorrectly.

# Cause

Rules evaluated in incorrect priority order.

# Resolution

Review transport rule order

Adjust rule priority

Enable or disable Continue Processing Message option carefully



---

# room-mailbox-booking-conflicts.md

# Problem

Room mailbox accepts overlapping meetings.

# Cause

AllowConflicts setting enabled.

Resolution

Run:

```Powershell Set-CalendarProcessing "Boardroom" -AllowConflicts $false```


---

# shared-mailbox-send-as-failure.md

# Problem

Emails sent from shared mailbox display personal sender address.

# Cause

Send As permission not fully propagated.

$ Resolution

Verify Send As permission assignment

Wait for propagation

Restart Outlook

Re-test mail flow



---

# Conclusion

This project demonstrates foundational Exchange Online administration skills including mailbox management, transport rule configuration, anti-spam protection, PowerShell administration, governance documentation, and operational troubleshooting.

The implementation improved communication management, security posture, phishing awareness, and compliance readiness for Harford Property Management.


---

# Author

Abosede Omowumi Adebayo M365 Engineer | Exchange Online Administrator | Microsoft 365 Administrator





