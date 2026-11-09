# 09. Pozycjonowanie stron (SEO) w powiązaniu z UX (Core Web Vitals & Search UX)

> **Pytanie kontrolne z audytu:** *Czy strona jest zoptymalizowana pod kątem Core Web Vitals i wytycznych Google Search Essentials?*

---

## 1. Wprowadzenie i znaczenie biznesowe

Nowoczesne SEO (Search Engine Optimization) i UX (User Experience) przestały być osobnymi dyscyplinami – połączyły się w jeden spójny obszar zwany **SXO (Search Experience Optimization)**. Algorytmy Google (m.in. Page Experience Update, Helpful Content System) nie nagradzają już stron nasyconych słowami kluczowymi, lecz te, które dostarczają **szybkich, stabilnych, bezpiecznych i wartościowych doświadczeń użytkownikom**.

Jeśli serwis jest wolny, przeskakuje podczas ładowania lub reaguje z opóźnieniem na dotyk, Google obniża jego pozycję w wynikach wyszukiwania, a użytkownicy natychmiast wracają do wyników wyszukiwania (zjawisko *pogo-sticking*).

---

## 2. Kluczowe wytyczne techniczne i projektowe

### 2.1. Metryki Core Web Vitals (Stan standardu 2024–2026)
Wskaźniki Core Web Vitals to oficjalne metryki Google mierzące rzeczywiste doświadczenia użytkowników (*field data* z raportu Chrome User Experience Report - CrUX):

#### 1. LCP (Largest Contentful Paint) – Szybkość renderowania największego elementu
* **Wymóg:** $\le$ **2.5 sekundy** na urządzeniach mobilnych (dla 75. percentyla wizyt).
* **Co mierzy:** Czas załadowania największego widocznego bloku treści w pierwszym widoku (viewport) – zazwyczaj jest to obraz hero, baner główny lub duży blok nagłówka `<h1>`.
* **Kluczowe optymalizacje:**
  * Preload zasobu krytycznego w sekcji `<head>`:
    ```html
    <link rel="preload" as="image" href="/images/hero.webp" fetchpriority="high">
    ```
  * Zastosowanie nowoczesnych formatów kompresji: **AVIF** lub **WebP**.
  * **Bezwzględny zakaz:** Nigdy nie dodawaj `loading="lazy"` do obrazu, który jest kandydatem na LCP (opóźnia to renderowanie o 1–3 sekundy).
  * Optymalizacja TTFB (*Time to First Byte*) poniżej **800 ms** (wydajny hosting, CDN np. Cloudflare, cache serwera).

#### 2. INP (Interaction to Next Paint) – Responsywność na interakcję
* **Wymóg:** $\le$ **200 milisekund**.
* **Status:** Od **12 marca 2024 r.** oficjalnie zastąpił stary wskaźnik FID (First Input Delay). INP mierzy opóźnienie **wszystkich** kliknięć, dotknięć ekranu i naciśnięć klawiszy w trakcie całej wizyty użytkownika na stronie.
* **Kluczowe optymalizacje:**
  * Eliminacja "długich zadań" JavaScript (*Long Tasks* przekraczających 50 ms blokowania wątku głównego).
  * Dzielenie kodu i asynchroniczne odraczanie ciężkich kalkulacji:
    ```javascript
    await scheduler.yield(); // Oddanie kontroli przeglądarce przed aktualizacją UI
    ```
  * Ograniczenie lub asynchroniczne ładowanie ciężkich bibliotek firm trzecich (tagi analityczne, piksele marketingowe, widgety czatów).

#### 3. CLS (Cumulative Layout Shift) – Stabilność wizualna układu
* **Wymóg:** $\le$ **0.1**.
* **Co mierzy:** Sumę nieoczekiwanych przesunięć elementów na ekranie podczas ładowania strony (np. gdy tekst ucieka w dół, bo nad nim niespodziewanie wczytał się baner reklamowy).
* **Kluczowe optymalizacje:**
  * Zawsze deklaruj wymiary `width` i `height` lub właściwość CSS `aspect-ratio` dla wszystkich obrazów i wideo:
    ```html
    <img src="produkt.jpg" width="600" height="400" alt="..." style="aspect-ratio: 3/2; width: 100%; height: auto;">
    ```
  * Rezerwowanie stałych slotów na banery i widżety dynamiczne.
  * Zapobieganie przesunięciom wynikającym z doładowywania fontów (*FOUT / FOIT*) poprzez `font-display: swap` oraz dopasowanie metryk fontu awaryjnego (`size-adjust`).

