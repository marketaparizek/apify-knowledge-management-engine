---
name: apify-wiki
description: Write a new page for the Apify Notion wiki, or review and fix an existing one, so it follows the Apify page standard. Use whenever someone wants to write, fix, review, clean up, merge or publish a wiki page, or pastes a Slack thread, Google Doc, notes or an old Notion page that should become one. Also use when someone asks "does this page follow the standard". Trigger even if they don't name the skill.
---

# Apify wiki skill

Turns any input into a wiki page that follows the Apify page standard, or checks an existing page against it.

The rules live in `references/page-standard.md`, a copy of the Notion page "How to write a page in the Apify wiki". That file is the only source of truth. If this SKILL.md and the standard disagree, the standard wins. The People team edits the standard, not this file.

## Settings

Fill these in once per workspace.

- `REGISTRY_DATA_SOURCE`: the Wiki registry, the review bot's database of core pages: collection://79fb0939-3018-48e5-a3cb-dfb6163edf4f
- `KNOWLEDGE_OWNER`: Markéta Pařízek, People team (Slack: @marketa). Owns hub pages and the standard, and is the fallback owner when a team hasn't named one.
- `GENERAL_TEAMSPACE_ID`: the General teamspace: 3feab6e4-e963-8133-b2bd-00424a851989 (in the test workspace, the HQ teamspace stands in for General).

## Two modes

- **Write.** Input is new content (Slack thread, doc, notes, screenshot). Output is a new page.
- **Review.** Input is a Notion URL. Output is a list of problems plus a rewritten page.

If it is unclear which mode the user wants, a Notion URL means review, anything else means write.

## Search order

Use this order every time the skill searches the wiki (duplicate check, finding links, checking facts):

1. The registry of core pages (`REGISTRY_DATA_SOURCE`). These pages have an owner and a recent review.
2. General (`teamspace_id = GENERAL_TEAMSPACE_ID`).
3. The Archive page and everything under it, last. Use an archived page only when nothing above answers the question, and say so in the answer: "This comes from an archived page, replaced by [page] on [date]."
4. Never personal spaces. If the only match is in someone's personal space, say so and ask whether it should move to General.

## What never counts as an answer

General itself isn't clean. Working docs sit there too. Even when search returns them, never use these as the answer, as a source for a fact, or as the page to keep:

- **Working docs:** 1:1 notes, meeting notes, retros, standups, plans, project notes, drafts, WIP. Spot them by title (for example "1:1", "Meeting notes", "Retro", "Plan Q3", "project notes", "Notes", "Untitled", "draft") or by a path through a team's notes area.
- **Personal pages:** anything in someone's personal space, even when it has more views than the wiki page.

The paths that mark both are in `references/config.md`.

When one of these is the only match, say so: "The only page on this is a working doc / a personal page: [page]. It isn't part of the wiki." Then suggest moving the content into a wiki page with this skill.

Report them, don't ignore them: in review mode, list them under "Problems found" with the page link, so the person can move or archive them. A working doc in General goes into the Review queue as "Working doc". A personal page on the same topic as a wiki page goes in as "Possible duplicate".

Archived pages have a title that starts with "Archived:", show "Company / Archive" in their path and start with a gray 🗄️ status line. Treat them as history, never as the current answer.

Search is keyword only and returns about 50 results. Run 3 to 4 short searches with different words people would type, including synonyms and old names (for example "SOP", "stock options", "incentive program").

## Steps

1. **Classify.** Is the input wiki content or a working doc (1:1 notes, meeting notes, retro, plan, personal notes, WIP)? Working docs don't go into General. Tell the user where it belongs under "What doesn't go in General" in the standard, and stop.
2. **Duplicate check.** Search as above. If a page on the same topic exists, propose updating it instead of creating a new one. If two pages cover the same topic, propose which to keep and which to archive, with the reason. Keep the page the topic owner confirms. Until then, propose the most recently edited page that isn't a draft. Page views and creation date don't decide.
3. **Split.** One topic, one page. If the input covers several topics, propose a hub page plus content pages. Only add layers when the input really has several topics.
4. **Rewrite to the standard.** Page type, structure top to bottom, writing rules. Never invent facts. Anything missing or unclear becomes `[TO CONFIRM: what is missing]` in the draft.
5. **No-AI-slop pass.** Run the no-ai-slop skill in edit mode on the draft. Keep facts, names and numbers exactly as they are.
6. **Check against the standard.** Go through the checklist below. `[TO CONFIRM]` never gets published. Before publishing, either the user answers it, or the skill writes a neutral sentence (or leaves the line out) and moves the question to "Questions for the owner" in its output. The person running the skill sends those questions to the owner in Slack. Once the review bot runs (Part 1c), it adds open questions to the owner's review message. Never ask in Notion comments: on Plus they can't be resolved or deleted through the API, so they would stay forever.
7. **Preview, then publish.** Show the full draft. Write to Notion only after the user confirms. In review mode, update the existing page. In write mode, create it under the parent the user names.

