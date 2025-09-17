---
title: Requirements
has_children: false
nav_order: 3
---

# Requirements

## User stories

In today's world full of technology, people often ignore that issues don't only come form the outside, but they can be oart of the problem, too, if not the problem itself. They are always concerned about major - and legit - problems in digital devices and technolgoies. First of all is probably security and privacy. 

Human beings daily interact with many services and/or products which require, trivially, a username and a password for identification and authentication purposes, but all experts keep suggesting to make up passwords that significantly differ from one another since, without discussing too much technicality, it is one of the best practices we can apply to better safeguard our accounts and personal information. The consequent risk is that people who would like to be compliant with this practice may risk to forget their passwords. One solution they might opt for is transcripting their passwords in a notebooks or even a piece of paper they stick, for instance, on the computer. Finding cybersecurity a very valuable discipline, we thought about trying to develop a quite essential desktop application which any kind of user could be able to use, encountering the basic needs involved in password management and providing an idoneous security level. 

We would not suggest this application for important levels of business, like adopting it as main system in a bank, jobs related with public security and so on. It would definitely require more security barriers, while we implemented for sure a strong encryption protocol, yet was it intended to offer a tool to private users or employers at lower business levels who are not daily exposed to serious attacks. It goes without saying that hackers and malicious users may be more interested in causing discomfort to relevant and well-known organizations, institutions and personalities rather than focusing on ordinary people. 

- Write down [user stories](https://www.atlassian.com/agile/project-management/user-stories) to devise the main __personas__ (user roles) and the activities they will perform via the system to be developed.

## Requirements analysis

The requirements observed to build the application can be divided into functional, non-functional and implementation needs. The former imply some functionality the software should provide to the user, while the non-functional are requiremnts that do not directly concern behavioral aspects (e.g., consistency, availability, security, efficiency). Implementation stuff involves constraints for the entire phase of system realization (e.g, requiring the use of a specific programming language and/or a specific software dependency). 

The **FUNCTIONAL REQUIREMENTS** involve: 
| ID  | Requirement |
|-----|-------------|
| F1  | The system must allow the user to set and use a **master password** to gain access to private data. |
| F2  | The system must allow the user to **add a new entry**, consisting of: website name, URL, username, email, and password. |
| F3  | The system must allow the user to **modify an existing entry**, including one or more fields (e.g., password change). |
| F4  | The system must allow the user to **delete an entry** when it is no longer needed. |
| F5  | The system must allow the user to **import entries** from existing files. |
| F6  | The system must allow the user to **export entries** to a file. |

# ACCEPTANCE CRITERIA FOR FUNCTIONAL REQUIREMENTS
F1 is checked when the user is prompted to set a master password on first use and cannot access entries without entering it correctly.
F2 is checked when a new entry is saved in the database and shown in the list after user submits the required fields.
F3 is checked when changes made to any field (website, URL, username, email, password) are saved and visible after update.
F4 is checked when an entry is permanently removed from the database and no longer appears in the list.
F5 is checked when data from a valid import file is successfully parsed and new entries appear in the system.
F6 is checked when an export process produces a file containing the current entries in the system in the correct format.
 

The **NON-FUNCTIONAL REQUIREMENTS** touch: 
| ID  | Requirement |
|-----|-------------|
| NF1 | The system must **double-check user identity** by requiring the master password again before sensitive modifications. |
| NF2 | The system must provide a **user-friendly GUI**, with: clear buttons, mouse interaction, and message boxes for feedback (warnings, errors, success messages). |
| NF3 | The system must ensure **passwords are never displayed in plain text**; they are automatically hidden when inserted or modified. |
| NF4 | The system must use **strong encryption** to secure passwords. (e.g., AES-256 standard) |

# ACCEPTANCE CRITERIA FOR NON-FUNCTIONAL REQUIREMENTS
NF1 is checked when any attempt to delete, modify, or export entries requires re-entering the correct master password.
NF2 is checked when buttons are clickable with a mouse, actions trigger confirmation dialogs, and success/error/warning messages are displayed.
NF3 is checked when password fields show masked characters (e.g., ••••) instead of plain text, and never display stored values unencrypted.
NF4 is checked when all stored passwords are encrypted before saving and cannot be retrieved in plaintext without proper decryption.


The **IMPLEMENTATION REQUIREMENTS**, which are more technical stuff, are about: 
| ID  | Requirement |
|-----|-------------|
| I1  | The system must use a **database** to store entries and associated credentials. |
| I2  | The database must be **SQL-compatible** for query execution. |
| I3  | The system must be developed in **Python**. |
| I4  | Passwords must be encrypted using the **AES-256 algorithm**. |

# ACCEPTANCE CRITERIA FOR IMPLEMENTATION REQUIREMENTS
I1 is checked when entries are stored in a structured database file (not just temporary memory).
I2 is checked when database queries (insert, update, delete, select) work using SQL syntax.
I3 is checked when the source code of the application is implemented in Python.
I4 is checked when the verification of the code shows AES-256 encryption is applied when saving passwords.

# POLITICAL, ECONOMIC AND ADMINISTRATIVE REASONS FOR IMPLEMENTATION REQUIREMENTS

    
        - ...otherwise, implementation choices should emerge *as a consequence of* design (and therefore described in the design section).
- If there are domain-specific terms, these should be explained in a **glossary**.
- Each requirement must have its own **acceptance criteria**.
    - These will be important for the validation phase. 

> You may consider adding a use-case diagram here (via PlantUML) to better visualize the requirements and their relationships
