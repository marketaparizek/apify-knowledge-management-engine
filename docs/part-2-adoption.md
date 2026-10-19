# Part 2: Get it adopted

Three Slack replies, a one-page pilot plan, and the #general announcement. Everything here uses what Part 1 built: the page standard, the apify-wiki skill, the Wiki registry and Review queue in Notion, and the Monday review bot.

Dates assume the pilot starts Monday 2 November 2026 and ends Friday 11 December 2026.

## 1. Slack replies to three leaders

### Engineering lead

> My team documents in GitHub. We're not going to maintain Notion pages on top of that, and nobody reads them anyway.

Agreed, and that's how the plan works. GitHub stays the source of truth for engineering docs. Nobody copies a README into Notion.

What changes is small. Each engineering topic gets one short link page in Notion: three sentences on what the doc covers, a link to the file in GitHub, and a line that says who owns it. If the link page and the README ever differ, the README is right. The standard says so.

Why bother at all: your team's wiki pages are read more than you'd think. Onboarding checklist - Engineering got 320 views in the last 90 days. It hasn't been edited for 23 months and the last person who touched it has left. New joiners read it, and so does Claude when someone asks how to set up. Of your 11 wiki pages, 8 have a problem like that.

Your part is one sitting, not a process. I've pre-filled a list: 11 pages, a proposed owner for each, and which ones should become a link to GitHub. You correct it. After that the review bot sends each owner one Slack DM every 3 months. Pressing "Mark as reviewed" takes about 10 minutes per page.

Can you give me 30 minutes in the week of 26 October to go through the list?

### Sales lead

> Love it in principle. But it's end of quarter and my team has zero time for this. Can People just do it for us?

Yes. People does the work, and Sales isn't in the pilot, so nothing lands on your team this quarter.

What I'll do: merge the three versions of the Sales playbook into one page with the wiki skill, archive the two old ones with a link to the new one, and fix the other two Sales pages that have a problem. Where the pages contradict each other or a fact is missing, I won't guess. I'll collect those as a short list of questions.

What I need from Sales: one name as owner of the Sales pages, and 20 minutes with that person after quarter close to go through the questions and approve the merged page. From then on the owner gets one Slack DM every 3 months and presses a button. That's about 10 minutes per page.

Can you reply with the owner's name by Friday 23 October, and a 20-minute slot in the first week after quarter close?

### CEO

> Good. Can we have this across the whole company within a month instead of piloting?

We can go company-wide within a month on the part that's safe, and pilot the part that isn't.

Safe to do now, company-wide: fix the content of the 35 most-read pages. 26 of them have a problem today: a competing version, no owner, or no edit in over a year. I do this with the wiki skill, owners only approve. The Company page is already done. On the same 10 questions, Claude went from 4 right answers to 8.

Not safe to roll out yet: the owner and reminder loop. The open question isn't the tool. It's whether 30 owners press "Mark as reviewed" when a bot asks them to. If we switch it on for 250 people and they don't, we've taught the whole company to ignore the bot, and that's hard to undo. Three teams for six weeks tells us, with numbers.

There's a second reason. The bot is a Claude scheduled task, which is right for 30 pages and a non-engineer can change it. For the whole company it needs a code-based scheduler, and the pilot tells us what that scheduler has to do before anyone builds it.

Can I start on Monday 2 November, and can you hold 15 minutes on Thursday 10 December for the week 6 numbers and the rollout decision?

## 2. Pilot plan: one page

**Goal.** The most-read pages of three teams are true for people and for Claude, and their owners keep them true without anyone chasing. Six weeks, 2 November to 11 December 2026.

**What's already in place.** The page standard, the apify-wiki skill, the Wiki registry and Review queue in Notion, the review bot (dry run done 19 October), and the Company page with its 9 subpages fixed as the worked example.

### Three teams and why

Each team tests a different way this can fail.

| Team | Why this team | Pages | With a problem | Hardest page |
|---|---|---|---|---|
| People | Owns the most-read policies. We go first on our own pages. | 20 | 16 | Vacation & time off, 394 views, 3 competing pages |
| Engineering | GitHub-first and skeptical. Tests the link page to GitHub. | 11 | 8 | Onboarding checklist - Engineering, 320 views, last editor left |
| Customer Success | Customer-facing risk. Few pages, high stakes. | 4 | 2 | Refund policy, 347 views, last editor left |

Sales joins after quarter close, with the content fix done for them. If Customer Success can't take part, Finance (6 pages, 3 with a problem) is the backup.

### What I ask of each team lead

About one hour over six weeks.