## Checklist

- Page type is clear: hub, content, link or archived.
- Title uses words people search for. Old name in a "Formerly called" line if people still use it. Archived pages: title starts with "Archived:".
- Status line callout right under the title, in the exact format below. The page icon is free for the topic and never shows the status.
- Brief summary answers the main question in 2 or 3 sentences: a callout on content pages, a plain paragraph on hubs.
- "On this page" label and table of contents only on content pages with 4+ H2 sections. Never on hub pages. H2 only. Every H2 starts with one emoji that fits the section. Lines naming a role, step or option may start with an emoji instead of a bullet (plain paragraph, never `- ` plus emoji). Lists of facts stay plain bullets. Never ✅ ⚠️ 🗄️ outside the status line.
- Every section makes sense on its own.
- One gray Notion icon as page icon (format `icons/<name>_gray`), never a status emoji. Cover only on hub pages (the Apify pattern). Callouts only for status, brief summary and reader warnings.
- Hub page: status line, then `<columns>` with ratio 44 and 56 (set by hand on Company, so the summary and callouts don't get too wide). Left: `###` group labels, `<page>` blocks, `---` between groups. Right: **Brief summary.** paragraph. No database views on a hub: the registry is for admins. No links that lead outside the workspace. Only the wiki home page (Company) adds: vision as `>` quote, then three callouts with gray Notion icons: "New at Apify? Start here" (blue_bg, numbered, up to 3 mentions), "What's new" (gray_bg, dated bullets newest first, each with a mention, only facts already on the linked page), "Can't find something?" (gray_bg, who to ask). No callouts except the status line. No archived pages in the groups, only the Archive page.
- Hub page titles: if a subpage title doesn't say what's on the page, list it under "Decisions needed" as a rename for that subpage. Don't fix it with text on the hub.
- No `[TO CONFIRM]` left in the published text, and no questions in Notion comments.
- Links are Notion mentions, never "see the X page" in plain text.
- Absolute dates, full names with role or channel, acronyms spelled out on first use.
- Images: content written as text, or one sentence under the image saying what it shows.
- No TODOs, no "WIP", no notes to self.
- Related pages: up to 5, at the end. Optional on hub pages.

## Status line

The review bot from Part 1c parses this line. Write it exactly like this, one line, in a callout:

```
Up to date · Owner: Full Name, Team (Slack: @handle) · Last reviewed: YYYY-MM-DD
```

A page nobody has checked yet: `Needs review · Owner: Full Name, Team (Slack: @handle) · Last reviewed: not yet`.

An archived page: `Archived · Replaced by: <mention-page> · Archived: YYYY-MM-DD`, and a second line in the same callout: "This page is out of date. Use the page that replaced it." Never use the word "current" in this line: keyword search matches it to every "current X" question.

An outdated page that nothing replaced: `Archived · No replacement · Archived: YYYY-MM-DD`, and a second line: "This page is out of date. Ask the People team before you use it."

Archiving never deletes text. Add "Archived: " to the start of the title (once, check it isn't there already), add the archived callout at the top, keep the old text under it, and move the page under the Archive page. Delete plain-text pointers like "see X instead": the callout already links the replacement.

| Status | Callout icon | Callout color |
|---|---|---|
| Up to date | ✅ | green_bg |
| Needs review | ⚠️ | orange_bg |
| Archived | 🗄️ | gray_bg |

Don't use ✅, ⚠️ or 🗄️ as a page icon, so the icon can't be mistaken for a status.

The skill writes the status line only when it creates a page or when the page has none. After that, only the review bot changes it. A page with no owner named by its team gets `KNOWLEDGE_OWNER` and status Needs review, until the team leader names one.

## Review mode output

1. **Problems found.** One line each: what is wrong, which rule it breaks. Group by: content, structure, links, for Claude.
2. **Questions for the owner.** Every open `[TO CONFIRM]` as one short question, ready to paste into Slack. Include the page link.
3. **Rewritten page.** Full text, ready to publish.

## Notion syntax

- Callout: `<callout icon="✅" color="green_bg">text</callout>`
- Table of contents: `<table_of_contents/>`
- Page link: `<mention-page url="https://app.notion.com/p/<id>"/>`
- Keep child pages as `<page url="...">Title</page>` when rewriting a parent page, or Notion deletes them.
- Before writing, fetch the page again and edit with the smallest change that works.
