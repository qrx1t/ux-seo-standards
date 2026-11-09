# 06. Dostępność cyfrowa (WCAG 2.2 & Digital Accessibility)

> **Pytanie kontrolne z audytu:** *Czy po stronie da się poruszać samą klawiaturą?*

---

## 1. Wprowadzenie i znaczenie biznesowe oraz prawne

Dostępność cyfrowa (ang. *Accessibility / a11y*) to projektowanie i programowanie stron internetowych w taki sposób, aby każda osoba – niezależnie od stopnia sprawności motorycznej, wzrokowej, słuchowej czy poznawczej – mogła z nich w pełni korzystać.

Od **28 czerwca 2025 roku** w Unii Europejskiej wchodzi w życie **Europejski Akt o Dostępności (European Accessibility Act - EAA)**, transponowany w Polsce ustawą o zapewnianiu spełniania wymagań dostępności niektórych produktów i usług przez podmioty gospodarcze. Wymogi te obejmują m.in. **cały sektor e-commerce, bankowość, usługi transportowe i telekomunikacyjne**. Niedopełnienie standardów WCAG 2.1 / 2.2 wiąże się z karami finansowymi oraz ryzykiem pozwów prawnych.

Dostępność to także ogromna rzesza użytkowników tymczasowo niepełnosprawnych (np. złamana ręka, korzystanie wyłącznie z klawiatury lub obsługa smartfona jedną ręką w zatłoczonym autobusie).

---

## 2. Kluczowe wytyczne techniczne i projektowe (WCAG 2.2)

Standard **WCAG 2.2** (oficjalna rekomendacja W3C z października 2023 r.) opiera się na 4 filarach **POUR**:
1. **Perceivable (Postrzegalność)** – informacje i komponenty muszą być prezentowane użytkownikom w sposób dostępny dla ich zmysłów.
2. **Operable (Funkcjonalność)** – interfejs musi umożliwiać nawigację i interakcję (w tym klawiaturą).
3. **Understandable (Zrozumiałość)** – informacje i obsługa interfejsu muszą być jasne i przewidywalne.
4. **Robust (Kompatybilność / Solidność)** – kod musi być interpretowany poprawnie przez różnorodne technologie asystujące (czytniki ekranu NVDA, JAWS, VoiceOver).

### 2.1. Nawigacja klawiaturą (Keyboard Accessible - WCAG 2.1.1 & 2.1.2)
* **Zasada 100% obsługi bez myszy (Kryterium 2.1.1 Poziom A):**
  * Użytkownik musi być w stanie obsłużyć każdą funkcję (otworzyć menu, przejrzeć galerię, wybrać wariant w sliderze, otworzyć modal, złożyć zamówienie) za pomocą klawiszy: `Tab` (następny element), `Shift + Tab` (poprzedni element), `Enter` / `Space` (aktywacja linku/przycisku), `Strzałki` (nawigacja wewnątrz komponentów jak radio czy menu) oraz `Esc` (zamknięcie okna modalnego / menu).
* **Brak pułapki na klawiaturę (No Keyboard Trap - Kryterium 2.1.2 Poziom A):**
  * Kursor klawiatury nie może zostać zablokowany wewnątrz żadnego elementu (np. w oknie modalnym lub odtwarzaczu wideo).
* **Link ominięcia nawigacji (Skip to Main Content - Kryterium 2.4.1 Poziom A):**
  * Pierwszy element po wciśnięciu klawisza `Tab` na świeżo załadowanej stronie musi być linkiem *"Przejdź do treści głównej"*, pozwalającym pominąć powtarzające się menu i od razu przejść do kontenera `<main>`.

### 2.2. Widoczność i niezasłanianie wskaźnika fokusu (Focus Visible & Not Obscured)
* **Kryterium 2.4.7 Focus Visible (Poziom AA):**
  * **Bezwzględny zakaz stosowania `outline: none;` lub `outline: 0;` w stylach CSS bez dostarczenia alternatywnego, wyraźnego stylu fokusu.**
  * Rekomendowany styl: `outline: 2px solid #005fcc; outline-offset: 2px;` o kontraście minimum 3:1 względem tła.
* **Nowość WCAG 2.2 – Kryterium 2.4.11 Focus Not Obscured (Minimum) (Poziom AA):**
  * Gdy komponent interfejsu otrzymuje fokus klawiatury, **nie może być całkowicie zasłonięty** przez przyklejone nagłówki (sticky headers), stopki, pływające banery cookies czy czaty wsparcia.
  * Rozwiązanie techniczne w CSS:
    ```css
    html {
      scroll-padding-top: 80px; /* Wysokość przyklejonego nagłówka */
      scroll-padding-bottom: 60px;
    }
    ```