| When | What | Time |
|---|---|---|
| Week of 26 October | Correct a pre-filled list: one owner per page, which pages become a link to GitHub or Drive, which can be archived. | 30 min |
| Weeks 1 to 5 | Answer one question from me when an owner doesn't reply or two pages contradict each other. | Up to 15 min total |
| Week of 7 December | Tell me what to keep and what to change. | 15 min |

Each page owner: about 20 minutes per page once, to check the fixed page and answer my open questions, then press "Mark as reviewed". After that, 10 minutes every 3 months.

### What I do

- Fill the Wiki registry for the three teams: about 30 core pages, owner, Slack ID.
- Fix every page with a problem with the wiki skill: owner and review date at the top, short summary, one topic per page, old versions archived with a link to the new one. Owners approve, I publish.
- Send each owner the questions the skill couldn't answer from the pages, in Slack.
- Run the review bot every Monday under my account, read every log, and chase by hand when a reminder goes unanswered, so we learn whether chasing is needed at all.
- Decide the Review queue weekly with the Notion admin: archive, keep or move.
- Ask the 30 baseline questions again in week 6.

### Timeline

| Week | Dates | What happens |
|---|---|---|
| 0 | 26 to 30 Oct | Leads correct the owner lists. Baseline: 10 real questions per team asked to Claude. Registry filled. |
| 1 to 2 | 2 to 13 Nov | Wave 1: the most-read pages of each team fixed and approved. Their registry rows start as "Needs review", so the first Monday run sends every owner a real reminder. |
| 3 to 4 | 16 to 27 Nov | Wave 2: the rest of the core pages, same loop. The reminder message gets adjusted from what wave 1 taught us. Review queue decided weekly. |
| 5 | 30 Nov to 4 Dec | Overdue reminders go out to anyone who hasn't pressed the button. I chase by hand and note how often. |
| 6 | 7 to 11 Dec | Baseline questions asked again. Numbers to the CEO on Thursday 10 December. Decision. |

Why two waves: a 3-month review cycle would never fall due inside six weeks. Every new registry row starts unreviewed, so the first reminder is real. Two waves mean the loop runs twice and we can fix the message in between.

### How we know it worked

| Metric | Baseline | Target in week 6 |
|---|---|---|
| Claude answers right on 30 real questions, 10 per team | Measured in week 0. On the Company page it was 4 of 10 before the fix. | 8 of 10 per team |
| Core pages with a named owner in the registry | 0 of about 30 | All |
| Core pages Up to date | 0 | 90% |
| Reminders answered by pressing "Mark as reviewed" within 7 days | None sent yet | 70% |
| Median days from reminder to review | None sent yet | 7 or fewer |
| Overdue pages I had to chase by hand | None sent yet | Fewer than 5 |
| Team leads who want to continue | | 3 of 3 |

### Decision in week 6

One of three outcomes, decided on the numbers above.

1. **Roll out.** Owners answer the bot. Next teams join three per week, in the order of their page views, and the code-based scheduler gets built in parallel for company-wide scale.
2. **Adjust and rerun.** Owners answer, but slowly or only after chasing. Change the cadence or the message, run four more weeks with the same three teams.
3. **Stop the loop, keep the content fix.** Owners don't answer. The 35 most-read pages stay fixed, the bot keeps only the duplicate and archive checks, and we look for a different owner model.

## 3. Announcement in #general

Hi all, a short one about the wiki.

We asked Claude 10 questions Apifiers really ask, like the meal allowance abroad or where to find the current OKRs. It got 4 right. The problem wasn't Claude. The wiki had 2 to 4 pages on the same topic and no way to tell which one was true. After we fixed the Company page and its subpages by one simple page format, Claude got 8 of 10.

So from Monday 2 November we're rolling that format out, starting with the pages of People, Engineering and Customer Success. Six weeks, then we decide how to go on.

What changes for you: look at the line right under a page title.
✅ Up to date, with the owner's name and when they last checked it.
⚠️ Needs review: read with care, and the owner knows.
🗄️ Archived: out of date, and the line links the page that replaced it.
No status line means the page isn't part of the wiki yet.

If you own a page, you'll get a Slack DM from me every 3 months with a link and any open questions. Check the page, press "Mark as reviewed". About 10 minutes. That's the whole process.

One ask for everyone: if you find a page that's wrong, message the owner named on it. Don't fix it quietly in a copy, that's how we got here.

Start at the Company page, it's the one place that's already in the new format. Questions to me in #wiki or a DM, by Friday 23 October if you want something changed before we start.
