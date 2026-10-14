# Hospital Management System

C++17 console application for Team H-12's Software Engineering mini-project, with SQLite persistence and a three-layer architecture: console interface, business services, and database access.

The Part-2 implementation is published on the fork's [`deliverables/part-2` branch](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/tree/deliverables/part-2). [Implementation PR #1](https://github.com/Sumukh-2006/SE-Mini-Project_Team-H-12/pull/1) was merged into the team repository on 12 October 2026. Open the branch link to see subsequent updates; the fork's default page displays `main`.

| Role | Available features |
|---|---|
| Admin | Manage doctors, weekly availability and user accounts; view daily totals; export patient and daily reports as CSV or text |
| Receptionist | Register patients with unique alphanumeric IDs, search records, update contacts, and book, cancel or reschedule appointments |
| Doctor | Search patient records, view their own daily schedule, and mark their own consultations completed |

Appointments use 15-minute slots within weekly availability. Conflict checks prevent double booking, and a failed reschedule preserves the original appointment. Business services enforce permissions before data access. Storage uses prepared SQL statements and transactions; passwords use salted SHA-256 through OpenSSL, following the submitted architecture. Billing, pharmacy, online payments and audit logging are outside the delivered numbered-SRS scope.

To build on Ubuntu 24.04 or Ubuntu in WSL, run:

```sh
git clone --branch deliverables/part-2 https://github.com/shashankd06/SE-Mini-Project_Team-H-12.git
cd SE-Mini-Project_Team-H-12
sudo apt-get update
sudo apt-get install -y build-essential cmake libsqlite3-dev libssl-dev libgtest-dev cppcheck valgrind python3-pexpect time
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build --parallel 2
./build/hms_app
```

On Windows with the `Ubuntu-24.04` WSL distribution installed, [Start-HMS.cmd](Start-HMS.cmd) launches the packaged Linux executable. The binaries are built for Ubuntu; they are not native Windows executables.

First run creates an administrator using credentials you choose. Sign in, add doctors and weekly availability, then create Receptionist and linked Doctor accounts. Records persist in `.local/hms.db`; working databases and credentials are excluded from version control. Enter `0` to log out and `q` at the username prompt to quit. See the [setup and user guide](docs/Part2/Setup.md) for input formats, report behavior and a separate fictional demo database.

| Deliverable | Location |
|---|---|
| Full package checklist and local sprint preparation reviews | [Delivery index](deliverables/Deliverables.md) |
| 39 proposed stories and supporting tasks | [Backlog](deliverables/planning/Backlog.md), [issue drafts](deliverables/planning/issue-drafts), [Project setup](deliverables/planning/project-setup.json) |
| Coverage of 20 functional, 6 non-functional and 3 security requirements | [Traceability matrix](deliverables/planning/Traceability.md) |
| Updated Software Requirements Specification | [SRS v1.1](docs/SRS/HMS_SRS_v1.1.docx) |
| Updated architecture and design | [Architecture v1.1](docs/Architecture_Design/HMS_ArchDesign_v1.1.docx), [implementation diagrams](docs/Part2/Architecture.md) |
| Updated test plan and local results | [Test Plan v1.1](docs/TestPlan/HMS_TestPlan_v1.1.docx), [execution evidence](deliverables/evidence) |
| Sprint-1 console demonstration, 60 seconds | [Video](deliverables/videos/Sprint-1-Demo.mp4) |
| Final console demonstration, 120 seconds | [Video](deliverables/videos/Sprint-2-Demo.mp4) |
| Build, tests, static analysis and memory checks | [GitHub Actions workflow](.github/workflows/ci.yml), [fork workflow runs](https://github.com/shashankd06/SE-Mini-Project_Team-H-12/actions) |
| Design decisions and team handoff | [Deviations](docs/Part2/Deviations.md), [publishing guide](docs/Part2/Publishing.md), [teammate PR drafts](deliverables/planning/PR-Drafts.md) |

Original version 1.0 documents and diagrams are preserved. Videos replay actual console output with captions and edited reading durations, using fictional patient data.

To verify a local build:

```sh
ctest --test-dir build --output-on-failure
python3 tools/verify_local.py
```

The verifier refreshes the files in `deliverables/evidence/`. Recorded local execution on 12 October 2026 passed all 29 GoogleTests, console checks and cppcheck. Valgrind reported zero errors and all heap blocks freed. Crash testing verified transaction rollback and database integrity. With 10,000 records, an ID query took about 0.055 seconds and a broad search with 9,999 displayed results took about 0.136 seconds; normal process RSS was 10,076 KB. These measurements apply to the documented Ubuntu WSL workstation. Hosted CI status is available from the workflow runs link above.

| Team member | Proposed Part-2 responsibility |
|---|---|
| Supreeth K | Patient features and user documentation |
| Shashank K | Database, doctors and appointments |
| Shashank D | Tests, traceability and reports |
| Sumukh Shandilya | Authentication, security, CI and demo tooling |

Sprint 1 is scheduled for 19-23 October 2026 and Sprint 2 for 26-30 October. The implementation and recorded evidence were prepared early, on 12 October. Runnable checkpoint executables are included in `deliverables/bin/`; the preparation checkout also retains the unpublished `sprint-1-local` and `sprint-2-local` tags.

Publication status was checked on 14 October 2026: the implementation branch is pushed and PR #1 is merged. The delivery index, setup guide and evidence retain their original local-preparation snapshot, including statements that publication was pending at that time. The shared GitHub Project and issue drafts still need publication; assigned teammates must make their own contributions, with owner reviews and actual sprint reviews recorded as they occur. The final development freeze remains scheduled for 30 October.

Academic use: Software Engineering mini-project, PES University, Team H-12.
