# Changelog

All notable changes to this project are documented in this file.

## [2026.09] - 2026-09-16

- Maintenance review of launch-chain-skill — the free companion pack for the Claude Code Skills video series: four chained Skills (`launch` orchestrator, `research`, `write`, `deploy`) that turn one `/launch "niche"` command into a researched, written and Vercel-deployed landing page.
- Status: public, MIT licensed, last commit 2026-07-27. Four `SKILL.md` markdown files under `skills/`, plus README and LICENSE — no build step, no dependencies, no code to install.
- Reviewed September 2026: docs refreshed, `## Status` line added to README, changelog started, versioned as v2026.09. No SKILL.md file was modified.
- Known gaps, already documented in the README: step 3 (`deploy`) does not work until the Vercel CLI is installed and logged in, and teams with Deployment Protection forced on also need a `VERCEL_TOKEN`; the landing pages the chain writes are demos with testimonials and stats marked `[replace]`.
- No automated checks exist for this repo — the Skills are prose instructions, so nothing here is testable in CI, and correctness depends on the Claude Code runtime that loads them.
