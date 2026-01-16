# Claude Code Instructions - C123 XML Tools

## Projekt

C123 XML Tools - kolekce jednoduchých nástrojů pro práci s XML soubory systému Canoe123 od Siwidata.

**GitHub:** OpenCanoeTiming/c123-xml-tools | **Licence:** MIT

---

## Cesty a dokumentace

| Účel | Cesta |
|------|-------|
| **Tento projekt** | `/workspace/timing/c123-xml-tools/` |
| **Protokol docs** | `../c123-protocol-docs/` |
| **XML formát** | `../c123-protocol-docs/c123-xml-format.md` |

---

## Jazyk

- Komunikace a dokumentace: **čeština**
- Kód, komentáře, commit messages: **angličtina**

---

## Struktura

```
c123-xml-tools/
├── penalties-quality-analyzer/
│   ├── penalties-quality-analyzer.html   # Standalone HTML nástroj
│   └── readme.md                         # Dokumentace
├── race-combinator/
│   ├── canoe-race-combine.html           # Standalone HTML nástroj
│   ├── docs.md                           # Detailní dokumentace
│   └── readme.md                         # Základní info
├── LICENSE
└── README.md
```

---

## Nástroje

### penalties-quality-analyzer
Analyzuje kvalitu zadaných penalizací v XML souboru C123.
- Detekuje nekonzistence a chyby
- Standalone HTML - otevřít v prohlížeči, drag & drop XML

### race-combinator
Kombinuje více XML souborů závodů do jednoho.
- Sloučení výsledků z více kol/dnů
- Standalone HTML - otevřít v prohlížeči

---

## Použití

Všechny nástroje jsou standalone HTML soubory:
1. Otevřít `.html` soubor v prohlížeči
2. Přetáhnout XML soubor(y) z Canoe123
3. Výsledek stáhnout nebo zkopírovat

---

## Vývoj

Nástroje používají vanilla JavaScript bez závislostí.
Pro testování stačí otevřít HTML v prohlížeči.

```bash
# Lokální server (volitelné)
npx serve .
```

---

## Commit message formát

```
feat: add new validation rule for gate penalties
fix: correct XML merge for overlapping runs
docs: update race-combinator documentation
```

---

*XML formát reference → viz `../c123-protocol-docs/c123-xml-format.md`*
