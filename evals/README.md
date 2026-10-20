# Before and after test

10 typical employee questions, with the right answer. I wrote them from the example pages, because the brief has no real questions from employees. Claude answered each one through the Notion connector before and after fixing the Company subpages. Open questions that only a page owner can answer are in [questions-for-owners.md](questions-for-owners.md).

Date: 2026-10-19, after fixing the Company subpages. Same method as the before test: one keyword search per question (Notion connector, whole test workspace), answer from the top results the way an agent would.

| # | Question | Search | Correct answer | What Claude finds | Before | After |
|---|---|---|---|---|---|---|
| 1 | What's the daily meal allowance abroad? | daily meal allowance abroad | 50 EUR | Top 3: Travel policy (archived, 50), Travel policy 2023 (archived, 45), Business travel policy (50). Archived pages point to Business travel policy | Conflicting | Correct |
| 2 | Who approves a business trip? | business trip approval | Team leader, request in #travel-requests | Top hit Business travel policy: team leader, #travel-requests | Conflicting | Correct |
| 3 | What's the office address? | office address | 100Yards, Prague 1 (no street address on any page) | Top hit still the archived Karlín guide, but its status line sends the reader to Office at 100Yards. Hit 2: 100Yards, Prague 1 | Wrong | Correct |
| 4 | How do stock options work? | stock options | Employee stock options (SOP) | Top hit Employee stock options (SOP) | Wrong | Correct |
| 5 | When do I get my equity grant? | equity grant vesting | After probation, usually next quarter | Found, clear answer, but the page still warns the 2025 changes are missing | Unreliable | Unreliable |
| 6 | What are our values? | company values | Open, Driven, Responsible, Flexible, Team | Core values | Correct | Correct |
| 7 | How do OKRs work? | OKRs | OKRs page | OKRs page | Correct | Correct |
| 8 | Where are the current OKRs? | current OKRs | Q4 2026 | OKRs page, Q4 2026. Then 5 archived pages (see side findings) | Correct | Correct |
| 9 | What's the Apify one-liner? | Apify one-liner | Not decided (brand owner question open) | Brand guidelines (personal) and Brand foundations (archived), two different one-liners | Conflicting | Conflicting |
| 10 | Where do I find sports groups? | sports groups | Free-time activities and sports | Free-time activities and sports | Correct | Correct |

**Before: 4 correct, 1 unreliable, 3 conflicting, 2 wrong.**
**After: 8 correct, 1 unreliable, 1 conflicting, 0 wrong.**

The two that are left aren't a page-format problem. They wait for an owner: the 2025 SOP changes (People team) and the valid one-liner (Brand). The page format can't fix missing facts. The review message to the owner can.

## What this test can and can't show

We can't fully verify the right answers yet, because no page owner has confirmed them. So this test is less precise than a real one on verified questions. Read 4 and 8 as a direction, not a score.

- **I wrote the questions and the right answers myself**, from the pages in the test workspace. No owner at Apify has confirmed them yet, and some of them wait for an owner's answer ([questions for owners](questions-for-owners.md)).
- **Each question ran once, in one wording.** Claude doesn't always answer the same way, and people ask the same thing in different words.
- **The workspace is a copy I built**, with 10 Company pages. The real wiki has 25,000 pages, so search results there will look different.

How I'd test it for real, in the pilot:

1. **100 verified questions.** We write them with AI, about 3 per key page, in the words people use, not the words on the page.
2. **The owner confirms each right answer** before a question goes into the test. Not me, not Claude.
3. **Each question in 3 wordings, each run 3 times.** A question counts as right when at least 2 of 3 runs match the owner's answer, in every wording.
4. **The real setup.** The same Claude and Notion connector employees use, on General. Once in week 1, once in the last week. The target is 95 of 100 ([pilot plan](../docs/part-2-adoption.md)).
5. **After the pilot the questions stay.** The test runs again every month, and when a page changes, its owner updates the right answer.

## Side findings

- **Our archive sentence matches "current".** Every archived page says "Don't use this page as the current answer." So "current OKRs" returns 5 archived pages right after the right one. We added a keyword collision while removing another. Fix: reword without "current".
- **Archived pages still rank first.** Archiving keeps the old text, so keyword ranking doesn't change. Questions 1 and 3 came out right only because the agent opened the page and read the gray status line. An agent that answers from the search snippet would still say Karlín.
- **The test workspace has no General filter.** That's why the personal Brand guidelines page ranks first on question 9. In the real setup the skill searches General only and the personal page drops out.
- **Working docs still say "our current office in Lucerna".** They're out of Company now, so in the real setup only the team sees them. Here they still show up in search.

## Fix and retest (2026-10-19, same day)

Changes:
- The 5 archived pages got "Archived:" at the start of the title.
- The archive line now says "This page is out of date. Use the page that replaced it." No "current".
- Standard (Notion page) and wiki skill updated to v2 with both rules.
- Brand foundations: deleted the plain-text "Please see Apify brand essentials instead". The callout already links it.

Retest of questions 1, 3 and 8:

| # | Search | Result |
|---|---|---|
| 1 | daily meal allowance abroad | Same order, but the 45 and 55 EUR hits now read "Archived: Travel policy 2023" and "Archived: Travel Policy (NEW)" in the result list. Business travel policy is the only non-archived hit. |
| 3 | office address | Top hit is now "Archived: Office guide (Karlin office)". An agent answering from the result list sees it's archived without opening it. |
| 8 | current OKRs | Archived pages in results: 5 before, 1 after (Brand foundations, matched by its old text "we are currently updating", which archiving keeps on purpose). |

Archived pages still rank where they ranked. The title prefix doesn't push them down, it labels them. Getting them out of results entirely would mean moving the Archive out of General, and then nobody could look up an old rule. We chose the label.
