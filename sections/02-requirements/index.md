---
title: Requirements
has_children: false
nav_order: 3
---

# Requirements

## User stories

In today's world full of technology, people often ignore that issues don't only come from the outside, but they can be part of the problem, too. They are always concerned about major - and legit - problems in digital devices and technolgoies. First of all is probably security and privacy. 

Human beings daily interact with many services and/or products which require a username and a password for identification and authentication purposes, but all experts keep suggesting to choose passwords that significantly differ from one another. The consequent risk is that people who would like to be compliant with this practice may risk to forget their passwords. One solution they might opt for is transcripting their passwords in a notebooks or even a piece of paper they stick, for instance, on the computer. Finding cybersecurity a very valuable discipline, we thought about trying to develop a quite essential desktop application which any kind of user could be able to use, encountering the basic needs involved in password management and providing an idoneous security level. 

We would not suggest this application for important levels of business, like adopting it as main system in a bank, jobs related with public security and so on. It would definitely require more security barriers, while we implemented for sure a strong encryption protocol, yet was it intended to offer a tool to private users or employers at lower business levels who are not daily exposed to serious attacks.

!["Visual representation of the user persona"](../../pictures/User-persona.png)

## Requirements analysis

The requirements observed to build the application can be divided into functional, non-functional and implementation needs. The former imply some functionality the software should provide to the user, while the non-functional are requirements that do not directly concern behavioral aspects (e.g., consistency, availability, security, efficiency). Implementation stuff involves constraints for the entire phase of system realization (e.g, requiring the use of a specific programming language and/or a specific software dependency). 

The **FUNCTIONAL REQUIREMENTS** involve: 
| ID  | Requirement | Acceptance Criteria |
|-----|-------------|---------------------|
| F1  | The system must allow the user to set and use a **master password** to gain access to private data. | checked when the user is prompted to set a master password at initial configuration and cannot visualize entries without entering it correctly. | checked when a new entry is saved in the database and shown in the list after user submits the required fields. |
| F2  | The system must allow the user to **add a new entry**, consisting of: website name, URL, username, email, and password. | checked when changes made to any field (website, URL, username, email, password) are saved and visible after update. |
| F3  | The system must allow the user to **modify an existing entry**, including one or more fields. | checked when an entry is permanently removed from the database and no longer appears in the list. |
| F4  | The system must allow the user to **delete an entry** when it is no longer needed. |  |
| F5  | The system must allow the user to **import entries** from existing files. | checked when data from a valid import file is successfully parsed and new entries appear in the system. |
| F6  | The system must allow the user to **export entries** to a file. | checked when an export process produces a file containing the current entries in the system in the correct format. | 
| F7  | The system must allow **duplicate entry prevention** to avoid inserting the same entry twice. | checked when a user inserts a new entry and an error message pups up when the field is identical to another one in an existing row. |
| F8  | The system must **validate input** so that the required fields (sitename, URL, username/email) are not empty before saving. | checked when the user tries to save a new entry or a modified row and an error message pops up warning that some of the compulsory fields appear empty. |
| F9  | The system must allow **initial setup** by creating required database schema and tables. | checked when a setup window pops up at the first launch of the application made by the user. |
| F10 | The system must allow users to **retrieve entries** by providing one or more fields (sitename, URL, email, username). | checked when the system returns to the user the asked row depending on the field(s) inserted. |
| F11 | Passwords should be automatically **copied to clipboard** when retrieved to preserve secrecy. | checked when it is enough for the user to paste a password where needed without writing it manually after password retrieval from the app. |
| F12 | If no email is provided when adding an entry, it must **default to an empty string**. | checked when the saving of a new/modified entry is successful even though no email has been inserted and the field is allowed to be empty. |
| F13 | The system must provide a **graphical login window** with username and password fields and a submit button. | checked when a graphical window with a field for inserting username and a field for inserting the relative master password is showed. |
| F14 | The system must allow the user to **press Enter** to submit login. | checked when the combination of username and password can be submitted by pressing key "enter" on keyboard. |
| F15 | The system must inform the user of **login failure through popup messages**. | checked when after login failure an error message box pops up. |


The **NON-FUNCTIONAL REQUIREMENTS** touch: 
| ID  | Requirement | Acceptance Criteria |
|-----|-------------|---------------------|
| NF1 | The system must **double-check user identity** by requiring the master password again before sensitive modifications. | checked when any attempt to delete, modify, or export entries requires re-entering the correct master password. |
| NF2 | The system must provide a **user-friendly GUI**, with: clear buttons, mouse interaction, and message boxes for feedback (warnings, errors, success messages). | checked when buttons are clickable with a mouse, actions trigger confirmation dialogs, and success/error/warning messages are displayed. | 
| NF3 | The system must ensure **passwords are never displayed in plain text**; they are automatically hidden when inserted or modified. | checked when password fields show masked characters (e.g., ••••) instead of plain text, and never display stored values unencrypted. |
| NF4 | The system must use **strong encryption** to secure passwords. (e.g., AES-256 standard) | checked when all stored passwords are encrypted before saving and cannot be retrieved in plaintext without proper decryption. |
| NF5 | The system must **strengthen the master password** by applying PBKDF2 with high iteration count. (e.g., 1,000,000 rounds) | checked when the PBKDF2 function is called when deriving the master key, the iteration count is set to 1,000,000 or more, the derived key has the correct length (e.g., 32 bytes for AES-256) and verifying the same master password with the same device secret produces the same key. |
| NF6 | The system must **handle wrong insertions** in the database providing an error message instead of crushing. | checked when the system displays a clear error message to the user explaining the failure and the application does not crash and remains responsive for further operations. |
| NF7 | The system must detect if configuration already exists to **avoid reconfiguration**. | checked when a warning message pops up when trying to re-configurate a database that already exists and to which the application has already been connected to. |
| NF8 | The system must ensure that **errors during database creation** are caught and reported clearly. | checked when a setup failure is recognized by the system and an error message appears to notify the user to allow him to retry. |
| NF9 | The device secret must be generated using a secure **random mechanism** to guarantee uniqueness. | checked when strong, widely recognized encryption standard (such as SHA) are utilized. |
| NF10| Generated passwords copied to clipboard should only reside **temporarily** (this is implied via pyperclip). | checked when copying to clipboard does not last forever yet has a time limit to safeguard passwords' secrecy. |
| NF11| Command-line errors should provide clear guidance for missing required fields. | checked when, if something is missing in the row, the system prints an explicit error message identifying which field is missing, or eventually lists multiple missing fields and stops the operation if it is incomplete but does not crash. |
| NF12| After login attempt (success or failure), input **fields must be cleared** for security. | checked when the system clears up the data initially put in the username and password field, independently from successful or failing process. |


