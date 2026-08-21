---
name: update-github-info
description: Refresh Mona's GitHub Info page with practical updates from official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
strict: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    allowed-files:
      - site/content/github-info.md
    draft: false
    if-no-changes: warn
---

# Update GitHub Info

Read `notes/mona-notes.md` before making any changes. Web fetch both official sources:

- https://github.blog/latest/
- https://github.blog/changelog/

Use the notes and fetched pages to identify useful, recent updates for developers. Keep
the writing short and practical, cite whether each update comes from the GitHub Blog or
GitHub Changelog, and preserve the existing structure and voice of
`site/content/github-info.md`.

Update only `site/content/github-info.md`. Then use the configured
`create-pull-request` safe output to open a pull request for Mona to review. Summarize
the changes and include links to the official source pages in the pull request body.
Do not write directly to the default branch. If no useful update is needed, call
`noop` with a brief explanation instead of opening an empty pull request.