### 2.3. Rozmiar celu dotykowego (Target Size - WCAG 2.2)
* **Nowość WCAG 2.2 – Kryterium 2.5.8 Target Size (Minimum) (Poziom AA):**
  * Każdy klikalny lub dotykowy element interfejsu (przycisk, link, ikona, checkbox) musi mieć minimalny rozmiar **24 × 24 piksele CSS** LUB wokół mniejszego elementu musi znajdować się wystarczający margines (spacing), aby okrąg o średnicy 24px wycentrowany na celu nie przecinał sąsiedniego celu.
* **Rekomendacja mobilna (WCAG 2.5.5 AAA / Apple HIG / Google Material):**
  * Rekomendowany rozmiar celu dla kciuka to **44 × 44px** (iOS) lub **48 × 48px** (Android).

### 2.4. Semantyka ARIA i czytniki ekranu
* **Pierwsza reguła ARIA (W3C):** *"Nie używaj ARIA, jeśli możesz użyć natywnego elementu HTML"*.
  * Używaj `<button>` zamiast `<div onclick="...">`. Natywny button ma wbudowaną obsługę klawiszy Enter i Spacja oraz informację o roli w drzewie dostępności.
* **Opisy alternatywne grafik (WCAG 1.1.1 Poziom A):**
  * Zdjęcia informacyjne: precyzyjny opis w atrybucie `alt` (np. `alt="Czarna skórzana torba męska z metalową klamrą"`).
  * Grafiki czysto dekoracyjne: pusty atrybut `alt=""` lub `aria-hidden="true"`, aby czytnik ekranu je pominął.
* **Okna modalne (Dialog pattern):**
  * Przy otwarciu modala fokus musi przenieść się do jego wnętrza.
  * Fokus musi być zapętlony wewnątrz modala (*Focus Trap*), a wciśnięcie klawisza `Esc` musi zamykać okno i przywracać fokus na przycisk wywołujący.

---

## 3. Sprawdzone źródła i autorytety

1. **W3C Web Accessibility Initiative (WAI):**
   * [*Web Content Accessibility Guidelines (WCAG) 2.2 Recommendation*](https://www.w3.org/TR/WCAG22/)
   * [*WAI-ARIA Authoring Practices Guide (APG)*](https://www.w3.org/WAI/ARIA/apg/)
   * [*WCAG 2.2 Criterion 2.5.8: Target Size (Minimum)*](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)
   * [*WCAG 2.2 Criterion 2.4.11: Focus Not Obscured (Minimum)*](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html)
2. **Europejski Akt o Dostępności (EAA):**
   * [*Dyrektywa Parlamentu Europejskiego i Rady (UE) 2019/882 (EAA)*](https://eur-lex.europa.eu/eli/dir/2019/882/oj)
3. **The A11Y Project:**
   * [*The A11Y Project Checklist & Guidelines*](https://www.a11yproject.com/checklist/)
4. **Nielsen Norman Group (NN/g):**
   * [*Accessibility & Usability: You Can't Have One Without the Other*](https://www.nngroup.com/articles/accessibility-usability/)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **`outline: none` w CSS** | Użytkownik klawiatury jest "ślepy" – nie widzi, gdzie znajduje się kursor | Projektowanie estetycznego, wyrazistego wskaźnika `:focus-visible` |
| **Niewidoczne lub brakujące Skip Links** | Konieczność wciskania Tab 50 razy przed dotarciem do artykułu | Dodanie linku "Przejdź do treści" na samej górze kodu |
| **Brak obsługi klawisza ESC w oknach modalnych** | Użytkownik zostaje uwięziony w okienku pop-up | Nasłuch zdarzenia `keydown` (Key: 'Escape') zamykającego modal |
| **Elementy `<div>` lub `<span>` symulujące przyciski** | Brak dostępności z klawiatury i dla czytników ekranowych | Używanie wyłącznie natywnych znaczników `<button>` i `<a>` |
| **Elementy dotykowe mniejsze niż 24x24px** | Trudność trafienia palcem, przypadkowe kliknięcia sąsiadujących linków | Zwiększenie paddingu do min. 24x24px (AA) lub 44x44px (AAA) |

