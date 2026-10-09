# Requirements Backlog — Mike's Scheduling App

**First-pass elicitation output.** Prioritized with MoSCoW, sized in story points,
tagged by epic/type/source, and linked by dependency. See
[`README.md`](README.md) §5 for the metadata legend.

- **FR** = Functional requirement · **NFR** = Non-functional requirement
- **Source:** `Stakeholder` = from the original problem statement · `Elicited` = expanded/inferred in this pass and **to be confirmed** with the owner
- Status of every item in this first pass is **Proposed**.

---

## E1 — Employee Management

| ID | Requirement (user story) | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| FR-01 | As a manager, I can add, edit, and deactivate employee records (name, contact info, role, pay rate) so the roster stays current. | Functional | Must | 5 | — | Elicited |
| FR-02 | As a manager, I can assign one or more **roles/positions** (e.g., cashier, stocker) to an employee so scheduling can match roles to shifts. | Functional | Should | 3 | FR-01 | Elicited |
| FR-03 | As a manager, I can set each employee's **employment type and weekly min/max hours** so the schedule respects their limits. | Functional | Must | 3 | FR-01 | Elicited |

## E2 — Availability & Time-Off

| ID | Requirement (user story) | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| FR-04 | As an employee, I can submit my **recurring weekly availability** as time ranges so I'm only scheduled when I can work. | Functional | Must | 5 | FR-01 | Stakeholder |
| FR-05 | As an employee, I can request **time off / blackout dates** for specific days. | Functional | Must | 3 | FR-01 | Elicited |
| FR-06 | As a manager, I can **approve or deny** time-off requests, and approved requests block scheduling for that period. | Functional | Must | 3 | FR-05 | Elicited |
| FR-07 | Availability and time-off are captured **within the store's operating window** and in the store's time zone so entries can't fall outside open hours. | Functional | Should | 2 | FR-04, FR-29 | Elicited |

## E3 — Schedule Generation (the core automation)

| ID | Requirement (user story) | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| FR-08 | As a manager, I can **auto-generate a draft weekly schedule** from employee availability and coverage rules with one action. | Functional | Must | 13 | FR-03, FR-04, FR-11 | Stakeholder |
| FR-09 | The generator only places shifts **within operating hours** (default 8:00 AM–2:00 AM). | Functional | Must | 3 | FR-08, FR-29 | Stakeholder |
| FR-10 | The generator creates shifts of **configurable length (default 6–10 hours)**. | Functional | Must | 3 | FR-08, FR-30 | Stakeholder |
| FR-11 | As a manager, I can define **minimum staffing per time block** (e.g., ≥1 cashier 8 AM–close) and the generator guarantees coverage. | Functional | Must | 8 | FR-08 | Elicited |
| FR-12 | The generator **never double-books** an employee into overlapping shifts. | Functional | Must | 3 | FR-08 | Elicited |
| FR-13 | The generator **respects each employee's max weekly hours** and does not exceed them. | Functional | Must | 3 | FR-03, FR-08 | Elicited |
| FR-14 | As a manager, I can **manually edit** the generated draft (move, add, delete, reassign shifts) before publishing. | Functional | Must | 8 | FR-08 | Elicited |
| FR-15 | As a manager, I can **publish/lock** a schedule so it becomes the official version for that week. | Functional | Must | 3 | FR-14 | Elicited |

## E4 — Shift Coverage & Swaps

| ID | Requirement (user story) | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| FR-16 | As a manager, I can mark a shift as **open/unfilled** when no one is assigned. | Functional | Should | 2 | FR-14 | Elicited |
| FR-17 | As an employee, I can **request to swap or pick up a shift**, subject to manager approval. | Functional | Should | 8 | FR-15 | Elicited |
| FR-18 | As a manager, I can record a **call-out** and the affected shift is flagged as open and re-offerable. | Functional | Should | 5 | FR-15, FR-16 | Elicited |

## E5 — Notifications

| ID | Requirement (user story) | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| FR-19 | When a schedule is **published**, affected employees are **notified**. | Functional | Should | 5 | FR-15, FR-26 | Elicited |
| FR-20 | When a **shift changes** (swap, call-out, edit after publish), affected employees are notified. | Functional | Should | 3 | FR-17, FR-19 | Elicited |
| FR-21 | As a manager, I can choose the **notification channel** (in-app, email, and/or SMS). | Functional | Could | 5 | FR-19 | Elicited |

## E6 — Reporting & Labor Cost

| ID | Requirement (user story) | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| FR-22 | As a manager, I can see **total scheduled hours per employee per week**. | Functional | Should | 3 | FR-15 | Elicited |
| FR-23 | As a manager, I can see an **estimated labor cost** (pay rate × scheduled hours). | Functional | Could | 3 | FR-01, FR-22 | Elicited |
| FR-24 | The system **flags overtime / over-max** hours before I publish. | Functional | Should | 3 | FR-13, FR-22 | Elicited |
| FR-25 | As a manager/employee, I can **export or print** the schedule (PDF and/or calendar feed). | Functional | Could | 5 | FR-15 | Elicited |

