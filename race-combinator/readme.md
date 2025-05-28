# Kombinace výsledků kanoistických závodů

Tato webová aplikace slouží k vytváření kombinovaných výsledkových listin pro kanoistické závody. Umožňuje spárovat kategorie z různých závodů nebo tratí a vytvořit z nich výsledky pro vyhlášení kombinace.

## Funkce aplikace

- **Nahrání XML souborů** s výsledky závodů
- **Párování kategorií** z různých závodů nebo tratí
- **Kombinování výsledků** podle součtu pořadí a součtu časů
- **Generování tabulek** s výsledky pro celkové pořadí i věkové kategorie
- **Export výsledků** ve formátu vhodném pro Excel

## Jak používat aplikaci

### 1. Nahrání souborů
- Klikněte na tlačítko "Vybrat soubory" nebo přetáhněte XML soubory do označené oblasti
- Aplikace zpracuje soubory a extrahuje z nich potřebná data
- Pro každý závod v XML souboru budou extrahované kategorie a výsledky

### 2. Párování kategorií
- Ze seznamů vyberte dvojice kategorií, které chcete zkombinovat
- Pro rychlejší vyhledávání můžete použít vyhledávací pole nad každým seznamem
- Klikněte na "Spárovat vybrané kategorie" pro vytvoření kombinace
- Kategorie, které již byly spárovány, jsou zvýrazněny
- Spárování můžete kdykoliv zrušit kliknutím na křížek u dané kombinace

### 3. Generování výsledků
- Klikněte na "Generovat výsledky" pro vytvoření kombinovaných výsledkových listin
- Výsledky jsou seřazeny primárně podle součtu pořadí a sekundárně podle součtu časů
- Pro každou kategorii se vytvoří samostatná záložka
- V každé záložce najdete tabulku s celkovým pořadím i pořadím ve věkových kategoriích

### 4. Export výsledků
- Klikněte na "Kopírovat aktuální tabulku do schránky"
- Vložte obsah schránky do Excelu nebo jiného tabulkového programu
- Výsledky lze dále upravovat a formátovat dle potřeby

## Poznámky

- Pokud závodník chybí v jednom ze závodů, je mu přiřazeno pořadí 999
- U věkových kategorií je závodník zařazen podle ročníku narození
- Pro každý závod je automaticky vybrán lepší/finální výsledek (druhá jízda), pokud existuje
- U kategorií je zobrazen počet závodníků

## Technické požadavky

- Aplikace běží kompletně ve webovém prohlížeči a nevyžaduje připojení k internetu
- Podporuje všechny moderní prohlížeče (Chrome, Firefox, Edge, Safari)
- Zpracovává XML soubory generované programem Canoe123