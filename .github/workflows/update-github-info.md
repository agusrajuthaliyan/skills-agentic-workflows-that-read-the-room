---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources. Uses Mona's notes, the GitHub Blog, and the GitHub Changelog.
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

Read `notes/mona-notes.md` before making changes.

Use these sources:
- `notes/mona-notes.md` — Mona's notes
- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/

Update `site/content/github-info.md` with concise, practical updates for readers and include source context when content comes from the GitHub Blog or GitHub Changelog.

Open a pull request for Mona to review.
Use a pull request title that mentions Mona or GitHub Info.
Do not write directly to `main`; rely on `safe-outputs` with `create-pull-request`.

## Agent Instructions

When creating or editing agentic workflow files, do not compile them. Only create or update the markdown workflow file.

- Read `notes/mona-notes.md` and use Mona's notes as a source.
- Use the GitHub Blog: https://github.blog/latest/.
- Use the GitHub Changelog: https://github.blog/changelog/.
- Update `site/content/github-info.md` with concise, practical updates for readers.
- Preserve frontmatter in that file if present; only replace or update the content/body section.
- Create a pull request for Mona to review using `safe-outputs.create-pull-request`.
