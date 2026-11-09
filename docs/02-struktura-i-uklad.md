# 02. Struktura i układ (Layout & Visual Hierarchy)

> **Pytanie kontrolne z audytu:** *Czy nagłówki tworzą hierarchię H1, H2, H3?*

---

## 1. Wprowadzenie i znaczenie biznesowe

Prawidłowa struktura i hierarchia wizualna decydują o tym, czy użytkownik zrozumie treść strony w ciągu pierwszych **3–5 sekund**. Użytkownicy internetu nie czytają tekstu słowo po słowie – zamiast tego **skanują stronę wzrokiem** (tzw. *scanning behaviour*).

Hierarchia nagłówków (H1–H6) pełni potrójną funkcję:
1. **Dla człowieka (UX):** Dzieli stronę na logiczne, strawne bloki informacyjne.
2. **Dla czytników ekranu (WCAG / Dostępność):** Stanowi spis treści umożliwiający niewidomym użytkownikom natychmiastowe przeskakiwanie między sekcjami klawiszem skrótu `H`.
3. **Dla robotów wyszukiwarek (SEO):** Wyznacza wagę merytoryczną haseł i tematów w algorytmach Google (Semantyka HTML5).

---

## 2. Kluczowe wytyczne techniczne i projektowe

### 2.1. Hierarchia nagłówków (H1 – H6)
* **Zasada jednego H1 na podstronę:**
  * Każda strona powinna zawierać dokładnie **jeden** nagłówek `<h1>`, który precyzyjnie definiuje główny temat strony (np. nazwa produktu, tytuł artykułu, cel strony głównej).
  * Wyjątek: Wielosekcyjne dokumenty HTML5 z niezależnymi `<article>`, choć z perspektywy WCAG i SEO rekomendowany jest pojedynczy, nadrzędny `<h1>`.
* **Kolejność bez przeskoków poziomów:**
  * Hierarchia musi być logiczna i schodkowa: `<h1>` ➔ `<h2>` ➔ `<h3>` ➔ `<h4>`.
  * **Zabronione jest pomijanie poziomów:** nie wolno przechodzić bezpośrednio z `<h1>` do `<h3>` tylko po to, by uzyskać mniejszy rozmiar czcionki (od formatowania wizualnego służy wyłącznie CSS).
* **Rozróżnienie semantyki od stylizacji:**
  ```html
  <!-- DOBRZE: Semantyczny H2 ostylowany klasą wyglądu -->
  <h2 class="text-subtitle-sm">Cechy produktu</h2>

  <!-- ŹLE: Użycie pogrubionego akapitu lub diva zamiast nagłówka -->
  <div class="bold-large-text">Cechy produktu</div>
  ```

### 2.2. Modele skanowania wzrokiem (Eye-tracking models)
* **Wzorzec F (F-Shape Pattern):**
  * Typowy dla stron o dużej ilości tekstu (blogi, dokumentacja, portale informacyjne).
  * Użytkownik czyta poziomo górną część (górna belka litery F), schodzi niżej i czyta krótszy fragment w poziomie, a następnie skanuje pionowo lewy margines.
  * *Zalecenie:* Umieszczaj kluczowe słowa kluczowe w pierwszych 2-3 słowach każdego nagłówka i punktorów.
* **Wzorzec Z (Z-Pattern):**
  * Typowy dla stron docelowych (landing pages) i stron głównych o niskiej gęstości tekstu.
  * Wzrok przemieszcza się: lewy górny róg (logo) ➔ prawy górny róg (główne CTA/login) ➔ przekątna do lewego dolnego rogu ➔ prawy dolny róg (ostateczne CTA).
* **Wzorzec tortu warstwowego (Layer-Cake Pattern):**
  * Użytkownik przeskakuje wzrokiem wyłącznie po nagłówkach sekcji, ignorując tekst ciągły, dopóki nie znajdzie poszukiwanej sekcji.

### 2.3. System siatki (Grid System) i 8-punktowa siatka bazowa (8pt Grid)
* **8pt Spacing System:** Wszystkie marginesy, paddingi, wysokości komponentów i odstępy między sekcjami powinny być wielokrotnością 8 pikseli (8px, 16px, 24px, 32px, 48px, 64px, 96px) lub 4px w drobnych elementach (tzw. *half-step*).
* **12-kolumnowy grid (Desktop):**
  * Standard dla widoków desktopowych (pozwala na podziały na 1, 2, 3, 4, 6 lub 12 równych kolumn).
  * Mobilny grid: 4 kolumny ze standardowym marginesem zewnętrznym 16px lub 20px.
