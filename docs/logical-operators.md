---
title: Logical operators
source_url: https://university.clay.com/docs/logical-operators
description: Automate decisions with AND, OR, and NOT expressions
last_synced: 2026-04-26T01:40:17.209Z
upstream_hash: 617ae8ae042101df1335fb0c26bdaf7d8611459f22be23261aa39f6fab0303fa
---

# Logical operators

Automate decisions with AND, OR, and NOT expressions

## Logical operators overview

A logical operator evaluates one or more conditions and returns a boolean value (`true` or `false`). In Clay, these operators let you combine and modify conditions to build complex logical expressions.

The three main types of logical operators are:

-   `AND` (`&&`): Returns true only if all conditions are true
-   `OR` (`||`): Returns true if at least one condition is true
-   `NOT` (`!`): Reverses a boolean value

## When do you use logical operators?

Logical operators are commonly used in several contexts within Clay.

**AI Formula Columns:** Create complex conditions for data transformation with multiple criteria.

**Conditional Runs:** Control when enrichments should execute by definingspecific trigger conditions.

**SOQL Queries:** Filter Salesforce objects based on multiple criteria.

## Best practices

When using logical operators, follow these guidelines:

-   Use parentheses to clearly group conditions and control evaluation order
-   Test edge cases to ensure correct behavior

## **`AND` statements**

### **Syntax**

`condition1 AND condition2`

### **Overview**

-   Returns true if **both conditions** are true.
-   Returns false if either condition is false.
-   In formulas, represented as `&&` .

### **Example cases**

**Example 1:** `true AND true` → `true`

**Example 2:** `true AND false` → `false`

**Example 3:** `false AND false` → `false`

### **Use case example**

**Scenario**: _You want to qualify a lead if they have more than 500 employees_ **_and_** _are located in the US._

**Formula:** `{{employee_count}} > 500 && {{location}} == "US"`

**Logic:** Returns true if the lead has more than 500 employees **and** is in the US.

## **`OR` statements**

### **Syntax**

`condition1 OR condition2`

### **Overview**

Returns true if **at least one condition** is true.

Returns false only if **both conditions** are false.

In formulas, represented as `||` .

### **Example cases**

**Example 1:** `true OR true` → `true`

**Example 2:** `true OR false` → `true`

**Example 3:** `false OR false` → `false`

### **Use case example**

**Scenario**: _You want to qualify a lead if they have more than 500 employees_ **_or_** _are located in the US._

**Formula:** `{{employee_count}} > 500 || {{location}} == "US"`

**Logic:** Returns true if the lead meets **either** condition.

## **`NOT` Statements**

### **Syntax**

`NOT condition1`

### **Overview**

Returns the **opposite** of the condition:

-   true becomes false.
-   false becomes true.

Often used to **exclude specific conditions**.

In formulas, represented as `!` .

### **Example cases**

**Example 1:** `NOT true` → `false`

**Example 2:** `NOT false` → `true`

### **Use Case Example**

**Scenario**: _You want to exclude leads marked as competitors from being qualified._

**Formula:** `!{{competitor}}`

**Logic:** Returns true if the lead is **not** a competitor.

## **Combining `AND`, `OR`, and `NOT`**

### **Syntax**

(condition1 AND condition2) OR NOT condition3

### **Use case example**

**Scenario**: You want to qualify a lead if either of the following is true:

1.  The lead has more than 500 employees **and** is based in the US.
2.  The lead is **not** a competitor.\*

**Formula:** `({{employee_count}} > 500 AND {{location}} == "US") OR !{{competitor}}`

**Logic Breakdown:**

-   **Part 1**: {{employee\_count}} > 500 && {{location}} == "US" → Returns true if the lead has more than 500 employees **and** is located in the US.
-   **Part 2**: !{{competitor}} → Returns true if the lead is **not** marked as a competitor.
-   The entire formula returns true if **either** part is true.
