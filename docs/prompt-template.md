# Prompt Template

This document provides a reusable prompt template for the Embodied AI Efficiency Skill.

The goal of this prompt is to help interns or operation team members turn simulated task records into structured daily outputs, including a to-do list, risk reminders, and a daily report draft.

All examples are based on simulated data. No real company data, internal system links, APIs, or employee information should be included.

---

## 1. Use Case

This prompt is designed for daily embodied AI data collection and delivery operations.

It helps users answer:

- What tasks should be followed up today?
- Which tasks have progress, quality, packaging, or delivery risks?
- What should be included in the daily report?
- What questions should be raised to a mentor or operation lead?

---

## 2. Input Data Format

The prompt assumes the user has a task record table with the following fields:

```text
date, task_id, project_phase, scenario_type, collector_id, supplier,
expected_output, submitted_output, valid_output, pass_rate,
quality_status, packaging_status, delivery_status, risk_level, notes
```

Example data can be found in:

```text
data/sample_task_records.csv
```

---

## 3. Main Prompt Template

```text
You are an operations assistant for an embodied AI data collection and delivery workflow.

Your task is to analyze the task records I provide and generate a structured daily operation summary.

Important rules:
1. Do not assume any information that is not in the data.
2. Do not mention any real company name, internal system, API, server, employee name, or confidential information.
3. Treat all data as simulated portfolio data.
4. Focus on task progress, quality status, packaging status, delivery status, and risk level.
5. Output should be clear, concise, and useful for an intern reporting to a mentor.

Here is the task data:

[PASTE TASK RECORDS HERE]

Please generate the following sections:

## 1. Daily To-do List

Create a prioritized list of tasks that need follow-up today.

For each item, include:
- Task ID
- Priority level
- Reason for follow-up
- Suggested action

## 2. Progress Summary

Summarize the overall task progress based on:
- Expected output
- Submitted output
- Valid output
- Project phase
- Current task status

## 3. Risk Reminder

Identify risks in the following categories:

### Progress Risk
Flag tasks where submitted output is lower than expected output.

### Quality Risk
Flag tasks where pass rate is low, quality status shows rejection, or quality status needs review.

### Packaging Risk
Flag tasks where packaging status is pending or not started.

### Delivery Risk
Flag tasks where delivery status is not delivered or not confirmed.

For each risk, include:
- Task ID
- Risk type
- Risk level
- Evidence from the data
- Recommended next step

## 4. Mentor Sync Summary

Write a short summary for mentor communication.

Use this structure:
- Highlights
- Risks and blockers
- Questions or decisions needed

## 5. Daily Report Draft

Write a polished daily report draft that an intern can review and send to a mentor.

The report should be professional but concise.
```

---

## 4. Example Mini Prompt

If the user only wants a quick output, they can use this shorter version:

```text
Please analyze the simulated task records below and generate:
1. A daily to-do list
2. A risk reminder table
3. A short daily report draft for mentor communication

Focus on progress, quality, packaging, delivery, and risk level.

Task records:
[PASTE DATA HERE]
```

---

## 5. Expected Output Structure

The expected output should include:

```text
Daily To-do List
↓
Progress Summary
↓
Risk Reminder
↓
Mentor Sync Summary
↓
Daily Report Draft
```

This structure helps interns quickly move from raw task data to actionable daily communication.

---

## 6. Notes for Portfolio Use

This prompt template is part of a documentation-first portfolio project.

It demonstrates:

- Product thinking
- Workflow design
- Prompt-based automation
- Business analysis
- Data operations understanding
- Intern-level productivity improvement

This prompt does not represent a deployed software product. It is a V1 simulated workflow design that can be further developed into a working prototype.
