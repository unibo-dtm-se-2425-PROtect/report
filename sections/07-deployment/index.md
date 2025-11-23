---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

##User Installation

To run PROtect, users need to have Python 3.9 or higher installed on their machine, along with Git to clone the repository. Users also need a local MySQL server running, which serves as the backend database for storing credentials. Once Python and MySQL are installed, the software can be installed by cloning the repository and installing dependencies:

```sh
git clone https://github.com/<your-repo>/PROtect.git
cd PROtect
pip install -r requirements.txt
After installing the dependencies, the user launches the application using:
python -m pm
```

On first launch, PROtect guides the user through initial configuration, including setting a master password and generating a device secret, which are then stored securely in the database. No additional configuration files or environment variables are required; the application handles database schema creation and all required tables (SECRETS and ENTRIES) automatically.

## Server-Side Installation

PROtect requires a MySQL server, which can be hosted locally or on a remote server if multiple users need access. The MySQL server must be configured with a database (default name protect) to store user credentials and secrets. If using a remote server, the application configuration must include the server host, username, password, and database name.

The installation of the MySQL server depends on the operating system:

Windows: Download the MySQL Community Server from the official site and run the installer, ensuring the server starts automatically.

macOS: Install via Homebrew with: _brew install mysql_ and start the service using _brew services start mysql_.

Linux (Ubuntu/Debian): Install with _sudo apt install mysql-server_ and start it using _sudo systemctl start mysql_.
Once the server is running, PROtect can connect to it automatically at first launch, creating the required database schema and tables if they do not already exist. 
No additional software is required beyond MySQL, Python, and the dependencies listed in _requirements.txt_.
