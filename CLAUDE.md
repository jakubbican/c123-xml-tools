# Claude Code Instructions - C123 XML Tools

## Project

C123 XML Tools - collection of simple tools for working with XML files from Siwidata's Canoe123 system.

**GitHub:** OpenCanoeTiming/c123-xml-tools | **License:** MIT

---

## Paths and Documentation

| Purpose | Path |
|---------|------|
| **This project** | `/workspace/timing/c123-xml-tools/` |
| **Protocol docs** | `../c123-protocol-docs/` |
| **XML format** | `../c123-protocol-docs/c123-xml-format.md` |

---

## Language

- User communication: **Czech**
- Documentation (README, docs): **English**
- Code, comments, commit messages: **English**

---

## Structure

```
c123-xml-tools/
├── penalties-quality-analyzer/
│   ├── penalties-quality-analyzer.html   # Standalone HTML tool
│   └── readme.md                         # Documentation
├── race-combinator/
│   ├── canoe-race-combine.html           # Standalone HTML tool
│   ├── docs.md                           # Detailed documentation
│   └── readme.md                         # Basic info
├── LICENSE
└── README.md
```

---

## Tools

### penalties-quality-analyzer
Analyzes quality of entered penalties in C123 XML file.
- Detects inconsistencies and errors
- Standalone HTML - open in browser, drag & drop XML

### race-combinator
Combines multiple race XML files into one.
- Merging results from multiple rounds/days
- Standalone HTML - open in browser

---

## Usage

All tools are standalone HTML files:
1. Open `.html` file in browser
2. Drag & drop XML file(s) from Canoe123
3. Download or copy result

---

## Development

Tools use vanilla JavaScript with no dependencies.
For testing, just open HTML in browser.

```bash
# Local server (optional)
npx serve .
```

---

## Commit Message Format

```
feat: add new validation rule for gate penalties
fix: correct XML merge for overlapping runs
docs: update race-combinator documentation
```

---

*XML format reference → see `../c123-protocol-docs/c123-xml-format.md`*
