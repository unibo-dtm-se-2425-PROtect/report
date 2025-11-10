---
title: Concept
has_children: false
nav_order: 2
---

# Concept

The type of product we intended to develop is a password manager in order to store, retrieve, delete, modify and, in general, perform whatever useful and essential query related to passwords, their management and security. The name "PROtect" and the way it is written with an alternance between upper- and lower-cases is voluntary to underline the main objective of the application, which is protection, with a recall to efficiency and proficiency through "PRO" and a recall to the word "technology" and its importance thanks to the assonance with the second part of the name "tect". 

The idea of developing a password manager came because of another exam we took during the semester, Cybersecurity, which caught a common interest of us all. We liked the idea of an interdisicplinary project which could put together teachings and skills from both cybersecurity and software engineering, also to give ourselves a demonstration of how coding is essential and can be applied to whatever need by just choosing and adapting the right functions and tools, and experimenting in a practical way rather than only theoretical. 

The desktop application should work both with CLI and GUI. Other useful libraries and tools, in our case, were of course all those related to cybersecurity and encryption (standard AES) to respect the security requirements. We chose to boost the security level by requesting a master password that is the one the user will select at the beginning to be identified later on, and this will not be useful only to access the app, but also to confirm one's identity when trying to save/modify a password so that we can be sure no one messes up our information. 

For safety and security purposes, we wanted to set up a system which automatically copies the password to clipboard when retrieved to avoid showing it on the screen, let it be in the CLI or the GUI. To let the user perform queries, we adopted mysql-connector-python as library to activate the SQL language to let the application understand what we intend to do. 

# IMPORTANT STEPS FOR THE DEVELOPMENT AND FUNCTIONING

### Configuration

- The master password is the first input while configuring, and the hash of it is saved in a file
- The device secret is generated randomly, also stored in a file
- Master Password + Device Secret are passed into a hashing function to create a valid key for AES-256. This is called Master Key
- The Master Key is then used to encrypt/decrypt new entries
- ENCRYPTED FIELDS: password
- PLAIN FIELDS: site name, site URL, email, username
- Table "ENTRIES" and table "SECRETS" 

### Process to add new entries

- Ask for Master Password
- Validate Master Password by hashing and checking with existing hash
- Make hash (Device Secret + Master Password) = Master Key
- Input fields of the entry: site name, site URL, email, username, password
- Encrypt password with Master Key and save the fields into the database 

### Process to get an entry

- Input the field to search for (e.g., site name, site URL, username...)
- Display all the entires that match the search, the password is hidden by default 
- If the user chooses to get the password (with -p flag) then: 
    - Ask for Master Password
    - Validate Master Password by hashing and checking with existing hash
    - Make hash (Device Secret + Master Password) = Master Key
    - Decrypt the password and copy to clipboard without showing it on screen

### Focus on the USERS

The users can belong to different levels of expertise, hence choosing whether using a CLI or a GUI. To reach this aim, we mastered the ttkbootstrap python library to make the GUI turn out good. We hypothesize the usage frequency to be high, yet it depends on the how many asswords they need to store depending on their digital activity. The information related to the user gest stored in the database called PROtect in the "ENTRIES" table. The secrets such as the master password and the device secret rely on a different table in the same database called "SECRETS" (this table is justified by the fact that more users may access the password manager, so we need to store secrets for different user profiles). 

# License 

We chose a MIT License because it’s the most adequate choice for academic projects that are just for didactic purposes and not intended to be used in organizations, it is permissive, clear and easy to use, it’s often utilized in the Python world and it’s ideal if we want the others to freely check and see our code, protecting responsibility anyways. 
