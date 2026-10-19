# apify-wiki skill

A Claude skill that writes new wiki pages, or reviews and fixes existing ones, so they follow the Apify page standard.

## What it does

- You give it a Notion link, or any text: a Slack thread, a Google Doc, notes.
- It looks for existing pages on the same topic first, so it doesn't create a duplicate.
- It rewrites the page by the standard and shows a draft. It changes Notion only after a person says yes.
- Anything it doesn't know becomes a question for the owner, never a guess on the page.

## Install

- **claude.ai:** zip the `apify-wiki` folder and upload it as a skill. Connect the Notion connector.
- **Claude Code:** copy the `apify-wiki` folder into `~/.claude/skills/`.

## Use

- "Review this page: https://app.notion.com/p/..." → list of problems, questions for the owner, rewritten page.
- "Turn this Slack thread into a wiki page under Office" → draft of a new page.

## Files

| File | What | Who edits it |
|---|---|---|
| `SKILL.md` | How the skill works: modes, search order, steps, checklist | Rarely, only when the process changes |
| `references/page-standard.md` | The page rules, copied from the Notion standard page | People team, when the Notion page changes |
| `references/config.md` | URLs and settings for the workspace | People team, when a URL changes |

To change how pages look, edit the standard, not `SKILL.md`.

## Changes

- **v2 (2026-10-19):** archived page titles start with "Archived:", so search results show it without opening the page. The archive line no longer says "current", because keyword search matched it to every "current X" question. Both came from the before and after test.
- **v1 (2026-10-19):** first version, used to fix the Company page and its subpages.
