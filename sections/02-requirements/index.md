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
  - Choosing a master password for the main user to be identified and gain access to private data;
  - Entering a new entry, where an entry is intended as name of website, its URL and the consequent username with associated email and password used to access and perform tasks on such website;
  - Deleting an entry because it is no more needed (e.g., the users unsubscribed and deleted their profile on a site);
  - Modifying an existing entry because the users may need to change password (e.g., they forgot it and recovered it, or decide to change it regularly for higher security guarantee);
  - The modification of an entry may involve one or more fields in the row
  - Adding a new entry (e.g., the users may subscribe to a new website or create another profile on an already known website);
  - Importing and exporting files that already contain the information about the entries they want to insert in the application's table 
 

The **NON-FUNCTIONAL REQUIREMENTS** touch: 
  - Since any modification in the password manager app impacts users' privacy, we double check their identity by asking them to insert the master password again to be sure they are who they say they are;
  - Rendering an user-friendly GUI so that any basic user experiences easy and intuitive usability, which involves letting message boxes (warnings, error and success messages, ...) pop up and interact with windows by means of the mouse thanks to clear and visible button;
  - Automatic encryption of password when it is modified or inserted for the first time in a new entry row, so that it is not showed on display
  - AES256 encryption to make password secret


The **IMPLEMENTATION REQUIREMENTS**, which are more technical stuff, are about: 
   - Initializing a database so that entries and passwords have a place where to be stored in the system;


    
- The requirements must explain **what** (not how) the software being produced should do.
    - You should not focus on the particular problems, but exclusively on what you want the application to do.
- Requirements must be clearly identified, and possibly numbered.
- Requirements are divided into:
    - **Functional**: some functionality the software should provide to the user.
    - **Non-functional**: requirements that do not directly concern behavioral aspects, such as consistency, availability, security, efficiency, etc.
    - **Implementation**: constrain the entire phase of system realization, for instance by requiring the use of a specific programming language and/or a specific software dependency.
        - These constraints should be adequately justified by political / economic / administrative reasons (which must be written down)...
        - ...otherwise, implementation choices should emerge *as a consequence of* design (and therefore described in the design section).
- If there are domain-specific terms, these should be explained in a **glossary**.
- Each requirement must have its own **acceptance criteria**.
    - These will be important for the validation phase. 

> You may consider adding a use-case diagram here (via PlantUML) to better visualize the requirements and their relationships
