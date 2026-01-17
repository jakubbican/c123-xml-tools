# Race Combinator

Combines results from multiple canoe slalom races into unified rankings for combined event awards.

**Live tool:** https://opencanoetiming.github.io/c123-xml-tools/race-combinator/canoe-race-combine.html

## What It Does

Creates combined standings by pairing categories from different races (e.g., Day 1 + Day 2, or Course A + Course B).

**Ranking calculation:**
1. Primary: Sum of placements from both races (1st + 3rd = 4 points)
2. Tiebreaker: Sum of times from both races

**Special handling:**
- If a competitor has two runs (BR1 + BR2), only the better/final result (BR2) is used
- Missing results count as rank 999
- Age categories are automatically determined from competitor birth year

## How To Use

1. **Upload XML files** - drag & drop one or more XML files from Canoe123
2. **Pair categories** - select matching categories from both file lists (e.g., "C1M Day 1" + "C1M Day 2")
3. **Generate results** - view combined standings with overall and age category rankings
4. **Export** - copy tables to clipboard for Excel

## Output

For each paired combination:
- **Overall ranking table** - all competitors sorted by combined rank
- **Age category tables** - separate rankings for each age group (U23, Senior, etc.)

Columns include: rank, age category rank, bib number, name, year, club, individual race results, and combined totals.

## Technical Notes

- Works entirely in your browser (no server)
- Supports multiple XML files from different events
- XML format details: see [c123-protocol-docs](https://github.com/OpenCanoeTiming/c123-protocol-docs)
