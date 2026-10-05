---
name: update-github-info
description: Keep the GitHub Info website current with useful, sourced updates from GitHub.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
model: gpt-4.1
tools:
  edit: true
  web-fetch: {}
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
    allowed-files:
      - site/content/github-info.md
---

Read `notes/mona-notes.md` and `site/content/github-info.md` first. Use the
web-fetch tool to fetch each source URL directly:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Do not use shell, `curl`, `wget`, or another tool to fetch these pages. If
web-fetch cannot read a source, do not retry with shell; continue only with
sources web-fetch can read.

Identify recent updates that are useful to developers and fit Mona's practical
editorial angle. Update only `site/content/github-info.md`, keeping the content
short and practical. Cite the relevant GitHub Blog or Changelog page directly
or Awesome Copilot workflows page for each sourced update. Do not add claims
that are not supported by the source pages, and do not make an empty or
speculative change.

Open one pull request for Mona to review, summarizing the update and linking its
sources in the pull request description. Do not push changes directly to the
default branch. If there is no useful, well-supported update to make, do not
open a pull request.
