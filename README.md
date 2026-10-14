# Hospital Management System

C++17 console application for hospital administration with local SQLite persistence, prepared for the Software Engineering mini-project by Team H-12.

## Overview

The Hospital Management System provides role-based workflows for managing patients, doctors, appointments, and reports through a console interface. The application uses a three-layer design:

- **Presentation layer:** Interactive console menus for Admin, Receptionist, and Doctor users.
- **Business layer:** Validation, authorization, scheduling rules, reporting, and workflow coordination.
- **Data-access layer:** SQLite persistence with prepared statements, foreign keys, transactions, and recovery safeguards.

Patients are managed records and do not have a separate login role.

## Implemented Features

- First-run administrator setup and authenticated user provisioning.
- Role-based login and logout for Admin, Receptionist, and Doctor accounts.
- Password storage using salted SHA-256 hashes.
- Patient registration, unique public patient IDs, search, and authorized contact updates.
- Doctor registration, specialization filtering, and weekly availability management.
- Appointment booking with availability and duplicate-slot checks.
- Appointment cancellation and atomic rescheduling.
- Doctor-owned daily schedules and consultation completion.
- Administrator daily appointment reports and patient/daily CSV or text exports.
- Parameterized SQLite queries and service-side permission checks.
- Crash-safe transactions and local database initialization when the database is missing.

## Technology Stack

- C++17
- SQLite
- OpenSSL
- CMake 3.20+
- GoogleTest
- cppcheck and Valgrind

## Build and Run

### Prerequisites

On Ubuntu or Ubuntu in WSL:

```bash
sudo apt-get update
sudo apt-get install -y build-essential cmake libsqlite3-dev libssl-dev libgtest-dev cppcheck valgrind python3-pexpect
```

### Build

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build --parallel 2
./build/hms_app
```

The first run prompts you to create an administrator. The default database path is `.local/hms.db`; use `--db PATH` to select another location.

On Windows, `Start-HMS.cmd` can launch the packaged application through Ubuntu in WSL when the Part 2 delivery branch is checked out.

## Verification

The recent Part 2 work added automated product and verification workflows, including:

- 29 passing GoogleTests covering authentication, patients, doctors, appointments, reports, security, performance, and recovery.
- Console workflow checks using a pseudoterminal.
- Static analysis with cppcheck.
- Valgrind memory checks.
- Crash-recovery validation for uncommitted database transactions.
- Performance and memory checks using a 10,000-record patient dataset.

Run the local test suite with:

```bash
ctest --test-dir build --output-on-failure
python3 tests/console_tests.py build/hms_app
python3 tests/system_checks.py build/hms_app
```

## Documentation and Delivery Materials

The original Phase 1 documents are preserved. The Part 2 delivery work updates the documentation to version 1.1 and adds implementation, traceability, setup, evidence, and planning materials.

- [Part 2 delivery index](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/blob/deliverables/part-2/deliverables/Deliverables.md)
- [Build and setup guide](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/blob/deliverables/part-2/docs/Part2/Setup.md)
- [Implemented architecture](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/blob/deliverables/part-2/docs/Part2/Architecture.md)
- [Requirements traceability](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/blob/deliverables/part-2/deliverables/planning/Traceability.md)
- [Product backlog](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/blob/deliverables/part-2/deliverables/planning/Backlog.md)
- [Version 1.1 SRS](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/blob/deliverables/part-2/docs/SRS/HMS_SRS_v1.1.docx)
- [Version 1.1 architecture and design](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/blob/deliverables/part-2/docs/Architecture_Design/HMS_ArchDesign_v1.1.docx)
- [Version 1.1 test plan](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/blob/deliverables/part-2/docs/TestPlan/HMS_TestPlan_v1.1.docx)

## Repository Structure

```text
.
├── README.md
├── CMakeLists.txt
├── include/                 # Public service and database interfaces
├── src/                     # Console, business, and SQLite implementation
├── tests/                   # GoogleTests and process-level checks
├── docs/                    # SRS, architecture, test plan, and setup guides
├── deliverables/            # Evidence, backlog, traceability, and demos
└── .github/workflows/       # Build and verification workflow
```

## Team H-12

| Member | Responsibility |
|---|---|
| Supreeth K | Patient features and user documentation |
| Shashank K | Database, doctors, and appointments |
| Shashank D | Tests, traceability, and reports |
| Sumukh Shandilya | Authentication, security, CI, and demo tooling |

## Academic Use

Software Engineering mini-project, Department of Computer Science and Engineering, PES University, Team H-12.
