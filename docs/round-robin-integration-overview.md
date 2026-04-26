---
title: Round-robin integration overview
source_url: https://university.clay.com/docs/round-robin-integration-overview
last_synced: 2026-04-26T01:40:33.683Z
upstream_hash: b7e8b7318fd7170b858c73cdd925b709273839287886cff056377a334511cb3d
---

# Round-robin integration overview

Route your leads in a round robin manner

## What is the round-robin feature?

The round-robin feature in Clay ensures leads are distributed fairly and evenly among your team members by assigning them in a rotating order. It eliminates the need for manual lead assignment, making your team’s workflow more efficient and ensuring balanced workloads.

There are two main types of round-robin distribution in Clay:

1.  **Standard round-robin:** Distribute leads evenly in a fixed order.
2.  **Weighted round-robin:** Allocate leads based on predefined weights, helping you route leads.

### Use cases

There are a few use cases where you can use round-robin routing.**‍**

**Use case #1: Lead assignment for sales teams:** Distribute inbound leads evenly or weighted among SDRs.

-   Example: Ensure workload balance across the team.

**Use case #2: Dynamic team assignments:** Adjust for changing team compositions or workloads.

-   Example: Account for “Out of Office” reps or ramp-up periods.

**Use case #3: Territory-based routing:** Assign leads based on regions or account sizes.

-   Example: Creating rotations for SMB vs. enterprise clients.

## Getting set up

### Key concepts

**Distribution**

In Clay, this can be done using **Standard Round Robin**, which assigns leads evenly in a fixed, repeating order, or **Weighted Round Robin**, which assigns leads based on predefined weights.

**Distribution weights**

Weights are numerical values used in **Weighted Round Robin** to determine how many leads each team member receives. Higher weights result in more leads being assigned to that member.

This allows you to adjust assignments based on factors like capacity, experience, or availability.

**Dynamic lists**

Dynamic lists handle changes in team composition or data. This includes accounting for new team members, removing inactive reps, or adapting to live data updates from sources like Salesforce.

Dynamic lists ensure lead distribution according to rules even as the input data evolves.

### Setup checklist

To setup round robin, you’ll need the following.

**Data Table**

Your data table should include all relevant information about your team members and leads. At a minimum, it should contain:

-   **Team Member Names:** The names of the individuals who will receive leads. For th
-   **Optional Columns:**
    -   **Weights:** Numerical values to prioritize certain team members (used for Weighted Round Robin).
    -   **Status:** A column indicating whether team members are active or unavailable, which is helpful for managing dynamic lists.

**Views for Filtering (Optional)**

If your data requires segmentation or filtering, create views to narrow down the list. For example:

-   Include only active team members.
-   Filter leads by specific criteria, such as region or account size.

**Choosing the Enrichment**

Select the type of Round Robin enrichment that suits your needs:

-   **Standard Round Robin:** For evenly distributing leads in a fixed order.
-   **Weighted Round Robin:** For assigning leads based on predefined weights.

**Integration with Data Sources (Optional)**

If you’re working with live data, such as from Salesforce or another CRM, ensure that it is integrated with Clay to keep your assignments up-to-date.

## How can I distribute leads?

Clay provides two primary options for distributing leads: **Standard Round Robin** and **Weighted Round Robin.** Below are step-by-step guides to help you configure each.

### Standard round-robin

**Step 1: Open the enrichment**

From the enrichment search bar, navigate to the **Distribute Leads Round Robin** enrichment.

**Step 2: Add Assignment Labels**

Input the names or identifiers of your team members (e.g., Bob, Alice, Charlie) as assignment labels.

**Step 3: Add Vales Associated with Labels**

Optionally along with assignment labels, you can add associated values, like Salesforce IDs, for reference.

**Step 4: Run the Enrichment**

Execute the enrichment, which outputs:

-   **Label:** The assigned team member.
-   **Value:** Any associated identifier (e.g., Salesforce ID).
-   **Raw Counter:** The position of the label in the rotation.

### Weighted round-robin

**Step 1: Open the enrichment**

From the enrichment search bar, navigate to the **Distribute Leads Weighted Round Robin** enrichment.

**Step 2: Select the reps table**

Choose the data table containing your representatives. This table should include information such as:

-   **Rep Names**: Names or identifiers of your team members.
-   **Weights**: Numeric values to control the proportion of leads each rep receives.
-   **Active Status (Optional)**: A column indicating whether a rep is active or unavailable.

**Step 3: Configure the enrichment**

Set up the fields in the configuration panel:

1.  **Active Reps View**: Select a filtered view of your table to include only active team members.
2.  **Rep Names Column**: Map the column containing the names of your team members.
3.  **Values Column (Optional)**: Optionally, map a column for identifiers like Salesforce IDs for future reference.
4.  **Weights Column**: Map the column containing numeric weights for lead distribution.

**Step 4: Save and run the enrichment**

Save your configuration and run the enrichment.

**Step 5: Adjust and refine**

Make adjustments to weights or filters as needed to reflect changes in team dynamics. You can also create advanced routing configurations by adding conditions (e.g., assigning leads based on company size or region).
