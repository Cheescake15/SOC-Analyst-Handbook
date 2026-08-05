# 04 — Windows Security

[← Back to the English contents](README.md) | [Magyar változat](../hu/04-windows-security.md)

## Introduction

Windows is widely used on workstations and servers, so SOC analysts often investigate alerts and logs created by Windows systems.

This chapter explains the basic concepts in a beginner-friendly way. The goal is not to cover every technical detail. The focus is on where useful evidence may appear and why an event may be relevant.

## 1. Why Windows Matters in a SOC

A Windows system regularly records activities such as:

- user logons
- program launches
- file changes
- background services
- PowerShell commands
- scheduled tasks
- security events

Most of these are normal. Analysts try to determine whether the activity is expected for the user and device.

## 2. Event Viewer

**Event Viewer** is a built-in Windows tool used to view recorded events.

Important logs include:

### Application

Contains events created by applications.

### Security

May contain:

- successful logons
- failed logons
- account changes
- privilege use
- process creation

### System

Contains events created by Windows system components.

### Applications and Services Logs

Provides more detailed logs for individual components such as:

```text
Microsoft-Windows-PowerShell
Microsoft-Windows-TaskScheduler
Microsoft-Windows-Windows Defender
```

## 3. What Is an Event ID?

An **Event ID** is a number that identifies an event type.

The number alone is not enough. Analysts should also review:

- user name
- computer name
- source IP address
- time
- logon type
- process name

## 4. Useful Event IDs

### 4624 — Successful Logon

Often normal, but it may deserve attention when it occurs at an unusual time, comes from an unknown address, or involves an administrator account.

### 4625 — Failed Logon

One failure may be a typing mistake. Many failures in a short period may indicate a configuration problem, brute force, or password spraying.

### 4688 — A New Process Was Created

A process is a running program.

Examples:

```text
notepad.exe
powershell.exe
cmd.exe
```

PowerShell and Command Prompt are legitimate tools. The important question is which command ran and in which context.

### 4720 — A User Account Was Created

This may be normal administration. It may be more suspicious outside working hours or when the new account quickly receives high privileges.

### 7045 — A Service Was Installed

A new service may be part of normal software installation. Attackers may also use services to keep a program running in the background.

## 5. Logon Type

| Logon Type | Simple meaning |
|---:|---|
| 2 | local logon |
| 3 | network logon |
| 5 | service logon |
| 7 | workstation unlock |
| 10 | Remote Desktop logon |
| 11 | cached corporate logon |

A Remote Desktop logon is not automatically malicious. Context is required.

## 6. Users and Privileges

Administrators can make major system changes.

The **principle of least privilege** means that users should receive only the access required for their work.

This can reduce damage if an account is compromised.

## 7. The Windows Registry

The **Registry** is a central configuration database.

Attackers may also use Registry changes to:

- start programs at logon
- modify system behaviour
- weaken security settings
- maintain persistence

Manual Registry editing can damage a system and should be tested only in a controlled lab.

## 8. Windows Services

A **service** is a program that normally runs in the background.

Examples include Windows Update and Microsoft Defender Antivirus Service.

A service may deserve investigation when:

- it has a misleading name
- it starts an unknown program
- it runs from a temporary directory
- it uses SYSTEM privileges
- it appears after another suspicious event

## 9. Scheduled Tasks

Task Scheduler can automatically start programs and commands.

A scheduled task has:

- a **trigger**, which defines when it starts
- an **action**, which defines what it does

Attackers may also use scheduled tasks for repeated or delayed execution.

## 10. PowerShell

PowerShell is a legitimate Windows command-line and automation tool.

Administrators use it for system management. Attackers may also misuse it because it is powerful and already installed.

Potentially suspicious examples include:

- long unreadable commands
- encoded content
- internet downloads
- security-setting changes
- unknown scripts
- PowerShell started by an Office application

PowerShell logs can be viewed in Event Viewer. Script Block Logging can provide more detail about executed code.

## 11. Processes and the Process Tree

A **process tree** shows which program started another program.

Normal example:

```text
explorer.exe
└── notepad.exe
```

More unusual example:

```text
winword.exe
└── powershell.exe
    └── rundll32.exe
```

This does not prove an attack, but it may justify further investigation.

## 12. Active Directory and Kerberos

Many organisations use **Active Directory**, or AD, to manage users, computers, and permissions centrally.

A **domain controller** helps manage authentication.

**Kerberos** is a common authentication protocol in Windows domains. It uses tickets so that users do not need to send their password to every service.

Key beginner points:

- AD manages corporate identities
- domain controllers are security-critical
- Kerberos uses tickets
- privileged accounts create higher risk

## 13. Simple Investigation Example

A SIEM reports:

```text
02:11 — several failed logons
02:15 — successful remote logon
02:17 — powershell.exe started
02:18 — a new scheduled task was created
```

A beginner analyst may check:

1. which account was used
2. where the logon came from
3. whether the user recognises the activity
4. which PowerShell command ran
5. what the scheduled task starts
6. whether a new file was created
7. whether an external connection occurred
8. whether similar activity appears elsewhere

The first goal is to build a clear timeline.

## 14. Useful Read-Only Commands

```powershell
Get-Process
Get-Service
Get-ScheduledTask
Get-WinEvent -LogName System -MaxEvents 20
eventvwr.msc
```

Use these commands only on systems you own or are authorised to examine.

## 15. Key Points for Beginners

- Event Viewer is an important source of Windows evidence.
- An Event ID identifies an event type, but the details also matter.
- PowerShell, services, and scheduled tasks are legitimate administration tools.
- Attackers may misuse the same tools.
- Events should always be interpreted in context.
- A sequence of events is often more meaningful than one isolated event.

## 16. Review Questions

1. What is Event Viewer used for?
2. How do Application, Security, and System logs differ?
3. What is an Event ID?
4. What may Event 4624 indicate?
5. What may Event 4625 indicate?
6. Why is Event 4688 useful?
7. What does least privilege mean?
8. What is the Windows Registry?
9. What is a Windows service?
10. What are a trigger and an action?
11. Why do administrators and attackers both use PowerShell?
12. What does a process tree show?
13. What is Active Directory?
14. What is the basic role of Kerberos?
15. Why is timeline building useful?

## References

1. Microsoft Learn  
   **4624: An account was successfully logged on**  
   https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4624

2. Microsoft Learn  
   **about Logging Windows PowerShell**  
   https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging

3. Microsoft Learn  
   **Get-WinEvent**  
   https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent

4. Microsoft Learn  
   **Task Scheduler**  
   https://learn.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page

5. Hungarian National Cyber Security Center  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

6. Gyaraki Réka, editor  
   **Az információbiztonság alapjai** [Hungarian]  
   National University of Public Service, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Previous chapter](03-network-fundamentals.md) | [Back to contents](README.md) | [Next chapter →](05-linux-security.md)
