---
name: update-github-info
description: Refresh the GitHub Info page with practical, sourced updates from the GitHub Blog and Changelog.
intent: Keep Mona's GitHub Info page current with concise, practical guidance backed by official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    title-prefix: "[GitHub Info] "
    draft: false
    base-branch: main
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

1. Read `notes/mona-notes.md` and the current `site/content/github-info.md`.
2. Fetch both `https://github.blog/latest/` and `https://github.blog/changelog/` with the web-fetch tool. Use these official sources to identify recent, useful updates for developers.
3. Update only `site/content/github-info.md`. Keep the page concise and practical, preserve its existing useful context, and include a direct source link for every new item drawn from the Blog or Changelog. Do not invent details or add an item unless the source supports it.
4. If there is a worthwhile update, open one non-draft pull request targeting `main` for Mona to review. Use the `create-pull-request` safe output, summarize the changes and their sources in the PR, and do not write directly to `main`.
5. If neither source provides a useful update, or the page needs no change, make no edits and call `noop` with a brief reason.
