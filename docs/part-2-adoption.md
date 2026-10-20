# Part 2: Get it adopted

Three Slack replies, the pilot plan and the #general announcement.

## Slack replies

### Engineering lead

> My team documents in GitHub. We're not going to maintain Notion pages on top of that, and nobody reads them anyway.

Fair, I wouldn't want another set of docs to maintain either. GitHub stays the source, but most people outside Engineering don't know their way around it. We need one place for shared company knowledge, and right now that's Notion.

Let's figure out how to make this work with as little input from your team as possible. The point is to follow how information already flows here, not to rebuild it. A rebuild would die anyway. For the docs other teams need, a short Notion summary links to the GitHub file. Someone in Engineering only picks what gets shared.

I think a bit of time setting this up properly could keep the ongoing work minimal. I'll DM you to find 30 minutes for it.

### Sales lead

> Love it in principle. But it's end of quarter and my team has zero time for this. Can People just do it for us?

I get it. I'll prepare the workflow and do as much of the cleanup as I can upfront, so you mostly have yes/no decisions to make.

I'd suggest a short 30-minute kickoff with you, whenever it fits around your deadlines. We agree on what's realistic for your team right now and when they can give it some attention. Until then I'll get the prep moving, so nothing stalls.

The point is to make your team's work easier, not add to it. Before we talk, think about where your team loses time because the info isn't easy to find. That's where I'd start.

### CEO

> Good. Can we have this across the whole company within a month instead of piloting?

I'd keep expectations a bit lower for the first month. We can get a working version in place for the pages people use most. The whole knowledge base will take longer.

I'd start with a few teams before opening it up to everyone. We need to understand how information moves around here. Today a basic question gets the right answer about 3 times in 10. If we roll out before we know what fixes that, we spread the same mess faster.

First we need to find out if these changes really make people more productive. Only then would I roll it out more widely.

## Pilot plan

The plan lives in Notion as a page everyone can read: [Notion wiki pilot](https://app.notion.com/p/3feab6e4e9638109ada3c2db2869ff30). Copy below.

**Brief summary.** From 26 October to 4 December 2026, People, Engineering and Customer Success test a few simple changes to make the wiki easier to trust: one owner for each key page, a review reminder every 3 months, and old versions clearly archived. Nothing changes for other teams yet. Sales starts preparing in parallel and joins right after the pilot. Results go to #general on 4 December 2026.

### 💡 Why we're doing this

A lot of us now ask Claude before asking a colleague. Claude looks in Notion, so its answers depend on what it finds there.

In a test copy of our wiki in October 2026, Claude got 4 out of 10 common questions right. Outdated pages, duplicates and meeting notes got in the way. Business travel alone has four pages with three different daily allowances.

Claude doesn't sound any less sure when it quotes an old page. We need to make it clear which page to trust, who looks after it and when it was last reviewed.

### 📄 What changes on a page

🏷️ A line at the top shows whether the page is up to date, who owns it and when it was last reviewed.
📝 A short summary underneath gives you the main answer.
📦 Old versions move to the Archive, with "Archived:" in the title and a link to the page that replaced them.

The full rules are in [How to write a page in the Apify wiki](https://app.notion.com/p/214ab6e4e96382a0a92e819d3eb0d1be).

### 👥 Who does what

🧭 **Team leaders** choose one owner for each key page and help decide which version to keep when there are duplicates. We aim to keep this under an hour per leader across the six weeks.
✍️ **Page owners** help check the facts during the cleanup. After that, they get a Slack reminder every 3 months, check the page and react ✅ in Slack. Open questions get answered in the same thread. No need to open Notion for it.
🤝 **The People team** runs the cleanup, coordinated by Markéta Pařízek. We use the wiki skill to help rewrite pages, merge duplicates, move 1:1s and meeting notes out of General, and set up the review reminders.
🛠️ **Engineering** keeps GitHub as the source for technical docs. For selected docs that other teams need, we add a short Notion summary with a link to the original.

### 🎯 Why these three teams

👥 **People** owns the most-read policies, like leave, benefits and onboarding. We go first with our own pages.
🛠️ **Engineering** keeps its docs in GitHub. If this works for them, it works anywhere.
🤝 **Customer Success** has the pages with the highest stakes. Refund policy has 347 views in 90 days and nobody looking after it.
💼 **Sales** isn't one of the three. End of quarter leaves them no time right now. We start in parallel anyway. The People team prepares their cleanup, so Sales mostly makes yes/no calls, and a 30-minute kickoff with the Sales lead sets a pace that fits. Sales joins right after the pilot.

### 🤖 Where automation helps

We automate review reminders and the status line at the top of each page.

People still make the decisions.
- The wiki skill prepares a draft. A person reviews it before it's published.
- The review bot lists pages that might need archiving in the [Review queue](https://app.notion.com/p/596932576a4f4df388ffeaeb9349ea80). A person decides.

We don't copy full technical docs into Notion.

### 🗓️ Six weeks, week by week

**26 to 30 Oct.** Team leaders name an owner for each key page. We write 100 test questions for the key pages with AI, owners confirm the right answers, and we test Claude on them.
**2 to 13 Nov.** We fix the key pages with the wiki skill. Owners check the facts. Duplicates get archived, 1:1s and meeting notes move out of General.
**16 to 27 Nov.** The review bot runs every Monday. Owners get their first reminder and confirm their pages with ✅ in Slack.
**30 Nov to 4 Dec.** We test Claude on the same questions again and share the results in #general on 4 December.

### 📊 What we'll check on 4 December 2026

- Claude answers at least 95 of the 100 verified questions correctly.
- Every key page across the three teams has a named owner.
- At least 80% of owners respond to a review reminder within 5 working days.
- No duplicates, 1:1s or meeting notes remain in the three teams' wiki sections.
- Each team leader has spent less than an hour on the pilot.

### 🚀 What happens next

On 4 December we decide together with the team leaders and the CEO how fast to bring in more teams.

If something doesn't work, we fix it before adding more teams.

### 🙋 How you can help

You don't need to be on one of the pilot teams to help.

❓ Give us a real question to test. DM Markéta Pařízek (@marketa) with something you recently tried to find in Notion but couldn't. You'll get the answer back.
🚩 Flag anything that looks wrong. Message the owner named at the top of the page. If there isn't one yet, message Markéta Pařízek (People team, @marketa).
🔒 If you're on a pilot team and keep 1:1 notes in General, move them to your Private section. If you're unsure what to move, Markéta Pařízek will follow up with you.

## #general announcement

> :wave: A small cleanup of our Notion wiki.
>
> Claude now uses Notion to answer questions for all of us. Which is useful, until it confidently gives you a travel policy from 2023. Better answers start with better pages.
>
> :test_tube: We're starting a *Knowledge Base Engine pilot* with *People, Engineering and Customer Success, from 26 Oct to 4 Dec.*
> • One owner for each key page, with a "last checked" date at the top
> • A Slack reminder for owners every 3 months
> • Duplicates merged, and 1:1s and meeting notes moved out of General
>
> A bit of automation to help with the upkeep. People still decide what's correct and what stays. Sales starts in parallel, at a pace that fits their quarter.
>
> :raised_hand: To help us test it, *DM me a question you recently tried to answer in Notion but couldn't.* I'll find you the answer and fix the page it should have been on. Questions from any team are welcome.
>
> More here: [Notion wiki pilot](https://app.notion.com/p/3feab6e4e9638109ada3c2db2869ff30)
