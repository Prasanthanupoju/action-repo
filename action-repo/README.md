# action-repo (Event Generator Repo)

This repository is used to generate GitHub events that will be delivered to `webhook-repo` via GitHub Webhooks.

## Steps to create `action-repo`

1) Create a new GitHub repository named **action-repo** (public is easiest for testing).
2) Clone it locally.
3) Create a `main` branch if it doesn’t exist.
4) Add at least one commit and push to `main` (triggers **push** event).

## Steps to trigger required events

### A) Push event

1) Edit any file (e.g., add `test.txt`)
2) Commit + push to `main`

### B) Pull request opened event

1) Create a new branch (e.g., `feature/demo`)
2) Commit changes on that branch and push it
3) Open a pull request **from** `feature/demo` **to** `main` (triggers **pull_request opened**)

### C) Merge event (detected)

1) Merge the pull request in GitHub UI (or via CLI)
2) This triggers **pull_request closed** with `merged=true`, which the receiver treats as **merge**

## Webhook configuration (in action-repo)

In GitHub: **Settings → Webhooks → Add webhook**

- Payload URL: `https://<ngrok-domain>/webhook`
- Content type: `application/json`
- Events: enable **Pushes** and **Pull requests**
- Secret: set it only if your `webhook-repo` `.env` sets `WEBHOOK_SECRET`
