# Analýza oprav penalizací kanoistických závodů

Jednoduchá webová aplikace pro analýzu ex-post oprav penalizací v kanoistických závodech z XML souborů závodů.

## Účel aplikace

Aplikace analyzuje XML soubory z kanoistických závodů a identifikuje ex-post opravy penalizací na jednotlivých brankách. Pomáhá odhalit problematické branky, kde dochází k opravám často, což může naznačovat problémy s jejich umístěním nebo s přiřazenými rozhodčími.

## Instalace a spuštění

1. Stáhněte všechny soubory do jedné složky
2. Otevřete soubor `index.html` v moderním webovém prohlížeči
3. Aplikace funguje lokálně ve vašem prohlížeči, není potřeba server

## Použití aplikace

1. **Nahrání souboru**
   - Klikněte na tlačítko "Vybrat soubor" a vyberte XML soubor se záznamy ze závodu
   - Nebo přetáhněte XML soubor přímo do označené oblasti

2. **Zobrazení výsledků**
   - Po nahrání souboru se automaticky zobrazí tabulka s analýzou oprav
   - Každý řádek představuje jeden závod/jízdu
   - Sloupce odpovídají jednotlivým brankám
   - Hodnoty v buňkách označují počet ex-post oprav na dané brance
   - Čím sytější barva, tím více oprav

3. **Export výsledků**
   - Klikněte na tlačítko "Kopírovat tabulku do schránky"
   - Vložte obsah schránky do Excelu nebo jiného tabulkového procesoru

## Jak se identifikují ex-post opravy

Aplikace detekuje ex-post opravy na základě časových značek (GateTimes) u jednotlivých branek. Oprava je identifikována pokud:

1. **Čas zadání je mimo interval jízdy**
   - Více než 5 sekund před začátkem jízdy (dtStart)
   - Více než 30 sekund po dokončení jízdy (dtFinish)

2. **Čas zadání se výrazně liší od ostatních časů**
   - Rozdíl od mediánu všech časů jízdy je větší než 10 minut

## Struktura XML souborů

Aplikace očekává XML soubory se strukturou obsahující následující elementy:

- `<Results>` - obsahuje výsledky jednotlivých jízd
  - `<RaceId>` - identifikátor závodu/jízdy
  - `<Id>` - identifikátor závodníka
  - `<dtStart>` - čas začátku jízdy (HH:MM:SS.mmm)
  - `<dtFinish>` - čas konce jízdy (HH:MM:SS.mmm)
  - `<Gates>` - penalizace na jednotlivých brankách
  - `<GateTimes>` - časy zadání penalizací (v milisekundách od půlnoci)

- `<CourseData>` - obsahuje konfiguraci tratí
  - `<CourseNr>` - číslo trati
  - `<CourseConfig>` - konfigurace trati (pořadí a typy branek)

- `<Schedule>` - obsahuje informace o rozvrhu závodů
  - `<RaceId>` - identifikátor závodu
  - `<CourseNr>` - číslo trati

## Tipy pro interpretaci výsledků

- **Vysoký počet oprav na jedné brance** může naznačovat:
  - Problém s viditelností pro rozhodčí
  - Technické problémy s elektronickým zadáváním
  - Složitost posouzení penalizace na dané brance

- **Vzorec oprav v celém závodě** může ukázat:
  - Problematické segmenty trati
  - Rozdíly mezi různými dny závodů
  - Rozdíly mezi různými typy tratí (střední vs. horní)

- **Doporučené úpravy organizace**:
  - Přesunutí problematických rozhodčích
  - Úprava umístění branek
  - Rozdělení segmentů pro lepší správu

## Technické detaily

Aplikace je napsána v čistém JavaScriptu bez externích závislostí. Využívá moderní webové API:

- FileReader API pro načítání souborů
- DOMParser pro zpracování XML
- Clipboard API pro kopírování výsledků

## Omezení

- Aplikace pracuje pouze s jedním XML souborem najednou
- Nerozlišuje typ závodu kromě základního rozřazení podle ST/HO a dne
- Nezohledňuje konkrétní jméno závodníka, pouze jízdu jako celek
