---
title: Claygent builder
source_url: https://university.clay.com/docs/claygent-builder
description: Build smarter agents faster
last_synced: 2026-04-26T01:39:45.201Z
upstream_hash: 3320a6f6da8bdff880352c3504f7f7efd34906353925e5937e89b42462518db2
---

# Claygent builder

Build smarter agents faster

Claygent builder is a **workspace-level tool** that lets teams design, test, and version their Claygents—the AI research agents that power Clay’s data workflows.

With Claygent builder, teams can build smarter agents faster, preview their reasoning, and update them once for every table in their workspace.

For example, you could create:

-   **ICP qualification agent:** Analyzes a professional profile and scores whether someone is a fit for outreach.
-   **Cold email composition agent:** Gathers parameters (name, professional social media, website), runs web research, and drafts a tailored outreach email.
-   **Email timing agent:** Pulls Salesforce data (via MCP), scores account readiness based on activity, outputs a timing recommendation.

## Creating a new agent in Claygent builder

1.  From your Clay home, click `Claygents` → `+ Create Agent`.
2.  Select your AI model.
3.  In the editor, draft your prompt logic using variables.
4.  Experiment with your prompt with test cases, Click `+ Add Test Case`.
    -   These test cases are free and help verify your prompt works as expected.
5.  When satisfied, click `Save`.
    -   You can access `Version History` to compare and restore previous saved versions.

## FAQs

### **What customer problem does** Claygent builder **solve?**

Previously, prompts were locked to individual tables, forcing teams to duplicate agents across workflows, tweak each one manually, and pay for trial-and-error runs. The result was wasted effort, inconsistent results, and higher costs.

Claygent builder solves this by centralizing prompt management at the workspace level. Teams can design and refine agents once, then deploy them everywhere.

### **How is** Claygent builder **different from templates?**

Templates live inside individual tables, making them useful for one-off enrichments but siloed and not reusable across workspaces. Claygent, while reliable at scale, doesn’t give users direct tools for testing or version control.

Claygent builder combines the strengths of both. It’s reusable across a workspace, version-controlled, free to test, and ensures global consistency, without the drawbacks of templates or standalone Claygent.

### **Who can create or edit agents?**

Agent access follows your workspace permissions. Editors can create and modify agents, while viewers can reference approved agents in tables—always respecting the permissions set at the workspace level.

### **Does testing cost credits?**

No, test cases (first 5 rows) are free. Standard runs follow your normal billing.

### **Can I A/B test versions?**

Yes, try testing multiple versions via sample runs, compare outputs, and publish the best.

### **What happens mid-run if an agent updates?**

In-flight runs finish on the started version. New runs pick up the latest or pinned prompt depending on your setting.

### **Can I still edit prompts locally?**

Yes, but centralizing in Claygent builder avoids drift and ensures consistency.