* **Biała przestrzeń (White Space / Negative Space):**
  * Przestrzeń wokół elementów nie jest "pustym miejscem", lecz aktywnym narzędziem budowania relacji i zmniejszania obciążenia poznawczego (*Cognitive Load*).

### 2.4. Semantyka HTML5
Wykorzystuj dedykowane znaczniki semantyczne zamiast zagnieżdżonych `<div>`:
* `<header>` – nagłówek strony lub sekcji,
* `<nav>` – blok nawigacyjny,
* `<main>` – unikalna treść główna strony (dokładnie jeden na podstronę),
* `<article>` – samodzielna treść nadająca się do dystrybucji (np. artykuł, post, karta produktu),
* `<section>` – tematyczny blok zawartości z własnym nagłówkiem,
* `<aside>` – treść poboczna (pasek boczny, powiązane linki),
* `<footer>` – stopka serwisu lub artykułu.

---

## 3. Sprawdzone źródła i autorytety

1. **Nielsen Norman Group (NN/g):**
   * [*F-Shaped Pattern of Reading on the Web: Eyetracking Findings* (Jakob Nielsen)](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/)
   * [*Visual Hierarchy: Organizing Content to Follow Natural Eye Movement Patterns*](https://www.nngroup.com/articles/visual-hierarchy-page-layout/)
2. **W3C Web Accessibility Initiative (WAI):**
   * [*WCAG 2.2 Success Criterion 1.3.1: Info and Relationships (Level A)*](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html)
   * [*WCAG 2.2 Success Criterion 2.4.6: Headings and Labels (Level AA)*](https://www.w3.org/WAI/WCAG22/Understanding/headings-and-labels.html)
   * [*WCAG 2.2 Success Criterion 2.4.10: Section Headings (Level AAA)*](https://www.w3.org/WAI/WCAG22/Understanding/section-headings.html)
3. **Google Search Central:**
   * [*Google Search Essentials: Headings and page structure*](https://developers.google.com/search/docs/essentials)
4. **Międzynarodowa Norma ISO 9241-110:**
   * [*ISO 9241-110:2020 Ergonomics of human-system interaction - Interaction principles*](https://www.iso.org/standard/75634.html)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **Brak H1 lub wiele H1 bez uzasadnienia** | Dezorientacja robotów wyszukiwarek i użytkowników czytników ekranu | Jeden nadrzędny H1 określający istotę podstrony |
| **Przeskoki nagłówków (np. H1 ➔ H4)** | Naruszenie standardu WCAG 1.3.1; zerwanie hierarchii nawigacyjnej | Zachowanie płynnej drabiny nagłówków (H1 ➔ H2 ➔ H3) |
| **Wybieranie tagu wg rozmiaru wizualnego** | Np. użycie `<h4>` bo jest mały, zamiast `<h2>` z klasą CSS | Oddzielenie semantyki od stylów CSS (`class="h4-style"`) |
| **Ściana tekstu bez podziału na akapity** | Natychmiastowe zniechęcenie użytkownika i wysoki bounce rate | Podział co 3–4 zdania, używanie list wypunktowanych i H2/H3 |
| **Niespójne odstępy (tzw. "pływający layout")** | Wrażenie nieprofesjonalizmu i chaosu wizualnego | Rygorystyczne stosowanie 8-punktowego systemu siatki |

---

## 5. Checklista weryfikacyjna

- [ ] Czy podstrona posiada dokładnie jeden semantyczny znacznik `<h1>`?
- [ ] Czy struktura nagłówków tworzy logiczną drabinę (H1 ➔ H2 ➔ H3) bez pomijania poziomów?
- [ ] Czy nagłówki informują o treści sekcji bez czytania akapitów (są samoopisowe)?
- [ ] Czy najważniejsze słowa kluczowe znajdują się na początku nagłówków (wzorzec F)?
- [ ] Czy układ jest osadzony w spójnym gridzie (np. 8pt grid, 12-kolumnowy layout)?
- [ ] Czy treść główna jest zawarta w pojedynczym elemencie `<main>`?
- [ ] Czy odległość nagłówka od sekcji poniżej jest mniejsza niż odległość od sekcji powyżej (Zasada Bliskości Gestalt)?
