My feedback is below each point, labeled as Action.

## A. Factual errors (I'd fix these before publishing)

**1. "The only hole that averages under a stroke over par" (Hole 4 callout) is wrong.** Six holes do: #4 (+0.84), #11 (+0.86), #8 (+0.89), #6 (+0.94), #13 (+0.94), #1 (+0.98). Suggested replacement: "The one breather, and the only hole on the course that plays under four strokes."

Action: Change approved

**2. "The front nine's other par 5" (Hole 5 callout) is wrong.** The front has three par 5s: 2, 5, and 8. Suggest "One of three par 5s on the front, and the only one that plays a full stroke and a half over."

Action: No. 2 also averages more than 1.5 over. Suggest a more accurate note.

**3. "Only two rounds of triple-or-worse" (Slattery, feature trio) should be two *holes*.** Slattery had 2 triple-bogey-or-worse holes across 117 holes, not 2 rounds. As written it understates how good he was. Same error exists in the recap markdown file.

Action: Change approved. Fix in both files.

**4. "Most pars" leaderboard skips a player.** Third place should be Brett Barclift with 43, not Austin Isaacson with 39. Barclift isn't in the points-race division, which leads to the next item.

Action: Update to include all players. The only stat that should be contest-only players is the season points total. Everything else should be based on all 32 players.

**5. Leaderboard scope is undeclared and inconsistent.** "Best avg gross" and "Most birdies" draw from all 32 players; "Most pars" appears to draw from contest players only. Pick one and label it. My recommendation: use all 32 (the course stats are full-field anyway) and add a small line under the section head saying so.

Action: See action for #4

## B. Technical (publishing blockers)

**6. No `<!DOCTYPE html>`.** Without it browsers render in quirks mode, which can break `box-sizing` and throw off the whole layout. Also missing `<html lang="en">`, `<head>`, and `<body>`. Worth adding all four for a hosted page.

Action: Add missing code

**7. The scorecard will break on phones.** At a 360px viewport each hole column gets about 15px, but "4.98" at 15px monospace needs roughly 36px. The grid will overflow or squash. Two options: (a) wrap the card in a horizontally scrollable container with a subtle "swipe" affordance, or (b) at narrow widths, stack the nines as two rows of nine mini-tiles instead of a table. I'd go with (a) — it preserves the scorecard metaphor.

Action: Option (a) is approved. Make sure it aligns with the action for #13.

**8. No Open Graph or meta description tags.** If this gets shared in a group text or on social, it'll show a bare URL. Worth adding `og:title`, `og:description`, and ideally an `og:image`.

Action: Walk me through adding this content.

**9. Heading order jumps from h2 to h4** in the leaderboards and difficulty columns. Minor accessibility issue, trivial fix.

Action: Change approved

**10. Dead CSS.** The `.netbox` rule set (5 declarations) is left over from an earlier draft and is unused. The `.num` class on the snapshot tiles is also inert, since `.tile .tn` has higher specificity and overrides the font.

Action: Remove unnecessary code

## C. Aesthetics and accessibility

**11. Some heat-map cells fail contrast.** White text on the mid-greens (#728944, #648447, #517F4A) and on the orange #CF752C lands around 3.3:1 to 3.9:1, below the 4.5:1 AA threshold for text that size. Fix: switch those to dark ink text, or darken the swatches slightly. The gold and red cells are fine.

Action: Change the text. Do not change the swatches. They should remain in an appropriate gradient.

**12. The heat map encodes difficulty by color alone.** The numbers are printed in each cell, so it isn't a hard failure, but the difficulty *rank* (1–18) isn't shown anywhere on the card. Adding a small rank row, or rank as a superscript, would make the card readable without relying on color.

Action: Add a Rank row under the average score.

**13. The scorecard is built from divs.** It's genuinely tabular data, so a real `<table>` with `<th scope>` would read correctly in a screen reader and would also make the mobile scroll fix easier.

Action: Sounds good. Change approved. Make sure this aligns with actions in #7.

**14. `.eff .ev` uses a float** for the big number. It works, but a two-column grid would be more predictable if you ever edit that text.

Action: I'm not sure what this means. Explain it before making any changes.

## D. Content and editorial

**15. Hole 11 is the biggest interpretive problem on the page.** Golf Genius scored it as a par 4, so it shows as one of the easiest holes. But if it actually played as a par 3 most of the season, a 4.86 average is nearly two over par, which would make it the *hardest* hole on the course. Right now the page presents the artifact as a finding, with the footnote quietly contradicting the headline. My recommendation: pull #11 out of "Most forgiving," promote #6 or #13 (both +0.94) into that slot, and give #11 its own note in the strip explaining the construction and why its numbers can't be compared to the rest. That turns a data problem into one of the more interesting stories on the page.

Action: No. 4 played more like a par 3.5 most of the season. Promote No. 6 and 13 and make a note about No. 4. Hopefully, it's a one-year problem, as the work on the tee is complete.

**16. Your two aces are verifiable in the hole data, and one is a nice tie-in.** Hole 9 and hole 12 each show exactly one eagle, matching the two holes-in-one. That means Joey Desimone's only eagle of the season *was* his ace, and one of Dennis McNicholl's two was his. Worth noting in the "Most birdies or better" or "Most eagles" blocks. It also connects to Desimone's "Great swing, no hardware" panel: he had the ace and still finished 23rd.

Action: What are the specific changes you are recommending?

**17. "Rarely a disaster" on hole 12 is a stretch.** 32% of scores there were double bogey or worse. It's below the league average of 35%, so the claim is defensible, but "rarely" oversells it. Suggest "Seldom a par, seldom a disaster, almost always a bogey" or just cut the clause.

Action: Change approved.

**18. The points system is never explained.** A reader outside the league won't know what 67 points means. One line would fix it: "10 points for a win, then 8-7-6-5-4-3-2, and a point for everyone else. Ties broken by the USGA system."

Action: Addition approved.

**19. The 26-of-32 context disappeared** when that tile was replaced. The points race now presents standings with no indication that not everyone competes. Suggest folding it into the points-race intro rather than restoring a tile.

Action: Addition approved, but it shoudl be a minor footnote. Nobody cares very much, but it should be recorded for accuracy.

**20. No mention of the weekly contests.** The World Cup Challenge was new for 2026, and there's Ringer, Circle 5, Longest Putt, and Closest to the Pin. A slim strip listing the season's contests, even without winners, would round out "Season in Numbers." Needs data you haven't given me yet.

Action: Great suggestion. There is a screenshot with all of the weekly standings and contest winners from our weekly email and another from my prize spreadsheet. You might be able to get more content out of email screenshot. Tell me before adding any sections to the recap page.

**21. Two small wording items.** "Bar one" in the snapshot intro reads British; "with one exception" is plainer. And the hole 11 explanation now appears twice, in the callout and the footnote, so one can be trimmed.

Action: Changes approved. Reword and trim as necesary.

**22. Prize detail is missing.** The $72 coupon to 35x70 Golf Co. is a nice concrete closer for the footer if you want it public.

Action: Let's add the 35x70 logo and a link to their website in the area suggested. Let me know if you can't get their logo from the website: https://35x70golfco.com/. Also, thank the owners by name, Katy and Dan Winters.