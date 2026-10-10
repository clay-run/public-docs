---
title: Workflows
description: Build multi-step automation workflows in Clay using code nodes, AI agents, and integrations. Currently in open beta on all plans.
last_synced: 2026-08-06T00:00:00.000Z
---

# Workflows

Currently in open beta — available on all plans including free and trial.

Workflows let you build multi-step automations in Clay using a visual graph of connected nodes. Each node performs a discrete task: a code node runs Python logic, an AI agent node applies AI reasoning, and a tool node calls a Clay integration. Workflows run against a trigger (such as a new audience member or an incoming webhook) and pass data from node to node until the run completes.

Workflows are distinct from Clay tables — they are graph-based pipelines designed to process a single input through a sequence of steps, rather than enriching rows in bulk.

## Code nodes

A code node runs a Python function inside your workflow. You write a `handler` function that receives the node's declared inputs and returns a dict of outputs. Those outputs are available to downstream nodes.

```python
def handler(context):
    company = context["hubspot_company"]
    return {"name": company["name"], "domain": company.get("domain", "")}
```

### Declaring inputs

When you configure a code node, you declare each input with a name and a type. The type tells the node what kind of value to expect from the upstream step you wire it to. The supported types are:

| Type | Python type in handler | Example |
|------|----------------------|---------|
| String | `str` | `"Acme Corp"` |
| Number | `float` / `int` | `250` |
| Boolean | `bool` | `True` |
| Object | `dict` | `{"name": "Acme", "domain": "acme.com"}` |
| Array | `list` | `["tag1", "tag2"]` |

### Passing objects from other steps

When a previous step returns an object — such as the result of a HubSpot company lookup — declare the input type as **Object**. The value arrives in your handler as a native Python dict. You do not need to call `json.loads()`:

```python
def handler(context):
    # "hubspot_company" is declared as type Object in the node's input configuration
    company = context["hubspot_company"]   # already a dict, no parsing needed
    name = company["name"]
    website = company.get("website", "")
    return {"company_name": name, "website": website}
```

Accessing a field that does not exist raises a `KeyError`. Use `.get()` to supply a fallback when a field may be absent.

### Accessing inputs

Two ways to read an input inside the handler:

- `context["key"]` — direct access; raises `KeyError` if the key is missing.
- `context.get("key", default)` — returns `default` if the key is missing.

For nested fields inside an Object input, use standard Python dict access:

```python
company = context["hubspot_company"]
revenue = company.get("annualRevenue", 0)
```

### Return value

The handler must return a Python dict with string keys. The returned fields become the outputs available to downstream nodes in the workflow:

```python
def handler(context):
    return {"status": "qualified", "score": 85}
```

If the node has an output schema configured, Clay validates the returned dict against it. If a required output field is missing or has the wrong type, the step fails with a descriptive error.
