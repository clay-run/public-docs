---
title: Comparison operators
source_url: https://university.clay.com/docs/comparison-operators
last_synced: 2026-04-26T01:39:47.140Z
upstream_hash: 466997404e1c5a1aa3631bdd24bb5bee4ec7c3ad0bf37de43e2938f25b31cfc7
---

# Comparison operators

Define workflow logic based on comparing numbers, text, or dates

## Comparison operators overview

A comparison operator evaluates the relationship between two values and returns a boolean value (`true` or `false`).

In Clay, these operators allow you to compare values to define conditions that can drive workflows and decision-making. For example, if a comparison operator evaluates to `true`, execute a specific action, and if `false`, take an alternative action.

The most common comparison operators are:

-   `==` (Equal to): Returns true if the values are equal.
-   `!=` (Not equal to): Returns true if the values are not equal.
-   `>` (Greater than): Returns true if the left value is greater than the right value.
-   `<` (Less than): Returns true if the left value is less than the right value.
-   `>=` (Greater than or equal to): Returns true if the left value is greater than or equal to the right value.
-   `<=` (Less than or equal to): Returns true if the left value is less than or equal to the right value.

## When do you use comparison operators?

Common applications of comparison operators in Clay workflows include:

### **Conditional Branching**

Use operators to create if/then logic in your workflows.

**Examples**

If `lead.score > 80`, mark as "Hot Lead".

If `email.domain contains "[gmail.com](<http://gmail.com>)"`, categorize as "Personal Email".

### **Data Validation**

Verify data meets specific criteria before processing.

**Examples**

Ensure `company.revenue >= 1000000` for enterprise leads.

Check if `[contact.name](<http://contact.name>) is not empty` before sending emails.

### **Data Filtering**

Use the **Filter** feature to refine your table view by applying specific rules to include or exclude records.

**Examples**

Filter where `date.created > "2024-01-01"`.

Exclude records where `status == "Inactive"`.

### **Lead Scoring**

Implement scoring rules based on multiple criteria.

**Examples**

If `employee_count >= 500 AND industry == "Technology"`, add 20 points.

If `last_activity_date <= "30 days ago"`, subtract 10 points.

## Numeric comparison operators

Numeric operators allow you to compare numerical fields (e.g., Lead Score, Revenue) to apply rules or filter data.**‍**

**Equal To (**`==`**)**‍

Filters records where the value matches exactly.

Example: Include rows where `Lead Score = 50`.**‍**

**Not Equal To (**`!=`**)**

Excludes records where the value matches exactly.

Example: Exclude leads with `Revenue == 0`.**‍**

**Greater Than (**`>`**)**

Includes records where the value is greater than specified.

Example: Show leads with `Employee Count > 500`.**‍**

**Greater or Equal To (**`>=`**)**

Includes records where the value is greater than or equal to specified.

Example: Include accounts with `Revenue >= 1,000,000`.**‍**

**Less Than (**`<`**)**

Includes records where the value is less than specified.

Example: Identify deals with `Probability < 50%`.**‍**

**Less or Equal To (**`<=`**)**

Includes records where the value is less than or equal to specified.

Example: Show tasks with `Priority <= 2`.**‍**

**Is Empty**

Filters records where the field is blank or missing.

Example: Find rows where `Lead Score is empty`.**‍**

**Is Not Empty**

Filters records where the field contains a value.

Example: Exclude rows where `Lead Score is missing`.

## String comparison operators

String operators compare text fields (e.g., Names, Email Domains, Industries) to match, include, or exclude records,**‍**

**Equal To (**`==`**)**

Checks if the text matches the specified value exactly.

**Example**: Filter leads where the `First name == "John"`.**`‍`**

**Not Equal To (**`!=`**)**

Excludes records where the text matches the specified value.

Example: Exclude companies where `Company Name != "Competitor Inc"`.**‍**

**Contains**

Filters records that include the specified substring.

Example: Find email domains where `Email contains "gmail" (e.g., john@gmail.com)`.

**Contains Any Of**

Checks if the text contains any value from a list.

Example: Filter industries where `Industry contains any of ["Tech", "Finance"]`.

**Does Not Contain**

Excludes records that contain the specified substring.

**Example:** Filter out email domains where `Email does not contain "gmail.com"`.

**Does Not Contain Any Of**

Excludes records that contain any values from a specified list.

**Example:** Filter out industries where `Industry does not contain any of ["Retail", "Healthcare"]`.

**Is Empty**

Identifies records where the field is blank.

Example: Find leads where `First Name is empty`.

**Is Not Empty**

Identifies records where the field contains any value.

Example: Include leads where `Email is not empty`.

## **Date comparison operators**

Date operators compare date fields (e.g., Created At, Last Updated) to filter or evaluate records based on specific timeframes.**‍**

**Equal To (`==`)**

Filters records with a date matching the specified value exactly.

Example**:** Find records where `Created At == "2023-01-01"`.

**Not Equal To (**!=**)**

Excludes records with a specific date.

Example: Exclude leads where `Created At != "2023-01-01"`.

**Greater Than (`>`)**

Filters records with dates after the specified value.

Example: Show leads where `Created At > "2023-01-01"`.

**Greater or Equal To (`>=`)**

Includes records created on or after the specified date.**‍**

Example: Find tasks where `Due Date >= "2023-01-01"`.

**Less Than (`<`)**

Filters records with dates before the specified value.

**Example:** Show leads where `Created At < "2023-01-01"`.

**Less or Equal To (`<=`)**

Includes records created on or before the specified date.

Example: Find leads where `Created At <= "2023-01-01"`.

**Is Empty**

Identifies records with no date value in the field.

Example: Find leads where `Created At is empty`.

**Is Not Empty**

Identifies records with a date value in the field.

Example: Include records where `Created At is empty`.

## Best Practices

-   Test edge cases thoroughly, including empty fields and boundary values
-   Include validation for missing or incorrect data
-   Provide clear error handling in formulas
