# 07. Estetyka i Spójność Marki (Aesthetics, Brand Identity & Design Systems)

> **Pytanie kontrolne z audytu:** *Czy design jest zgodny z identyfikacją marki?*

---

## 1. Wprowadzenie i znaczenie biznesowe

Estetyka w projektowaniu produktów cyfrowych to znacznie więcej niż "dekoracja". W psychologii poznawczej i badaniach UX kluczowe znaczenie ma **efekt użyteczności estetycznej** (*Aesthetic-Usability Effect* – po raz pierwszy udokumentowany przez badaczy Masaaki Kurosu i Kaori Kashimura w 1995 r., a następnie potwierdzony przez Nielsen Norman Group).

Użytkownicy postrzegają estetyczny, spójny wizualnie interfejs jako **łatwiejszy w obsłudze, bardziej godny zaufania i mniej podatny na błędy**. Z kolei brak spójności (np. 5 różnych stylów przycisków, niespójna paleta kolorów, losowe fonty) natychmiast wzbudza podejrzliwość i podświadome poczucie amatorszczyzny.

---

## 2. Kluczowe wytyczne techniczne i projektowe

### 2.1. System Projektowy (Design System) i Tokeny (Design Tokens)
* **Jedno źródło prawdy (Single Source of Truth):**
  * Wszystkie elementy interfejsu (kolory, typografia, promienie zaokrągleń, cienie, odstępy) muszą być zdefiniowane za pomocą tzw. **Design Tokens** (zmienne CSS / Figma Tokens).
  ```css
  :root {
    /* Brand Tokens */
    --color-brand-primary: #0A66C2;
    --color-brand-primary-hover: #084e96;
    --color-brand-secondary: #00A669;

    /* Semantic Tokens */
    --color-feedback-error: #D9383A;
    --color-feedback-success: #1E8E3E;
    --color-feedback-warning: #F2994A;

    /* Elevation & Radii */
    --radius-sm: 4px;
    --radius-md: 8px;
    --radius-lg: 16px;
    --shadow-card: 0 4px 12px rgba(0, 0, 0, 0.08);
  }
  ```
* **Metodologia Atomic Design (Brad Frost):**
  * Podział architektury UI na:
    1. **Atomy:** kolory, typografia, ikony, tagi HTML (np. input, button).
    2. **Cząsteczki (Molecules):** pole wyszukiwania (input + ikona + przycisk).
    3. **Organizmy (Organisms):** nagłówek (header), karta produktu, pasek boczny.
    4. **Szablony (Templates) i Strony (Pages).**

### 2.2. Fundamentalne Prawa UX (Laws of UX)
* **Prawo Jakoba (Jakob's Law):**
  * *"Użytkownicy spędzają większość czasu na INNYCH stronach WWW"*.
  * Oznacza to, że użytkownicy oczekują, iż Twoja strona będzie zachowywać się tak samo, jak znane im witryny (koszyk w prawym górnym rogu, logo kierujące na główną, wyszukiwarka z lupą). Innowacja w elementach bazowych nawigacji tworzy opór poznawczy.
* **Prawo Fittsa (Fitts's Law):**
  * Czas dotarcia do celu jest funkcją odległości od celu i jego rozmiaru.
  * Kluczowe przyciski akcji (CTA) muszą być **duże i łatwo dostępne** (np. szerokie przyciski mobilne "Kup teraz" osadzone u dołu ekranu).
* **Prawo Hicka (Hick's Law):**
  * Czas podjęcia decyzji rośnie logarytmicznie wraz z liczbą i złożonością dostępnych opcji.
  * Ograniczaj liczbę opcji w cennikach (np. 3 plany abonamentowe zamiast 8) oraz pozycje w menu głównym.

### 2.3. Psychologia barw i spójność semantyczna
* **Hierarchia akcji (Button Hierarchy):**
  * **Primary Action:** tylko JEDEN dominujący przycisk w głównym polu widzenia (np. "Dodaj do koszyka", "Zarejestruj się").
  * **Secondary Action:** przycisk obrysowy (Ghost Button) lub o niższym kontraście dla akcji alternatywnych ("Zapisz na później").
  * **Destructive Action:** zarezerwowane odcienie czerwieni ostrzegawczej dla akcji nieodwracalnych ("Usuń konto").
* **Zasady Percepcji Wizualnej Gestalt:**
  * **Prawo Bliskości (Proximity):** Elementy znajdujące się blisko siebie są postrzegane jako powiązane ze sobą (np. etykieta blisko inputu, a dalej od poprzedniego pola).
  * **Prawo Podobieństwa (Similarity):** Elementy o tym samym kolorze i kształcie powinny pełnić tę samą funkcję.

---

## 3. Sprawdzone źródła i autorytety

1. **Jon Yablonski:**
   * [*Laws of UX: Using Psychology to Design Better Products*](https://lawsofux.com/)
2. **Brad Frost:**
   * [*Atomic Design Methodology*](https://atomicdesign.bradfrost.com/)
3. **Nielsen Norman Group (NN/g):**
   * [*The Aesthetic-Usability Effect* (Kate Moran)](https://www.nngroup.com/articles/aesthetic-usability-effect/)
   * [*Design Systems 101* (Therese Fessenden)](https://www.nngroup.com/articles/design-systems-101/)
4. **Międzynarodowa Norma ISO 9241-210:**
   * [*ISO 9241-210:2019 Human-centred design for interactive systems*](https://www.iso.org/standard/77520.html)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **Wiele konkurujących stylów przycisków (CTA)** | Chaos decyzyjny; użytkownik nie wie, co jest główną akcją | Ścisła hierarchia: Primary, Secondary, Tertiary/Text |
| **Przesycenie kolorami i brak spójności z logo** | Odbiór serwisu jako podejrzanego lub mało wiarygodnego | Ustalenie palety: 60% neutralne, 30% bazowe, 10% akcent |
| **Wymyślanie koła na nowo (Łamanie Prawa Jakoba)** | Frustracja, gdy ikona lub zachowanie jest niezrozumiałe | Stosowanie powszechnie przyjętych konwencji rynkowych |
| **Brak stanów interaktywnych (Hover, Active, Focus, Disabled)** | Uczucie "martwego" lub zepsutego interfejsu | Projektowanie pełnej palety mikrostany dla każdego komponentu |


