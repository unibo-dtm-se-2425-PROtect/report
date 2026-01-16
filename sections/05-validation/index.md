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
  | 12               | F1, NF4           | Database connection establishment; Schema initialization; Configuration deletion; Handling of connection timeouts or credential failures |  Unit |
  
- `test_tkinter_bootstrap_sample.py`
  | Tests           | Requirements | Tested features    | Type  |
  |-----------------|------------  |--------------------|-------|
  | 4               | F1, S1           | GUI login window initialization; Theme application; Input field focus management; Mocked login verification logic |  Unit / Mock UI |

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
- **F3**: validated by `test_cli_retrieve_entries`. The aim was to verify that the `extract` command executes the search logic and rendersthe results table.
- **F5**: validated by `test_cli_delete_entry_success`. The aim was to verify that the `rem` command accepts an `--id` and triggers the deletion workflow.
- **F6**: validated by `test_cli_import_file`. The aim was to verify that the `imp` command accepts a file path and initiates the bulk ingestion process.

Security requirements mapping: 
- **S1**: validated by `test_cli_master_password_failure`. The aim was to verify that providing an incorrect Master Password resulted in immediate termination of the session with a "Access Denied" error.
- **S2**: validated by `test_cli_remove_missing_id`. The aim was to verify that potentially destructive commands fail safely if required arguments are missing. 

The test success related to the test file of reference (`pm.py`) achieved a 100% rate. The code coverage, instead, is 80%, indicating the tests successfully exercised all command routing logic, argument parsing branches, and error handling routines, with the remainder untested scenarios referring to OS-level interrupts and rare I/O exceptions that are difficult to simulate in a test environment.

At this stage no containers were utilized. As already mentioned earlier, we decided to rely on a "mockist" testing strategy, which allowed us to avoid spinning up heavy containers for the MySQL database at every test run. Thanks to this choice it was possible to run tests with no overhead caused by container orchestration or eventual network latency. Real database connectivity was reserved for the manual acceptance testing phase. 

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


