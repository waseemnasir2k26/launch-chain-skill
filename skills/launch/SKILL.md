---
name: launch
description: Use when the user says "/launch", "launch <niche>", or asks to research, build, AND deploy a landing page for a business/niche from scratch in one command. Orchestrates three skills end-to-end — research → write → deploy — and returns a live URL.
---

# launch — one command → a live landing page

You are the orchestrator. When invoked with a niche (e.g. `/launch "cold-plunge studio"`),
run these three skills **in strict order**, passing each output to the next. Do NOT skip steps
and do NOT ask the user questions between steps — the whole point is hands-off.

1. **research** — invoke the `research` skill with the niche. It writes `./out/research.md`.
2. **write** — invoke the `write` skill. It reads `./out/research.md` and writes `./out/site/index.html`.
3. **deploy** — invoke the `deploy` skill. It deploys `./out/site/` and returns the live URL.

When all three finish, report ONE line to the user:

> ✅ Live: <URL> · built from one command (research → write → deploy)

## Rules

- Create the `./out/` working dir if missing. Keep every artifact there.
- Each stage must complete before the next starts (the chain is sequential — output feeds input).
- If a stage fails, stop and report which stage + the error. Never fake a URL.
- Keep narration terse — this runs live on camera.
