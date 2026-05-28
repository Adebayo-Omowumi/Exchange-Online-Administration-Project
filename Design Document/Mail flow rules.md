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



