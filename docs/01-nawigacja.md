# 01. Nawigacja (Navigation UX)

> **Pytanie kontrolne z audytu:** *Czy z każdej podstrony wrócisz na stronę główną?*

---

## 1. Wprowadzenie i znaczenie biznesowe

Nawigacja jest szkieletem architektury informacji (IA - *Information Architecture*) każdej witryny. Użytkownik wchodzący na dowolną podstronę (często z bezpośredniego linku w wyszukiwarce lub social media) musi w ułamku sekundy zrozumieć:
1. Gdzie się znajduje? (*Where am I?*)
2. Gdzie może pójść? (*Where can I go?*)
3. Jak wrócić do punktu wyjścia / na stronę główną? (*How do I get back?*)

Błędy w nawigacji prowadzą do tzw. *pętli zagubienia* (disorientation loop), drastycznego wzrostu współczynnika odrzuceń (Bounce Rate) oraz porzucania procesów zakupowych.

---

## 2. Kluczowe wytyczne techniczne i projektowe

### 2.1. Identyfikator witryny (Logo) jako powrót na stronę główną
* **Umiejscowienie:** Lewy górny róg ekranu (dla języków LTR - *Left-to-Right*). W badaniach eyetrackingowych NN/g lewy górny róg otrzymuje pierwszą i najbardziej stabilną uwagę użytkownika.
* **Interakcja:** Logo musi być klikalnym linkiem prowadzącym bezpośrednio do adresu `/` (root domain).
* **Dostępność i atrybuty:** 
  * Element `<a>` musi posiadać czytelny atrybut dostępności, np. `aria-label="Strona główna [Nazwa Firmy]"` lub znacznik `alt` w obrazie SVG/PNG: `alt="[Nazwa Firmy] - przejdź do strony głównej"`.
  * Na samej stronie głównej dopuszczalne i rekomendowane jest oznaczenie linku jako nieaktywnego lub z atrybutem `aria-current="page"`.
* **Wyjątek:** Izolowane tunele konwersji (ang. *Distraction-Free Checkout*). Podczas finalizacji zamówienia usuwa się pełne menu, jednak kliknięcie logo powinno pytać o zachowanie koszyka lub przenosić do koszyka/strony głównej.

### 2.2. Ścieżki nawigacji okruszkowej (Breadcrumbs)
* **Zastosowanie:** Obowiązkowe na wszystkich podstronach leżących na poziomie 2 i głębszym (np. Strona główna > Kategoria > Podkategoria > Produkt).
* **Format:**
  ```html
  <nav aria-label="Okruszki chleba (ścieżka nawigacyjna)">
    <ol itemscope itemtype="https://schema.org/BreadcrumbList">
      <li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem">
        <a itemprop="item" href="/"><span itemprop="name">Strona główna</span></a>
        <meta itemprop="position" content="1" />
      </li>
      ›
      <li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem">
        <a itemprop="item" href="/kategoria"><span itemprop="name">Elektronika</span></a>
        <meta itemprop="position" content="2" />
      </li>
      ›
      <li aria-current="page">Smartfony</li>
    </ol>
  </nav>
  ```
* **Zasady UX:**
  * Ostatni element (bieżąca strona) **nie powinien** być klikalnym linkiem.
  * Separatory (np. `/`, `›`, `»`) powinny być ukryte przed czytnikami ekranu (`aria-hidden="true"`).

### 2.3. Menu główne i architektura poziomów
* **Zasada 7 ± 2 (Prawo Millera):** Liczba pozycji pierwszego rzędu w menu desktopowym powinna wynosić od 5 do 7 elementów.
* **Sticky Navigation (Przyklejony nagłówek):**
  * Rekomendowany przy długich stronach typu *one-page* lub portalach artykułowych.
  * Zmniejsza czas dotarcia do nawigacji o 22% (wg badań NN/g).
  * Na urządzeniach mobilnych wysokość przyklejonego paska nie może przekraczać 10-12% wysokości ekranu (*viewport height*).

### 2.4. Nawigacja mobilna (Mobile Navigation UX)
* **Ikona hamburgera:**
  * Musi posiadać etykietę tekstową (np. słowo "Menu" obok ikony trzech kresek). Badania A/B wykazują do 20% większą klikalność nawigacji z etykietą tekstową w porównaniu z samą ikoną.
* **Dolny pasek nawigacji (Bottom Tab Bar):**
  * Zgodnie z zasadą *Thumb Zone* (strefa kciuka), najważniejsze 3–5 akcji (np. Home, Szukaj, Koszyk, Profil) powinny znajdować się w zasięgu dolnej krawędzi smartfona.

---

## 3. Sprawdzone źródła i autorytety

1. **Nielsen Norman Group (NN/g):**
   * [*Homepage Usability: 50 Websites Deconstructed* (Jakob Nielsen)](https://www.nngroup.com/articles/homepage-usability/)
   * [*Breadcrumbs: 11 Design Guidelines for Desktop and Mobile* (Raluca Budiu)](https://www.nngroup.com/articles/breadcrumbs/)
   * [*Sticky Headers: When to Use Them, When to Avoid Them* (Kara Pernice)](https://www.nngroup.com/articles/sticky-headers/)
2. **W3C Web Accessibility Initiative (WAI):**
   * [*WAI-ARIA Authoring Practices Guide: Breadcrumb Pattern*](https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)
   * [*WCAG 2.2 Criterion 2.4.5: Multiple Ways (Level AA)*](https://www.w3.org/WAI/WCAG22/Understanding/multiple-ways.html)
3. **Baymard Institute:**
   * [*Navigation & Category Architecture UX Benchmark*](https://baymard.com/research/ecommerce-search)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **Logo jako statyczny obrazek** | Użytkownik klika bez reakcji, frustracja, utrata punktu orientacyjnego | Opakowanie logo w tag `<a>` z linkiem do `/` |
| **Brak breadcrumbs w głębokich strukturach** | Użytkownik z wyszukiwarki nie wie, w jakiej kategorii się znajduje | Wdrożenie semantycznych okruszków z mikrodanymi Schema.org |
| **Mystery Meat Navigation** | Ikony bez podpisów tekstowych zmuszają do zgadywania funkcji | Dodanie stałych podpisów lub czytelnych tooltipów |
| **Brak stanu aktywnego (Active state)** | Użytkownik nie wie, w której sekcji menu aktualnie przebywa | Wyróżnienie wizualne linku i atrybut `aria-current="page"` |
| **Zablokowany przycisk "Wstecz" (Back button trap)** | Pułapki historii przeglądarki niszczą zaufanie | Respektowanie historii `history.pushState` i standardowego zachowania przeglądarki |

---

