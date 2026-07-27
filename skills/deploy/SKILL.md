---
name: deploy
description: Use to deploy a static site folder to Vercel and return the live production URL. Runs the vercel CLI (must already be logged in). Called as step 3 of the launch chain.
---

# deploy — static folder → a real live URL

## Prerequisite

The `vercel` CLI must be installed and already authenticated on this machine:

```bash
npm i -g vercel
vercel login
```

If `vercel whoami` errors, stop and tell the user to log in. Never fake a URL.

## Steps

1. Confirm the CLI is available and authed: `vercel whoami`.
2. Deploy the site folder to production and capture the full output:

   ```bash
   vercel deploy "./out/site" --prod --yes
   ```

3. Parse the `Production:` (and any `Aliased:`) URL from the CLI output.

4. **Kill the auth wall (only if your account enables it).** Vercel Team/Pro accounts
   default new projects to SSO "Deployment Protection" — the `.vercel.app` URL then
   redirects to a Vercel login and nobody but you can open it. Check step 5 first; if the
   URL is walled, disable protection via the API.

   The CLI writes the project + org ids to `./out/site/.vercel/project.json` on first
   deploy, so read them from there rather than hard-coding anything:

   ```bash
   # A Vercel API token you created yourself:
   #   https://vercel.com/account/tokens  →  export VERCEL_TOKEN=...
   # (Never commit a token, and never read one out of the CLI's credentials file.)
   PID=$(python -c "import json;print(json.load(open('./out/site/.vercel/project.json'))['projectId'])")
   TID=$(python -c "import json;print(json.load(open('./out/site/.vercel/project.json'))['orgId'])")

   curl -s -X PATCH "https://api.vercel.com/v9/projects/$PID?teamId=$TID" \
     -H "Authorization: Bearer $VERCEL_TOKEN" -H "Content-Type: application/json" \
     -d '{"ssoProtection":null}'
   ```

   On a personal (hobby) account there is no team — drop the `?teamId=` query entirely.

5. **Verify it is actually public** — a redirect to `vercel.com/login` = still walled, DO NOT
   report success:

   ```bash
   curl -sL -o /dev/null -w "%{http_code} %{url_effective}\n" <URL>
   # MUST be: 200 <URL>/   (NOT 200 https://vercel.com/login?...)
   ```

6. Return exactly one line: `Live: <URL>` — the real, clickable, PUBLIC production URL.

## Rules

- The URL must be real, PUBLIC (no auth wall), and load 200. Never invent or guess a URL.
- If deploy fails, report the CLI error verbatim and stop.
- Never print, log, or embed the token. Read it from the `VERCEL_TOKEN` environment
  variable only.
- `.vercel/` is generated per-machine and is git-ignored — it is not part of this repo.
- The public-verify (step 5) is MANDATORY. The whole value of the chain is that anyone can
  open the URL you hand them.
