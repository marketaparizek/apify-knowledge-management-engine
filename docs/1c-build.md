# Part 1c: Build

## Every Monday, a bot checks the key pages. People make the calls.

A Claude scheduled task reads one Notion table, checks how fresh each key page is, reminds owners in Slack and suggests what to archive. It never rewrites a page. It only updates the status line, adds owners' answers from Slack word for word, and archives what the admin approved.

- **Wiki registry:** [Notion](https://app.notion.com/p/046c9b6acf9949ecaccebd31179332b4), one row per key page: owner, last review, status.
- **Review queue:** [Notion](https://app.notion.com/p/596932576a4f4df388ffeaeb9349ea80), what the bot found. The admin decides.
- **The bot:** [automation/wiki-bot-prompt.md](../automation/wiki-bot-prompt.md), one prompt with settings on top. No code.

## What happens every Monday

1. **Checks how fresh each page is.** Reviewed in the last 90 days and no open questions: up to date. Otherwise: needs review. Updates the status line on the page.
2. **Checks the owner is still here.** Owner's Slack account is gone: the page goes to the People team until the team leader names someone.
3. **Reminds owners.** One direct message per owner, 7 days before the review is due, and one more if it's overdue. Never more. The message says why it arrives and what to do in three steps. Each page gets a reply in the thread with its open questions. The owner reacts ✅ or answers there. A short daily run reads the replies, adds answers to the page and turns the status green the next morning. Owners never open the registry.
4. **Finds duplicates and outdated pages.** Pages with the same topic as a key page, pages with no edit in 12 months, and 1:1s or meeting notes in General.
5. **Carries out decisions.** What the admin marked "Archive" gets archived: title prefix, gray status line, moved under Archive. Old text stays.
6. **Writes the log.** What changed, who got a reminder, what failed. In a private channel.

## The bot counts. People decide.

| Job | The bot | A person |
|---|---|---|
| Owner | Notices when an owner leaves and hands the page to the People team. | Team leader names the owner. Once, a few minutes per team. |
| Review | Counts days, sets the status, sends reminders with the open questions, reads ✅ and answers in Slack. | Owner checks the page and reacts ✅ in the reminder thread. Answers open questions in the same thread. About 10 minutes per page every 3 months. |
| Duplicates | Finds pages on the same topic as a key page. | Topic owner says which page is valid. Once per duplicate. |
| Archiving | Lists outdated pages and working docs. Archives what was approved. | Notion admin sets Archive, Keep or Move. A few minutes a week. |
| Content | Never rewrites it. Adds only owners' answers from Slack, word for word. | Owner, with the wiki skill from Part 1b. |

The status is never set by hand. ✅ only sets the date. Otherwise every page says "up to date" forever.

## Who sees what

Owners only hear about their own pages, in a direct message. The run log goes to a private channel for the people who run the wiki.

## Not automated, on purpose

The bot counts dates, sends reminders and lists pages. People decide, and people write.

### Never automated

| What | Who does it instead | Why not the bot |
|---|---|---|
| Writing page content | The page owner. The wiki skill only drafts, and a person approves every page. | AI as the main author would fill the wiki with AI slop that nobody owns or checks. |
| Choosing owners | The team leader names one owner per key page. A few minutes per team, once. | Knowing who understands a topic is a judgement about people. Slack and Notion data can't tell it. |
| Archiving without a yes | The Notion admin sets Archive, Keep or Move on each row of the Review queue. A few minutes a week. | If the bot archived the valid page, people would lose the right answer. One click from the admin costs less than that mistake. |
| Picking the valid duplicate | The owner of the topic says which page is right, once per duplicate. | Views don't show which page is right. The personal copy of Brand guidelines has 410 views, the Marketing one 138. |

### Planned for company scale

Done by hand in the pilot. These are the next steps once the wiki grows past the pilot teams.

| What | Who does it now | Why by hand for now | When |
|---|---|---|---|
| Chasing owners who don't reply | I follow up by hand during the pilot. | With three teams I can see how often it happens before building anything for it. | If more than a few pages a month stay overdue. |
| Picking key pages | The triage picks them from a views export, about 30 key pages for the pilot. The People team imports that list and each team leader confirms the owner. | Page views aren't in the Notion API, so the bot can't tell which pages people read most. | When views can be exported on a schedule, the import can run every month. |
| Turning Slack threads into pages | The page owner, with the wiki skill. It turns a Slack thread into a page draft, and the owner approves it. | The bot only reads its own reminder threads. Deciding which other thread holds a decision, and which page it belongs to, is a call about content. | If the pilot shows that answers keep living only in Slack threads. |

## Why a Claude scheduled task, and where it stops

At 30 pages a week, a written checklist is enough, and anyone in the People team can change it without an engineer. Every Apifier already has Claude with the Notion and Slack connectors, so nothing new needs hosting.

It won't scale to the whole company. The Notion connector returns about 50 results per search, so it can't walk 25,000 pages, and a model shouldn't be the thing that counts dates for 250 people. Before rollout, the same checklist moves into a code-based scheduler, for example Google Apps Script or GitHub Actions. Which one depends on who maintains it, and that's a decision for after the pilot.

## Change it live

All rules sit in the Settings table at the top of the prompt: review cycle (90 days), reminder lead time (7 days), when a page counts as stale (12 months), which sections to scan, log channel, dry run. A change is one line.

## See it run

Four runs on 19 October 2026 in the test workspace, each logged with what every step did:

- [Dry run](../automation/runs/2026-10-19-dry-run.md). Found two prompt bugs, both fixed.
- [First live run](../automation/runs/2026-10-19-run.md). Status lines, the first owner DM, 4 rows in the Review queue.
- [Second live run](../automation/runs/2026-10-19-run-2.md). The first reminder in the Slack format, with one thread reply per page.
- [Third live run](../automation/runs/2026-10-19-run-3.md). Fired by the scheduled task itself, not by hand.

Not shown yet: the bot reading an owner's ✅ and answers (step 0), and archiving a page the admin approved (step 5). Both need a person to act first.
