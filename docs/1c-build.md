# Part 1c: Build

## Every Monday, a bot checks the key pages. People make the calls.

A Claude scheduled task reads one Notion table, checks how fresh each key page is, reminds owners in Slack and suggests what to archive. It never changes what a page says.

- **Wiki registry:** [Notion](https://app.notion.com/p/046c9b6acf9949ecaccebd31179332b4), one row per key page: owner, last review, status.
- **Review queue:** [Notion](https://app.notion.com/p/596932576a4f4df388ffeaeb9349ea80), what the bot found. The admin decides.
- **The bot:** [automation/wiki-bot-prompt.md](../automation/wiki-bot-prompt.md), one prompt with settings on top. No code.

## What happens every Monday

1. **Checks how fresh each page is.** Reviewed in the last 90 days: up to date. Older or never: needs review. Updates the status line on the page.
2. **Checks the owner is still here.** Owner's Slack account is gone: the page goes to the People team until the team leader names someone.
3. **Reminds owners.** One direct message per owner, 7 days before the review is due, and one more if it's overdue. Never more.
4. **Finds duplicates and outdated pages.** Pages with the same topic as a key page, pages with no edit in 12 months, and 1:1s or meeting notes in General.
5. **Carries out decisions.** What the admin marked "Archive" gets archived: title prefix, gray status line, moved under Archive. Old text stays.
6. **Writes the log.** What changed, who got a reminder, what failed. In a private channel.

## The bot counts. People decide.

| Job | The bot | A person |
|---|---|---|
| Owner | Notices when an owner leaves and hands the page to the People team. | Team leader names the owner. Once, a few minutes per team. |
| Review | Counts days, sets the status, sends reminders with the open questions. | Owner checks the page and presses "Mark as reviewed". About 10 minutes per page every 3 months. |
| Duplicates | Finds pages on the same topic as a key page. | Topic owner says which page is valid. Once per duplicate. |
| Archiving | Lists outdated pages and working docs. Archives what was approved. | Notion admin sets Archive, Keep or Move. A few minutes a week. |
| Content | Never touches it. | Owner, with the wiki skill from Part 1b. |

The status is never set by hand. The button only sets the date. Otherwise every page says "up to date" forever.

## Who sees what

Owners only hear about their own pages, in a direct message. The run log goes to a private channel for the people who run the wiki.

## Not automated, on purpose

| What | Why not | When that changes |
|---|---|---|
| Choosing owners | It's a call about people. The bot can't tell who knows a topic. | Never. |
| Archiving without a yes | Archiving the valid page costs more than one click from the admin. | Never. |
| Picking the valid duplicate | Views don't decide: a draft can be read more than the real policy. | Never. |
| Chasing owners who don't reply | In a pilot with 3 teams, I do it by hand and learn if it's needed. | If more than a few pages a month stay overdue. |
| Filling the registry | 30 pages, about an hour, once. | When we go past the pilot. |
| Slack decisions into Notion | We don't know yet if it's the biggest gap. | If the pilot shows answers live only in threads. |

## Why a Claude scheduled task, and where it stops

At 30 pages a week, a written checklist is enough, and anyone in the People team can change it without an engineer. Every Apifier already has Claude with the Notion and Slack connectors, so nothing new needs hosting.

It won't scale to the whole company. The Notion connector returns about 50 results per search, so it can't walk 25,000 pages, and a model shouldn't be the thing that counts dates for 250 people. Before rollout, the same checklist moves into a code-based scheduler, for example Google Apps Script or GitHub Actions. Which one depends on who maintains it, and that's a decision for after the pilot.

## Change it live

All rules sit in the Settings table at the top of the prompt: review cycle (90 days), reminder lead time (7 days), when a page counts as stale (12 months), which sections to scan, log channel, dry run. A change is one line.

## See it run

The first dry run, step by step with what each step found and what it taught us: [automation/runs/2026-10-19-dry-run.md](../automation/runs/2026-10-19-dry-run.md). The live run (status callouts rewritten, DMs sent, queue rows added) is the first thing the pilot does in week 1.
