# Product Requirements Document

**Project:** Embodied AI Efficiency Skill
**Type:** Documentation-First Portfolio Project
**Version:** 1.0 — Documentation & Simulated Workflow Stage
**Last Updated:** May 2026
**Status:** In Progress

> **Portfolio Note:** This is a V1 documentation and simulated workflow project. It is not a deployed application. The goal is to design and document a structured prompt-based workflow that could realistically address operational inefficiencies observed in embodied AI data collection work. All data is simulated. No real company data, internal systems, APIs, or employee information are referenced anywhere in this repository.

---

## Table of Contents

1. [Product Name & Overview](#1-product-name--overview)
2. [Product Positioning](#2-product-positioning)
3. [Target Users](#3-target-users)
4. [User Pain Points](#4-user-pain-points)
5. [User Needs](#5-user-needs)
6. [Core Features](#6-core-features)
7. [Input and Output](#7-input-and-output)
8. [User Flow](#8-user-flow)
9. [Success Metrics](#9-success-metrics)
10. [Business Value](#10-business-value)
11. [Scope](#11-scope)
12. [Out of Scope](#12-out-of-scope)
13. [Future Improvements](#13-future-improvements)

---

## 1. Product Name & Overview

**Product Name:** Embodied AI Efficiency Skill

**One-line Summary:**
A prompt-driven workflow assistant that helps data operations interns in embodied AI projects generate daily to-do lists, write structured daily reports, and surface task, quality, and delivery risks — using a standardized task record as input.

**Current Stage:**
This project is at the **V1 documentation and simulated workflow stage**. The deliverables are a workflow design, a sample dataset, and example outputs. A prompt template may be added in a future version. The intent is to demonstrate product thinking and operational analysis skills applicable to PM, business analysis, and data operations roles.

---

## 2. Product Positioning

Embodied AI data collection involves coordinating multiple stages simultaneously: scenario execution, output submission, quality review, packaging, and delivery. For new interns, the challenge is not that any individual task is difficult — it is that **knowing what to look at, what to prioritize, and how to communicate status clearly** takes time and experience to develop.

This skill is designed as a structured prompt workflow that transforms a daily task record export into actionable outputs: a to-do list, a report draft, and a set of risk flags.

**Positioning Statement:**
> For data operations interns in embodied AI projects who struggle with daily task prioritization and reporting, the Embodied AI Efficiency Skill is a prompt-based workflow that converts structured task records into daily to-do lists, report drafts, and risk flags — so interns can spend less time organizing information and more time acting on it.

---

## 3. Target Users

**Primary User: Data Operations Intern**

| Attribute | Description |
|-----------|-------------|
| Role | Intern coordinating data collection tasks, tracking output quality, and following up on packaging and delivery |
| Experience Level | Entry-level; 0–3 months in the role |
| Technical Background | Non-technical to semi-technical; comfortable with spreadsheets |
| Daily Workflow | Reviews task records, tracks output and quality status, flags issues, writes daily reports, syncs with mentors |
| Key Challenge | Difficulty prioritizing tasks; reporting is slow and inconsistent; risks are often identified too late |

**Secondary User: Mentor / Team Lead**

| Attribute | Description |
|-----------|-------------|
| Role | Supervises multiple interns; reviews daily reports; makes task adjustment decisions |
| Pain Point | Receives reports in inconsistent formats; must ask follow-up questions to understand task status |
| Benefit from This Skill | Receives standardized, structured reports that reduce back-and-forth |

---

## 4. User Pain Points

**P1 — Difficulty Prioritizing Daily Tasks**
When facing multiple task records across different stages and risk levels, interns without domain experience often struggle to determine where to start. The `risk_level` and multi-status fields in the task record contain relevant signals, but they require synthesis to be actionable.

**P2 — Daily Reporting Is Time-Consuming and Inconsistent**
Writing a daily report from scratch requires manually reviewing each record, summarizing progress, and identifying issues. Without a template or workflow, different interns produce reports of varying depth and format, which creates overhead for mentors.

**P3 — Risk Identification Is Reactive**
Without a systematic review process, interns tend to notice problems only after they escalate. Signals like a low `pass_rate`, a stalled `packaging_status`, or a high `risk_level` flag are present in the data but not always acted on proactively.

**P4 — Communication with Mentors Is Unstructured**
Without a standard sync format, interns spend meeting time explaining context rather than discussing decisions. Mentors often need to ask "what's the current status of X?" before any action can be taken.

---

## 5. User Needs

| User Need | Priority | Description |
|-----------|----------|-------------|
| Know what to work on today | High | A prioritized action list derived from current task statuses and risk levels |
| Write a daily report quickly | High | A structured report draft generated from the task record, ready to review and send |
| Spot task progress risks early | High | Flags for tasks where output submission or quality review appears stalled |
| Spot quality risks early | High | Flags for low pass rates or quality statuses that indicate potential rework |
| Spot packaging and delivery risks | High | Flags for tasks stuck in packaging or not yet confirmed as delivered |
| Verify data is analysis-ready | Medium | A field completeness check before attempting efficiency or output analysis |
| Communicate clearly with mentors | Medium | A concise sync summary that replaces unstructured verbal status updates |

---

## 6. Core Features

### Feature 1 — Daily To-Do Generator

Reads current task records and produces a prioritized action list for the day. Items are ordered by `risk_level` and status signals, such as quality issues pending, packaging not started, or delivery unconfirmed.

**Output:** Numbered action list with task ID, recommended action, and the signal driving its priority.

---

### Feature 2 — Daily Report Drafting

Generates a structured daily report covering:

- Overall progress summary across all active tasks
- Key completions or milestones
- Issues and blockers identified
- Plan for the following day

The draft is intended to require only light review and editing before sharing with a mentor.

**Output:** Markdown report with section headers, suitable for sharing in a team channel or via message.

---

### Feature 3 — Task Progress Risk Flag

Scans task records for signals that suggest a task may fall behind, including:

- Tasks where `submitted_output` is significantly below `expected_output`
- Tasks where `valid_output` is low relative to `submitted_output`
- Tasks with `risk_level` marked as High

**Output:** Risk table with task ID, risk type, relevant field values, and suggested follow-up action.

---

### Feature 4 — Quality Risk Flag

Identifies quality-related signals that may affect downstream packaging and delivery, including:

- Tasks where `pass_rate` falls below a defined review threshold
- Tasks where `quality_status` indicates rejection or pending re-review

**Output:** Risk table with task ID, `pass_rate`, `quality_status`, and recommended action, such as flagging for re-collection or escalating for review.

---

### Feature 5 — Packaging / Delivery Risk Flag

Surfaces logistics-related risks, including:

- Tasks where `packaging_status` has not advanced despite `quality_status` being passed
- Tasks where `delivery_status` remains unconfirmed

**Output:** Risk table with task ID, current `packaging_status`, `delivery_status`, and recommended next step.

---

### Feature 6 — Data Field Completeness Check

Validates whether the task record contains all fields needed to run the above features and to support efficiency analysis.

**Required fields and their purpose:**

| Field | Used For |
|-------|----------|
| `date` | Tracking record recency and daily snapshot identification |
| `task_id` | Unique task identification across all features |
| `project_phase` | Grouping tasks by workflow stage |
| `scenario_type` | Categorizing task type for output comparison |
| `collector_id` | Per-collector output tracking |
| `supplier` | Supplier-level aggregation and risk review |
| `expected_output` | Baseline for progress and output gap analysis |
| `submitted_output` | Actual submission volume for progress tracking |
| `valid_output` | Quality-adjusted output volume |
| `pass_rate` | Quality risk flagging |
| `quality_status` | Quality review state, such as Passed, Need review, or Rejected |
| `packaging_status` | Packaging pipeline state |
| `delivery_status` | Final delivery confirmation state |
| `risk_level` | Pre-assessed risk flag for prioritization |
| `notes` | Contextual information for edge cases and manual flags |

**Output:** Pass/Fail checklist noting any missing or ambiguously populated fields, with a recommendation on whether the dataset is ready for analysis.

---

### Feature 7 — Mentor Sync Summary

Condenses the day's outputs into a brief, mentor-ready summary designed to make check-ins more focused. It replaces unstructured verbal updates with a written brief that enables faster, higher-quality conversations.

**Output:** A three-section brief — Highlights, Risks & Blockers, and Questions or Decisions Needed.

---

## 7. Input and Output

### Input

| Input | Format | Description |
|-------|--------|-------------|
| Task records | CSV (`data/sample_task_records.csv`) | One row per task; covers output volume, quality, packaging, and delivery status |
| Current date | Text | Provided manually; used to interpret record recency |
| Review thresholds | Inline in prompt | For example, the pass rate below which a task is flagged for quality review |

**Fields in `data/sample_task_records.csv`:**

```text
date, task_id, project_phase, scenario_type, collector_id, supplier,
expected_output, submitted_output, valid_output, pass_rate,
quality_status, packaging_status, delivery_status, risk_level, notes
```

All values in this file are **simulated**. They are designed to be structurally realistic for an embodied AI data collection context without referencing any real project, company, or individual.

### Output

| Output | Format | Typical Use |
|--------|--------|-------------|
| Daily to-do list | Markdown / plain text | Reviewed at the start of the workday |
| Daily report draft | Markdown | Lightly edited and sent to mentor at end of day |
| Risk flag tables | Markdown table | Included in report or raised in a separate message |
| Field completeness check | Checklist | Run before starting analysis to verify data quality |
| Mentor sync summary | Markdown brief | Used in 1:1 meeting or async check-in |

See `examples/daily_report_demo.md` for a complete example output.

---

## 8. User Flow

```text
┌──────────────────────────────────────────────┐
│              START OF WORK DAY               │
└─────────────────────┬────────────────────────┘
                      │
                      ▼
        ┌─────────────────────────┐
        │  Export daily task      │
        │  records as CSV         │
        └────────────┬────────────┘
                     │
                     ▼
        ┌─────────────────────────┐
        │  Run Field Completeness │
        │  Check  (Feature 6)     │
        └────────────┬────────────┘
                     │
          ┌──────────┴──────────┐
          │ All fields present? │
          ├─ NO ──► Resolve     │
          │         gaps first  │
          └─ YES ───────────────┘
                     │
                     ▼
        ┌─────────────────────────┐
        │  Generate Daily To-Do   │
        │  List  (Feature 1)      │
        └────────────┬────────────┘
                     │
                     ▼
        ┌─────────────────────────┐
        │  Run Risk Flags         │
        │  Features 3 / 4 / 5     │
        └────────────┬────────────┘
                     │
                     ▼
        ┌─────────────────────────┐
        │  Work through tasks;    │
        │  address flagged risks  │
        └────────────┬────────────┘
                     │
                     ▼
             END OF WORK DAY
                     │
                     ▼
        ┌─────────────────────────┐
        │  Generate Daily Report  │
        │  Draft  (Feature 2)     │
        └────────────┬────────────┘
                     │
                     ▼
        ┌─────────────────────────┐
        │  Generate Mentor Sync   │
        │  Summary  (Feature 7)   │
        └────────────┬────────────┘
                     │
                     ▼
        ┌─────────────────────────┐
        │  Review, edit lightly,  │
        │  send to mentor         │
        └─────────────────────────┘
```

---

## 9. Success Metrics

Because this is a V1 documentation and simulated workflow project, the metrics below are **intended evaluation criteria** rather than measured results. They define what success would look like if this workflow were adopted and tested in a real operational setting.

### Potential Efficiency Indicators

| What to Measure | Evaluation Approach |
|-----------------|---------------------|
| Time spent writing daily reports | Compare self-reported time before and after adopting the workflow template |
| Time spent identifying daily priorities | Observe how long it takes an intern to produce a to-do list with vs. without the structured prompt |
| Lag between a risk emerging and being flagged | Review historical records to assess whether the flag logic would have surfaced issues earlier than they were manually reported |

### Potential Quality Indicators

| What to Measure | Evaluation Approach |
|-----------------|---------------------|
| Report format consistency across interns | Assess whether reports produced using the template are more structurally consistent than freeform reports |
| Coverage of risk flags | Test the prompt against a set of labeled sample records and check whether known risks are surfaced |
| Mentor comprehension | Gather qualitative feedback on whether the sync summary reduces the need for follow-up questions in check-ins |

### Portfolio-Level Indicators

- Workflow is fully documented end-to-end in `docs/workflow.md`
- At least one complete example output is available in `examples/daily_report_demo.md`
- Sample dataset passes the field completeness check defined in Feature 6
- PRD and README clearly communicate the project's purpose and value to a non-technical reviewer

---

## 10. Business Value

### For the Intern

- **Faster onboarding:** A new intern can follow the workflow from their first week without needing to have already developed operational intuition.
- **Reduced cognitive load:** The to-do generator and risk flags reduce the amount of manual synthesis required each morning.
- **Stronger communication habits:** Structured report templates encourage interns to consistently document progress, blockers, and plans — skills that transfer directly to PM and business analysis roles.

### For the Team

- **More consistent reporting:** A standardized output format reduces the mentor's effort to interpret and follow up on intern reports.
- **Earlier risk visibility:** Risk flags are derived from the same data that interns already collect, but applied systematically rather than ad hoc.
- **Low overhead to adopt:** The workflow requires no new tools — only a structured prompt and an existing task record export.

### Broader Relevance

This workflow addresses a recurring challenge in data operations: **raw records exist, but the translation from data to action is inconsistent and slow.** The same design logic applies in other operational contexts — vendor management, content operations, QA pipelines — where structured data is already being collected but daily synthesis is done manually and inconsistently.

---

## 11. Scope

The following are within scope for this V1 portfolio project:

- Workflow design and documentation for all 7 features listed above
- A simulated task record dataset (`data/sample_task_records.csv`) using the 15 fields defined in this PRD
- A complete example output demonstrating the daily report and risk flags (`examples/daily_report_demo.md`)
- End-to-end workflow documentation (`docs/workflow.md`)
- This PRD (`docs/product-requirements.md`)
- All features operate on a static CSV export; no live data connection is required or implied

---

## 12. Out of Scope

| Item | Reason |
|------|--------|
| Real company task records or operational data | Confidentiality; inappropriate for a public portfolio |
| Internal system links, dashboards, or APIs | Cannot be shared externally |
| Real collector or employee names | Privacy |
| Deployed code, scripts, or automation pipelines | Beyond the scope of a documentation-first V1 |
| Web or mobile UI | Not the focus; the prompt workflow is the core deliverable |
| Live or real-time data integration | V1 operates on static daily exports only |
| Multi-team or cross-project coordination | V1 is scoped to a single intern's daily workflow |

---

## 13. Future Improvements

### Near-Term (V1.1)

- **Configurable thresholds:** Allow users to set their own pass rate floor and output gap threshold in a simple config file, rather than defining them inline in each prompt.
- **Collector-level summary:** Add a per-collector output breakdown using `collector_id` to help identify workload concentration or output gaps within a task batch.
- **Supplier-level view:** Aggregate `pass_rate` and `quality_status` by `supplier` to surface vendor-level quality trends across tasks.

### Medium-Term (V2.0)

- **Multi-day trend analysis:** Compare records across multiple `date` values to detect patterns — for example, a `pass_rate` that has declined over several days, or a `packaging_status` that consistently stalls at the same stage.
- **Weekly digest format:** A weekly variant of the report summarizing progress, risk resolution, and delivery outcomes across the full work week.
- **Prompt evaluation framework:** A lightweight method for testing prompt outputs against labeled sample scenarios to assess the reliability and coverage of risk flags.

### Long-Term / Exploratory

- **Pipeline bottleneck analysis:** Use multi-day data to identify which stage — collection, quality review, packaging, or delivery — most frequently causes delays, and explore root causes using available fields like `scenario_type`, `supplier`, and `project_phase`.
- **Scenario-type benchmarking:** Compare `pass_rate` and output gap across `scenario_type` values to identify which task categories are systematically harder to execute at quality.
- **Workload distribution suggestions:** Based on `collector_id` output patterns, surface observations about how tasks might be redistributed to improve delivery consistency.

---

## Appendix: Glossary

| Term | Definition |
|------|------------|
| Task record | A single row in the task data export, representing one data collection task and its current status |
| Collector | An individual responsible for executing data collection according to task specifications |
| Supplier | The organization or team providing collector resources for a given task |
| Expected output | The target number of data units to be collected for a task |
| Submitted output | The actual number of data units submitted by the collector |
| Valid output | The number of submitted units that passed quality review |
| Pass rate | `valid_output / submitted_output`; the proportion of submissions that meet quality standards |
| Quality status | The current state of the QC review process, such as Passed, Need review, or Rejected |
| Packaging status | The current state of the data packaging process prior to delivery |
| Delivery status | Whether the packaged data has been confirmed as delivered to the downstream recipient |
| Risk level | A pre-assessed flag indicating the overall risk level of a task, such as Low, Medium, or High |

---

*This document is part of a portfolio project created to demonstrate product management and business analysis skills. All data is simulated. No proprietary or confidential information is included.*
