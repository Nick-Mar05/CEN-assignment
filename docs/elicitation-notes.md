# First-Pass Elicitation Notes

These capture the thinking behind the backlog: what was assumed, what still needs
to be asked, and what was deliberately left out. In a real engagement these go
back to the stakeholder (the store owner) for confirmation before estimates and
priorities are trusted.

## Assumptions (to confirm with the owner)

1. **Roster size** is small — on the order of ~5–25 employees — so schedule
   generation does not need heavy optimization infrastructure.
2. Scheduling is done on a **weekly** cycle.
3. The owner wants to keep **final manual control** — the system proposes a draft,
   the owner edits and approves. It is an assistant, not a fully autonomous scheduler.
4. Employees have **smartphones** and can receive notifications and submit
   availability online (justifies NFR-05, FR-04).
5. There is **one location** in the first release.
6. "Minimal capital" (from the original statement) means the solution should favor
   **free/low-cost hosting** and avoid paid per-seat software (NFR-06).

## Open questions (to send back to the stakeholder)

- What are the **minimum staffing levels** by time of day? (Drives FR-11.)
- Are there **distinct roles** that must be covered separately (cashier vs. stocker),
  or is any employee interchangeable? (Drives FR-02.)
- Do any employees have **fixed/preferred shifts** that should seed the schedule?
- Are there **legal constraints** (minors, mandated breaks, max consecutive days)
  that must be enforced vs. merely flagged? (Drives FR-31, currently deferred.)
- Preferred **notification channel** — is SMS worth the cost, or is email/in-app enough?
- How far in advance are schedules published, and how are **last-minute call-outs**
  handled today?
- Is **pay-rate data** in scope (enables labor-cost reporting FR-23) or too sensitive
  to store in a first release?
- Should the system integrate with an existing **payroll or POS** system?

## Out of scope for this release (acknowledged, deferred)

- Multi-location / franchise scheduling.
- Payroll processing and time-clock / punch-in tracking.
- Demand forecasting (predicting busy periods from sales data).
- Automated labor-law compliance enforcement (FR-31 is deferred to a later release).
- Native iOS/Android apps — a mobile-friendly web app covers the first release (NFR-05).

## Prioritization rationale (MoSCoW)

- **Must** items form the smallest system that actually solves the owner's stated
  pain: capture availability → auto-generate a valid, conflict-free schedule within
  the store's hours and shift lengths → edit → publish, secured by login.
- **Should** items (swaps, notifications, reporting) make it pleasant and sticky but
  the owner could still operate without them on day one.
- **Could** items are nice-to-haves gated on time.
- **Won't (this release)** acknowledges labor-law automation as real but out of the
  first-release budget.