## E7 — Authentication & Access

| ID | Requirement (user story) | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| FR-26 | Users can **create an account and log in**. | Functional | Must | 5 | — | Elicited |
| FR-27 | The system enforces **role-based access** (manager vs. employee) so employees can't edit schedules or other employees' data. | Functional | Must | 5 | FR-26 | Elicited |
| FR-28 | Users can **reset a forgotten password**. | Functional | Should | 2 | FR-26 | Elicited |

## E8 — Business Rules & Compliance

| ID | Requirement (user story) | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| FR-29 | As a manager, I can **configure operating hours** rather than having them hard-coded, so the app fits businesses with other hours. | Functional | Must | 3 | — | Stakeholder |
| FR-30 | As a manager, I can **configure shift-length rules and minimum rest** between an employee's shifts. | Functional | Should | 3 | FR-29 | Elicited |
| FR-31 | The system supports **minor/labor-law constraints** (e.g., limits for employees under 18). | Functional | Won't (this release) | 8 | FR-03, FR-30 | Elicited |

## E9 — Quality Attributes (Non-Functional)

| ID | Requirement | Type | Priority | Est | Depends on | Source |
|---|---|---|---|---|---|---|
| NFR-01 | **Usability:** a non-technical owner can generate and publish a weekly schedule in **under 15 minutes** with no training beyond a quick-start guide. | Non-Functional | Must | 5 | FR-08 | Stakeholder |
| NFR-02 | **Performance:** a draft weekly schedule for up to ~25 employees generates in **under 10 seconds**. | Non-Functional | Should | 3 | FR-08 | Elicited |
| NFR-03 | **Availability:** the app is reachable 24/7 with ≥99% monthly uptime (employees check during an 8 AM–2 AM operation). | Non-Functional | Should | 3 | — | Elicited |
| NFR-04 | **Security/Privacy:** passwords are hashed and employee PII (contact info, pay rate) is access-controlled and encrypted in transit. | Non-Functional | Must | 5 | FR-26, FR-27 | Elicited |
| NFR-05 | **Mobile-friendly:** employees can view schedules and submit availability from a phone browser. | Non-Functional | Must | 5 | FR-04 | Elicited |
| NFR-06 | **Low operating cost:** the solution runs on low-cost/free-tier infrastructure to suit a small business with minimal capital. | Non-Functional | Should | 2 | — | Stakeholder |
| NFR-07 | **Data durability:** schedule and employee data are backed up so a failure doesn't lose historical schedules. | Non-Functional | Should | 3 | — | Elicited |

---

## Acceptance criteria for the MVP (Must-have) requirements

> Acceptance criteria are drafted for the first-release (`Must`) items. Remaining
> items get criteria when they are pulled into a sprint.

**FR-08 — Auto-generate draft schedule**
- Given employees with saved availability and defined coverage rules, when the manager clicks "Generate," then a draft schedule is produced for the selected week.
- Every placed shift falls within operating hours (FR-09) and allowed shift lengths (FR-10).
- No employee is double-booked (FR-12) or scheduled beyond their max hours (FR-13).
- If coverage cannot be met, the manager sees which time blocks are **short-staffed** rather than a silent failure.

**FR-04 — Submit weekly availability**
- An employee can enter available time ranges per day of week and save them.
- Saved availability persists and is used by the next generation run.

**FR-11 — Minimum staffing per time block**
- The manager can define required headcount (optionally by role) for named time blocks.
- The generator does not leave a required block below its minimum without flagging it.

**FR-29 — Configurable operating hours**
- Default operating hours are 8:00 AM–2:00 AM, editable by the manager.
- Changing operating hours constrains future availability entry and generation.

**FR-26 / FR-27 — Login & role-based access**
- A user must authenticate to access any schedule data.
- An employee account cannot view other employees' PII or edit/publish schedules.

**NFR-01 — Usability target**
- In usability testing, a first-time non-technical user completes "generate + publish a week" in under 15 minutes using only the quick-start guide.

---

## Backlog summary

| Priority | Count |
|---|---|
| Must | 19 |
| Should | 15 |
| Could | 3 |
| Won't (this release) | 1 |
| **Total** | **38** (31 functional + 7 non-functional) |

**Suggested first release (MVP)** = all `Must` items: FR-01, FR-03, FR-04, FR-05,
FR-06, FR-08, FR-09, FR-10, FR-11, FR-12, FR-13, FR-14, FR-15, FR-26, FR-27, FR-29,
plus NFR-01, NFR-04, NFR-05. These deliver the core promise: *enter availability →
auto-generate a valid schedule → edit → publish*, behind a secure login.
