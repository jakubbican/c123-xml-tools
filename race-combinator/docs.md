# Technická dokumentace - Kombinace výsledků kanoistických závodů

Tento dokument popisuje technické aspekty aplikace pro kombinování výsledků kanoistických závodů. Je určen pro vývojáře, kteří by chtěli na aplikaci dále pracovat nebo ji rozšiřovat.

## Architektura aplikace

Aplikace je implementována jako single-page aplikace (SPA) s využitím čistého JavaScriptu, HTML a CSS. Nepoužívá žádné externí frameworky nebo knihovny, což zajišťuje jednoduchost a přenositelnost.

### Struktura souborů

Celá aplikace je obsažena v jediném HTML souboru, který obsahuje:
- HTML strukturu aplikace
- CSS styly v sekci `<style>`
- JavaScript kód v sekci `<script>`

## Datový model

Aplikace pracuje s následujícím datovým modelem:

### Hlavní globální proměnné

- `loadedFiles` - seznam nahraných souborů
- `parsedData` - objekt obsahující zpracovaná data z XML souborů
- `availableCategories` - seznam dostupných kategorií pro párování
- `categoriesInfo` - detailní informace o kategoriích
- `pairedCategories` - seznam spárovaných kategorií
- `combinedResults` - výsledné kombinované výsledky

### Struktura parsedData

```javascript
parsedData = {
    participants: {},  // Informace o účastnících (závodníci)
    results: {},       // Výsledky závodů
    classes: {},       // Definice tříd (kategorií)
    events: {},        // Informace o událostech
    categories: {}     // Mapování věkových kategorií
}
```

## Proces zpracování dat

### 1. Nahrání a parsování XML

Proces začíná nahráním XML souborů pomocí funkce `handleFiles()`. Pro každý soubor se provede:
1. Načtení obsahu souboru pomocí `FileReader`
2. Parsování XML pomocí DOMParser
3. Extrakce dat z XML do datového modelu `parsedData`

Při parsování se zpracovávají tyto sekce XML:
- `<Participants>` - informace o závodníkovi
- `<Results>` - výsledky závodníků
- `<Classes>` - definice kategorií a věkových skupin
- `<Schedule>` - rozpis závodů
- `<Events>` - informace o události

### 2. Extrakce kategorií

Funkce `extractCategories()` zpracovává výsledky a vytváří seznam dostupných kategorií pro párování.

**Důležitý aspekt:** Aplikace detekuje, když existují dvě jízdy téže kategorie (BR1 a BR2) a automaticky vybere finální výsledek (typicky BR2). Toto je implementováno pomocí vytvoření mapy `dailyBestResults`, která pro každou kategorii a den ukládá ID závodu s finálními výsledky.

```javascript
// Příklad detekce nejlepší jízdy
if (disId === 'BR2') {
    const dayMatch = raceId.match(/(.+)_BR\d+_(\d+)$/);
    if (dayMatch) {
        const baseClass = dayMatch[1];
        const day = dayMatch[2];
        const dailyKey = `${baseClass}_${day}`;
        
        // Zaznamenáme, že pro tento den a kategorii je BR2 finální výsledek
        dailyBestResults[dailyKey] = raceId;
    }
}
```

### 3. Párování kategorií

Uživatel interaktivně páruje kategorie, které chce zkombinovat. Každý pár je uložen v poli `pairedCategories` s následující strukturou:

```javascript
{
    id: uniqueId,           // Unikátní ID
    race1: race1Id,         // ID prvního závodu
    race2: race2Id,         // ID druhého závodu
    name: combinedName      // Vygenerovaný název kombinace
}
```

### 4. Generování kombinovaných výsledků

Funkce `generateCombinedResults()` je klíčovou částí aplikace. Pro každý pár kategorií:

1. Získá výsledky obou závodů
2. Sloučí seznam závodníků z obou závodů
3. Pro každého závodníka:
   - Získá výsledky z obou závodů (použije pořadí 999 a čas 999999 pro chybějící záznamy)
   - **Klíčový bod**: Použije `totalRnk` a `totalTotal` (pokud jsou k dispozici), které reprezentují lepší výsledek z více jízd
   - Vypočítá kombinované pořadí jako součet pořadí z obou závodů
   - Určí věkovou kategorii závodníka
4. Seřadí závodníky:
   - Primárně podle součtu pořadí (`combinedRank`)
   - Sekundárně podle součtu časů (`combinedTime`)
