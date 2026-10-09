# Requirement Dependency Graph

Arrows point **from a prerequisite to the requirement that depends on it**
(`A --> B` means "B depends on A"). Rendered with Mermaid — GitHub displays this
automatically.

```mermaid
graph LR
    %% Foundations
    FR01[FR-01 Employee records]
    FR26[FR-26 Login]
    FR29[FR-29 Operating hours config]

    %% Employee Management
    FR01 --> FR02[FR-02 Roles]
    FR01 --> FR03[FR-03 Min/max hours]

    %% Availability
    FR01 --> FR04[FR-04 Availability]
    FR01 --> FR05[FR-05 Time-off request]
    FR05 --> FR06[FR-06 Approve time-off]
    FR04 --> FR07[FR-07 Within-hours capture]
    FR29 --> FR07

    %% Generation core
    FR03 --> FR08[FR-08 Auto-generate]
    FR04 --> FR08
    FR11[FR-11 Min staffing] --> FR08
    FR08 --> FR09[FR-09 Operating-hours rule]
    FR29 --> FR09
    FR08 --> FR10[FR-10 Shift length]
    FR30[FR-30 Shift/rest rules] --> FR10
    FR08 --> FR11
    FR08 --> FR12[FR-12 No double-book]
    FR03 --> FR13[FR-13 Max hours]
    FR08 --> FR13
    FR08 --> FR14[FR-14 Manual edit]
    FR14 --> FR15[FR-15 Publish/lock]

    %% Coverage & swaps
    FR14 --> FR16[FR-16 Open shift]
    FR15 --> FR17[FR-17 Swap/pickup]
    FR15 --> FR18[FR-18 Call-out]
    FR16 --> FR18

    %% Notifications
    FR15 --> FR19[FR-19 Publish notify]
    FR26 --> FR19
    FR17 --> FR20[FR-20 Change notify]
    FR19 --> FR20
    FR19 --> FR21[FR-21 Channels]

    %% Reporting
    FR15 --> FR22[FR-22 Hours report]
    FR01 --> FR23[FR-23 Labor cost]
    FR22 --> FR23
    FR13 --> FR24[FR-24 Overtime flag]
    FR22 --> FR24
    FR15 --> FR25[FR-25 Export/print]

    %% Auth
    FR26 --> FR27[FR-27 Role-based access]
    FR26 --> FR28[FR-28 Password reset]

    %% Business rules
    FR29 --> FR30
    FR03 --> FR31[FR-31 Labor law]
    FR30 --> FR31

    %% Non-functional (key links)
    FR08 --> NFR01[NFR-01 Usability]
    FR08 --> NFR02[NFR-02 Performance]
    FR26 --> NFR04[NFR-04 Security]
    FR27 --> NFR04
    FR04 --> NFR05[NFR-05 Mobile]
```

## Critical path

The highest-leverage chain — nothing else in the core product works until this is
in place:

**FR-01 (employees)** → **FR-04 (availability)** + **FR-03 (hours limits)** +
**FR-11 (coverage rules)** + **FR-29 (operating hours)** → **FR-08 (auto-generate)**
→ **FR-14 (edit)** → **FR-15 (publish)**.

Login (**FR-26 → FR-27**) is an independent foundation that gates notifications and
is required by the security NFR-04.
