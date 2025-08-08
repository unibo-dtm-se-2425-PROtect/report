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
