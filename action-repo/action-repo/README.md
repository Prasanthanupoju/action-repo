# action-repo (Event Generator Repo)

This repository is used to generate GitHub events that will be delivered to `webhook-repo` via GitHub Webhooks.

## Steps to create `action-repo`

This folder already includes starter files (`main.py`, `CHANGELOG.md`, `.gitignore`) so you can immediately commit/push and create PRs.

1) Create a new GitHub repository named **action-repo** (public is easiest for testing).
2) Initialize this folder as git and push it:

```bash
cd p:\assignment\action-repo
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <YOUR_GITHUB_REPO_URL>
git push -u origin main
```

That first push triggers the **push** webhook event.

## Steps to trigger required events

### A) Push event

1) Edit any file (e.g., add `test.txt`)
2) Commit + push to `main`

Example:

```bash
echo update>>CHANGELOG.md
git add CHANGELOG.md
git commit -m "Update changelog"
git push
```

### B) Pull request opened event

1) Create a new branch (e.g., `feature/demo`)
2) Commit changes on that branch and push it
3) Open a pull request **from** `feature/demo` **to** `main` (triggers **pull_request opened**)

Example:

```bash
git checkout -b feature/demo
echo pr-change>>CHANGELOG.md
git add CHANGELOG.md
git commit -m "PR change"
git push -u origin feature/demo
```

### C) Merge event (detected)

1) Merge the pull request in GitHub UI (or via CLI)
2) This triggers **pull_request closed** with `merged=true`, which the receiver treats as **merge**

## Webhook configuration (in action-repo)

In GitHub: **Settings → Webhooks → Add webhook**

- Payload URL: `https://<ngrok-domain>/webhook`
- Content type: `application/json`
- Events: enable **Pushes** and **Pull requests**
- Secret: set it only if your `webhook-repo` `.env` sets `WEBHOOK_SECRET`
