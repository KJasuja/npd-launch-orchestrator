# Scenario 1 — Task Assignment Notifier

## Overview
Automatically notifies a task owner via Slack the moment a new task is assigned to them in Airtable — eliminating manual communication and ensuring zero lag between task creation and owner awareness.

---

## Trigger
- **Platform:** Airtable
- **Event:** New record created in the **Tasks** table

---

## Flow

```
[Airtable] New task created
        ↓
[Make] Watches Tasks table for new records
        ↓
[Make] Reads: Task Name, Owner, Due Date, Priority, Linked Workstream
        ↓
[Slack] Sends DM to task owner
```

---

## Slack Message Format

```
📋 New Task Assigned to You

Task: Finalize pack artwork
Workstream: Packaging Design
Due Date: 10 Sep 2025
Priority: 🔴 High

Log in to Airtable to view full details.
```

---

## Make Modules Used
1. **Airtable — Watch Records** (trigger on Tasks table)
2. **Airtable — Get a Record** (fetch linked workstream name)
3. **Slack — Create a Message** (DM to owner)

---

## Business Impact
- Owner is notified within seconds of task creation
- Replaces manual WhatsApp/email follow-up from the launch manager
- Creates accountability from day one of task assignment
