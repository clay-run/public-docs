# Clay public docs

Public, markdown-only mirror of selected [Clay University](https://university.clay.com/docs) documentation pages.

Each file in `docs/` has frontmatter linking back to its source page:

```yaml
---
title: <page title>
source_url: <university.clay.com URL>
---
```

Updates to these docs are managed by an agent that opens PRs against this repo in response to tickets, Slack mentions, and similar intake signals.
