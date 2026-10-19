# Review bot (Part 1c)

Keeps the key pages of the wiki true after they are fixed. Every Monday it checks how fresh each page is, reminds owners in Slack and suggests what to archive. Every working day it reads what owners answered in Slack. It never rewrites a page. It only updates the status line, adds owners' answers from Slack word for word, and archives what the admin approved. People make every decision.

Owners do the whole review in Slack. They never open the registry.

It runs as a Claude scheduled task with the Notion and Slack connectors. The whole bot is one prompt: [wiki-bot-prompt.md](wiki-bot-prompt.md).

## What it works with

| Thing | Where | What it holds |
|---|---|---|
| Wiki registry | [Notion](https://app.notion.com/p/046c9b6acf9949ecaccebd31179332b4) | One row per key page: owner, Slack ID, last review, status, open questions, the Slack thread of the last reminder. On Notion Plus, only database rows can have properties. |
| Review queue | [Notion](https://app.notion.com/p/596932576a4f4df388ffeaeb9349ea80) | Pages the bot found: possible duplicates, stale pages, working docs. The Notion admin sets Archive, Keep or Move. |
| #wiki-bot | Slack, private | The run log, for the people who run the wiki. |
| Owner DMs | Slack | One message per owner, only about their own pages. Owners answer in its thread. |

## What happens every working day

0. **Owner replies.** Reads the threads of the reminder DMs. ✅ on a page's reply means "still true": the bot sets Last reviewed to today and the page turns Up to date at the next working day's run. A reply like "3: Tomáš Kovář" answers an open question: the bot adds it to the page as an "Added by the owner" block, word for word, and closes the question. If it can't tell which question an answer belongs to, it asks in the thread and writes nothing.

The log goes to #wiki-bot only when something changed.

## What happens every Monday

Step 0, then:

1. **Freshness check.** Reviewed in the last 90 days and no open questions: ✅ Up to date. Otherwise: ⚠️ Needs review. Updates the registry and the status line on the page.
2. **Owner check.** If the owner's Slack account is gone, the page goes to the fallback owner until the team leader names someone.
3. **Reminders.** One DM per owner, 7 days before the review is due, and one more when it's overdue. Never more. Pages are numbered. Each page gets its own reply in the thread, with its open questions, so the owner can react ✅ to it or answer under it.
4. **Duplicates and outdated pages.** Pages on the same topic as a key page, pages with no edit in 12 months, and 1:1s or meeting notes in General go to the review queue.
5. **Decisions.** What the admin marked Archive gets archived: "Archived:" in the title, gray status line, moved under Archive. Old text stays.
6. **Log.** What changed, who got a reminder, what failed.

## The bot counts, people decide

| Job | The bot | A person |
|---|---|---|
| Owner | Notices when an owner leaves. | Team leader names the owner. Once, a few minutes per team. |
| Review | Counts days, sets the status, sends reminders, reads ✅ and answers in Slack. | Owner checks the page and reacts ✅ in the reminder thread. About 10 minutes per page every 3 months. |
| Open questions | Asks them in Slack, adds the owner's answer to the page word for word. | Owner answers in the thread. Folds the answer into the page at the next review. |
| Duplicates | Finds pages on the same topic. | Topic owner says which page is valid. |
| Archiving | Lists outdated pages, archives what was approved. | Notion admin sets Archive, Keep or Move. A few minutes a week. |
| Content | Never rewrites it. Adds only owners' answers from Slack, word for word. | Owner, with the [wiki skill](../skills/apify-wiki). |

The status is never set by hand. ✅ only sets the date. A page with open questions stays Needs review even after ✅.

Working docs and personal pages never count as a key page or as the valid version of a topic, even when they sit in General or have more views. The bot only lists them in the review queue.

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
| Asking authors to move working docs | The People team asks them. | `created_by` changes when a page moves, so the bot can't tell who wrote a page. | If Notion shows a reliable author. |

## Where it stops

At 30 pages a week, a written checklist is enough, and anyone in the People team can change it. It won't scale to the whole company: the Notion connector returns about 50 results per search, and a model shouldn't count dates for 250 people. Before rollout, the same steps move into a code-based scheduler, for example Google Apps Script or GitHub Actions. Which one is a decision for after the pilot.

## Set it up

1. Make #wiki-bot a private channel for the People team and the Notion admin.
2. Create a Claude scheduled task, every working day in the morning, with the Notion and Slack connectors on. Paste [wiki-bot-prompt.md](wiki-bot-prompt.md) as the prompt. The prompt itself knows which day is the full run.
3. First run with `DRY_RUN = true`. Read the log. When it's right, set `DRY_RUN = false`.

## Change it

All rules sit in the Settings table at the top of the prompt: review cycle, reminder lead time, when a page counts as stale, which sections to scan, log channel, dry run. A change is one line.

## Changes

- **2026-10-19, review moves to Slack:** owners review in the reminder thread instead of the registry. ✅ on a page's reply marks it reviewed, ✅ on the DM marks all its pages. Answers to open questions go in the thread and the bot adds them to the page as "Added by the owner" blocks, word for word. The bot now runs every working day: the daily run only reads replies, so a ✅ shows on the page the next morning, not a week later. New registry property Reminder thread. This replaces the decision below that the bot shouldn't read Slack: owners don't open the registry, so the button was a step most of them would skip.
- **2026-10-19, after the live run** ([log](runs/2026-10-19-run.md)): a page stays Needs review while it has open questions, even after "Mark as reviewed". The owner name on the page now comes from the registry, so a new owner shows up. The bot never archives a personal page, it asks for Move or Keep instead. The owner DM explains why it arrives and what to do in three steps, with open questions in the thread. The log uses full sentences and separates what changed from what waits for a decision. The Review queue has two views: To decide and Done.
- **2026-10-19, after the first dry run** ([log](runs/2026-10-19-dry-run.md)): owner-left pages stay Needs review until a new owner is named (step 1 no longer overwrites it), and personal pages in the scanned sections go to the queue even when no key page covers their topic.
- **2026-10-19:** first version. Claude scheduled task instead of an Apify Actor, to keep it simple. Owners confirm with a button in the registry instead of a Slack reply, so the bot doesn't need to read Slack.
