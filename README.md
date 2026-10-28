# IT PMO Board (v2)

A single-file Kanban board demo for an IT project management office. This is the v2 redesign: a purple theme, a horizontal board lane and a built-in security layer.

**Live demo:** https://pwtham.github.io/kanban8-v2/

The first version stays online at https://pwtham.github.io/kanban8/.

## Features

- Four columns (Backlog, In Progress, Blocked, Done) in one horizontal, scrollable lane
- Drag and drop between columns, with a keyboard-friendly "Move" menu on every card
- Filters by project, assignee and priority, plus a live summary with overdue counts
- Add and delete tasks, with inline validation and an inline delete confirmation
- Light and dark themes, starting from your system setting
- Security panel showing the status of each control, a blocked-input counter and an activity log

## Security controls

| Control | What it does |
| --- | --- |
| Content Security Policy | Allows only the page's own hashed script and style, and network calls only to FormSubmit |
| Input sanitisation | Strips control and hidden text-direction characters, rejects HTML-like markup, caps field lengths |
| Allow-list validation | Checks dropdown values and dragged card IDs against fixed lists |
| Output escaping | HTML-escapes all user text before display |
| Rate limit | 5 new tasks per minute, which protects the email endpoint |
| Bot trap | Hidden form field that drops automated submissions |
| Clickjacking guard | Refuses to run inside another site's frame |
| No data at rest | No cookies or browser storage; a refresh resets the board |

This is a static demo with no sign-in. These controls reduce abuse and injection risk but do not replace server-side access control.

## Run locally

Open `index.html` in a browser. There is no build step and no dependencies.

## Changing the page

The CSP in `index.html` is tied to a SHA-256 hash of the inline script and the inline style. If you edit either one, recompute both hashes and update the `Content-Security-Policy` meta tag, or the page will not run.

New-task email notifications use FormSubmit. Set your address in `FORMSUBMIT_ENDPOINT` near the top of the script; the placeholder in the repo is not a real address.

## Deployment

A GitHub Actions workflow (`.github/workflows/pages.yml`) publishes `index.html` to GitHub Pages on every push to `main`.
