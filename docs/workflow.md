# Workflow Design

This document explains how the Embodied AI Efficiency Skill works from a product and business workflow perspective.

All examples are simplified and based on simulated data.

---

## 1. Workflow Goal

The goal of this workflow is to help interns or operation team members quickly turn scattered task information into structured daily outputs.

The skill is designed to support three main tasks:

1. Identify today's follow-up priorities
2. Generate a daily report summary
3. Highlight potential risks in data collection and delivery

---

## 2. Input Data

The workflow starts from task-level data.

Example input fields include:

| Field | Meaning |
|---|---|
| date | Date of the task record |
| task_id | Unique task identifier |
| project_phase | Current phase, such as collection, review, or packaging |
| scenario_type | Type of data collection scenario |
| collector_id | Anonymized collector identifier |
| supplier | Supplier or team group |
| expected_output | Expected daily output |
| submitted_output | Actual submitted output |
| valid_output | Output that passed basic validation |
| pass_rate | Quality pass rate |
| quality_status | Review result |
| packaging_status | Packaging progress |
| delivery_status | Delivery progress |
| risk_level | Risk level based on progress and quality |
| notes | Additional remarks |

---

## 3. Processing Logic

The skill can use simple rules to identify operational priorities.

### 3.1 Progress Check

If submitted output is lower than expected output, the task may need follow-up.

Example:

```text
submitted_output < expected_output
→ Progress risk
