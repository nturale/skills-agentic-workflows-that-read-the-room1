---
name: update-github-info
description: Refresh Mona's GitHub Info content with recent GitHub Blog, Changelog, and Awesome Copilot workflow updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine:
  id: copilot
  copilot-sdk: true
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    max: 1
---

# Update GitHub Info

Refresh Mona's GitHub Info content with useful, current information from official GitHub sources.

## Instructions

1. Read `notes/mona-notes.md` for Mona's editorial guidance and `site/content/github-info.md` for the current content.
2. Use the `web-fetch` tool to fetch `https://github.blog/latest/`, `https://github.blog/changelog/`, and `https://awesome-copilot.github.com/workflows/`. Follow relevant links from those pages to verify any specific update before writing about it.
3. Select only recent developments that are useful to developers and fit the site's existing themes. Avoid duplicating information already covered.
4. Update only `site/content/github-info.md`. Keep additions short and practical, preserve useful existing material, and link each new claim to its specific GitHub Blog, Changelog, or Awesome Copilot workflows source.
5. Do not invent details or include an item that cannot be verified from an official source. If there are no materially useful updates, leave the file unchanged and do not create an empty pull request.
6. When the file changes, use the `create-pull-request` safe output to open one pull request for Mona to review. Summarize the changes and cite the sources in the pull request description. Never push changes directly to `main` or merge the pull request.