The **IMPLEMENTATION REQUIREMENTS**, which are more technical stuff, are about: 
| ID  | Requirement | Acceptance Criteria |
|-----|-------------|---------------------|
| I1  | The system must use a **database** to store entries and associated credentials. | checked when entries are stored in a structured database file (not just temporary memory). |
| I2  | The database must be **SQL-compatible** for query execution. | checked when database queries (insert, update, delete, select) work using SQL syntax. |
| I3  | The system must be developed in **Python**. | checked when the source code of the application is implemented in Python. |
| I4  | Passwords must be encrypted using the **AES-256 algorithm**. | checked when the verification of the code shows AES-256 encryption is applied when saving passwords. |
| I5  | Master keys must be derived using PBKDF2 with SHA-512 as **key derivation standard**. | checked when the system uses PBKDF2 as the key derivation function, SHA-512 is explicitly used as the hash function in PBKDF2, the derived key length matches the required AES key size (e.g., 32 bytes for AES-256), the derivation process correctly combines the master password and the device secret (salt) and using the same master password and device secret produces consistent keys on repeated derivations. |
| I6  | The system must **generate a device secret** using uppercase letters + digits, length ≥ 10 characters. | checked when the generated device secret respects the parameters. |
| I7  | The database must contain at least **two tables**: secrets (for hashed master password and device secret) and entries (for user credentials). | checked when the two tables are correctly created at initial setup and contain all needed fields. |
| I8  | The system must initially connect to a **database server running on localhost**. | checked when, on startup, the application attempts a connection to a MySQL (or SQL-compatible) database with host set to localhost. |
| I9  | The system must use **argparse** for handling command-line options. | checked when the app accepts commands passed through CLI (e.g., python pm.py add -s sitename -u url -l username -e email), flags (e.g., -s, -l) are parsed correctly, the system provides a help text (--help) and if a user omits required arguments, the system displays clear error messages without crashing. |
| I10 | Passwords generated must be copyable to clipboard via **pyperclip**. | checked when a generated/retrieved password is automatically copied to clipboard, the user is notified of that, the password stays in the clipboard until replaced or cleared by the user/system, the application does not expose the password on-screen unless explicitly requested. If the clipboard functionality fails, an error message gets displayed. |
| I11 | The system must use **Tkinter with ttkbootstrap** for theming. | checked when the whole GUI is created by means of the quoted Python library. |
| I12 | The system must use **tkinter.messagebox** to display informational and error messages. | checked when message boxes showed on display to send visible warnings to the user adopt tkinter formats. |
<br>

# POLITICAL, ECONOMIC AND ADMINISTRATIVE REASONS FOR IMPLEMENTATION REQUIREMENTS
I1 Databases provide scalable and cost-effective storage compared to flat files, they make backup, auditing, and access management easier. Ensures compliance with privacy and data protection regulations (e.g., GDPR).<br>
I2 SQL databases are widely available and free/open-source, lowering costs. Staff and developers are already familiar with SQL, reducing training effort. SQL is a well-established industry standard, reducing risk of vendor lock-in.<br>
I3 Python is free and open-source, reducing licensing costs. It flatters a large community support and abundant libraries speed up development and maintenance. Python is widely accepted in government, academia, and industry for secure applications.<br>
I4 Using a well-tested open algorithm avoids costs of proprietary solutions and reduces risk of breaches (which are financially damaging). It simplifies audits and certifications since AES-256 is widely recognized by IT security standards. AES-256 is an international encryption standard, endorsed by organizations like NIST, ensuring compliance with security policies.<br>
I9 Increases trust and transparency, reduces maintenance costs, since future developers won’t need to rewrite argument handling (using a standard library like argparse is cheaper than custom parsers), having standardized CLI parsing makes the tool easier to maintain, document, and test.<br>
I10 Aligns with privacy and security regulations, improves user experience and productivity (fewer failed logins, faster workflows), simplifies daily workflow for users.<br>
I11 and I12 comprehend a public and easy-to-retrieve and user-friendly library available on Python that just needs to be imported in the project code, no additional costs or license.<br>

    
        **- ...otherwise, implementation choices should emerge *as a consequence of* design (and therefore described in the design section).**
- If there are domain-specific terms, these should be explained in a **glossary**.


> You may consider adding a use-case diagram here (via PlantUML) to better visualize the requirements and their relationships
