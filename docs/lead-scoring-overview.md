---
title: Lead scoring overview
description: Generate custom scores based on the data points that matter.
last_synced: 2026-04-26T01:40:13.624Z
---

# Lead scoring overview

Generate custom scores based on the data points that matter.

## Lead scoring overview

Lead scoring is a method to prioritize leads based on various attributes like employee count, job titles, and online behavior to identify the leads most likely to convert to customers.

## Types of lead scoring

Customer/Account Fit Scoring

-   Evaluates prospect alignment with ICP, and is based on company size, industry, and technology stack.

Lead/Account Engagement Scoring

-   Tracks interactions like email responses, website visits, and event participation.

Lead Grade

-   Comprehensive evaluation combining fit and engagement metrics.

## Lead scoring prerequisites

Ensure you have the following to successfully lead score within Clay:

-   Data points for scoring
-   Lead scoring criteria
-   CRM fields for score syncing

## Setting up lead scoring with Score Row in Clay

**Score Row in Clay** is a built-in enrichment that scores each row based on up to 15 criteria you define — no formula required. Each criterion compares a column value against a set of keywords and assigns a numerical score. The enrichment outputs a total **Score** and a **Score Reasons** list explaining which criteria matched.

### **Step 1: Add the Score Row enrichment**

In your table, click **+ Enrichment**, search for **Score Row in Clay**, and add it.

### **Step 2: Set the number of criteria**

In the **# of Scoring Criteria** field, enter how many criteria you want to use (up to 15).

### **Step 3: Configure each criterion**

For each criterion, fill in four fields:

-   **Values to Score** — Map this to the column whose value you want to evaluate. If this field is empty or the column has no value for a row, that criterion contributes 0 to the score for that row.
-   **Comparison Type** — Choose how to compare the value:
    -   **Equals (Text, Number, Boolean)** — exact match
    -   **Contains (Text)** — substring match
    -   **Between (Number)** — checks whether the value falls within a numeric range
-   **Keywords** — The values or ranges to match against, comma-separated. For **Between (Number)**, each keyword must use the format `min - max` with the smaller number first (e.g., `5 - 10` or `100 - 500`). If the format does not match, or if the numbers are in reverse order (e.g., `10 - 5`), that keyword is skipped and contributes 0 to the score.
-   **Scores** — A comma-separated list of numeric point values, one per keyword. The number of keywords and scores must match exactly, or the enrichment will return an error.

### **Step 4: Review the output**

Each row receives a **Score** (the sum of all matching criteria) and a **Score Reasons** list that shows which criteria matched and how many points each contributed.

### Troubleshooting: why criteria don't contribute to the score

A criterion silently contributes 0 points when:

-   The **Values to Score** field is empty or not mapped to a column for that row.
-   The column value is not a number and the comparison type is **Between (Number)**.
-   The **Keywords** for a **Between (Number)** criterion are not in the correct `min - max` format, or have the numbers in reverse order — for example, `5–10` (em dash), `5 to 10`, a single number like `10`, or a reversed range like `10 - 5` (max before min) will all be skipped. Always put the smaller number first: `5 - 10`, not `10 - 5`.

## Setting up lead scoring with custom formulas

Follow these steps to create a lead scoring system using a formula column.

### **Step 1: Add a formula column**

Go to your table and create a new column.

Set the column type to **Formula**.

### **Step 2: Enter your custom formula**

Use the **Formula Generator** to create a formula that matches your scoring criteria.

-   **For Number-Based Scoring:** Use formulas to calculate a total score by adding points for attributes like company size, role, or revenue.
-   **For Grade-Based Scoring:** Use conditional rules to assign letter grades based on combinations of criteria.
-   **For Fit Criteria:** Use binary rules to label leads as "Yes" or "No" depending on whether they meet your defined requirements.

### **Step 3: Verify and save**

Review your lead scores within Clay and save the formula.

## Setting up lead scoring with Claygent

Claygent — Clay's built-in AI agent — evaluates ICP fit through judgment-based reasoning. Use it when your scoring criteria require contextual assessment that keywords or formulas can't capture: for example, evaluating whether a company's business model aligns with your ICP, or combining multiple data signals into a single score with a written rationale.

### **Step 1: Add a Claygent column**

In your table, click **+ Enrichment**, search for **Claygent**, and add it.

### **Step 2: Write your ICP evaluation prompt**

Describe your ICP and the output format you want. For example: *"Evaluate this company against our ICP: B2B SaaS, 50–500 employees, North America, uses Salesforce. Return a score from 0–100 and a one-sentence rationale."*

Enable **web search** if the agent needs to research the company live. Disable it when all required data is already in your table.

### **Step 3: Define output fields**

In the **Configure** tab, add named output fields — for example, a numeric `score` field and a text `rationale` field. Explicit fields make results more consistent and easier to filter or reference in downstream columns.

For templates, Sculptor-assisted agent building, and advanced configuration, see [Claygent builder](claygent-builder.md).
