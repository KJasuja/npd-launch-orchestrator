# Scenario 2 — Deadline Reminder Alert

## Overview
Runs a scheduled daily check on all tasks and sends a Slack reminder to task owners for any task due within 48 hours — enabling proactive deadline management without any manual follow-up.

---

## Trigger
- **Platform:** Make (Scheduled)
- **Event:** Runs every day at 9:00 AM

---

## Flow

```
[Make] Scheduled trigger fires at 9:00 AM daily
        ↓
[Airtable] Search Records — Tasks where Due Date = today + 48 hours
           AND Status ≠ Complete
        ↓
[Make] For each matching task:
        ↓
[Slack] Send DM to task owner with deadline alert
```

---

## Slack Message Format

```
⏰ Deadline Reminder

Your task is due in less than 48 hours!

Task: Submit regulatory docs
Workstream: Regulatory Approvals
Due Date: 05 Sep 2025
Priority: 🔴 High
Status: In Progress

Please update your task status in Airtable.
```

---

## Make Modules Used
1. **Make — Scheduled Trigger** (daily at 9:00 AM)
2. **Airtable — Search Records** (filter by due date and status)
3. **Make — Iterator** (loops through each matching task)
4. **Slack — Create a Message** (DM to each task owner)

---

## Business Impact
- Prevents missed deadlines across 18+ tasks simultaneously
- No manual tracking needed by the launch manager
- Owners get a consistent, timely nudge every morning
