# Review bot (Part 1c, in progress)

Keeps core pages up to date after they are fixed.

Design so far:
- A registry database lists the core pages, with owner and last review date as properties. On Notion Plus, only database rows can have properties.
- Every 3 months the bot sends the owner a Slack reminder, together with any open questions about the page.
- The owner confirms "still true" in Slack. The bot sets the date and the status line. Nobody sets the status by hand.
- No confirmation and the last review is older than 3 months: the bot sets ⚠️ Needs review.
- Once a month the bot lists pages with no reads in 90 days and no edit in a year. The Notion admin approves the list, then the bot archives the pages.
- The bot has its own account ("Wiki bot"), not a person's.
