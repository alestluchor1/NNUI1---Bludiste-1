# 🧩 Hledání cesty v bludišti

### Semestrální práce – NNUI1: Základy umělé inteligence 1

Desktopová aplikace vytvořená v jazyce **C#** s využitím frameworku **WPF**, která umožňuje hledání optimální cesty bludištěm pomocí algoritmů A* a BIDI.

Aplikace zpracovává obrazové soubory bludišť, rozpoznává průchozí cesty a neprůchozí stěny a následně hledá cestu mezi zvoleným počátečním a cílovým bodem.

---

## 📌 Informace o projektu

| Informace | Hodnota |
|---|---|
| Předmět | NNUI1 – Základy umělé inteligence 1 |
| Projekt | Semestrální práce |
| Autor | Aleš Tlučhoř |
| Univerzita | Univerzita Pardubice |
| Fakulta | Fakulta elektrotechniky a informatiky |
| Jazyk | C# |
| Framework | WPF |
| Platforma | .NET 10 |
| Vývojové prostředí | Microsoft Visual Studio 2026 |

---

## 🚀 Funkce aplikace

- Načítání různých bludišť ve formátech BMP, PNG a JPG.
- Automatické rozpoznávání průchozích cest a neprůchozích stěn.
- Výběr počátečního a cílového bodu přímo kliknutím do bludiště.
- Nastavení počáteční orientace agenta.
- Výběr vyhledávacího algoritmu A* nebo BIDI.
- Postupné zobrazování průběhu vyhledávání.
- Nastavení rychlosti animace v rozsahu 10–1000 ms.
- Zobrazení výsledné cesty a jejích celkových nákladů.
- Zobrazení počtu prohledaných stavů, počtu stavů na cestě a času hledání.
- Výpočet efektivního faktoru větvení.
- Možnost pozastavení animace a okamžitého zobrazení výsledku.

---

## 🧠 Implementované algoritmy

### A* (A-star)

Algoritmus A* využívá heuristické vyhledávání a vybírá další stav podle hodnoty:

\[
F = G + H
\]

- **G** – dosavadní cena cesty.
- **H** – odhad ceny zbývající cesty k cíli.

Jako heuristická funkce je použita Manhattanovská vzdálenost násobená cenou jednoho kroku.

\[
H = 5 \cdot (|X-X_c| + |Y-Y_c|)
\]

### BIDI (obousměrné prohledávání)

Algoritmus BIDI provádí hledání současně z počátečního a cílového bodu. Při prohledávání zohledňuje dosavadní náklady jednotlivých akcí.

Používá dva samostatné otevřené seznamy a postupně propojuje obě části hledání. Cílem je nalézt cestu s co nejnižšími celkovými náklady.

---

## 🤖 Akce agenta a jejich náklady

Agentův stav je určen souřadnicemi X, Y a aktuální orientací.

| Akce | Cena |
|---|---:|
| Krok vpřed o jedno pole | 5 bodů |
| Otočení o 90° doprava | 2 body |
| Otočení o 90° doleva | 2 body |
| Otočení o 180° | 3 body |

Agent se může pohybovat pouze po průchozích polích a nesmí opustit hranice bludiště.

---

## 🖼️ Zpracování obrazu

Obrázky bludišť jsou při načítání převedeny do formátu BGRA32.

Pro rozpoznávání průchozích cest a stěn se používají následující hodnoty:

- Minimální hodnota jednotlivých barevných složek RGB pro rozpoznání světlého pixelu: **205**.
- Minimální podíl tmavých pixelů při hledání hranice bludiště: **60 %**.
- Minimální podíl světlých pixelů pro označení buňky jako průchozí: **75 %**.
- Maximální rozměr zpracované mapy je přibližně **100 polí** na delší straně.

Při zpracování se omezují drobné barevné nepřesnosti a okolní části obrázku mimo bludiště jsou ignorovány.

---

## 🎮 Ovládání aplikace

1. V nabídce **Bludiště** vyber požadovaný obrázek.
2. Levým kliknutím myši nastav počáteční bod agenta.
3. Pravým kliknutím myši nastav cílový bod.
4. Vyber počáteční orientaci agenta.
5. V nabídce **Algoritmus** vyber A* nebo BIDI.
6. Nastav rychlost animace.
7. Klikni na tlačítko **Spustit hledání**.

### Barevná legenda

| Barva | Význam |
|---|---|
| 🟨 Žlutá | Agent / počáteční bod |
| 🟩 Zelená | Cílový bod |
| 🟦 Modrá | Prohledaný prostor |
| 🟥 Červená | Výsledná nalezená cesta |
| ⬛ Černá | Stěna bludiště |
| ⬜ Bílá | Průchozí cesta |

Po dokončení hledání se zobrazí výsledné informace o nalezené cestě.

---

## 📂 Struktura projektu

```text
NNUI1SemPrace/
│
├── Algorithms/
│   ├── AlgoritmusAStar.cs
│   └── AlgoritmusBIDI.cs
│
├── Images/
│   ├── agent.png
│   ├── Bludiste.bmp
│   ├── Bludiste 2.bmp
│   ├── Bludiste_barevne.png
│   ├── bludiste_nosorozec.png
│   └── robot.ico
│
├── Models/
│   ├── Agent.cs
│   ├── Bludiste.cs
│   ├── ObrazekNacitac.cs
│   └── Stav.cs
│
├── MainWindow.xaml
├── MainWindow.xaml.cs
├── App.xaml
├── App.xaml.cs
└── NNUI1SemPrace.csproj
