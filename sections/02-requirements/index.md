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
| F7  | The system must allow **duplicate entry prevention** to avoid inserting the same site entry twice. |
| F8  | The system must **validate input** so that the required fields (sitename, URL, username/email) are not empty before saving. |
| F9  | The system must allow **initial setup** by creating required database schema and tables. |
| F10 | The user must **create and confirm a master password** during initial configuration. |

# ACCEPTANCE CRITERIA FOR FUNCTIONAL REQUIREMENTS
F1 is checked when the user is prompted to set a master password on first use and cannot access entries without entering it correctly.<br>
F2 is checked when a new entry is saved in the database and shown in the list after user submits the required fields.<br>
F3 is checked when changes made to any field (website, URL, username, email, password) are saved and visible after update.<br>
F4 is checked when an entry is permanently removed from the database and no longer appears in the list.<br>
F5 is checked when data from a valid import file is successfully parsed and new entries appear in the system.<br>
F6 is checked when an export process produces a file containing the current entries in the system in the correct format.<br>
F7 is checked when a user inserts a new entry and an error message pups up when the field is identical to another one in an existing row.<br>
F8 is checked when the user tries to save a new entry or a modified row and an error message pops up warning that some of the compulsory fields appear empty.<br>
F9 is checked when a setup window pops up at the first launch of the application made by the user.<br>
F10 is checked when during the initial configuration the system allows the user to **set a master password** that will be used at every access.<br>

The **NON-FUNCTIONAL REQUIREMENTS** touch: 
| ID  | Requirement |
|-----|-------------|
| NF1 | The system must **double-check user identity** by requiring the master password again before sensitive modifications. |
| NF2 | The system must provide a **user-friendly GUI**, with: clear buttons, mouse interaction, and message boxes for feedback (warnings, errors, success messages). |
| NF3 | The system must ensure **passwords are never displayed in plain text**; they are automatically hidden when inserted or modified. |
| NF4 | The system must use **strong encryption** to secure passwords. (e.g., AES-256 standard) |
| NF5 | The system must **strengthen the master password** by applying PBKDF2 with high iteration count. (e.g., 1,000,000 rounds) |
| NF6 | The system must **handle wrong insertions** in the database providing an error message instead of crushing. |
| NF7 | The system must detect if configuration already exists to **avoid reconfiguration**. |
| NF8 | The system must ensure that **errors during database creation** are caught and reported clearly. |
| NF9 | The device secret must be generated using a secure **random mechanism** to guarantee uniqueness. |

# ACCEPTANCE CRITERIA FOR NON-FUNCTIONAL REQUIREMENTS
NF1 is checked when any attempt to delete, modify, or export entries requires re-entering the correct master password.<br>
NF2 is checked when buttons are clickable with a mouse, actions trigger confirmation dialogs, and success/error/warning messages are displayed.<br>
NF3 is checked when password fields show masked characters (e.g., ••••) instead of plain text, and never display stored values unencrypted.<br>
NF4 is checked when all stored passwords are encrypted before saving and cannot be retrieved in plaintext without proper decryption.<br>
NF5 is checked when the PBKDF2 function is called when deriving the master key, the iteration count is set to 1,000,000 or more, the derived key has the correct length (e.g., 32 bytes for AES-256) and verifying the same master password with the same device secret produces the same key.<br>
NF6 is checked when the system displays a clear error message to the user explaining the failure and the application does not crash and remains responsive for further operations.<br>
NF7 is checked when a warning message pops up when trying to re-configurate a database that already exists and to which the application has already been connected to.<br>
NF8 is checked when a setup failure is recognized by the system and an error message appears to notify the user to allow him to retry.<br>
NF9 is checked when strong, widely recognized encryption standard (such as SHA) are utilized.<br>

The **IMPLEMENTATION REQUIREMENTS**, which are more technical stuff, are about: 
| ID  | Requirement |
|-----|-------------|
| I1  | The system must use a **database** to store entries and associated credentials. |
| I2  | The database must be **SQL-compatible** for query execution. |
| I3  | The system must be developed in **Python**. |
| I4  | Passwords must be encrypted using the **AES-256 algorithm**. |
| I5  | Master keys must be derived using PBKDF2 with SHA-512 as **key derivation standard**. |
| I6  | The system must **generate a device secret** using uppercase letters + digits, length ≥ 10 characters. |
| I7  | The database must contain at least **two tables**: secrets (for hashed master password and device secret) and entries (for user credentials). |
| I8  | The system must initially connect to a **database server running on localhost**. |

# ACCEPTANCE CRITERIA FOR IMPLEMENTATION REQUIREMENTS
I1 is checked when entries are stored in a structured database file (not just temporary memory).<br>
I2 is checked when database queries (insert, update, delete, select) work using SQL syntax.<br>
I3 is checked when the source code of the application is implemented in Python.<br>
I4 is checked when the verification of the code shows AES-256 encryption is applied when saving passwords.<br>
I5 is checked when the system uses PBKDF2 as the key derivation function, SHA-512 is explicitly used as the hash function in PBKDF2, the derived key length matches the required AES key size (e.g., 32 bytes for AES-256), the derivation process correctly combines the master password and the device secret (salt) and using the same master password and device secret produces consistent keys on repeated derivations.<br>
I6 is checked when the generated device secret respects the parameters.<br>
I7 is checked when the two tables are correctly created at initial setup and contain all needed fields.<br>
I8 is checked when, on startup, the application attempts a connection to a MySQL (or SQL-compatible) database with host set to localhost<br>

# POLITICAL, ECONOMIC AND ADMINISTRATIVE REASONS FOR IMPLEMENTATION REQUIREMENTS
I1 Databases provide scalable and cost-effective storage compared to flat files, they make backup, auditing, and access management easier. Ensures compliance with privacy and data protection regulations (e.g., GDPR).<br>
I2 SQL databases are widely available and free/open-source, lowering costs. Staff and developers are already familiar with SQL, reducing training effort. SQL is a well-established industry standard, reducing risk of vendor lock-in.<br>
I3 Python is free and open-source, reducing licensing costs. It flatters a large community support and abundant libraries speed up development and maintenance. Python is widely accepted in government, academia, and industry for secure applications.<br>
I4 Using a well-tested open algorithm avoids costs of proprietary solutions and reduces risk of breaches (which are financially damaging). It simplifies audits and certifications since AES-256 is widely recognized by IT security standards. AES-256 is an international encryption standard, endorsed by organizations like NIST, ensuring compliance with security policies.<br>

    
        - ...otherwise, implementation choices should emerge *as a consequence of* design (and therefore described in the design section).
- If there are domain-specific terms, these should be explained in a **glossary**.
- Each requirement must have its own **acceptance criteria**.
    - These will be important for the validation phase. 

> You may consider adding a use-case diagram here (via PlantUML) to better visualize the requirements and their relationships
