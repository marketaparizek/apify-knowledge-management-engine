# CLAUDE.md

Context for Claude Code working in this repo.

## What this is

Apify knowledge management engine: Markéta Pařízek's home assignment for the People Automations Partner role at Apify. It keeps Apify's Notion wiki true and findable, for people and for Claude.

Brief, short version:
- **1a Diagnose:** what's wrong for a person and for an AI agent, what to fix first across 25,000 pages. Done: `docs/1a-diagnose.md`.
- **1b Fix:** rework the example pages, explain how to get to final content. Done: `docs/1b-fix.md`, `skills/apify-wiki/`, `evals/`.
- **1c Build:** a working automation that assigns owners, sends review reminders and archives what's outdated. Done: `docs/1c-build.md`, `automation/`. Dry run and first live run logged in `automation/runs/`.
- **2 Adoption:** Slack replies to the Engineering lead, Sales lead and CEO, a one-page pilot plan for 3 teams, a #general announcement. Done: `docs/part-2-adoption.md`, written together with Markéta. The pilot plan's source is the Notion page Notion wiki pilot.

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
- Status is computed by the bot from the review date and open questions: Up to date only when reviewed in the last 90 days and the row has no open questions. Nobody sets it by hand. The owner only presses "Mark as reviewed" in the Wiki registry, which sets the date.
- Archived page with no replacement: `Archived · No replacement · Archived: YYYY-MM-DD`.
- Page icon is for the topic, never ✅ ⚠️ 🗄️.
- Archiving never deletes text: title gets "Archived:" prefix, gray callout, page moves under Archive.
- Working docs and personal pages never count as an answer or as the valid version, even inside General. The skill and the bot list them instead.
- Open questions go to owners in Slack, never Notion comments (on Plus the API can't resolve or delete them).
- Fallback owner: Markéta Pařízek, People team (Slack: @marketa).
- Review cycle for core pages: 3 months. Core pages: about 30.
- Bot runs weekly (Monday). Finds duplicates, stale pages (no edit 12+ months) and working docs, writes them to the Review queue. The Notion admin sets Archive, Keep or Move, the bot acts on it. In the pilot it only scans the pilot teams' sections.
- Reminders: one DM 7 days before the due date, one when overdue. Log goes to private #wiki-bot.
- **Part 1c runtime: a Claude scheduled task for the pilot, kept simple. Not an Apify Actor.** A code-based scheduler (Google Apps Script or GitHub Actions) gets picked later, after research, for company-wide scale.
- In the pilot the scheduled task runs under a People team member's account, so DMs come from that person. In production the bot gets its own account ("Wiki bot").

## Test workspace (Notion)

- HQ teamspace stands in for General: 3feab6e4-e963-8133-b2bd-00424a851989.
- Under Company, "Personal pages (test setup)" and "Team working docs (test setup)" copy the real wiki's mess on purpose. Never treat their subpages as wiki pages.
- Company hub: https://app.notion.com/p/dcdab6e4e9638394b69e8124566358a4
- Page standard: https://app.notion.com/p/214ab6e4e96382a0a92e819d3eb0d1be
- Archive: https://app.notion.com/p/3feab6e4e963815cb308c24aff1f9741
- Wiki admin (holds the two tables below): https://app.notion.com/p/3feab6e4e9638118babfc0456d1bd129
- Wiki registry: https://app.notion.com/p/046c9b6acf9949ecaccebd31179332b4 (collection://79fb0939-3018-48e5-a3cb-dfb6163edf4f)
- Review queue: https://app.notion.com/p/596932576a4f4df388ffeaeb9349ea80 (collection://c5c3ae49-d341-4bc4-a683-5d6e0edaa197)
- Slack test workspace, log channel #wiki-bot (C0CAD3CLQGZ)

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
