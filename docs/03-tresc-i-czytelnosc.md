# 03. Treść i czytelność (Content, Typography & Readability)

> **Pytanie kontrolne z audytu:** *Czy rozmiar i kontrast tekstu ułatwiają czytanie?*

---

## 1. Wprowadzenie i znaczenie biznesowe

Nawet najbardziej przemyślana architektura i zaawansowane funkcjonalności serwisu zawiodą, jeśli treść będzie męcząca w odbiorze lub fizycznie nieczytelna. Zgodnie z danymi Światowej Organizacji Zdrowia (WHO) oraz W3C, setki milionów ludzi na świecie cierpią na wady wzroku (w tym obniżoną ostrość widzenia, daltonizm i prezbiopię), a ponad 80% użytkowników korzysta ze smartfonów w warunkach niekorzystnego oświetlenia zewnętrznego (np. w pełnym słońcu).

Współczynniki kontrastu i czytelność typograficzna to nie kwestia "gustu grafika", lecz **mierzalny wymóg prawny i techniczny**.

---

## 2. Kluczowe wytyczne techniczne i projektowe

### 2.1. Współczynniki kontrastu kolorystycznego (WCAG 2.2)
Zgodnie z algorytmem relatywnej luminancji W3C:
* **Poziom AA (Wymóg bezwzględny):**
  * **Zwykły tekst (poniżej 18pt / ok. 24px lub poniżej 14pt bold / ok. 18.66px bold):** minimalny kontrast **4.5:1** w stosunku do tła.
  * **Duży tekst (co najmniej 18pt / 24px lub 14pt bold / 18.66px bold):** minimalny kontrast **3.0:1**.
  * **Elementy interfejsu i grafiki informacyjne (WCAG 1.4.11):** kontrolki formularzy, ramki inputów, ikony nawigacyjne i stany focus muszą posiadać kontrast minimum **3.0:1** względem sąsiadujących barw.
* **Poziom AAA (Podwyższony standard):**
  * Zwykły tekst: minimalny kontrast **7.0:1**.
  * Duży tekst: minimalny kontrast **4.5:1**.
* **Zakaz polegania wyłącznie na kolorze (WCAG 1.4.1):**
  * Błąd, stan aktywny lub link w tekście nie mogą być komunikowane wyłącznie kolorem. Linki w bloku tekstu muszą mieć podkreślenie (`text-decoration: underline`) lub różnicę kontrastu min. 3:1 plus inny wyróżnik przy najechaniu.

### 2.2. Parametry typograficzne (Web Typography)
* **Rozmiar bazowy czcionki (Base Font Size):**
  * Minimum **16px** (1rem) dla tekstu akapitowego (body text). 
  * Teksty pomocnicze, dopiski, etykiety prawne: nie mniej niż **12–14px** (0.75rem – 0.875rem), zachowując rygorystyczny kontrast.
* **Wysokość linii (Line-height / Interlinia):**
  * Dla tekstu akapitowego interlinia powinna wynosić od **1.4 do 1.6** (rekomendowane `line-height: 1.5;`).
  * Odstęp między akapitami powinien być co najmniej 1.5 raza większy niż interlinia wewnątrz akapitu (np. `margin-bottom: 1.25em`).
  * Nagłówki o dużym rozmiarze powinny mieć interlinię ściślejszą: **1.1 – 1.25**, aby uniknąć wizualnego rozrywania frazy.
* **Długość wiersza (Measure / CPL - Characters Per Line):**
  * Optymalna szerokość bloku tekstu dla płynnego czytania wynosi **45 do 75 znaków** ze spacjami w wierszu (tzw. "złoty standard" to 60–66 znaków).
  * Zbyt długi wiersz powoduje, że oko gubi początek kolejnej linii podczas powrotu.
  * W CSS: `max-width: 65ch;` dla kontenerów artykułowych.
* **Wyrównanie tekstu:**
  * Wyrównanie do lewej (dla języków LTR). 
  * **Nigdy nie justuj tekstu na stronach WWW (`text-align: justify;`):** przeglądarki internetowe nie posiadają zaawansowanego składu zecerskiego, co tworzy tzw. "rzeki bieli" (rivers of white) drastycznie utrudniające czytanie osobom z dysleksją i zaburzeniami poznawczymi.

### 2.3. Skanowalność i Prosty Język (Plain Language)
* **Zasada odwróconej piramidy (Inverted Pyramid):** Najważniejsza informacja (wniosek/sedno) na samym początku tekstu, następnie szczegóły wspierające, a na końcu tło historyczne.
* **Formatowanie:**
  * Użycie list punktowanych zamiast długich wyliczeń po przecinku.
  * Pogrubienia (`<strong>`) dla kluczowych 2-3 słów w akapicie.
  * Akapity składające się z maksymalnie 3 do 4 zdań.

---

## 3. Sprawdzone źródła i autorytety

1. **W3C Web Content Accessibility Guidelines (WCAG) 2.2:**
   * [*Success Criterion 1.4.3: Contrast (Minimum) (Level AA)*](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)
   * [*Success Criterion 1.4.6: Contrast (Enhanced) (Level AAA)*](https://www.w3.org/WAI/WCAG22/Understanding/contrast-enhanced.html)
   * [*Success Criterion 1.4.12: Text Spacing (Level AA)*](https://www.w3.org/WAI/WCAG22/Understanding/text-spacing.html)
2. **Nielsen Norman Group (NN/g):**
   * [*How Users Read on the Web: Scannability and Inverted Pyramid* (Jakob Nielsen)](https://www.nngroup.com/articles/how-users-read-on-the-web/)
   * [*Legibility, Readability, and Comprehension: Making Web Copy Easy to Read* (Kate Moran)](https://www.nngroup.com/articles/legibility-readability-comprehension/)
3. **The Elements of Typographic Style for the Web (Robert Bringhurst / Richard Rutter):**
   * [*The Elements of Typographic Style Applied to the Web*](http://webtypography.net/)
4. **Międzynarodowa Norma ISO 24495-1:**
   * [*ISO 24495-1:2023 Plain language - Governing principles and guidelines*](https://www.iso.org/standard/78907.html)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **Jasnoszary tekst na białym tle (np. #999 na #FFF)** | Całkowita nieczytelność w świetle dziennym i dla osób 40+ | Zwiększenie kontrastu do minimum #595959 na białym tle (4.5:1) |
| **Czcionka 11–13px jako tekst główny** | Zmęczenie wzroku, konieczność uciążliwego powiększania | Zastosowanie min. 16px jako standardowego rozmiaru bazowego |
| **Justowanie tekstu obustronne (`text-align: justify`)** | Nierówne odstępy między wyrazami, dezorientacja czytelnika | Zastosowanie naturalnego wyrównania do lewej (`text-align: left`) |
| **Linia tekstu na całą szerokość monitora (1920px)** | Gubienie kolejnych linii przy czytaniu, spadek zrozumienia | Ograniczenie kontenera za pomocą `max-width: 65ch` |
| **Tekst osadzony jako grafika rastrowa (obrazek)** | Utrata ostrości przy skalowaniu, brak indeksowania i czytania | Użycie żywego tekstu HTML z webfontami (WOFF2) |

