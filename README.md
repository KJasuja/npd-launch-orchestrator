# 🚀 NPD Launch Orchestrator
### Product Launch Automation System | Airtable · Make · Slack

> An end-to-end GTM operations system that automates task tracking, escalation alerts, and weekly reporting across new product launches — replacing manual follow-ups with intelligent, real-time workflows.

---

## 📌 Overview

Managing multiple simultaneous product launches is chaotic — missed deadlines, no visibility into blockers, and endless status meetings. The **NPD Launch Orchestrator** solves this by wiring together a structured Airtable database, 5 Make automation scenarios, and Slack notifications into a single launch operations system.

**Built with:** Airtable · Make (formerly Integromat) · Slack  
**Type:** No-Code / Low-Code Automation  
**Use Case:** FMCG / CPG New Product Development Operations

---

## 📊 Impact at a Glance

| Metric | Result |
|--------|--------|
| GTM workflows automated | **5** |
| Platforms integrated | **3** (Airtable + Make + Slack) |
| Critical task response time | **↓ 75%** |
| Weekly reporting effort | **↓ 80%** |
| Launches tracked | **5** |
| Workstreams managed | **14** |
| Tasks monitored | **18** |

---

## 🗂️ Database Architecture

4 linked Airtable tables forming a relational launch operations database:

```
┌─────────────┐     ┌──────────────────┐     ┌───────────────┐
│   LAUNCHES  │────▶│   WORKSTREAMS    │────▶│     TASKS     │
│             │     │                  │     │               │
│ Launch Name │     │ Workstream Name  │     │ Task Name     │
│ Brand       │     │ Linked Launch    │     │ Owner         │
│ Category    │     │ Owner            │     │ Due Date      │
│ Launch Date │     │ Status           │     │ Status        │
│ Status      │     │ % Complete       │     │ Priority      │
└─────────────┘     └──────────────────┘     │ Linked WS     │
                                              └───────────────┘
                                                      │
                                              ┌───────────────┐
                                              │ ESCALATION LOG│
                                              │               │
                                              │ Task Linked   │
                                              │ Escalation Lvl│
                                              │ Triggered At  │
                                              │ Notified To   │
                                              └───────────────┘
```



## ⚙️ Automation Scenarios (Make)

### Scenario 1 — Task Assignment Notifier
**Trigger:** New task created in Airtable  
**Action:** Instant Slack DM to task owner with task name, due date, and priority  
**Impact:** Zero lag between task creation and owner awareness

---

### Scenario 2 — Deadline Reminder Alert
**Trigger:** Scheduled daily check — tasks due within 48 hours  
**Action:** Slack reminder to task owner with task details and deadline  
**Impact:** Proactive deadline management without manual follow-up

---

### Scenario 3 — Blocked Task Alert
**Trigger:** Task `Status` field changes to `Blocked`  
**Action:** Immediate Slack alert to task owner and workstream lead  
**Impact:** Blockers surfaced in real-time instead of at weekly check-ins

---

### Scenario 4 — 3-Tier Escalation Ladder
**Trigger:** Blocked task unresolved after defined thresholds  
**Action:** Auto-escalates across 3 levels with Slack notifications  
**Impact:** Critical blockers reach the right decision-maker automatically

```
Level 1  →  Task Owner          (immediate alert)
Level 2  →  Workstream Manager  (if unresolved: escalate)
Level 3  →  Launch Director     (if still unresolved: escalate)
```
Each escalation is logged in the **Escalation Log** table with timestamp and level.

---

### Scenario 5 — Weekly Launch Summary Report
**Trigger:** Every Monday at 9:00 AM (scheduled)  
**Action:** Slack message to `#launch-updates` channel with:
- Total tasks by status (On Track / At Risk / Blocked / Complete)
- Upcoming deadlines this week
- Active escalations
- Overall launch health snapshot

**Impact:** Replaces the Monday status meeting entirely

---

## 📱 Live Dashboard (Airtable Interface)

A built-in Airtable Interface provides real-time visibility across all launches:

- **Launch Health Overview** — status of all 5 active launches
- **Workstream Tracker** — completion % per workstream
- **Task Board** — filterable by owner, status, priority
- **Escalation Log** — live feed of all escalated tasks
- **KPI Summary** — aggregate metrics across the entire launch portfolio


---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    AIRTABLE (Database)                   │
│   Launches → Workstreams → Tasks → Escalation Log        │
└──────────────────────┬──────────────────────────────────┘
                       │ Make watches for triggers
                       ▼
┌─────────────────────────────────────────────────────────┐
│                  MAKE (Automation Engine)                │
│  Scenario 1: Task Assignment  │  Scenario 2: Deadlines  │
│  Scenario 3: Blocked Alert    │  Scenario 4: Escalation │
│  Scenario 5: Weekly Report    │                         │
└──────────────────────┬──────────────────────────────────┘
                       │ Pushes alerts & reports
                       ▼
┌─────────────────────────────────────────────────────────┐
│                   SLACK (Notifications)                  │
│   DMs to owners · Channel alerts · Weekly digest         │
└─────────────────────────────────────────────────────────┘
```

---

## 📁 Repository Structure

```
npd-launch-orchestrator/
│
├── README.md                        # This file
│
├── database/
│   ├── airtable-schema.md           # Full table schema with field types
│   └── sample-data.md               # Sample launch data structure
│
├── automations/
│   ├── scenario-1-task-assignment.md
│   ├── scenario-2-deadline-reminder.md
│   ├── scenario-3-blocked-alert.md
│   ├── scenario-4-escalation-ladder.md
│   └── scenario-5-weekly-report.md
│
├── dashboard/
│   └── interface-overview.md        # Airtable Interface layout & views
│
└── assets/
    └── screenshots/                 # UI screenshots (Airtable, Make, Slack)
```

---

## 🚀 How to Replicate This Project

1. **Airtable** — Create a new base with the 4 tables (schema in `/database/`)
2. **Make** — Create a free account and build the 5 scenarios using the docs in `/automations/`
3. **Slack** — Create a workspace + `#launch-updates` channel, generate a bot token
4. **Connect** — Link Make to Airtable (API key) and Slack (OAuth)
5. **Test** — Add a task in Airtable and verify the Slack notification fires

---

## 💡 Key Design Decisions

| Decision | Reasoning |
|----------|-----------|
| Airtable over spreadsheets | Relational linking between tables enables cascading automation triggers |
| Make over Zapier | More flexible multi-step scenarios; better for conditional escalation logic |
| Slack over email | Faster response time; channel-based visibility for team awareness |
| Airtable Interface over Looker Studio | Real-time sync, no middleware needed, shareable via public link |

---

## 👩‍💻 Built By

**Kriti Jasuja**  
IIT Madras  
[LinkedIn](www.linkedin.com/in/kriti-jasuja-83777033b) · [GitHub](https://github.com/KJasuja)

---

*Self Project | 2026*
