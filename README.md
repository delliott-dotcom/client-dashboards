# Tripleview Client Dashboards

Interactive, web-published status dashboards for client projects. One folder per client, one subfolder per project, each containing a self-contained `index.html` dashboard.

## Structure

```
client-dashboards/
  index.html                      <- placeholder landing page (no client links)
  spokane/
    fa-org-restructure/
      index.html                  <- City of Spokane, FA Org Restructure
  winston-salem/
    v45-upgrade/
      index.html                  <- City of Winston-Salem, FMS v45 Upgrade
  confederated-tribes/
    ap-ach-setup/
      index.html                  <- Confederated Tribes, AP ACH Setup
    purchasing-workflow/
      index.html                  <- Confederated Tribes, Purchasing Workflow
  sarasota/
    historical-data/
      index.html                  <- City of Sarasota, Historical Data
  <client>/
    <project>/
      index.html
```

Each dashboard is a single HTML file. All project data lives in the `const DATA = {...}` block near the bottom of the file, so the page works locally (double-click to open) and on GitHub Pages with no build step.

## Published URLs

Once GitHub Pages is enabled on this repo, each dashboard is available at:

`https://<github-username>.github.io/client-dashboards/<client>/<project>/`

Example: `https://<github-username>.github.io/client-dashboards/spokane/fa-org-restructure/`

## Update workflow (after each client call)

1. Give Claude the call transcript (paste it, or point to the file in the Meeting Transcripts folder).
2. Claude updates the `DATA` block in the project's `index.html`:
   - status pill and summary narrative
   - new / completed action items
   - decisions made on the call
   - timeline and milestone changes
   - risks opened or resolved
   - adds the meeting to the meeting log and sets the next meeting date
   - bumps `lastUpdated`
3. Review the dashboard locally before publishing.
4. Publish: `git add -A; git commit -m "Spokane update after <date> call"; git push`
   GitHub Pages redeploys automatically within a minute or two.

## Adding a new client or project

Ask Claude to "create a dashboard for <client> / <project>". It copies the template structure into a new folder and pre-fills it from whatever context is available.

## Content rules (important)

This repository is PUBLIC (required for free GitHub Pages). Dashboards must contain status-level information only:

- OK: project phase, milestones, action items, decisions, first names / roles
- NOT OK: rates, contract terms, credentials, internal-only commentary, security details, anything the client has not already seen

Every page carries `<meta name="robots" content="noindex, nofollow">` so search engines skip it, and the landing page links to nothing, but anyone with the link (or who finds the repo) can view the content. Write accordingly.
