# Flash-Tattoo-Giveaway
### Purpose: Develop a random username selector for an online ig flash tattoo giveaway that falls within giveaway requirements/parameters.

This is to ensure that users are fairly picked at random.

## Constraints:
This section documents the rules the draw will enforce, what the input data structure must look like, and what this tool intentionally excludes.

### Eligibility Rules (what qualifies as an entry)
An entry is one comment that introduces at least one NEW tagged friend for the commenting username. More comments = higher odds; there is no cap.

- The comment's author must not be an already-specified ineligible handle (Sapphic Weekly ATX members, tattoo studio, and tattoo artist)
- The comment must tag at least one handle the author has not tagged before in any earlier comment
- Self-tags do not qualify -  tagging your own handle earns nothing.
- Tags of blocked handles do not count - tagging only Sapphic Weekly ATX members, tattoo studio, and tattoo artist
- Multiple tags in one comment still count as one entry. The unit of entry is the comment, not the tag.
- Re-tagging a previously tagged friend does not qualify
- Each author's comments are processed oldest to newest

### Input constraints (what the tool expects)
- Input is a JSON array of comment objects from third-party tool Apify to perform a web scrape of a specific IG post (collects all surrounding data for this post: likes, saves, reposts, comments, etc.)
- Each object needs ownerUsername, text, and timestamp. Apify export shapres are accepted.
- Replies will be excluded at scrape time.
- Handle matching is case-insensitive, leading/trailing dots are trimmed; usernames are matched as [A-Za-z0-9._]
- Ticket counts depend on accurate timestamp values. Missing or wrong timestamps change the oldest to newest ordering and thus which comment first "introduces" a friend

## Fairness and determinism
- The winner is chosen with crypto.getRandomValues and rejection sampling, giving a uniform distribution with no modulo bias
- Draws are independent and not seeded
- The full list of eligible entrants and each person's ticket count is displayed before drawing for transparency
- The tool runs entirely client-side. No data is uploaded, stored, or logged, and reloading the page clears all state.
