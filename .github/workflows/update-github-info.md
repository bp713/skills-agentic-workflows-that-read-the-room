---
name: update-github-info
description: Draft updates to Mona's GitHub information page from notes, GitHub Blog posts, and changelog updates.
engine: copilot
model: auto 
permissions:
    copilot-requests: write
on:
  workflow_dispatch:
  schedule:
    - cron: '17 9 * * *'
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.com
    - github.blog
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
---

# Update Mona's GitHub info page

Read `notes/mona-notes.md` before drafting any changes.

Use `web-fetch` to read external public guidance and announcements from:
- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/
- Awesome Copilot workflows: https://awesome-copilot.github.com/workflows/

Use `web-fetch` on https://awesome-copilot.github.com/workflows/ to gather relevant workflow examples and public guidance when they support the content update.

Use GitHub repository API tools to read repository guidance or reference files instead of terminal, CLI, or sandboxed commands.

Check that the workflow configuration syntax is valid before finishing, but do not compile the workflow.

Update `site/content/github-info.md` with concise, practical improvements informed by Mona's notes and the official GitHub Blog / GitHub Changelog content.

Keep the content relevant for readers of the site and include source context when the update is based on the GitHub Blog or GitHub Changelog.

Open a pull request for Mona to review. Do not write directly to `main`; rely on `safe-outputs` with `create-pull-request` so the agent can propose the patch and let Mona review it before merging.
