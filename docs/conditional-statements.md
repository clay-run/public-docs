---
title: Conditional statements
source_url: https://university.clay.com/docs/conditional-statements
last_synced: 2026-04-26T01:39:47.787Z
upstream_hash: 1b73b1cb0146f5fd07eb60ff39516302e717c60a6842f19a1ab933b116c9b7be
---

# Conditional statements

Control the logic of your workflow

## Conditional statements overview

Conditional statements in Clay help you control the flow of logic of your workflow, allowing you to perform different actions based on conditions. For example, if `Company Size > 100`, the output will be `true`.

In Clay, you can use conditional statements in:

-   **Conditional runs:** Run a certain enrichment based on certain criteria.
-   **AI formulas**: Transform data, like scoring leads or qualifying opportunities.
-   **Conditional Snippets**: Embed conditional logic to send outbound messages based on contact criteria.
-   **Waterfalls**: Maximizing coverage with multiple providers.

## Conditional statement structure

Conditional statements have the following structure:

1.  **IF (Condition)** – Executes a command when the condition is true.
2.  **ELSE IF (secondCondition)** – Executes a command if the second condition is true (optional).
3.  **ELSE** – Executes a command when none of the above conditions are true.

### Walkthrough

`IF Condition`

**(command to execute if condition is true)**

`ELSE IF secondCondition`

**(command to execute if secondCondition is true)**

`ELSE`

**(command to execute if no conditions are true)**

## Best practices

### **Testing**

Prevent unexpected errors with edge cases or missing data.

**Examples**

-   **Empty fields**: `IF({{company_size}} > 100) THEN "Qualified" ELSE "Not Qualified"` , Ensure blank company\_size defaults to "Not Qualified".
-   **Boundary values**: Test company\_size = 50 in `IF({{company_size}} >= 50) THEN "Medium" ELSE "Small"` to avoid misclassification.
-   **Unexpected formats**: Handle `company_size = "unknown"` by defaulting to "Not Qualified".

### **Error handling**

Handle missing or invalid data properly.

**Examples**:

-   **Missing fields**: In `IF({{company_size}} AND {{location}}) THEN "Valid" ELSE "Invalid"`, return "Invalid" if fields are missing.
-   **Clear errors**: Use `IF({{email}} == "") THEN "Error: Missing Email" ELSE "Valid Email"` to flag missing inputs.

### **Parentheses for clarity**

Use parentheses to group conditions clearly, especially when combining multiple logical operators (AND, OR, NOT).

**Examples**:

-   **Unclear**: `{{size}} > 100 AND {{location}} == "US" OR {{revenue}} > 1M` could qualify the wrong leads.
-   **Clear**: `(size > 100 AND location == "US") OR revenue > 1M` ensures correct grouping.

**Use cases:** Lead qualification, CRM updates, or email campaigns where errors could disqualify valid leads or waste resources.

## Example conditional statements within Clay

### Example #1: Basic email validation

Validate email formats to flag personal email addresses.

#### Formula

IF (person.email contains @gmail.com OR @yahoo.com)return "Invalid email format"

ELSEreturn "Valid email format"

#### **Test cases**

-   **Input:** [john.doe@gmail.com](mailto:john.doe@gmail.com)**Result:** Invalid email format
-   **Input:** [john.doe@yahoo.com](mailto:john.doe@yahoo.com)**Result:** Invalid email format
-   **Input:** [john.doe@company.com](mailto:john.doe@company.com)**Result:** Valid email format

### Example #2: Message snippets based on company size

Serve different message snippets based on the company’s size.

#### Formula

IF (company.size > 500)

return enterprise\_message\_snippet

ELSE IF (company.size > 50)

return midmarket\_message\_snippet

ELSE

return small\_message\_snippet

#### **Test cases**

-   **Input:** company.size = 750**Result:** enterprise\_message\_snippet
-   **Input:** company.size = 100**Result:** midmarket\_message\_snippet
-   **Input:** company.size = 25**Result:** small\_message\_snippet
-   **Input:** company.size = 0**Result:** small\_message\_snippetNote: Since this input doesn't satisfy any of the conditions, the final else statement is returned, but we should add some input validation here.

### **Example #3: Regional discounts based on geography**

Apply different discount rates based on the region.

#### **Formula**

IF (region == "US")

return "10% Discount"

ELSE IF (region == "EMEA")

return "15% Discount"

ELSE

return "No Discount Available”

#### Test cases

-   **Input:** region = "US"**Result:** 10% Discount
-   **Input:** region = "EMEA"**Result:** 15% Discount
-   **Input:** region = "APAC"**Result:** No Discount Available
