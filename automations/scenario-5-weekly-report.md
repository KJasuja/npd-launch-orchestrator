# Scenario 5 — Weekly Launch Summary Report

## Overview
Every Monday at 9:00 AM, automatically compiles and sends a complete launch health summary to the Slack channel — replacing the weekly status meeting with a single, structured digest.

---

## Trigger
- **Platform:** Make (Scheduled)
- **Event:** Every Monday at 9:00 AM

---

## Flow

```
[Make] Scheduled trigger fires every Monday 9:00 AM
        ↓
[Airtable] Fetch all Launches (1 record — summary view)
        ↓
[Airtable] Fetch all Tasks — count by Status
        ↓
[Airtable] Fetch active Escalations from Escalation Log
        ↓
[Make] Aggregate data into weekly digest
        ↓
[Slack] Post summary message to #launch-updates channel
```

---

## Slack Message Format

```
📊 Weekly Launch Status Report — Week of 08 Sep 2025

━━━━━━━━━━━━━━━━━━━━━━━━
🚀 ACTIVE LAUNCHES (5)
━━━━━━━━━━━━━━━━━━━━━━━━
✅ GlowRich Body Lotion — On Track
⚠️  NutriBoost Protein Bar — At Risk
🔄 FreshBreeze Shampoo — In Progress
🔄 CleanHome Floor Cleaner — In Progress
🔄 SparkWhite Toothpaste — In Progress

━━━━━━━━━━━━━━━━━━━━━━━━
📋 TASK SUMMARY (18 Total)
━━━━━━━━━━━━━━━━━━━━━━━━
✅ Complete: 4
🔄 In Progress: 9
🚨 Blocked: 3
📌 To Do: 2

━━━━━━━━━━━━━━━━━━━━━━━━
🚨 ACTIVE ESCALATIONS
━━━━━━━━━━━━━━━━━━━━━━━━
• Submit regulatory docs — Level 2 (Escalated to Manager)
• Confirm vendor pricing — Level 1 (Owner notified)

━━━━━━━━━━━━━━━━━━━━━━━━
📅 DUE THIS WEEK
━━━━━━━━━━━━━━━━━━━━━━━━
• Finalize pack artwork — 10 Sep (Priya Sharma)
• Set up D2C product page — 10 Sep (Vikram Nair)
• Complete shelf planogram — 12 Sep (Neha Kapoor)

Have a great week! 🚀
```

---

## Make Modules Used
1. **Make — Scheduled Trigger** (every Monday 9:00 AM)
2. **Airtable — Search Records** (Launches table — max 1 record)
3. **Airtable — Search Records** (Tasks table — max 1 record)
4. **Airtable — Search Records** (Escalation Log — active only)
5. **Slack — Create a Message** (post to `launch-updates` channel)

> **Note:** Each Airtable module is set to return a maximum of 1 record to prevent the scenario from looping and sending duplicate messages.

---

## Business Impact
- Replaces the Monday morning status meeting entirely
- Entire team gets consistent visibility every week
- Launch managers save ~2 hours/week on status compilation
- Reduces weekly reporting effort by **80%**
