# Mike's Scheduling App — Requirements Backlog

A software project to replace manual, error-prone employee scheduling at a small
business ("Mike's Liquor and Beer") with an automated scheduling application
tailored to the unusual hours and shift patterns of small retail operations.

This repository is the deliverable for a requirements-elicitation assignment. It
contains the **outcome of an initial (first-pass) requirements elicitation**,
captured as a prioritized product backlog with metadata tags and inter-requirement
dependencies.

---

## 1. Problem statement

The store is open **8:00 AM – 2:00 AM every day** (an 18-hour operating window)
and staffs **6–10 hour shifts**. Scheduling is currently done by hand by the
owner. Manual scheduling:

- is **time-consuming** (hours of the owner's week),
- is **error-prone** (double-bookings, gaps in coverage, missed availability),
- does not easily account for **irregular, long operating hours** and odd shift
  lengths, and
- offers **no self-service** for employees to see schedules or request changes.

**Goal:** automate schedule generation while respecting employee availability,
time-off, and business coverage rules, and give employees self-service visibility
into their schedules.

## 2. Primary stakeholders

| Stakeholder | Role / interest |
|---|---|
| **Owner / Manager** (e.g., Mike) | Creates and approves schedules; owns labor cost; final authority on coverage rules |
| **Employees** | Submit availability and time-off; view schedules; request swaps |
| **Shift leads** (future) | May assist with coverage decisions |
| **Developer** (course author) | Builds and maintains the system |

## 3. How this backlog was produced

Following the assignment, a large language model (Anthropic's Claude) was used to
conduct a **first-pass requirements elicitation** from the original problem
statement. The model was instructed to:

1. Expand the brief problem statement into discrete, testable requirements.
2. Tag each requirement with **metadata** (type, priority, epic, estimate, status, source).
3. Identify **dependencies** between requirements.
4. Surface **assumptions** and **open questions** that a real elicitation would
   send back to the stakeholder for clarification.

This is deliberately a *first pass*: priorities, estimates, and the open questions
are starting points to be refined with the stakeholder, not final commitments.

## 4. Repository contents

| File | Purpose |
|---|---|
| [`BACKLOG.md`](BACKLOG.md) | The full requirements backlog — human-readable, grouped by epic, with metadata and dependencies |
| [`backlog.csv`](backlog.csv) | The same backlog in a machine-readable table (import into Jira/Trello/Excel) |
| [`docs/elicitation-notes.md`](docs/elicitation-notes.md) | Assumptions, open questions, and out-of-scope items from this first pass |
| [`docs/dependency-graph.md`](docs/dependency-graph.md) | A visual (Mermaid) dependency graph of the requirements |

## 5. Metadata legend

Each requirement carries the following tags.

**ID** — `FR-nn` for functional requirements, `NFR-nn` for non-functional.

**Type**
- `Functional` — a behavior the system performs.
- `Non-Functional` — a quality attribute / constraint (performance, security, usability…).

**Priority (MoSCoW)**
- `Must` — required for a usable first release (MVP).
- `Should` — important but not vital to the first release.
- `Could` — desirable; included if time permits.
- `Won't (this release)` — acknowledged but deferred.

**Epic** — the feature area the requirement belongs to (see §6).

**Estimate** — rough relative size in **story points** (Fibonacci: 1, 2, 3, 5, 8, 13).

**Status** — lifecycle state. In a first-pass backlog everything is `Proposed`.

**Source** — where the requirement came from (`Stakeholder` = original problem
statement; `Elicited` = inferred/expanded by analysis and flagged for confirmation).

**Depends on** — IDs of requirements that must be in place first.

## 6. Epics

| Epic | Description |
|---|---|
| **E1 — Employee Management** | Maintain the roster of employees and their attributes |
| **E2 — Availability & Time-Off** | Capture when employees can and cannot work |
| **E3 — Schedule Generation** | Automatically build a valid schedule from rules + availability |
| **E4 — Shift Coverage & Swaps** | Handle call-outs, open shifts, and employee-initiated swaps |
| **E5 — Notifications** | Tell people about published schedules and changes |
| **E6 — Reporting & Labor Cost** | Give the owner visibility into hours and cost |
| **E7 — Authentication & Access** | Accounts, login, and role-based permissions |
| **E8 — Business Rules & Compliance** | Operating-hours, shift-length, and labor-rule constraints |
| **E9 — Quality Attributes** | Non-functional requirements across the whole system |

See **[BACKLOG.md](BACKLOG.md)** for the requirements themselves.