### 2.2. Google Search Essentials i architektura informacji
* **Mobile-First Indexing:**
  * Google indeksuje i ocenia stronę **wyłącznie na podstawie jej wersji mobilnej**. Jeśli treść lub linki są ukryte na smartfonie, Google traktuje je tak, jakby nie istniały.
  * Viewport musi być zadeklarowany: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.
* **Zakaz inwazyjnych nakładek (Intrusive Interstitials):**
  * Wyskakujące okienka (pop-upy newslettera, reklamy) zasłaniające treść natychmiast po przejściu z wyszukiwarki skutkują karą algorytmiczną (*Google Interstitial Penalty*).
  * Dopuszczalne są jedynie prawnie wymagane banery cookies i weryfikacja wieku.
* **Semantyczny HTML i dane ustrukturyzowane (Schema.org JSON-LD):**
  * Zapewnienie robotom semantycznego spisu treści (H1, H2, H3, `<article>`, `<main>`).
  * Wdrożenie mikrodanych Schema.org w formacie JSON-LD:
    * `BreadcrumbList` – czytelna ścieżka w wynikach wyszukiwania.
    * `Product` i `Offer` – gwiazdki ocen, stan magazynowy i cena widoczne bezpośrednio w Google SERP (*Rich Snippets*).
    * `FAQPage` – rozwijane pytania i odpowiedzi w wynikach.
* **Metatagi i Kanoniczność:**
  * `<title>` (50–60 znaków) z unikalną korzyścią i frazą kluczową.
  * `<meta name="description">` (120–155 znaków) z jasnym Call to Action.
  * Kanoniczne tagi `<link rel="canonical" href="...">` na stronach z parametrami filtrów i sortowania, aby zapobiec kanibalizacji i duplikacji treści.

---

## 3. Sprawdzone źródła i autorytety

1. **Google Search Central:**
   * [*Google Search Essentials Documentation*](https://developers.google.com/search/docs/essentials)
   * [*Understanding Page Experience in Google Search Results*](https://developers.google.com/search/docs/appearance/page-experience)
   * [*Avoiding Intrusive Interstitials and Dialogs Guidelines*](https://developers.google.com/search/docs/appearance/avoid-intrusive-interstitials)
2. **Web.dev / Google Chrome Team:**
   * [*Core Web Vitals Documentation*](https://web.dev/explore/learn-core-web-vitals)
   * [*Interaction to Next Paint (INP) – Official Web Metric*](https://web.dev/articles/inp)
   * [*Optimize Largest Contentful Paint (LCP)*](https://web.dev/articles/optimize-lcp)
   * [*Optimize Cumulative Layout Shift (CLS)*](https://web.dev/articles/optimize-cls)
3. **W3C Schema.org Community Group:**
   * [*Schema.org Full Vocabulary for Structured Data*](https://schema.org/)
4. **Moz & Ahrefs Research:**
   * [*Core Web Vitals & Page Experience Ranking Study*](https://ahrefs.com/blog/core-web-vitals/)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **Leniwe ładowanie (`loading="lazy"`) na bannerze LCP** | Opóźnienie LCP o 1.5–3 sekundy, spadek pozycji w Google | Usunięcie lazy loading i dodanie `fetchpriority="high"` |
| **Brak atrybutów `width` i `height` na obrazkach** | Skoki układu (CLS > 0.25), przypadkowe kliknięcia w złe linki | Dodanie jawnych wymiarów lub `aspect-ratio` w CSS |
| **Monolityczny JavaScript blokujący wątek główny** | Zablokowanie interakcji (INP > 500 ms), zawieszanie strony na mobile | Dzielenie kodu (*Code splitting*), defer/async na skryptach |
| **Pełnoekranowy pop-up z newsletterem na wejściu** | Kara algorytmiczna od Google i natychmiastowe opuszczenie strony | Zastąpienie pop-upa subtelnym banerem w treści lub exit-intent |
| **Brak tagów kanonicznych przy filtrach e-commerce** | Indeksowanie tysięcy zduplikowanych stron parametrów URL | Wdrożenie `<link rel="canonical">` wskazującego kategorię bazową |

