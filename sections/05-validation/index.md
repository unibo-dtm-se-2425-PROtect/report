---
title: Validation
has_children: false
nav_order: 6
---

# Validation

## Testing approach

For this project, we adopted a comprehensive automated testing strategy that focused on "behavior verification". Since it is a Password Manager we're dealing with, and its security-critical nature, the main priority was ensuring both cryptographic operations and database interactions always occur without exposing sensitive data. In other words, the greater part of the application followed a Test-After approach to verify the correctness of the implemented logic. On the other hand, whenever there were critical security components to be tested, the approach switched to the TDD methodology (Test-First), so as to ensure robustness before implementation. 

We chose the `pytest` framework for all automated testing because of its concise assertion syntax, its powerful `fixture` system (which in multiple occasions allowed us to simulate database connections without boilerplate), and its ability to handle parameterized tests for complex security scenarios, such as verifying multiple password policy failures. 

## Testing (automated)

For automated testing, a total of 94 tests were implemented, which were all organized in separate files corresponding to each functional module. In general, these tests all aimed at validating the security requirements and CRUD operations of the vault.

We'll proceed now at providing a breakdown of the test suites, mapped to the project requirements: 

- `test_pm.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 18               | S1, NF1           | Argument parsing and routing; Master Password authentication flow; Handling of missing arguments; Error message propagation to the user interface |  System |

- `test_AES256util.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 9               | S2, S3           | AES-256-CBC encryption/decryption roundtrip; Hex vs. ASCII key handling; Padding validation; Master Password hashing and verification; Tamper detection |  Unit |
  
- `test_add.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 24               | F2, S2, S4           | Database insertion logic; Prevention of "Double Encryption"; Input validation for optional fields; Handling of duplicate entries |  Integration |
  
- `test_retrieve.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 7               | F3, F4, NF2           | Dynamic SQL WHERE clause generation; Handling of empty results; "Ambiguity Guard" (warning on multiple results); Decryption flow to clipboard; Graceful handling of schema changes (missing columns) |  Integration |
  
- `test_delete.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 8               | F5, S4          | User confirmation flow (Y/n); SQL deletion execution; Handling of non-existent IDs; Error propagation from DB to CLI |  Integration |
  
- `test_import.py` / `test_export.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 12               | F6, F7, NF3           | CSV parsing and writing; Bulk encryption/decryption loops; Atomic transaction handling (handling errors mid-process); File system I/O mocking |  Integration |
  
- `test_config.py` / `test_dbconfig.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 12               | F1, NF4           | Database connection establishment; Schema initialization; Configuration deletion; Handling of connection timeouts or credential failures |  Unit / Integration |
  
- `test_tkinter_bootstrap_sample.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 4               | F1, S1           | GUI login window initialization; Theme application; Input field focus management; Mocked login verification logic |  Unit |

### Unit testing

- Describe the unit tests you developed, and their rationale
- Report success rate and test coverage here

### Integration testing

- Describe couples of components that you tested together, and the corresponding test rationale/plan

- Report success rate and test coverage here

- If you used [test doubles](https://en.wikipedia.org/wiki/Test_double), describe her which type of double you used, and why

### System testing

- Describe the tests that you developed to automatically test the system as a whole
    + and the corresponding test rationale/plan
    + better would be to have system tests that match the acceptance criteria of the requirements

- Report success rate and test coverage here

- If you adopted containers (e.g. Docker compose) for testing, describe how you used them here
    + e.g. to run the system in a clean environment, or to run the tests in a clean environment

## Acceptance tests (manual)

All functional, security, and non-functional requirements have been successfully verified through a manual audit of the application's CLI and GUI, ensuring the three main components (the Database, the Cryptography, and the UI) integrate optimally, utlimately providing a cohesive user experience. Manual testing has been carried out through three main stages:

- Stage 1: Inizialization. The `con` command is issued via CLI to verify the database schema creation on a clean MySQL instance. This also ensures everything works fine at setup and startup of the application.
- Stage 2: CRUD lifecycle. We manually walked through the full lifecycle of a secret, consisting of the Creation of an entry, its Retrieval (to verify correct masking of the secret), Updating any of its fields, the correct copying to the clipboard and, finally, the Deletion of the same entry to ensure database cleanup.
- Stage 3: Stress and security testing. While manually assessing the CRUD lifecycle, we also tried to assess the application's robustness and security by providing incorrect Master Passwords and malformed CSV files. The aim was to make sure that the application, when such cases occur, fails gracefully without leaking sensitive data or crashing. 

The following acceptance criteria were specifically addressed and verified:

Functional Requirements

- **F1**: The user can configure the application connection to a local MySQL database via the `con` command.
- **F2**: The user can securely add new entries containing Site, URL, Email, Username, and Password.
- **F3**: The user can retrieve and view a table of stored entries, with sensitive passwords hidden by default (masked as `{hidden}`).
- **F4**: The user can securely decrypt and copy a specific password to the system clipboard using the `--copy` flag.
- **F5**: The user can modify existing entries, like updating an expired password, or delete obsolete entries by their ID.
- **F6**: The application supports bulk operations, allowing the user to import credentials from a CSV file.
- **F7**: The application allows the user to export their entire encrypted vault to a plaintext CSV file for backup purposes (requiring Master Password re-verification).

Security Requirements

- **S1**: Access to the vault is strictly guarded by a Master Password; no operation can be performed without authentication.
- **S2**: Passwords are never stored in plaintext; they are encrypted using AES-256-CBC before saving to the database.
- **S3**: The Master Password itself is never stored; only its SHA-256 hash is saved for verification.
- **S4**: The application prevents "Double Encryption" (encrypting already encrypted data) and "Accidental Deletion" (requiring explicit yes or no confirmation).

Non-Functional Requirements 

- **NF1**: The CLI utilizes color-coded output (green for success, red for errors, yellow for warnings) to enhance readability.
- **NF2**: Data is presented in structured, auto-sized tables (using the `rich` library) rather than raw text.
- **NF3**: The application handles large datasets (bulk import/export) without crashing or timing out.
- **NF4**: The system cleans up resources (database connections) automatically, even if an error occurs during execution.

The overall test success rate for acceptance tests was 100%.


