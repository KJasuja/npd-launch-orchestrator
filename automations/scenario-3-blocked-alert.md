# Scenario 3 — Blocked Task Alert

## Overview
Detects the moment a task is marked as "Blocked" in Airtable and instantly fires a Slack alert to both the task owner and the workstream lead — surfacing blockers in real-time instead of at weekly check-ins.

---

## Trigger
- **Platform:** Airtable
- **Event:** Record updated in the **Tasks** table where `Status` changes to `Blocked`

---

## Flow

```
[Airtable] Task Status updated to "Blocked"
        ↓
[Make] Watches Tasks table for status change
        ↓
[Airtable] Get Record — fetch Task Name, Owner, Workstream, Notes
        ↓
[Slack] Alert sent to task owner (DM)
        ↓
[Slack] Alert sent to workstream lead (DM)
```

---

## Slack Message Format

```
🚨 Task Blocked — Immediate Attention Required

Task: Submit regulatory docs
Workstream: Regulatory Approvals
Owner: Rahul Mehta
Blocked Since: 04 Sep 2025

Notes: Awaiting sign-off from QA team before submission.

Please resolve this blocker or escalate immediately.
```

---

## Make Modules Used
1. **Airtable — Watch Records** (trigger on Status field change)
2. **Make — Filter** (condition: Status = "Blocked")
3. **Airtable — Get a Record** (fetch full task + workstream details)
4. **Slack — Create a Message** (DM to task owner)
5. **Slack — Create a Message** (DM to workstream lead)

---

## Business Impact
- Blockers are visible within seconds — not days
- Both owner and lead are looped in simultaneously
- Feeds into the Escalation Ladder (Scenario 4) if unresolved
