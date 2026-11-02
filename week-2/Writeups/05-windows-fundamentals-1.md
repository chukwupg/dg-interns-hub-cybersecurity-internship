<!-- DRAFT: rewrite in your own words. No room answers or flags. Fill every [[ ]]. -->
# Windows Fundamentals 1 (TryHackMe)

**Link:** https://tryhackme.com/room/windowsfundamentals1xbx

## Goal
Getting comfortable with the Windows desktop, file system, user accounts, UAC and Task Manager. 

## Task-by-task
| Task | What it covered | My note |
|---|---|---|
| 1. Windows Editions | Windows desktop and server editions, version history and support lifecycle | Reviewed the evolution of Windows, from earlier versions such as XP and Windows 7 to Windows 10 and 11. Also introduced Windows Home and Pro editions and Windows Server. The lab machine runs Windows Server 2019 Standard. |
| 2. Introduction to Windows | Lab environment setup and remote access | Started the AttackBox and Windows lab machine, with the option to access the target through the browser or Remote Desktop Protocol (RDP) using the supplied credentials. |
| 3. The Desktop (GUI) | Windows graphical interface, Desktop, Start menu, Taskbar and Notification Area | Explored the Windows GUI, including desktop shortcuts, Start menu sections, pinned applications, Task View, taskbar toolbars and notification icons. Learned how to personalize the desktop and manage display settings. |
| 4. The File System | NTFS, file permissions and Alternate Data Streams | Learned about NTFS features such as journaling, file permissions, compression and encryption. Explored permissions including Full Control, Modify, Read, Write and Read & Execute. Also learned how Alternate Data Streams (ADS) can store hidden data and potentially be abused by malware. |
| 5. The Windows\\System32 Folders | Windows directory structure, environment variables and critical system files | Explored the Windows installation directory (`C:\\Windows`), the `%windir%` environment variable and the `System32` folder. Learned that System32 contains essential operating system files and that modifying or deleting its contents can damage Windows. |
| 6. User Accounts, Profiles, and Permissions | Administrator and Standard accounts, user profiles and local groups | Learned how account types determine user privileges and how Windows stores user profiles under `C:\\Users`. Explored Local Users and Groups Management (`lusrmgr.msc`) to inspect accounts, groups and their assigned permissions. |
| 7. User Account Control | Privilege elevation and administrative approval | Learned how User Account Control (UAC) helps prevent unauthorized system changes by prompting for approval or administrator credentials when an operation requires elevated privileges. |
| 8. Settings and the Control Panel | Windows configuration interfaces and installed applications | Explored Settings and Control Panel as interfaces for managing system configurations. Used Programs and Features to inspect installed applications and learned that some configuration options in Settings redirect to Control Panel. |
| 9. Task Manager | Running applications, processes and system resource monitoring | Explored Task Manager to inspect running applications and processes, monitor CPU and RAM usage, and access detailed system information. Learned to switch from Simple View to the expanded view for more administrative and troubleshooting details. |

## Screenshot
![Windows Fundamentals 1 room](/Findings/TryHackMe/windows-fundamentals-1.png)

## What I Learned
- Windows editions serve different environments, from personal desktop use to enterprise and server deployments. Understanding the edition and version of a target system helps establish its capabilities and support status.
- The Windows GUI provides several ways to access applications, files and system tools. Knowing how to navigate the Desktop, Start menu, Taskbar and Notification Area improves system administration efficiency.
- NTFS provides important security and reliability features, including journaling, access control permissions, compression and encryption.
- Alternate Data Streams (ADS) allow additional data to be attached to files on NTFS volumes. Although they have legitimate uses, attackers can abuse them to conceal malicious data.
- The C:\Windows\System32 directory contains critical operating system components. Understanding its role is important when investigating suspicious files, processes and system modifications.
- Windows distinguishes between Administrator and Standard accounts to enforce privilege boundaries. Users should operate with only the permissions required for their tasks.
- User profiles are created when users first log in and are stored under C:\Users. Local groups simplify permission management because users inherit permissions assigned to their groups.
- User Account Control (UAC) helps prevent unauthorized administrative changes by requiring approval or administrator credentials when elevated privileges are needed.
- Settings and Control Panel provide access to Windows configuration options, while Programs and Features can help identify installed software during system audits.
- Task Manager is useful for troubleshooting and basic security monitoring because it exposes running processes, resource consumption and other system activity.
- Understanding Windows file systems, permissions, account privileges and built-in management tools provides a foundation for Windows administration and security investigations.

## How this shows up in my lab
- I created `labtest` with `net user` and added it to Administrators (events 4720 and 4732), then signed in as that user (4624, logon type 2).

    **Simulation user creation and adding to Administrator group**
    ![user creation](/Findings/windows-events/simulating-new-user-and-add-administrator.png)

    **Event log**
    ![4624 logon type 2 log](/Findings/windows-events/event-viewer-successful-logon-type-2.png)
