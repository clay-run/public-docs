---
title: Keyboard shortcuts
description: Work faster in Clay with keyboard shortcuts.
last_synced: 2026-04-27T18:10:15.366Z
---

# Keyboard shortcuts

Work faster in Clay with keyboard shortcuts.

## Navigation shortcuts

### Jump to locations

-   `Cmd/Ctrl` + `↑` — Jump to the top of the table
-   `Cmd/Ctrl` + `↓` — Jump to the bottom of the table
-   `Cmd/Ctrl` + `→` — Jump to the end (rightmost column) of the table
-   `Cmd/Ctrl` + `←` — Jump to the start (leftmost column) of the table
-   `Arrow keys` — Navigate between cells (viewport scrolls automatically)

### Search and access

-   `Cmd/Ctrl` + `F` — Open table search
-   `Cmd/Ctrl` + `K` (or `Cmd/Ctrl` + `P`) — Open search to jump between tables in your workbook
-   `Cmd/Ctrl` + `E` — Open the enrichment panel
-   `Cmd/Ctrl` + `I` — Toggle the Sculptor AI chat panel
-   `Cmd/Ctrl` + `G` — Jump to a specific row number

### Quick actions

-   `Spacebar` — Preview the selected row in detail view
-   `Esc` — Close cell details panel or single-page record view
-   `Double-click` on an enrichment or formula column header — Edit column configuration
-   `Single delayed click` on a column name — Rename the column

## Selection shortcuts

### Basic selection

-   `Cmd/Ctrl` + `A` — Select all cells in the table
-   `Cmd/Ctrl` + `click` — Select multiple non-adjacent columns or cells
-   `Shift` + `click` — Select all cells in a range
-   `Shift` + `↑/↓` — Extend selection up or down by row
-   `Shift` + `→/←` — Extend selection left or right by column
-   `Cmd/Ctrl` + `Shift` + `↑` — Extend selection to the top of the table
-   `Cmd/Ctrl` + `Shift` + `↓` — Extend selection to the bottom of the table
-   `Cmd/Ctrl` + `Shift` + `→` — Extend selection to the rightmost column
-   `Cmd/Ctrl` + `Shift` + `←` — Extend selection to the leftmost column

### Drag selection

-   `Click and drag` — Select a range of cells
-   `Drag to table edge` while selecting — Viewport automatically scrolls to continue selection

## Copy, cut, and paste

### Standard operations

-   `Cmd/Ctrl` + `C` — Copy selected cells
-   `Cmd/Ctrl` + `X` — Cut selected cells
-   `Cmd/Ctrl` + `V` — Paste clipboard content

### Advanced copy-paste features

**Bulk copy-paste**

Copy large amounts of data across many rows. Clay asynchronously fetches stored cell data, so you're no longer limited to only what's visible in the current viewport.

**List parsing**

When you paste comma-separated lists, Clay automatically detects and parses them as distinct rows or cell objects.

**Single cell range fill**

Copy a single cell, select multiple destination cells, then paste. The copied value fills all selected cells.

**Pattern detection and extension**

Use the drag-fill handle (small square in the bottom-right corner of a selected cell) to extend patterns automatically. Clay detects and continues these pattern types:

-   Basic number sequences (e.g., 1, 2, 3)
-   Geometric sequences (e.g., 2, 4, 8, 16)
-   Fibonacci sequences (e.g., 1, 1, 2, 3, 5)
-   Date sequences
-   Alphanumeric sequences (e.g., A1, A2, A3)
-   Symbol patterns
-   Text patterns

## Undo and redo

-   `Cmd/Ctrl` + `Z` — Undo the last action
-   `Cmd/Ctrl` + `Shift` + `Z` — Redo the last undone action

### What you can undo or redo

-   Single or multiple cell edits
-   Cut, copy, and paste operations
-   Table and column width, order, and color changes
-   Column setting edits (restores draft settings)
-   Row deletions

### What you cannot undo or redo

-   Enrichment cell runs (because they consume credits)
-   Column deletions

## Workflow canvas shortcuts

These shortcuts apply in the Clay **Workflows editor** — the node-based workflow builder. To see the full list of workflow canvas shortcuts inside Clay, open the workflow title dropdown at the top of the editor and click `Keyboard shortcuts`. The canvas tooltips for select, pan, zoom in, zoom out, fit view, and auto-arrange also show each control's shortcut keys.

Workflow canvas shortcuts only work when the canvas has focus — they don't fire while you're typing in a text field, menu, or dialog.

### Zoom and view

-   `+` (or `Z` + `click`) — Zoom in
-   `-` (or `Alt/Option` + `Z` + `click`) — Zoom out
-   `Cmd/Ctrl` + `0` — Zoom the canvas to 100%
-   `Shift` + `1` — Fit the whole workflow in view

### Select and pan

-   `V` — Switch the canvas to select mode
-   `H` — Switch the canvas to pan mode
-   `Space` + `drag` — Pan the canvas temporarily in any direction
-   `Click and drag` on empty canvas area — Draw a selection rectangle to select multiple nodes at once
-   `Cmd/Ctrl` + `A` — Select all

### Organize nodes

-   `Cmd/Ctrl` + `G` — Create group
-   `Cmd/Ctrl` + `Shift` + `G` — Ungroup
-   `Shift` + `A` — Auto-arrange nodes: arranges the selected nodes when two or more are selected, otherwise arranges the whole workflow. Auto-arrange isn't available on read-only or empty workflows.

## FAQs

**Can I undo an enrichment after it runs?**

No, you cannot undo enrichments because they consume credits. However, you can undo changes to enrichment column settings before running them.
