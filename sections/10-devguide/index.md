---
title: Developer guide
has_children: false
nav_order: 11
---

# Developer Guide

### Organizational information

New contributors can contact the team through GitHub Discussions or by opening GitHub Issues to report bugs, request features, or suggest improvements. Private communication via the institutional email is also possible. For internal team communication, a group chat is typically used.

### Internal Conventions

Follow standard Python conventions, primarily using snake_case for function and variable names (e.g., computeMasterKey, export_entries, masterpassword_hash).

The Graphical User Interface (GUI) components strictly adhere to the Model-View-Controller (MVC) architectural pattern:
- VIEW ( `ui/VIEW`): Components are "dumb" (e.g.,  `GUIview.py`) and are only responsible for displaying information and collecting user input. They communicate user actions exclusively through callable controller methods.
- CONTROLLER ( `ui/CONTROLLER`): Components (e.g.,  `GUIcontroller.py`) handle all application logic, manage the flow between the View and the Model, and process user input.
- MODEL ( `ui/MODEL`): Components (e.g.,  `GUImodel.py`) manage the application data, database interactions, and core business logic (like cryptography).

Database and Connection:
- Database Naming: The application's main database schema must be named  `PROtect`.
- Data Types: Encrypted passwords are stored in the  `PROtect.entries` table using the  `VARBINARY ` type.

Cryptography and Security:
- Master Key Derivation: The Master Key (MK) is derived by computing the SHA256 digest of the concatenation of the Master Password ( `mp`) and the Device Secret ( `ds`) (i.e.,  `hashlib.sha256((mp + ds).encode()).digest()`).
- Encryption Standard: All password encryption/decryption operations must use AES-256 in CBC mode, handled by the utility functions in  `project/AES256util.py`
- Master Password Policy: For security, a master password must meet some minimum requirements, such as 8 chars length, at least one uppercase, one digit, one special character
- GUI Security Check: Any sensitive operation in the GUI (e.g., editing, deleting, or exporting entries) must trigger a secondary password prompt to re-verify the user's identity before proceeding.

Testing Frameworks:
All new code requires unit tests using the pytest framework. 

The team follows conventional commits to keep the commit history clean and organized, which also facilitates automated release workflows. For each new feature, contributors are generally expected to add tests to the project’s test suite. 

### Development Environment 

The project uses Python 3.12. To contribute:
1) Clone the repository:  `git clone https://github.com/unibo-dtm-se-2425-PROtect/artifact`
2) Install dependencies:  `pip install -r requirements-dev.txt`
3) Run tests with:  `python -m unittest discover -s tests -t . -p "test_*.py"` (specifies the start directory, specifies the top-level directory of the project, specifies the pattern to match test files)
4) To run a specific test file:  `python -m pytest tests/test_config.py` (demonstration purposes)

### Development Workflow

The project's development workflow is automated using GitHub Actions (CI/CD) and relies on Conventional Commits for versioning and releases.
We did not use the subdivision in branches (we have developed, tested, fixed and in general modified everything in the master branch). The development can be started by creating a new branch off the main development branch (likely main). 
Continuous pull and push. 

### Development Tools

Recommended IDE: Visual Studio Code 
GitHub Actions: the  `check.yml` (testing) and  `deploy.yml` (release) workflows are pre-configured. Contributors only need to ensure all tests pass before opening a pull request.

