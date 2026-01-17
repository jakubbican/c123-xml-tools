# C123 XML Tools

Collection of standalone web tools for working with XML files from Siwidata's Canoe123 timing system.

**Live tools:** https://opencanoetiming.github.io/c123-xml-tools/

## Tools

### [Penalties Quality Analyzer](penalties-quality-analyzer/)
Analyzes penalty correction patterns in race results. Helps identify problematic gates where ex-post corrections occur frequently - useful for evaluating judge positions and gate placements.

### [Race Combinator](race-combinator/)
Combines results from multiple races into unified rankings. Pairs categories from different days or courses, calculates combined standings by sum of rankings and times.

## Usage

All tools are standalone HTML files that run entirely in your browser:

1. Open a tool from the [live site](https://opencanoetiming.github.io/c123-xml-tools/) or download the HTML file
2. Drag & drop XML file(s) exported from Canoe123
3. View results and copy to clipboard for Excel

No server required. No data leaves your browser.

## XML Format

These tools work with XML files exported from Canoe123. For XML format documentation, see [c123-protocol-docs](https://github.com/OpenCanoeTiming/c123-protocol-docs).

## License

MIT
