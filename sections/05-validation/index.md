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
  | 18               | S1, F1, NF11, I9           | Argument parsing and routing; Master Password authentication flow; Handling of missing arguments; Error message propagation to the user interface |  System |

- `test_AES256util.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 9               | S2, S3, NF4, NF5, NF9, I4, I5          | AES-256-CBC encryption/decryption roundtrip; Hex vs. ASCII key handling; Padding validation; Master Password hashing and verification; Tamper detection |  Unit |
  
- `test_add.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 24               | S4, F2, F7, F8, F12           | Database insertion logic; Prevention of "Double Encryption"; Input validation for optional fields; Handling of duplicate entries; Defaulting empty emails |  Integration |
  
- `test_retrieve.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 7               | F10, F11, NF3, I10       | Retrieval by fields; Masking passwords as {hidden}; Decryption to clipboard |  Integration |
  
- `test_delete.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 8               | S4, F4, NF1, NF6         | Re-verification of Master Password; User confirmation flow (Y/n); SQL deletion execution; Handling of non-existent IDs; Error propagation from DB to CLI |  Integration |
  
- `test_import.py` / `test_export.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 12               | F5, F6, NF3           | CSV parsing and writing; Bulk encryption/decryption loops; Atomic transaction handling (handling errors mid-process); File system I/O mocking |  Integration |
  
- `test_config.py` / `test_dbconfig.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 12               | F9, NF7, NF8, I1, I7, I8         | Database/Table creation; Database connection establishment; Detecting existing configs; Catching DB creation errors; Localhost connection logic; |  Unit |
  
