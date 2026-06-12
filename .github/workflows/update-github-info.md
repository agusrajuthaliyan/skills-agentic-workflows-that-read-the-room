---
name: update-github-info
description: Update local GitHub info page from GitHub Blog and local notes; propose changes via PR for Mona to review.
on:
  schedule:
    - cron: "0 6 * * *" # daily at 06:00 UTC
  workflow_dispatch: {}
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: false
    fallback-as-issue: false
permissions:
  contents: read
network:
  allowed:
    - github.com
    - github.blog
---

# Update GitHub Info

This agentic workflow updates [site/content/github-info.md](site/content/github-info.md) by reading local notes and fetching the GitHub Blog, then proposing changes in a pull request for Mona to review.

## Agent Instructions

- Read `notes/mona-notes.md` from the repository and extract any items relevant to GitHub platform news or changelog entries.
- Web fetch the following URLs and extract recent headlines and summaries:
  - https://github.blog/latest/
  - https://github.blog/changelog/
- Combine the fetched items with the local notes, deduplicate, and write a concise, human-friendly update into `site/content/github-info.md`. Preserve frontmatter in that file if present; only replace or update the content/body section.
- Use the `create-pull-request` tool with `safe-outputs: true` to propose the change. Create a branch named `update/github-info-YYYYMMDD` (use today's date), and open a PR against `main` titled `Update GitHub info — YYYY-MM-DD` with a clear description and request Mona's review.
- Do not auto-compile this workflow. The markdown file is the source of truth and should remain uncompiled in the repo.

## Safety & Access

- This workflow runs daily and can also be triggered manually via `workflow_dispatch`.
- The `create-pull-request` tool is configured with `safe-outputs: true` so the agent proposes changes via a PR rather than pushing directly to `main`.
- Network access is restricted to `https://github.blog` as declared in `network.allowed`.

## Usage

Run on demand with `gh aw run update-github-info` or wait for the scheduled daily run.

## Notes for maintainers

- Do not compile this agentic workflow here — it should remain as the single markdown source used by `gh aw`.
- If you change the target file path, update both the agent instructions and the workflow `permissions` accordingly.
