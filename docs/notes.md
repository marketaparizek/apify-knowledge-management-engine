# Notes

## Time spent

| Part | Hours |
|---|---|
| 1a Diagnose | [fill in] |
| 1b Fix | [fill in] |
| 1c Build | [fill in] |
| 2 Adoption | [fill in] |

## AI tools and why

- **Claude in a claude.ai Project.** One place for the brief, the data and every decision. The project instructions include a "council" of five reviewers (automation engineer, AI retrieval, people lead, Engineering skeptic, hiring panel) that pushes back on each proposal.
- **Claude with the Notion connector.** Reads and edits the test pages, and runs the before and after test the same way an Apifier's Claude would.
- **The apify-wiki skill.** Built here, used to fix the Company subpages. Every rewrite was checked by hand, and mistakes went back into the rules.
- **no-ai-slop skill.** An editing pass on every page and deliverable.
- [fill in: anything else]

## Assumptions

- The owner of a core page is one person from the team whose area the page sits in. The team leader confirms. Until then, the fallback owner is me.
- Core pages are reviewed every 3 months.
- Page views in the export probably don't count reads by Claude through the API.
- `created_by` in the export isn't reliable: it changes when a page moves.

## Test workspace vs the real setup

- In the test workspace, the HQ teamspace stands in for General. Company and all wiki pages sit there.
- Two pages under Company copy the mess of the real wiki on purpose: "Personal pages (test setup)" and "Team working docs (test setup)". At Apify, both kinds sit in General. The skill and the bot have to skip them as answers and list them, and the test shows they do.
- Limiting search to General isn't enough at Apify: 51 working docs sit inside General. So the skill and the bot also skip working docs and personal pages by title and path, and list them instead.
- Two pages linked from Company ("How we work" and "Apify brand essentials") live outside the test workspace. A person opens them in the browser, Claude gets a 404 through the connector.
- Notion comments can't be resolved or deleted through the connector on Plus. That's why open questions go to owners in Slack, not into comments.
- The review bot runs as a Claude scheduled task under my account, so owner DMs come from me. In production it gets its own Slack and Notion account.
- The Slack workspace is a test workspace created for the demo.
