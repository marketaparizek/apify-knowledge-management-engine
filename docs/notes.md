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

- The test workspace has no General teamspace, so search runs on the whole workspace. In the real setup the skill searches General only, and personal pages drop out.
- Two pages linked from Company ("How we work" and "Apify brand essentials") live outside the test workspace. A person opens them in the browser, Claude gets a 404 through the connector.
- Notion comments can't be resolved or deleted through the connector on Plus. That's why open questions go to owners in Slack, not into comments.
