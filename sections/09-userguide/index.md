---
title: User guide
has_children: false
nav_order: 10
---

# User Guide

PROtect is a secure and user-friendly password manager designed to simplify password management for both casual and advanced users. The application offers two modes of interaction: a command-line interface (CLI) for users comfortable with terminal operations, and a graphical user interface (GUI) for those who prefer an intuitive, visually guided experience. Both interfaces allow users to add, retrieve, modify, and delete credentials, while ensuring that all passwords are encrypted using the robust AES-256 standard.

Upon first launch, users are guided through an initial setup where they create a master password and generate a device secret. 

These two components are combined to produce a Master Key, which is subsequently used to encrypt all stored passwords and decrypt them when needed. This ensures that sensitive information remains protected at all times. 

When retrieving passwords, the system never displays them in plain text by default; instead, passwords are automatically copied to the clipboard, minimizing the risk of accidental exposure.

PROtect allows users to search for entries efficiently by site name, URL, or username/email. Sensitive operations, such as modifying or deleting credentials, require re-entering the master password to confirm identity and prevent unauthorized changes. 

The system also includes input validation, preventing empty or incomplete entries, and duplicate detection, ensuring the database remains organized and error-free. Users receive clear feedback through message boxes in the GUI or printed messages in the CLI, providing confirmation of successful actions or guidance in case of errors.

The application is lightweight and requires minimal system resources, making it accessible across a wide range of hardware. Overall, PROtect is designed to provide a secure, seamless, and flexible password management experience, combining strong encryption, practical usability, and comprehensive support, with troubleshooting guidance and updates available through the GitHub repository.
