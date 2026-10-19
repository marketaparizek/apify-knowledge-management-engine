# Part 1b: Fix

## Same 10 questions to Claude. Right answers went from 4 to 8.

I wrote down how a wiki page should look, built a Claude skill that rewrites pages by those rules, and used it to fix the Company page and its 9 subpages.

- **The rules:** [How to write a page in the Apify wiki](https://app.notion.com/p/214ab6e4e96382a0a92e819d3eb0d1be), one Notion page.
- **The result:** [Company and its subpages](https://app.notion.com/p/dcdab6e4e9638394b69e8124566358a4), fixed by the rules.
- **The skill:** [skills/apify-wiki](../skills/apify-wiki), Claude skill that applies the rules.

## What every key page looks like now

- **Owner and review date at the top.** Anyone, person or Claude, can see if the page is still true and who to ask.
- **A short summary first.** 2 or 3 sentences that sum up the topic. Claude reads a page from the top.
- **One topic, one page.** Old versions are archived, not deleted. Their title starts with "Archived:", so Claude sees it in search results without opening them.
- **Plain text Claude can read.** Real links instead of "see the travel policy", full names, real dates, text instead of screenshots.

## What the skill fixes, and what it asks the owner

The skill fixes what it can check in the wiki. Facts it can't check go to the page owner as a question. On Company that was 34 questions ([list](../evals/questions-for-owners.md)).

| Problem | What the skill does | Fixes | Asks |
|---|---|---|---|
| No owner, no date. Nobody can tell if the page is still true. | Adds the owner and review date at the top. | ✓ | |
| The title isn't what people search for, like "SOP" for stock options. | Renames the page to the words people type. | ✓ | |
| The point is buried in a long intro. | Writes a short summary at the top. | ✓ | |
| Two or more pages on one topic say different things. | Archives the old ones with a link to the new one. Asks which is valid when it isn't clear. | ✓ | ✓ |
| "See the travel policy", "ask Tomáš", "currently". | Real link, full name, real date. Asks when it can't find them. | ✓ | ✓ |
| Screenshots Claude can't read. | Writes the content as text. Asks what the image shows when it can't tell. | ✓ | ✓ |
| Missing facts, like the office address or what changed in 2025. | Never guesses. Asks the owner. | | ✓ |

## Did it work

10 questions employees really ask. Claude answered each one through the Notion connector, before and after the fix.

| Question | Right answer | Before | After |
|---|---|---|---|
| What's the daily meal allowance abroad? | 50 EUR | Two pages say different things | Right |
| Who approves a business trip? | Team leader, request in #travel-requests | Two pages say different things | Right |
| What's the office address? | 100Yards, Prague 1 | Wrong | Right |
| How do stock options work? | Employee stock options (SOP) page | Wrong | Right |
| When do I get my equity grant? | After probation, usually next quarter | Right, but the page warns it may be outdated | Right, but the page warns it may be outdated |
| What are our values? | Open, Driven, Responsible, Flexible, Team | Right | Right |
| How do OKRs work? | OKRs page | Right | Right |
| Where are the current OKRs? | Q4 2026 | Right | Right |
| What's the Apify one-liner? | Not decided yet | Two pages say different things | Two pages say different things |
| Where do I find sports groups? | Free-time activities and sports | Right | Right |

**Before: 4 of 10. After: 8 of 10.**

The 2 that are left wait for a person, not a format: the 2025 changes to stock options (People team) and which company one-liner is valid (Brand). The review bot sends these questions to the owners.

Test workspace, 19 October 2026. One keyword search per question, answer from the top results, the way an agent works. Full results and side findings: [evals](../evals/README.md).

## The skill

- You give it a Notion link, or any text: a Slack thread, a Google Doc, notes.
- It looks for existing pages on the same topic first, so it doesn't create a duplicate.
- It rewrites the page by the rules and shows a draft. It changes Notion only after a person says yes.
- Anything it doesn't know becomes a question for the owner, never a guess on the page.
- The rules live in one file. To change how pages look, People edits the rules, not the skill.

## At 25,000 pages

Nobody reads 25,000 pages. We sort them by what we can see without opening them: the title, where the page sits, when someone last edited it, and how many people read it.

1. **Rules sort most pages.** A title like "1:1 notes", "Retro" or "Meeting notes" means a working doc, and it moves out of General. In the sample, the title alone caught half of all pages.
2. **Pages nobody reads go to the archive.** No reads in 90 days and no edit in a year puts a page on a monthly list. The Notion admin approves the list, then the bot archives the pages. Any page can come back. Automated in Part 1c.
3. **Claude reads only what the rules can't decide.** A few hundred pages, not 25,000.
4. **Team leaders confirm, they don't sort.** They get a ready proposal for their team's pages and reply only when something should stay.
5. **Key pages come from questions.** The 30 questions people ask most in Slack point to about 30 pages. I fix those with the skill, and each owner checks the facts.

Not automated on purpose: the skill never publishes alone, the bot never archives without the admin's yes, and nobody rewrites pages that nobody reads.

Shares are from the 154-page sample, so they show a pattern, not exact numbers. Page views aren't in the Notion API, so the archive list needs a views export like the one in this case study.
