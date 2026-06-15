# Airtable Database Schema
## NPD Launch Orchestrator

4 linked tables forming a relational launch operations database.

---

## Table 1 — Launches

| Field Name | Field Type | Description |
|---|---|---|
| Launch Name | Single line text | Name of the product launch (e.g., GlowRich Body Lotion) |
| Brand | Single line text | Brand name |
| Category | Single select | FMCG category (e.g., Skincare, Haircare, Home Care) |
| Launch Date | Date | Target market launch date |
| Status | Single select | Not Started / In Progress / At Risk / Launched |
| Launch Manager | Single line text | Person responsible for the launch |
| Linked Workstreams | Link to Workstreams | All workstreams under this launch |

**Sample Data:**

| Launch Name | Brand | Category | Status |
|---|---|---|---|
| GlowRich Body Lotion | GlowRich | Skincare | In Progress |
| FreshBreeze Shampoo | FreshBreeze | Haircare | In Progress |
| CleanHome Floor Cleaner | CleanHome | Home Care | Not Started |
| NutriBoost Protein Bar | NutriBoost | Nutrition | At Risk |
| SparkWhite Toothpaste | SparkWhite | Oral Care | In Progress |

---

## Table 2 — Workstreams

| Field Name | Field Type | Description |
|---|---|---|
| Workstream Name | Single line text | Name of the workstream (e.g., Packaging Design) |
| Linked Launch | Link to Launches | Parent launch this workstream belongs to |
| Owner | Single line text | Workstream owner name |
| Status | Single select | Not Started / In Progress / Blocked / Complete |
| % Complete | Number | Overall completion percentage (0–100) |
| Linked Tasks | Link to Tasks | All tasks under this workstream |

**Workstream Categories across launches:**
- Demand Planning
- Packaging Design
- Regulatory Approvals
- Supply Chain
- Marketing & Comms
- Trade & Distribution
- Quality Assurance
- Digital & E-Commerce

---

## Table 3 — Tasks

| Field Name | Field Type | Description |
|---|---|---|
| Task Name | Single line text | Name of the task |
| Linked Workstream | Link to Workstreams | Parent workstream this task belongs to |
| Owner | Single line text | Person responsible for the task |
| Due Date | Date | Task deadline |
| Status | Single select | To Do / In Progress / Blocked / Complete |
| Priority | Single select | High / Medium / Low |
| Notes | Long text | Additional context or blockers |

**Sample Tasks:**

| Task Name | Owner | Due Date | Status | Priority |
|---|---|---|---|---|
| Finalize pack artwork | Priya Sharma | 2025-09-10 | In Progress | High |
| Submit regulatory docs | Rahul Mehta | 2025-09-05 | Blocked | High |
| Confirm vendor pricing | Anjali Singh | 2025-09-15 | To Do | Medium |
| Draft launch PR brief | Rohan Das | 2025-09-20 | In Progress | Medium |
| Complete shelf planogram | Neha Kapoor | 2025-09-12 | To Do | Low |
| Set up D2C product page | Vikram Nair | 2025-09-18 | In Progress | High |

---

## Table 4 — Escalation Log

| Field Name | Field Type | Description |
|---|---|---|
| Escalation ID | Auto number | Unique ID auto-generated |
| Linked Task | Link to Tasks | The blocked task that triggered escalation |
| Escalation Level | Single select | Level 1 / Level 2 / Level 3 |
| Notified To | Single line text | Name of person notified at this level |
| Triggered At | Date & Time | Timestamp when escalation was triggered |
| Resolved | Checkbox | Whether the blocker has been resolved |
| Resolution Notes | Long text | How the blocker was resolved |

**Escalation Logic:**
```
Level 1 → Task Owner notified immediately when status = Blocked
Level 2 → Workstream Manager notified if unresolved after threshold
Level 3 → Launch Director notified if still unresolved
```

---

## Table Relationships

```
LAUNCHES (1)
    └── WORKSTREAMS (many)
            └── TASKS (many)
                    └── ESCALATION LOG (many)
```

Each table links to its parent via Airtable's **Link to another record** field type, enabling cascading views, rollups, and automation triggers across the entire hierarchy.

---

## Key Airtable Features Used

| Feature | Used For |
|---|---|
| Linked Records | Connecting all 4 tables relationally |
| Single Select | Status fields used as Make automation triggers |
| Rollup Fields | Calculating % complete at workstream & launch level |
| Airtable Interface | Building the live ops dashboard |
| Automations (native) | Supporting Make webhook triggers |
| Views | Filtered views per owner, per launch, per status |
