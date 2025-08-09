---
title: Concept
has_children: false
nav_order: 2
---

# Concept

The type of product we intended to develop is a password manager in order to store, retrieve, delete, modify and, in general, perform whatever useful and essential query related to passwords, their management and security. The name "PROtect" and the way it is written with an elternance between upper- and lower-cases is a voluntary catch to underline the main objective of the application, which is protection, with a recall to efficiency and proficiency through "PRO" and a recall to the word "technology" and its importance thanks to the assonance with the second part of the name "tect". 

The idea of developing a password manager came because of another exam we took during the semester, Cybersecurity, which caught a common interest of us all. We liked the idea of an interdisicplinary project which could put together teachings and skills from both cybersecurity and software engineering, also to give firstly to ourselves a demonstration of how coding is essential and can be applied to whatever need by just choosing and adapting the right functions and tools, and experimenting in a practical way rather than only theoretical. 

The desktop application was first conceived and carried on with a CLI which represented the first base of the whole code, and than we tried to implement a GUI to allow normal users with lower level of expertise who don't generally perform stuff on the computer using a CLI to have easier access to the utilization of the application. To reach this aim, we mastered the ttkbootstrap python library to make the GUI turn out good.

Other useful libraries and tools, in our case, were of course all those related to cybersecurity, encryption and so on to respect the security requirements, hence we installed pycryptodome and cryptography in order to make an AES encryption possible, which is the current, safest standard. We chose to boost the security level by requesting a master password that is the one the user will select at the beginning to be identified later on, and this will not be useful only to access the app, but also to confirm one's identity when trying to save/modify a password so that we can be sure no one messes up our information. 

For safety and security purposes, we wanted to set up a system which automatically copies the password to clipboard when retrieved to avoid showing it on the screen, let it be in the CLI or the GUI. To let the user perform queries, we adopted mysql-connector-python as library to activate the SQL language to let the application understand what we intend to do. 

### IMPORTANT STEPS FOR THE DEVELOPMENT AND FUNCTIONING

# Configuration

- The master password is the first input while configuring, and the hash of it is saved in a file
- The device secret is generated randomly, also stored in a file
- Master Password + Device Secret are passed into a hashing function to create a valid key for AES-256. This is called Master Key
- The Master Key is then used to encrypt/decrypt new entries
- ENCRYPTED FIELDS: email, username, password
- PLAIN FIELDS: site name, site URL 
- The information related to the user get stored in the database called PROtect in the "entires" table. The secrets such as the master password and the device secret rely on a different table in the same database called "secrets". 

# Process to add new entries

- Ask for Master Password
- Validate Master Password by hashing and checking with existing hash
- Make hash (Device Secret + Master Password) = Master Key
- Input fields of the entry: site name, site URL, email, username, password
- Encrypt email, username and password with Master Key and save the fields into the database 

# Process to get an entry

- Input the field to search for (e.g., site name, site URL, username...)
- Display all the entires that match the research, the password is hidden by default 
- Is the user chooses to get the password (with -p flag) then: 
    - Ask for Master Password
    - Validate Master Password by hashing and checking with existing hash
    - Make hash (Device Secret + Master Password) = Master Key
    - Decrypt the password and copy to clipboard 

# Focus on the USERS

The users can belong to different levels of expertise, hence choosing whether using a CLI or a GUI. Their interaction with the system depends on how many passwords they need to store depending on how many sites and applications they use, which can differ on the basis of their knwoledge, social and/or work background. We hypothesize the frequency to be high since a password manager is a comfortable, useful and safe tool for anybody and people nowadays have access to many sites, owning multiple of profiles. 

They can interact with the application via computer through CLI and GUI, or smartphones with GUI. The system will have to store the data the users provide with the aim of recognizing which user credentials for which sites are associated with a certain password. The only information needed are username and email (no need for name and surname because these two are already identifying the user themselves), site name, site URL and password. They are quite sensible data considering the degree of confidentiality to assure. The information gets stored in the database we created, called PROtect. The table dedicated to it is "entries". We find another table in such DB, too: "secrets" with master password and device secret in it. 

The password manager is accessible by anyone who knows the Master Password. Ideally, this is the administrator and owner of the device. (Lasciamo così o creiamo diverse tabelle per diverse persone all'interno dello stesso password mabager così se su un computer sono registrati più profili ognuno ha il proprio spazio nel password manager e in base alla master password che viene inserita l'app preleva la giusta password dalla giusta tabella per l'user?)

# License 

We chose a MIT License because it’s the most adequate choice for academic projects that are just for didactic purposes and not intended to be used in organizations, it is permissive, clear and easy to use, it’s often utilized in the Python world and it’s ideal if we want the others to freely check and see our code, protecting responsibility anyways. 






Here you should explain:
- The type of product developed with that project, for example (non-exhaustive):
    - Application (with GUI, be it mobile, web, or desktop)
    - Command-line application (CLI could be used by humans or scripts)
    - Library
    - Web-service(s)
    - Data processing toolkit (= Library + CLI, or Jupyter Notebook)

- Use case collection
    - Where are the users?
    - When and how frequently do they interact with the system?
    - How do they interact with the system? Which devices are they using?
    - Does the system need to store user's data? Which data? Where?
    - Most likely, there will be multiple roles.
