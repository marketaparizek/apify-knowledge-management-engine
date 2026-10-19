# Apify knowledge management engine

Keeps Apify's Notion wiki true and findable, for people and for Claude.

Home assignment for the People Automations Partner role. Markéta Pařízek, October 2026.

**Result so far:** the same 10 employee questions, asked to Claude through the Notion connector. Right answers went from 4 to 8 after fixing the Company page and its subpages.

## What's here

| Part | What | Where |
|---|---|---|
| 1a Diagnose | What's wrong for people and for Claude, what to fix first | [docs/1a-diagnose.md](docs/1a-diagnose.md) |
| 1b Fix | Page standard, the wiki skill, fixed pages, before and after test | [docs/1b-fix.md](docs/1b-fix.md), [skills/apify-wiki](skills/apify-wiki), [evals](evals) |
| 1c Build | Weekly review bot: freshness check, owner reminders, duplicates, archiving | [docs/1c-build.md](docs/1c-build.md), [automation](automation) |
| 2 Adoption | Slack replies to three leaders, pilot plan, #general announcement | [docs/part-2-adoption.md](docs/part-2-adoption.md), [Notion wiki pilot](https://app.notion.com/p/3feab6e4e9638109ada3c2db2869ff30) |
| Notes | Time spent, AI tools, assumptions | [docs/notes.md](docs/notes.md) |

## In Notion

- [How to write a page in the Apify wiki](https://app.notion.com/p/214ab6e4e96382a0a92e819d3eb0d1be): the page standard. The Notion page is the source of truth. The skill keeps a copy in `skills/apify-wiki/references/page-standard.md`.
- [Company](https://app.notion.com/p/dcdab6e4e9638394b69e8124566358a4): the hub page and its subpages, fixed by the standard.
- [Wiki admin](https://app.notion.com/p/3feab6e4e9638118babfc0456d1bd129): the [Wiki registry](https://app.notion.com/p/046c9b6acf9949ecaccebd31179332b4) and [Review queue](https://app.notion.com/p/596932576a4f4df388ffeaeb9349ea80), what the review bot reads and writes.

## Install the skill

See [skills/apify-wiki/README.md](skills/apify-wiki/README.md).
