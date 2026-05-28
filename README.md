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

# Shared Mailbox Configuration

Shared Mailboxes Created

| Mailbox | Purpose |
|:----:|:----:|
| info@harford.com | General customer enquiries |
| accounts@harford.com | Finance and billing |
| support@harford.com |	IT support and technical requests |


# Permissions Assigned

| Shared Mailbox | Group |	Permission |
|:----:|:----:|:----:|
| info@harford.com | Management-Team | Full Access + Send As|
| accounts@harford.com	| Finance-Team	| Full Access + Send As |
| support@harford.com	| Support-Team	| Full Access + Send As |



---

# Distribution Lists

 Distribution Lists Created

| Distribution List	| Purpose |
|:----:|:----:|
| allstaff@harford.com	| Company-wide announcements |
| finance@harford.com	| Finance department communication |
| management@harford.com	| Leadership communication |


# Security Configuration

External sender authentication was enabled on all distribution lists to prevent spam and phishing attempts from external sources.


---

# Resource Mailboxes

Room Mailbox

| Resource	| Configuration |
|:----:|:----:|
| Boardroom	| Capacity 10 |
| Booking Type	| Auto Accept |
| Double Booking | Prevention	Enabled |


# Equipment Mailbox

| Resource	| Purpose |
|:----:|:----:|
| Projector	| Meeting equipment booking |



---

# Mail Flow Rules

Rules Configured

| Rule Name	| Purpose |
|:----:|:----:|
| External Disclaimer |	Warn users about external emails |
| HR Redirect	| Redirect HR emails automatically |
| Dangerous Attachment Block | 	Block malicious file types |
| [EXTERNAL] Subject Prefix	| Improve phishing awareness |


# Dangerous File Types Blocked

.exe

.bat

.vbs



---

# Anti-Spam Policy

Custom Policy

| Setting	| Value |
|:----:|:----:|
| Policy Name	| Management Strict Policy |
| Bulk Email Threshold |	5 |
| Applied To |	Management Group |


# Reason for Configuration

Management users are commonly targeted by phishing and impersonation attacks. A stricter spam filtering threshold reduces risk exposure.


---

# Mobile Authentication Security

Security Configuration

Basic Authentication for Exchange ActiveSync was blocked.

Only Modern Authentication is permitted.

# Benefits

Supports MFA
Reduces password spray attacks
Prevents legacy authentication abuse
Improves tenant security posture



---

# Leaver Mailbox Governance

# Access Process
The following approval process was documented before granting mailbox access:

1. HR request submitted
2. Legal approval obtained
3. Manager approval obtained
4. IT grants temporary mailbox access
5. Access reviewed and removed after requirement ends



# Access Granted

| Mailbox	| Access Given To	| Permission |
|:----:|:----:|:----:|
| Former IT Manager Mailbox	| IT Admin	| Full Access |



---

# PowerShell Commands Used

## Connect to Exchange Online

```Powershell Connect-ExchangeOnline```

## Prevent Room Double Booking

```Powershell Set-CalendarProcessing "Boardroom" -AllowConflicts $false```

# Grant Mailbox Permissions

```Powrshell Add-MailboxPermission -Identity accounts@harford.com -User Finance-Team -AccessRights FullAccess```

# Grant Send As Permission

```Powershell Add-RecipientPermission -Identity accounts@harford.com -Trustee Finance-Team -AccessRights SendAs```


---

# Lessons Learned

# Mail Flow Rule Ordering Matters

Transport rules are processed by priority order. Improper rule ordering can cause unintended mail processing behaviour.

# Send As Permission Delays

Send As permissions may take up to 60 minutes to propagate across Exchange Online.

# Room Mailbox Configuration Requires Additional Controls

Auto Accept alone does not prevent double bookings. Additional PowerShell configuration is required.

# Security Awareness Controls Are Important

The [EXTERNAL] subject prefix significantly improves user awareness against phishing emails.

# Governance Documentation Is Critical

Technical implementation alone is insufficient. Proper legal and HR approval processes are required for compliance-related tasks.


---

# Challenges Faced

# Send As Permission Delay

After assigning Send As permissions, emails initially continued showing the sender's personal mailbox.

# Resolution

Waited for Exchange Online permission propagation and re-tested after approximately 60 minutes.


---

# Mail Flow Rule Conflict

Two transport rules attempted to process similar email conditions.

# Resolution

Adjusted rule priority and reviewed conditions carefully.


---

# Room Mailbox Double Booking

Boardroom mailbox initially accepted overlapping meetings.

# Resolution

Configured:

```Powershell Set-CalendarProcessing "Boardroom" -AllowConflicts $false```


---

# External Prefix Applied Internally

The [EXTERNAL] tag initially applied to internal emails.

# Resolution

Updated rule scope to apply only to external senders.


---

# Skills Demonstrated

Exchange Online Administration

Microsoft 365 Administration

Shared Mailbox Management

Distribution List Configuration

Mail Flow Rule Administration

Anti-Spam Security Configuration

PowerShell Administration

Documentation and Governance

Identity and Access Management

Troubleshooting and Incident Resolution



---

# Design Documents

# mailbox-architecture.md

# Purpose

This document defines the Exchange Online mailbox architecture implemented for Harford Property Management.

# Mailbox Types Implemented

| Mailbox Type |	Quantity |
|:----:|:----:|
| Shared Mailboxes | 3 |
| Room Mailboxes |	1 |
| Equipment Mailboxes	| 1 |
| User Mailboxes	| Existing |


# Architecture Decisions

# Shared Mailboxes

Shared mailboxes were used for departmental communication to:

Centralise communication

Allow multiple users to manage incoming emails

Reduce dependency on individual mailboxes


# Room Mailboxes

Room mailboxes were configured for meeting scheduling and resource management.

Equipment Mailboxes

Equipment mailboxes were used for tracking shared resources.


---

# Shared-mailbox-design.md

# Objective

Design secure and manageable shared mailbox access for departments.

# Shared Mailbox Standards

| Standard	| Value |
|:----:|:----:|
| Naming Convention	| department@company.com|
| Access Type	| Group-based permissions |
| Delegation	| Full Access + Send As |


# Security Controls

1. Permissions assigned to groups instead of individuals

2. Least privilege principle applied

3. Auditing enabled through Microsoft 365



---

# Mail-flow-rules.md

# Objective

Improve email security, routing, and phishing awareness.

# Rules Implemented

# External Disclaimer

Warns users when email originates externally.

# HR Redirect

Automatically routes HR emails to designated mailbox.

# Dangerous Attachment Blocking

Blocks executable and script-based file types.

# External Subject Prefix

Adds [EXTERNAL] prefix to external emails.

# Security Benefits

1. Reduces phishing risk

2.Improves user awareness

3. Prevents malicious attachment delivery



---

# anti-spam-configuration.md

# Objective

Implement stricter anti-spam protection for management users.

# Configuration

| Setting	| Value |
|:----:|:----:|
| Bulk Threshold	| 5 |
| Target Users	| Management |
| Protection Level	| High |


# Reasoning

Executives and management users are high-risk phishing targets.


---

# mobile-access-policy.md

# Objective

Secure Exchange Online mobile access.

# Policy Implemented

| Configuration	| Status |
|:----:|:----:|
| Basic Authentication	| Blocked |
| Modern Authentication	| Enabled |
| MFA Compatibility	| Supported |


# Security Benefits

Prevents legacy authentication abuse

Supports Conditional Access

Improves overall tenant security



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





