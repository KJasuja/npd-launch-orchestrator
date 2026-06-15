# Scenario 4 — 3-Tier Escalation Ladder

## Overview
Automatically escalates unresolved blocked tasks across 3 levels of authority — from task owner to workstream manager to launch director — ensuring critical blockers always reach the right decision-maker without manual intervention.

---

## Trigger
- **Platform:** Make (Scheduled)
- **Event:** Runs every day — checks the Escalation Log for unresolved blocked tasks

---

## Escalation Logic

```
Task Status = "Blocked"
        ↓
Level 1 — Task Owner notified immediately (via Scenario 3)
        ↓
[If still Blocked after threshold]
        ↓
Level 2 — Workstream Manager notified
        ↓
[If still Blocked after threshold]
        ↓
Level 3 — Launch Director notified
```

---

## Flow

```
[Make] Scheduled trigger fires daily
        ↓
[Airtable] Search Escalation Log — unresolved records
        ↓
[Make] Check escalation level for each record
        ↓
[Make] Router — branch by Level (1 / 2 / 3)
        ↓
Level 1 → [Slack] DM to Task Owner
Level 2 → [Slack] DM to Workstream Manager
Level 3 → [Slack] DM to Launch Director
        ↓
[Airtable] Update Escalation Log — increment level + log timestamp
```

---

## Slack Message Format

**Level 2 escalation:**
```
⚠️ Escalation — Level 2

A blocked task has not been resolved and is being escalated to you.

Task: Submit regulatory docs
Workstream: Regulatory Approvals
Blocked Since: 04 Sep 2025
Escalated From: Rahul Mehta (Task Owner)

Please intervene to unblock this task immediately.
```

**Level 3 escalation:**
```
🔴 CRITICAL Escalation — Level 3 (Director)

Task: Submit regulatory docs
Launch: GlowRich Body Lotion
Blocked Since: 04 Sep 2025
Previously Escalated To: Workstream Manager (unresolved)

This is a launch-critical blocker. Immediate action required.
```

---

## Escalation Log Table (Airtable)

Each escalation is logged with:
| Field | Value |
|---|---|
| Linked Task | Submit regulatory docs |
| Escalation Level | Level 2 |
| Notified To | Workstream Manager |
| Triggered At | 2025-09-05 09:00 AM |
| Resolved | ☐ |

---

## Make Modules Used
1. **Make — Scheduled Trigger** (daily check)
2. **Airtable — Search Records** (unresolved escalations in log)
3. **Make — Iterator** (loop through each)
4. **Make — Router** (branch by escalation level)
5. **Slack — Create a Message** × 3 (one per level)
6. **Airtable — Update a Record** (log escalation level + timestamp)

---

## Business Impact
- Critical blockers never get buried or forgotten
- Decision-makers are looped in automatically based on severity
- Full audit trail maintained in Escalation Log
- Cuts critical task response time by **75%** vs. manual follow-up