5. Přidá absolutní pořadí
6. Rozdělí závodníky podle věkových kategorií
7. Vypočítá pořadí v rámci každé věkové kategorie

```javascript
// Klíčový kód pro výpočet kombinovaného pořadí
const rank1 = result1.totalRnk && !result1.missing ? result1.totalRnk : result1.rnk;
const rank2 = result2.totalRnk && !result2.missing ? result2.totalRnk : result2.rnk;
const time1 = result1.totalTotal && !result1.missing ? result1.totalTotal : result1.total;
const time2 = result2.totalTotal && !result2.missing ? result2.totalTotal : result2.total;

const combinedRank = rank1 + rank2;
const combinedCatRank = catRank1 + catRank2;
const combinedTime = time1 + time2;

// Seřazení výsledků
competitorsResults.sort((a, b) => {
    // Nejprve podle součtu pořadí
    if (a.combinedRank !== b.combinedRank) {
        return a.combinedRank - b.combinedRank;
    }
    
    // Pak podle součtu časů
    return a.combinedTime - b.combinedTime;
});
```

### 5. Vytvoření výstupních tabulek

Funkce `createResultTable()` generuje HTML kód pro tabulky s výsledky:
1. Vytvoří hlavní tabulku s celkovým pořadím
2. Pro každou věkovou kategorii vytvoří samostatnou tabulku

## Zpracování věkových kategorií

Aplikace zjišťuje věkovou kategorii závodníka dvěma způsoby:
1. Nejprve zkusí přímé `CatId` z dat závodníka
2. Pokud není k dispozici, vypočítá věkovou kategorii podle roku narození a definice kategorií

```javascript
// Určení věkové kategorie
let ageCategory = competitor.catId || ''; // Nejprve zkusíme přímé CatId

// Pokud nemáme přímé CatId, zkusíme najít podle věku
if (!ageCategory && parsedData.classes[classId]) {
    const categories = parsedData.classes[classId].categories;
    
    for (const cat of categories) {
        if (year >= cat.firstYear && year <= cat.lastYear) {
            ageCategory = cat.catId;
            ageCategoryName = cat.category;
            break;
        }
    }
}
```

## Formátování času

Časy jsou v XML uloženy v milisekundách (např. 87660 = 87.66 sekund). Funkce `formatTime()` převádí tyto hodnoty na čitelný formát.

```javascript
function formatTime(timeInMs) {
    if (timeInMs === 999999) return 'N/A';
    
    const seconds = Math.floor(timeInMs / 1000);
    const milliseconds = timeInMs % 1000;
    
    return `${seconds}.${String(milliseconds).padStart(2, '0')}`;
}
```

## Možnosti rozšíření

### Potenciální vylepšení

1. **Podpora více formátů souborů**
   - Implementace podpory pro CSV, JSON nebo jiné formáty

2. **Možnost ručně upravit výsledky**
   - Přidání rozhraní pro ruční úpravu výsledků v případě chyb

3. **Ukládání konfigurací**
   - Přidání možnosti ukládat a načítat konfiguraci párování kategorií

4. **Export do více formátů**
   - Implementace přímého exportu do PDF, CSV nebo XLSX

5. **Podpora více typů kombinací**
   - Možnost kombinovat výsledky více než dvou závodů
   - Různé způsoby výpočtu celkového pořadí (např. bodový systém)

### Implementace nového výpočetního algoritmu

Pro implementaci nového algoritmu výpočtu kombinovaného pořadí upravte funkci `generateCombinedResults()` v části, kde se provádí výpočet pořadí:

```javascript
// Současný algoritmus (součet pořadí, při rovnosti součet časů)
competitorsResults.sort((a, b) => {
    if (a.combinedRank !== b.combinedRank) {
        return a.combinedRank - b.combinedRank;
    }
    return a.combinedTime - b.combinedTime;
});

// Příklad alternativního algoritmu (např. bodový systém)
competitorsResults.forEach(competitor => {
    // Výpočet bodů na základě pořadí
    competitor.points = calculatePoints(competitor.results[0].rank) + 
                        calculatePoints(competitor.results[1].rank);
});

// Seřazení podle bodů (sestupně)
competitorsResults.sort((a, b) => b.points - a.points);
```

## Známá omezení

1. Aplikace předpokládá standardní strukturu XML souboru z programu Canoe123
2. Při změně formátu vstupních souborů je nutné upravit parsovací funkce
3. Není implementována kontrola integrity dat - aplikace předpokládá korektní vstupní data
4. Práce s velkými soubory (>10MB) může způsobit zpomalení prohlížeče