# Part 1a: Diagnose

## Most of what people read is pages nobody updates

21 of the 35 most-read pages weren't edited for over a year. They get 33% of all views. The 14 that someone keeps updated get 19%.

| Group | Share of pages | Share of views |
|---|---|---|
| Most-read, not updated for 1 year+ | 14% | 33% |
| Less-read, not updated | 12% | 8% |
| Most-read, updated | 9% | 19% |
| Less-read, updated | 11% | 8% |
| Working docs | 47% | 10% |
| Hub pages | 6% | 21% |

154 pages from the inventory export, 1 October 2026. 20,810 views in 90 days. Most-read means 200+ views.

## What's wrong

26 of the 35 most-read pages have at least one of these problems.

### 1. Many topics have 2 to 4 pages that say different things

- Travel has 4 pages. Time off, expenses, onboarding and the sales playbook have 3 each.
- The most-read version often sits in someone's Personal space. Brand guidelines there has 410 views, the Marketing one 138.
- Asked about the meal allowance abroad, Claude can quote 45 EUR from a 2023 FAQ. Our plan has no date filter, so it can't tell which page is newer.

### 2. No page says who owns it or when someone last checked it

- The only date on the example pages is "Last updated: March 2023". Nobody can tell if a page is still true, and neither can Claude.
- 23 pages were last edited by someone who left. Among them: Refund policy (347 views), Onboarding checklist - Engineering (320), Holiday & sick leave (260).
- The export can't tell us owners either. `created_by` changes when a page moves: Plan Q2 2026 was "created" by someone who left in 2023.

### 3. Private working docs fill the company wiki

- 51 working docs (1:1s, meeting notes, retros, plans) sit in General.
- 6 of 10 1:1 notes are in General, open to all 250 people. That's a privacy problem.
- Claude's search returns about 50 results per query. Meeting notes push the policy pages out.

### 4. Entry pages and titles don't lead to the answer

- The two most-visited pages, Office (829 views) and Engineering (771), are bare lists of links.
- The Company hub puts brand, OKRs, the office move, sports and travel all under "People".
- People type "stock options", the page is called "SOP". Claude's keyword search misses it too. Other titles: "Notes", "Untitled", "Project: API" (3 pages).

### 5. Old and retired text still reads as current

- Brand foundations [retired] keeps the full old text and doesn't link to the page that replaced it.
- The office page still describes a construction site two months after the move. Pages name three offices: Lucerna, Karlin, 100Yards.
- "Currently", "right now" and "soon" have no date. Claude reads them as today.

### 6. Pages assume the reader already knows the context

- Core values examples is 16 screenshots and 40 words. Claude only gets the 40 words.
- "See the Travel policy" with no link. Which of the 4?
- "Ask Tomáš", "I send this to everyone", "Depends on the program version". No last name, no author, no actual answer.

## What to fix first

1. Competing versions of the most-read pages.
2. An owner for every page people read.
3. 1:1s and meeting notes out of General.
4. One page format: owner and review date in the text, real links, text instead of screenshots.
5. Everything else, flagged by the automation.

At 25,000 pages we start from what people read. The views export shows the most-read pages, and about 30 of them become key pages. Working docs move in bulk by title pattern. A person only reads the key pages.

## The 35 most-read pages and their problems

Sorted by number of problems. "In Personal": the page sits in one person's private space, not in General. You can't find it by browsing, and it has no owner once that person leaves.

| Page | Views 90d | Not edited 1 yr+ | Last editor left | Competing version | In Personal |
|---|---|---|---|---|---|
| Onboarding checklist - Engineering | 320 | 23 months | ✓ | ✓ |  |
| Holiday & sick leave | 260 | 20 months | ✓ | ✓ |  |
| Brand guidelines | 410 |  |  | ✓ | ✓ |
| Vacation & time off | 394 | 28 months |  | ✓ |  |
| Refund policy | 347 | 14 months | ✓ |  |  |
| Referral bonus | 311 | 18 months |  | ✓ |  |
| Expense policy | 279 | 14 months |  | ✓ |  |
| Core values examples (screenshots) | 220 | 36 months | ✓ |  |  |
| Travel Policy (NEW) | 210 |  |  | ✓ | ✓ |
| NDA template | 398 | 16 months |  |  |  |
| Parental leave | 387 | 18 months |  |  |  |
| Budget process | 382 | 24 months |  |  |  |
| All Hands archive | 365 | 20 months |  |  |  |
| How we work | 364 | 12 months |  |  |  |
| Vision, mission & strategy | 362 | 27 months |  |  |  |
| Office guide 100Yards | 361 |  |  | ✓ |  |
| Performance review guide | 354 | 24 months |  |  |  |
| PRD template | 343 | 27 months |  |  |  |
| Dev environment setup | 337 | 14 months |  |  |  |
| Home office policy | 332 | 13 months |  |  |  |
| Desk booking | 320 | 25 months |  |  |  |
| Hiring process | 316 | 22 months |  |  |  |
| Sales playbook | 314 |  |  | ✓ |  |
| Parking | 301 |  |  | ✓ |  |
| Data processing agreements | 258 | 24 months |  |  |  |
| Release process | 215 | 12 months |  |  |  |
| Feedback guide | 373 |  |  |  |  |
| Code review guidelines | 306 |  |  |  |  |
| Webinar playbook | 283 |  |  |  |  |
| Feature launch checklist | 265 |  |  |  |  |
| Blog style guide | 264 |  |  |  |  |
| Multisport card | 260 |  |  |  |  |
| Incident postmortem template | 247 |  |  |  |  |
| CRM hygiene rules | 231 |  |  |  |  |
| Offboarding checklist | 200 |  |  |  |  |

## Who should own what

81 wiki pages by the team whose space they sit in. Working docs are left out: they move out of the wiki instead of getting an owner. First proposal: each team leader confirms it and names one owner.

| Owner team | Pages | With a problem | Views on problem pages |
|---|---|---|---|
| People | 20 | 16 | 3,483 |
| Engineering | 11 | 8 | 1,396 |
| Leadership | 10 | 7 | 1,423 |
| Office | 7 | 6 | 1,223 |
| Sales | 7 | 3 | 434 |
| Finance | 6 | 3 | 716 |
| Product | 6 | 3 | 559 |
| Marketing | 6 | 2 | 548 |
| Legal | 4 | 3 | 715 |
| Customer Success | 4 | 2 | 473 |

## About the data

154 pages is a sample, so the numbers show a pattern to check on all 25,000. `created_by` isn't reliable. Page views probably don't count reads by Claude through the API.
