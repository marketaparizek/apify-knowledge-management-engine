# How to write a page in the Apify wiki

Copy of the Notion page https://app.notion.com/p/214ab6e4e96382a0a92e819d3eb0d1be (2026-10-19, v6). When the Notion page changes, copy it here again.

**Brief summary.** Every page in General, the Notion teamspace every Apifier can see, covers one topic, shows whether it is up to date and who owns it, and works for both people and Claude. Claude finds pages by keyword search and reads one page at a time, so the title and this summary decide whether a page gets found. Core pages, the roughly 30 most-read pages, also get a named owner and a review every 3 months.

## 🗂️ Four types of pages

- **Hub page.** The entry page for an area, like Company or Office. It has a status line and a brief summary, then its subpages grouped under H2 headings by topic. A hub has two columns. The left column (a bit under half the width) is the navigation: H3 group labels, the subpages under each, a divider between groups, titles only. The wide right column holds the brief summary as a plain paragraph starting with bold "Brief summary.". Links that lead outside the workspace don't go on a hub. The wiki home page (Company) is the one hub with more: the vision as a quote, then three callouts. "New at Apify? Start here" (blue) lists up to 3 pages to read first. "What's new" (gray) lists dated changes, newest first, each with a link to the page that has the details. "Can't find something?" (gray) says who to ask. The People team keeps "What's new" current. Other hubs don't get these, because nobody would keep ten news lists true. If a title doesn't tell the reader what's on the page, rename the subpage, don't add text to the hub.
- **Content page.** Answers one group of questions, like business travel. Most pages are this type. A content page sits at most two levels below a hub page.
- **Link page.** Summarises a document that lives in GitHub or Google Drive and links to it. If the link page and the source differ, the source is right.
- **Archived page.** A page that another page replaced, or that is out of date and nothing replaced. It moves under the Archive page and keeps its old text. Its title starts with "Archived:", so people and Claude see it in search results without opening the page. A gray 🗄️ status line at the top says which page replaced it and when. Claude looks in archived pages last, and when it answers from one, it says so.

## 🧱 How a page is built, top to bottom

1. **Title.** Use the words people type when they search. ✓ How to get an invoice approved. ✗ Invoices v2 FINAL. If people know the page by an old name, add one line under the title, like "Formerly called SOP."
2. **Status line.** A callout right under the title. Its emoji shows the status. The page icon stays free for the topic of the page.
   - ✅ Up to date: reviewed in the last 3 months
   - ⚠️ Needs review: the last review is older than 3 months
   - 🗄️ Archived: another page replaced this one, or the page is out of date and nothing replaced it
   A page nobody has checked yet says "Last reviewed: not yet" and stays ⚠️ Needs review. An archived page says "Archived · Replaced by: [page] · Archived: YYYY-MM-DD" and, on a second line, "This page is out of date. Use the page that replaced it." Don't use the word "current" there: keyword search would match it to every question about what is current. An outdated page that nothing replaced says "Archived · No replacement · Archived: YYYY-MM-DD" and "This page is out of date. Ask the People team before you use it."
   The wiki skill adds the status line when it creates a page. After that, only the review bot changes it. Format: `Up to date · Owner: Full Name, Team (Slack: @handle) · Last reviewed: YYYY-MM-DD`
3. **Brief summary.** A callout with 2 or 3 sentences that answer the main question (on a hub page, a plain paragraph instead of a callout). A reader who stops here still has the right answer. If a rule applies only to some people, say who.
4. **On this page.** Only on content pages with 4 or more sections, never on hub pages. Bold "On this page" label and the table of contents block. H2 headings only.
5. **Sections.** One H2 heading per question, named after what the section answers. Each section has to make sense alone.
6. **Related pages.** Up to 5 links at the end.

## ✏️ Writing rules

- **Short.** Short sentences, everyday words, answer first. Delete sentences that don't help the reader act or understand.
- **Full sentences.** ✓ "Jana Nováková from Finance approves invoices within 5 working days." ✗ A table full of abbreviations.
- **Who does what.** ✓ "Finance pays the invoice." ✗ "The invoice gets paid."
- **Dates.** ✓ "Since 1 September 2026." ✗ "currently", "soon", "right now"
- **People.** ✓ "Ask Tomáš Král (Office manager, #office)." ✗ "Ask Tomáš."
- **Links.** ✓ A Notion mention. ✗ "See the Travel policy." ✗ "See above."
- **Acronyms.** Spell out every acronym on first use.
- **Images.** Write the content as text. If an image stays, add one sentence under it that says what it shows.
- **Filler.** Cut "just", "actually", "basically", "in order to", "it's worth noting", "leverage".
- **Formatting.** Numbered lists for steps, bullets for options, sentences for explanations. Tables only for lookup data. Start every H2 heading with one emoji that fits the section, so the page is easy to scan. Bullets that name a role, a step or an option can start with an emoji too. Lists of facts or criteria stay plain. Never use ✅, ⚠️ or 🗄️ outside the status line.

## 🎨 Icons, covers and callouts

- **Icon.** Every page has one gray Notion icon for its topic, like the airplane for travel (Notion icon picker, Icons tab, gray). Colour emoji make a hub look busy. Never ✅, ⚠️ or 🗄️, because those show the status. The icon shows in the sidebar, in search results and in every link, so it helps people spot the page.
- **Cover.** Only hub pages have a cover, and all hubs use the same Apify pattern. Content pages have no cover, because it pushes the answer one screen down.
- **Callouts.** Use them for three things only: the status line, the brief summary, and a warning that applies to the reader. The wiki home page adds its three reader callouts (see Hub page). Not for decoration or quotes.

## 🎯 One topic, one page

- One page answers one group of questions. "Business trips FAQ" and "Travel policy" are one topic.
- Split a page when parts have different readers or owners, or past 1,500 words.
- When two pages cover the same topic, keep one and archive the other.
- **Which page to keep:** the one the owner of the topic confirms. Until then, the candidate is the most recently edited page that isn't a draft. Page views and creation date don't decide: a draft can have more views than the valid policy.

## 🚫 What doesn't go in General

- **1:1 notes** go to your Private section, shared with the other person only.
- **Team meeting notes, retros and plans** go on one page in your team's area, with access limited to your team.
- **Time-limited pages,** like a pilot or a company-wide project, can go in General when the whole company needs them. Put the end date in the brief summary. When it ends, the owner adds the results to the page. Later the owner archives it through the Review queue.
- **The wiki skill and the review bot never use working docs or personal pages as an answer,** even when search finds them. They list them, so they can be moved out of General.

## 🔁 Reviews

- Every core page has a row in the Wiki registry (https://app.notion.com/p/046c9b6acf9949ecaccebd31179332b4) with its owner and the date of the last review.
- The review bot runs every Monday. 7 days before a review is due, the owner gets a Slack message with a link to the page and any open questions. If the review is overdue, the owner gets one more message.
- The owner fixes what changed and presses "Mark as reviewed" on the page's row in the registry, even when nothing changed.
- On its next run, the review bot sets the status to ✅ Up to date. If the last review is older than 3 months, it sets ⚠️ Needs review.
- The review bot also lists possible duplicates, pages with no edit in 12 months and working docs in the Review queue (https://app.notion.com/p/596932576a4f4df388ffeaeb9349ea80). The Notion admin decides what gets archived.
- Before you leave Apify or change teams, hand your pages to a new owner.
