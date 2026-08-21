---
name: Weekly Report Status
description: Weekly activity report covering commits, issues, and pull requests from the previous 7 days
engine: copilot
on:
  schedule:
    - cron: "0 10 * * 1" # weekly, Monday 10:00 UTC
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Generate a concise activity report for this repository covering the **last 7
full days ending at workflow start (UTC)**.

## Task

1. Gather activity for the 7-day window using `gh` commands (or the GitHub
   tools) for:
   - **Commits**: commits pushed to the default branch.
   - **Issues**: issues opened and closed.
   - **Pull requests**: pull requests opened, merged, and closed.
2. Summarize each category concisely — counts plus a short list of the most
   notable items (title, author, link).
3. If there was **no activity** in a category, or across the entire window,
   state this clearly and explicitly rather than omitting the section.

## Report Structure

Use this structure for the report body:

### Summary
- Commits: `<count>`
- Issues opened / closed: `<count>` / `<count>`
- Pull requests opened / merged / closed: `<count>` / `<count>` / `<count>`

### Commits
Short list of notable commits, or a clear statement that no commits occurred.

### Issues
Short list of notable issues opened/closed, or a clear statement that no issue
activity occurred.

### Pull Requests
Short list of notable pull requests opened/merged/closed, or a clear statement
that no pull request activity occurred.

## Safe Outputs

- Publish the report as a new issue using the configured `create-issue` safe
  output.
- Always create the issue, even when there was no activity — in that case,
  the report must clearly state that no activity occurred during the window.
