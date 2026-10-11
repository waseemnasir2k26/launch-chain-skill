# `/launch` — one command → a live landing page

A chain of **four Claude Code Skills** wired behind one command. You type
`/launch "some niche"`, and it **researches** the market, **writes** a landing page, and
**deploys** it live — hands-off, nothing typed in between.

## Status

Last reviewed: October 2026 · release v2026.10

This is the free pack from the Claude Code Skills video series. No email, no gate.

## What's inside

```
skills/
  launch/     ← the orchestrator — one entry point, fires the other three in order
  research/   ← step 1: market + buyer + competitor research → out/research.md
  write/      ← step 2: out/research.md → a self-contained landing page (out/site/index.html)
  deploy/     ← step 3: deploy that folder to Vercel → a real, public live URL
```

Four folders, four `SKILL.md` files, no build step and no dependencies to install. A Skill is
just a markdown file with frontmatter — that is the whole trick.

## Prerequisite — read this before you run it

**Steps 1 and 2 work out of the box. Step 3 (`deploy`) does not, until you authenticate
Vercel.** This is the single thing that trips people up, so it is stated plainly:

- The `deploy` skill shells out to the [Vercel CLI](https://vercel.com/docs/cli). You need it
  installed and **already logged in** on your machine, or the chain will stall at step 3 asking
  for credentials.
- Optionally, if your Vercel team turns on SSO "Deployment Protection" by default, `deploy`
  can switch it off for the new project via the Vercel API. That call needs a
  [Vercel API token](https://vercel.com/account/tokens) you create yourself, exported as
  `VERCEL_TOKEN`. On a personal hobby account you can usually skip this entirely.

```bash
npm i -g vercel
vercel login
vercel whoami            # must print your username before /launch will finish

# only if your team force-enables Deployment Protection:
export VERCEL_TOKEN=your_token_here
```

No token of ours ships in this repo, and none is needed to read it — you use your own account.

## Install (2 minutes)

1. Copy the four folders inside `skills/` into your Claude Code skills directory:

   ```bash
   git clone https://github.com/waseemnasir2k26/launch-chain-skill.git
   cp -r launch-chain-skill/skills/* ~/.claude/skills/
   ```

   You should end up with `~/.claude/skills/launch/`, `~/.claude/skills/research/`,
   `~/.claude/skills/write/` and `~/.claude/skills/deploy/`, each holding a `SKILL.md`.

   On Windows the same directory is `%USERPROFILE%\.claude\skills\`.

2. Authenticate Vercel (see the prerequisite above).

3. Open Claude Code in any working folder and run:

   ```
   /launch "cold-plunge studio"
   ```

Artifacts land in `./out/` — `research.md`, then `site/index.html` — and you get a live URL at
the end.

## How the chain passes work along

```
/launch "cold-plunge studio"
        │
        ├─ research  →  ./out/research.md         who buys · their fears · competitor claims · the angle
        ├─ write     →  ./out/site/index.html     headline · offer · sections, written off that brief
        └─ deploy    →  https://….vercel.app      shipped, then verified to return 200 and not a login wall
```

Each stage has to finish before the next starts, because the output _is_ the next stage's input.
If a stage fails, the chain stops and tells you which one — it will never hand you a fake URL.

## Make it yours

The skills are plain markdown. Edit the `write` skill's design bar to your own brand, swap the
`research` sections for the questions your niche actually needs, or replace `deploy` with your
own host. The pattern is the point:

> A single Skill is a tool. **Several Skills behind one command is a system** — the boring middle
> runs itself.

## Notes

- The landing pages this writes are **demos**. The `write` skill is explicitly instructed never
  to invent proof, and to mark testimonials and stats as `[replace]` — swap in real ones before
  anything goes to a client.
- `out/` and `.vercel/` are machine-local build artifacts and are git-ignored.

## Watch

- Video #1 — [Stop Re-Prompting Claude Code — Use Skills Instead](https://www.youtube.com/watch?v=6-a_N5Dpog4) (build your first Skill)
- Video #2 — chaining Skills into `/launch`, which is where this pack comes from

More: [skynetjoe.com](https://skynetjoe.com)

## Licence

MIT — see [LICENSE](LICENSE). Use it, sell with it, no attribution required.

Built by Waseem Nasir · **SkynetLabs**

## Work with SkynetLabs

Built by [Waseem Nasir](https://www.skynetjoe.com/?utm_source=github&utm_medium=readme&utm_campaign=launch-chain-skill) at SkynetLabs — n8n + AI automation for small businesses.

- Hire on Fiverr: https://www.fiverr.com/agencies/skynetjoellc
- Hire on Upwork: https://www.upwork.com/freelancers/muhammadwaseemnasir
- Book a free call: https://calendly.com/skynetlabs/schedule-a-free-consultation
