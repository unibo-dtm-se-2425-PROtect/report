# PROtect - password manager

This repository contains the project report and documentation related to PROtect, a secure, Python-based password manager which uses a master password, a device secret and SHA-256 encryption to store and retrieve credentials. It includes both a CLI (Command Line Interface) and a GUI (Graphical User Interface). </br>
- To access the full project documentation, click [here](https://unibo-dtm-se-2425-protect.github.io/report/)
- To access the code base of the discussed project, click [here](https://github.com/unibo-dtm-se-2425-PROtect/artifact)
- To access the template used for this report, click [here](https://github.com/unibo-dtm-se/template-project-work)

# Features

1. Master Password Protection
2. Device-specific secret generation
3. SHA-256 encryption for stored passwords (never in clear)
4. Secure storage using MySQL 
5. CLI for terminal lovers
6. Simple GUI with tkinter and ttkbootstrap librrìary for more basic users
7. Add, Modify or Delete an entry
8. Import/Export entry data for scripts
9. Lock to keep the app secure without closing it
10. Retrieve entries by numeric ID
11. All entires listed in a table in GUI visualization
12. Default is password never showed, possibility of disclosing clear text for a fixed time amount

# Installation 
### by cloning the repository
'''
bash 
git clone https://github.com/unibo-dtm-se-2425-PROtect

pip install -r requirements.txt if using requirements.txt 

poetry install (via bash) if using Poetry 
'''

# Security Principles

1. Passwords are hashed using SHA-256 via 'hashlib'
2. Master Password never stored in plaintext
3. Database access protected by MySQL login credentials
4. No passwords are exposed in logs or errors (but option still available on user demand)

## How to install Ruby and Jekyll

Follow instructions from here: <https://jekyllrb.com/docs/installation/>

<!-- References -->

[template-repo]: https://github.com/unibo-dtm-se/template-project-work
[template-site]: https://unibo-dtm-se.github.io/template-project-work
[course-site]: https://www.unibo.it/en/study/phd-professional-masters-specialisation-schools-and-other-programmes/course-unit-catalogue/course-unit/2024/466765
[general-forum]: https://virtuale.unibo.it/mod/forum/view.php?id=1885625
[project-forum]: https://virtuale.unibo.it/mod/forum/view.php?id=1885626
[markdown-cheatsheet]: https://www.markdownguide.org/cheat-sheet
[jeckyll-home]: https://jekyllrb.com/
