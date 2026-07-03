# Phase 1: Lead Qualifier
## Overview

It focuses on automating lead intake, qualification, and initial engagement using Make and integrated business tools.
The system captures inbound leads from a form, evaluates them against budget and fit criteria using AI, and automatically routes them to communication channels (Gmail and Slack). Qualified leads are scheduled for meetings via Calendly, while all activity is logged in Airtable.

---

## Tech Stack
- Make - automation platform
- Tally - lead capture form
- Airtable - database
- Gmail - email notification
- Slack - internal notification
- Calendly - meeting scheduling

## Workflow Architecture

Tally Form
↓
Airtable (Store Lead)
↓
Airtable Watch Records (Trigger)
↓
OpenAI (Lead Qualification + Message Generation)
↓
Router
├── Gmail Notification
└── Slack Notification
↓
Calendly (Meeting Scheduling)
↓
Airtable Update (Contacted Time + Status)

---

## Process Description

### Lead Capture
- Leads are collected through the Tally form.
- Each form field is mapped directly to the corresponding Airtable.

### Data Storage
- Airtable stores all incoming lead data.
- Each submission creates a new record.

### Trigger Mechanism
- Airtable is configured with a **"Watch Records"** trigger.
- The automation activates when a new record is created.

### AI Qualification
- Each lead is evaluated based on predefined criteria.
- An AI prompt is used to generate:
  - Lead qualification status (Qualififed/Not Qualified)
  - A descriptive summary of the lead.

### Routing Logic
- A router splits the workflow into two parallel paths:
  - Gmail notification
  - Slack notification

This prevents sequential delays and ensures simultaneous delivery.

### Communication Layer
- Gmail sends an external email with lead summary and meeting link.
- Slack sends an internal notification with the same structured information.

### Data Update
- Airtable is updated after execution:
  - Lead contacted timestamp
  - Qualification result
  - Communication status
 
## Output

Each processed lead results in:

- Qualification decision
- AI-generated lead summary
- Email sent via Gmail
- Slack notification sent
- Optional Calendly meeting scheduled
- Airtable record fully updated

---

## Design Decisions

- **Airtable as central database:** Simplifies integration across tools without requiring a backend.
- **Make as orchestration layer:** Enables visual workflow control and fast iteration.
- **AI-based qualification:** Ensures flexible evaluation instead of rigid rule-based filtering.
- **Parallel routing (Gmail + Slack):** Reduces latency and avoids sequential dependency issues.

---

## Benefits

- Eliminates manual lead screening
- Standardizes qualification logic
- Speeds up response time
- Ensures consistent communication
- Centralizes all lead data in Airtable
