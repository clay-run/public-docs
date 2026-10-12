---
title: Workflow code nodes
description: How to define input schemas and work with object and array inputs in Clay Workflows code nodes — currently in beta.
last_synced: 2026-08-06T00:00:00.000Z
---

# Workflow code nodes

> **This feature is currently in beta.** Code nodes are being rolled out progressively. If you do not see a code node option when building a workflow, your workspace may not have access yet. Contact support to request beta access.

A code node lets you run Python inside a Clay workflow step. You define a handler function that receives inputs from upstream nodes, executes custom logic, and returns outputs to downstream nodes.

```python
def handler(context):
    company = context.get_input("company")
    domain = company.get("domain", "")
    return {"domain": domain}
```

## Defining an input schema

Each code node has an **input schema** that declares the inputs your handler expects. For each input you set:

- **Name** — the key your code uses to retrieve the value (`context.get_input("name")`)
- **Type** — one of `string`, `number`, `boolean`, `object`, or `array`
- **Required** — whether the node fails if the input is missing

The type declaration controls how Clay handles the value at runtime.

## How input types affect your code

### object and array inputs

When you declare an input as type `object` or `array`, the value from the upstream node passes through to your Python handler as a native Python dict or list. No parsing is required.

```python
def handler(context):
    # Input schema: hubspot_company declared as type "object"
    company = context.get_input("hubspot_company")
    # company is a Python dict — access fields directly
    name = company.get("name", "")
    return {"company_name": name}
```

This is the recommended approach when an upstream enrichment (such as a HubSpot company lookup or similar) returns a structured object.

### string inputs wired to an object or array

If you declare an input as type `string` but the upstream node provides an object or array, Clay automatically serializes the value to a JSON string before passing it to your handler. Your code receives a string, and you must call `json.loads()` to work with it as a dict or list.

```python
import json

def handler(context):
    # Input schema: hubspot_company declared as type "string"
    # Clay auto-serialized the upstream object to a JSON string
    raw = context.get_input("hubspot_company")
    company = json.loads(raw)
    name = company.get("name", "")
    return {"company_name": name}
```

This works, but declaring the input as type `object` (above) is cleaner and avoids the extra `json.loads()` call.

## FAQ

### Can I use type "object" for a runtime value whose shape I don't know at build time?

Yes. The `object` type in the input schema means "pass this through as a Python dict." Clay does not validate the shape of the object — it accepts any dict from the upstream node.

### Why did I get a JSON string when I expected a dict?

This happens when the input schema declares type `string` for an input that is actually an object or array at runtime. Clay serializes the value to a JSON string automatically. To receive the value as a native dict instead, change the input type to `object` in the input schema editor.

### The code editor won't save — what should I check?

Common causes:

- **Syntax error in Python** — The editor runs a syntax check before saving. Check the error message in the editor's output panel for a line number and description.
- **Input schema conflict** — If an input name in your schema conflicts with a reserved name or is empty, the save will fail. Use distinct, non-empty names for all inputs.
