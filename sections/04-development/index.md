---
title: Development
has_children: false
nav_order: 5
---

# Development

## DVCS

The project was managed using Git as a Distributed Version Control System (DVCS), with GitHub hosting the repository. Unlike more complex workflows that rely on multiple branches (e.g., dev, feature/*, hotfix/*), we chose to work exclusively on the main branch. This decision was motivated by the small team size, the academic nature of the project, and the need for rapid coordination without the overhead of managing parallel development lines.

Even though branch-based workflows (such as Git Flow or GitHub Flow) are common in larger or industry-level teams, using only the main branch can be effective for small projects because it simplifies merging, avoids branch divergence, and reduces the need for complex reviews. To maintain clarity despite the absence of branching, commit messages followed a consistent structure, summarizing changes clearly and logically. 

Although formal conventions like semantic commits (feat:, fix:, docs:) were not strictly applied, the team maintained descriptive commit messages to ensure that the evolution of the codebase remained understandable.

Pull requests and code reviews were not used formally, as all development went directly into the main branch. Coordination happened informally within the team, a workflow acceptable for small-scale academic projects where the risk of conflicting contributions is low and communication is direct. Issues on GitHub were used mainly to track tasks or bugs when needed, providing lightweight project management without enforcing rigid processes.

## Implementation Details

### Network Protocols:

PROtect relies on TCP, used implicitly by MySQL for database communication. TCP ensures reliable and ordered communication, which is fundamental when transferring sensitive or encrypted data such as passwords or authentication hashes. No additional protocols (HTTP, gRPC, or WebSockets) were needed, as the application does not require distributed communication or client–server interactions beyond the database.

### In-Transit Data Representation:
All communication between the application and the database occurs through SQL queries, with parameters passed securely via the MySQL connector. Data is stored and processed in its native relational form, and no external serialization formats like JSON, XML, or Protocol Buffers are required, since there is no network API layer. Sensitive information—specifically passwords—is encrypted using AES-256, while the master password is hashed with SHA-256.

### Database Querying:
The application uses SQL with MySQL, chosen for its reliability, structured schema, referential integrity, and ability to efficiently handle CRUD operations. MySQL also guarantees ACID properties, which help prevent inconsistencies during write operations such as adding, deleting, or modifying entries.

### Authentication and Authorization:
Authentication is strictly based on the master password, which the user sets during initial configuration. The password hash and device secret together generate the Master Key, used for encryption and decryption. Because PROtect is intended as a single-user desktop application, no centralized authentication mechanisms (OAuth, JWT) or role-based access control (RBAC) systems were required. However, security is reinforced by requiring the master password again for sensitive operations such as retrieving or modifying a stored credential.

## Technological Details

### Programming Language and Frameworks:
The project is developed entirely in Python, chosen for its readability, extensive library ecosystem, and suitability for both CLI and GUI development.

### Libraries Used:
- mysql-connector-python: database communication with MySQL
- ttkbootstrap (with tkinter): modern GUI components
- pyperclip: secure clipboard operations
- argparse: CLI parsing

These libraries were selected for their stability, documentation quality, and compatibility with Python 3.

### External Technologies:

PROtect does not rely on external APIs, cloud services, or third-party authentication providers. The only external component required is the MySQL server, used to store secret information and user entries securely.
