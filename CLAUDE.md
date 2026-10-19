# CLAUDE.md

Context for Claude Code working in this repo.

## What this is

Apify knowledge management engine: Markéta Pařízek's home assignment for the People Automations Partner role at Apify. It keeps Apify's Notion wiki true and findable, for people and for Claude.

Brief, short version:
- **1a Diagnose:** what's wrong for a person and for an AI agent, what to fix first across 25,000 pages. Done: `docs/1a-diagnose.md`.
- **1b Fix:** rework the example pages, explain how to get to final content. Done: `docs/1b-fix.md`, `skills/apify-wiki/`, `evals/`.
- **1c Build:** a working automation that assigns owners, sends review reminders and archives what's outdated. Next: `automation/`.
- **2 Adoption:** Slack replies to the Engineering lead, Sales lead and CEO, a one-page pilot plan for 3 teams, a #general announcement. Not started.

Debrief: 15 min walkthrough, 15 min live change to the automation, 30 min role play.

## Hard constraints

- Notion **Plus**, permanently. Nothing that needs Business or Enterprise. No Notion AI.
- Notion search via MCP: keyword only, about 50 results, no date or author filters, no sorting.
- Public Notion API: yes. Buttons and UI-only actions: no. Regular pages have no properties, only database rows do.
- All company content is in one open teamspace, General.
- Must be maintainable by a non-engineer in the People team.
- Culture: 90/10, premature automation is evil (they will ask what wasn't automated and why), use AI but no slop.

## Decisions (don't reopen without a reason)

- The Notion page "How to write a page in the Apify wiki" is the source of truth. `skills/apify-wiki/references/page-standard.md` is a copy.
- Status line under the title, exact format the bot parses:
  `Up to date · Owner: Full Name, Team (Slack: @handle) · Last reviewed: YYYY-MM-DD`
  Unchecked page: `Needs review · ... · Last reviewed: not yet`. Archived: `Archived · Replaced by: <page> · Archived: YYYY-MM-DD`.
- Status is computed by the bot from the review date. Nobody sets it by hand. The owner only confirms "still true" in Slack.
- Page icon is for the topic, never ✅ ⚠️ 🗄️.
- Archiving never deletes text: title gets "Archived:" prefix, gray callout, page moves under Archive.
- Open questions go to owners in Slack, never Notion comments (on Plus the API can't resolve or delete them).
- Fallback owner: Markéta Pařízek, People team (Slack: @marketa).
- Review cycle for core pages: 3 months. Core pages: about 30.
- Archiving unread pages: monthly list, the Notion admin approves, then the bot archives.
- **Part 1c runtime: a Claude scheduled task for the pilot, kept simple. Not an Apify Actor.** A code-based scheduler (Google Apps Script or GitHub Actions) gets picked later, after research, for company-wide scale.
- Bot uses its own account ("Wiki bot"), not a person's.

## Test workspace (Notion)

- Company hub: https://app.notion.com/p/dcdab6e4e9638394b69e8124566358a4
- Page standard: https://app.notion.com/p/214ab6e4e96382a0a92e819d3eb0d1be
- Archive: https://app.notion.com/p/3feab6e4e963815cb308c24aff1f9741

## Repo conventions

- No version numbers in file names. Git keeps versions. Note changes in the relevant README's "Changes" section.
- Never commit tokens or `.env`. The repo is public.
- Deliverables are `.md` files in `docs/`. No HTML.
- Root README stays one screen: what's where, the result, how to run things.

## Writing style for everything in this repo

- English. Short sentences, everyday words, startup register. Contractions fine. No idioms or wordplay.
- Answer first. Cut anything that carries no information.
- No em dash. No exclamation marks. No emoji as decoration (✓ ✗ → are fine).
- Banned words: delve, leverage, synergy, pivot, foster, comprehensive, robust, seamless, unlock, empower, elevate, journey, ecosystem, game changer, no brainer, low hanging fruit, circle back, touch base.

## Working with Markéta

- Talk to her in Czech. Files stay in English.
- Propose a solution first, then its weak points. No false balance.
- Show changes before committing anything that goes into a deliverable.