- `test_tkinter_bootstrap_sample.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 4               | F13, F14, F15, NF12, I11, I12          | GUI login window initialization; Theme application; Input field focus management; Mocked login verification logic |  Unit / Mock UI |

### Unit testing

A dedicated test file was created for each core component to verify its functioning in complete isolation. This proved to be particularly important for the AES256util module, as we had to mathematically prove that the encryption and hashing algorithms functioned correctly without relying on the state of the database.
The GUI component was tested using a "fake widget" strategy. Frontend logic (like clearing password fields on failed login) was validated via mocking `ttkbootstrap` and `tkinter` classes, hence doing so in a headless environment.

The overall test success rate was 100%. 

### Integration testing

Integration testing was employed to verify the interactiong between the logic layer (the Python application), the data access layer (involving MySQL), and the system layer (comprising the OS clipboard and File System).
In particular, the couples of components that were tested together will be listed down below:
- `retrieve.py` / `AES256util`: verifying that the encrypted data fetched from the database via the retrieval module is correctly passed to the decryption utility.
- `export.py` / **File System**: verifying the interaction between the database extraction logic and the OS's file handling.
- `delete.py` / **User Input**: verifying the interaction between the application logic and the user's standard input stream.
- `add.py` / `dbconfig.py`: verifying that the application logic correctly handles contraints imposed by the database schema.
- `pm.py` / **Backend Modules**: verifying the routing logic between the CLI and the functional modules.
- `tkinter_bootstrap_sample` / **Logic Layer**: verifying the communication between the GUI and the backend authentication logic. 

100% test success rate was achieved, confirming that all listed components interacted as expected. 

Since the involvement of real, live production database was too computationally demanding, and physical user interaction was as much difficult to get, at need, we employed various kinds of test doubles to perform these integration tests. In particular, the test doubles involved can be categorized in:
- **Fake objects**: we implemented fake entities such as `FakeDB` and `FakeCursor` that mimicked the real associated components. For example, `FakeDB` is a custom class that mimics the behaviour of the `mysql.connector` interface.
- **Mocks and stubs**: standard mocks were used to system interfaces that are outside the control of the code. We relied specifically on `unittest.mock.MagicMock` for mocking, and on stubs like `builtins.input` (patched to simulate a user typing something in standard input), or `getpass.getpass` (patched to simulate the secure entry of the Master Password).
- **Spies**: mocks were also used on the `rich.print` functions to "spy" on the output, allowing us to assert that the application was providing the correct visual feedback to the user. 

### System testing

System testing was conducted via the `pm.py` test suite, treating the entire application as a "black box". By this it is meant that the tests of this suite simulate a user invoking the `pm.py` script via the CLI, passing arguments via `sys.argv`, and interacting with the iput/output streams.
Specific automated system tests were mapped to the project's acceptance criteria, as it will be now shown:

Functional requirements mapping: 
- **F1**: validated by `test_cli_config_setup`. The aim was to verify that the `con` command trigers the database setup sequence.
- **F2**: validated by `test_cli_add_entry_success`. The aim was to verify that the `add` command parses flags and successully invokes the storage logic.
- **F4**: validated by `test_cli_delete_entry_success`. The aim was to verify that the `rem` command accepts an `--id` and triggers the deletion workflow.
- **F5**: validated by `test_cli_import_file`. The aim was to verify that the `imp` command accepts a file path and initiates the bulk ingestion process.
- **F10**: validated by `test_cli_retrieve_entries`. The aim was to verify that the `extract` command executes the search logic and rendersthe results table.

Security  and Non-Functional requirements mapping: 
- **S1**: validated by `test_cli_master_password_failure`. The aim was to verify that providing an incorrect Master Password resulted in immediate termination of the session with a "Access Denied" error.
- **NF11**: validated by `test_cli_remove_missing_id`. The aim was to verify that potentially destructive commands fail safely if required arguments are missing. 

The test success related to the test file of reference (`pm.py`) achieved a 100% rate. The code coverage, instead, is 80%, indicating the tests successfully exercised all command routing logic, argument parsing branches, and error handling routines, with the remainder untested scenarios referring to OS-level interrupts and rare I/O exceptions that are difficult to simulate in a test environment.

At this stage no containers were utilized. As already mentioned earlier, we decided to rely on a "mockist" testing strategy, which allowed us to avoid spinning up heavy containers for the MySQL database at every test run. Thanks to this choice it was possible to run tests with no overhead caused by container orchestration or eventual network latency. Real database connectivity was reserved for the manual acceptance testing phase. 

## Acceptance tests (manual)

All functional, security, and non-functional requirements have been successfully verified through a manual audit of the application's CLI and GUI, ensuring the three main components (the Database, the Cryptography, and the UI) integrate optimally, utlimately providing a cohesive user experience. Manual testing has been carried out through three main stages:

- Stage 1: Inizialization. The `con` command is issued via CLI to verify the database schema creation on a clean MySQL instance. This also ensures everything works fine at setup and startup of the application.
- Stage 2: CRUD lifecycle. We manually walked through the full lifecycle of a secret, consisting of the Creation of an entry, its Retrieval (to verify correct masking of the secret), Updating any of its fields, the correct copying to the clipboard and, finally, the Deletion of the same entry to ensure database cleanup.
- Stage 3: Stress and security testing. While manually assessing the CRUD lifecycle, we also tried to assess the application's robustness and security by providing incorrect Master Passwords and malformed CSV files. The aim was to make sure that the application, when such cases occur, fails gracefully without leaking sensitive data or crashing. 

The following acceptance criteria were specifically addressed and verified:

Functional Requirements

- **F1**: The user cannot view entries without setting and providing a master password.
- **F2**: The user can securely add new entries containing Site, URL, Email, Username, and Password.
- **F3**: The user can modify an entry, ensuring the operation updates the specific fields and that those changes persist.
- **F4**: The user can delete an entry, assured of the fact that it will be permanently removed from the list.
- **F5**: The system parses a valid import file and populates the database.
- **F6**: The export process produces a valid file matching current system entries.
- **F7**: The insertion of an identical site/username combination triggers an error message. 
- **F8**: Attempting to save with empty compulsory fields triggers a warning popup/message.
- **F9**: The setup window appears on first launch and creates the schema.
- **F10**: The system returns specific rows based on search terms.
- **F11**: The password is available in the clipboard immediately after retrieval.
- **F12**: The omission of an email results in an empty string stored in the database.
- **F13**: The graphical login window appears with all required widgets.
- **F14**: Pressing the "Enter" key submits the login credentials.
- **F15**: An incorrect login attempt triggers an explicit error popup.

Security Requirements

- **S1**: Access to the vault is strictly guarded by a Master Password; no operation can be performed without authentication.
- **S2**: Passwords are never stored in plaintext; they are encrypted using AES-256-CBC before saving to the database.
- **S3**: The Master Password itself is never stored; only its SHA-256 hash is saved for verification.
- **S4**: The application prevents "Double Encryption" (encrypting already encrypted data) and "Accidental Deletion" (requiring explicit yes or no confirmation).

Non-Functional Requirements 

- **NF1**: The `modify`, `delete`, and `export` commands always require re-entering the Master Password. 
- **NF2**: The GUI buttons are clickable and feedback messages are distinct.
- **NF3**: Table inspection allows to see that passwords appear as masked characters.
- **NF4**: Code inspection and DB analysis allow to verify passowrds are stored as AES-256 ciphertext.
- **NF5**: The Master Password is hashed and compared against the stored digest.
- **NF6**: SQL errors (like duplicates) display a clear message and keep the app responsive.
- **NF7**: Running `con` on an existing setup triggers a warning.
- **NF8**: Connection failures during setup are reported clearly to the user.
- **NF9**: Code review ensures that `secrets.token_hex` is used for the device secret.
- **NF10**: The clipboard functionality is invoked.
- **NF11**: Missing CLI arguments result in explicit error messages identifying the missing field.
- **NF12**: The username/password fields are cleared after both successful and failed login attempts.

Implementation Requirements
- **I1** and **I7**: Entries and secrets are persisted in `secrets` and `entries` tables.
- **I2**: Queries use standard SQL syntax.
- **I3**: Source code is written in Python.
- **I4**: Usage of `AES256util` module implementing AES-256.
- **I5**: SHA-256 is used for key derivation
- **I6**: Generated device secrets meet length and character constraints.
- **I8**: Default connection string targets `localhost`.
- **I9**: `argparse` handles flags like `-s`, `-u`, `-l`.
- **I10**: `pyperclip` dependency is used for clipboard operations.
- **I11**: GUI is built using `ttkbootstrap`.
- **I12**: Verified usage of `tkinter.messagebox` for all user alerts.

The overall test success rate for acceptance tests was 100%.


