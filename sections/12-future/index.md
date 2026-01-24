---
title: Future work
has_children: false
nav_order: 13
---

# Known issues and future work

Some issues are encountered in the overall project:
- Not all features in the GUI correctly work (e.g., `export` does not reach the end because we can't select the type of file we want to save, but the connection works fine; `import` completes the logical connection but does not display the csv lines of the imported file in the GUI).
- We have implemented a `Lock` button to hide the credentials, but we need to rerun the app to go back to the initial state. We should make the "Lock" button turn into **Unlock** so that we can reverse the procedure, but this is just a UI inconsistency, not a serious problem. This is something that can be added in the future for a user-friendly interface.
- Another improvement to leave to future updates is adding a **Logout** button so that the user can leave the program in a safer way instead of just closing the window, and to allow the switch between users if needed without rerunning the application from scratch.
- A minor, uncomfortable problem that worses the user experience is that when a new entry has to be added, the window passes into the background so we need to manually bring it back to the foreground.
- Since the main code was developed during many months, it is possible to encounter some discrepancies and redundancies in what e feature should accomplish and how it does so, but the validation and testing part of the work already solved many bugs and incongruities with the requirements.
- At the beginning, we implemented a feature to **generate cryptographically secure, random password for new entires** in case the user did not want to decide one by himself. We removed it when the coding part was becoming heavy and complex to focus on the main functionalities and reach a high-functionality state of the application, but we can reintegrate it in future versions.
- In the CLI not all argparse commands work properly. This is because we had initially completely the CLI part of code, and then we wanted to build the GUI on this base, but we focused too much on implementing a working GUI and we introduced lots of inconsistencies between GUI and CLI commands (e.g., in the GUI we can choose any password, while in the CLI the guidelines to choose a secure password are correctly followed (min number of characters, at least an uppercase...); in the GUI the login allows to choose the account of the specific user, while in the CLI since there is no specific login we can't fully access functionalities because it does not recognize a user and consequently can't recognize the right master password. Only initial configuration works. We should integrate the two to make them equal to use. 
- Integrate a real-time visual password strength indicator into the entry creation/editing forms to implement user-firendliness and UI design principles.
- Implement **automatic re-locking** of the vault session after a configurable period of inactivity.
- **Migrate** from a separate, external MySQL or MariaDB database to a lightweight, embedded database solution like **SQLite**



