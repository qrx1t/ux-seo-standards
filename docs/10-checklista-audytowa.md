# 10. Zbiorcza Checklista Audytowa UX, Dostępności i SEO

Niniejszy dokument to kompletny arkusz audytowy w formacie checklisty, przeznaczony dla zespołów UX/UI, programistów frontendowych, audytorów dostępności oraz specjalistów SEO. Umożliwia szybką i bezkompromisową weryfikację jakości serwisu internetowego.

---

## Matryca Oceny i Punktacji

| Obszar | Liczba punktów | Status weryfikacji |
|---|:---:|:---:|
| 1. Nawigacja | / 10 | [ ] Zgodny / [ ] Do poprawy |
| 2. Struktura i układ | / 10 | [ ] Zgodny / [ ] Do poprawy |
| 3. Treść i czytelność | / 10 | [ ] Zgodny / [ ] Do poprawy |
| 4. Formularze | / 10 | [ ] Zgodny / [ ] Do poprawy |
| 5. Funkcjonalność i e-commerce | / 10 | [ ] Zgodny / [ ] Do poprawy |
| 6. Dostępność cyfrowa (WCAG 2.2) | / 10 | [ ] Zgodny / [ ] Do poprawy |
| 7. Estetyka i Spójność Marki | / 10 | [ ] Zgodny / [ ] Do poprawy |
| 8. Bezpieczeństwo i Zaufanie | / 10 | [ ] Zgodny / [ ] Do poprawy |
| 9. Pozycjonowanie i Core Web Vitals | / 10 | [ ] Zgodny / [ ] Do poprawy |
| **SUMA CAŁKOWITA** | **/ 90** | **Ocena Dojrzałości UX** |

---

## 1. Nawigacja
- [ ] **1.1.** Logo w lewym górnym rogu jest klikalne na **100% podstron** i prowadzi do adresu `/` (root domain).
- [ ] **1.2.** Logo posiada jednoznaczną etykietę dostępności (`aria-label="Strona główna [Firma]"`).
- [ ] **1.3.** Menu główne na desktopie mieści się w limicie **5–7 pozycji** pierwszego poziomu (Prawo Millera).
- [ ] **1.4.** Wszystkie podstrony od poziomu 2 posiadają semantyczną ścieżkę okruszkową (`Breadcrumbs`).
- [ ] **1.5.** Ostatni element w breadcrumbs jest nieaktywnym linkiem i posiada `aria-current="page"`.
- [ ] **1.6.** Separatory okruszków są ukryte przed czytnikami ekranu (`aria-hidden="true"`).
- [ ] **1.7.** Bieżąca pozycja w menu głównym jest wizualnie wyróżniona i oznaczona semantycznie.
- [ ] **1.8.** Menu mobilne (hamburger) posiada czytelną etykietę słowną "Menu" obok ikony.
- [ ] **1.9.** Przycisk menu mobilnego informuje o stanie (`aria-expanded="true/false"`) i zamyka się klawiszem `Esc`.
- [ ] **1.10.** Na podstronach transakcyjnych użytkownik ma łatwą drogę powrotu lub zachowania koszyka.

---

## 2. Struktura i układ
- [ ] **2.1.** Na każdej podstronie występuje dokładnie jeden semantyczny nagłówek `<h1>`.
- [ ] **2.2.** Hierarchia nagłówków jest ściśle zachowana (H1 ➔ H2 ➔ H3) bez przeskoków poziomów.
- [ ] **2.3.** Rozmiary czcionek są sterowane klasami CSS, a nie przypadkowym wyborem tagów H1–H6.
- [ ] **2.4.** Treść główna witryny znajduje się wewnątrz pojedynczego znacznika `<main>`.
- [ ] **2.5.** Układ jest oparty o spójną siatkę bazową (np. 8pt grid) i standaryzowane marginesy.
- [ ] **2.6.** Długość wiersza w blokach tekstu nie przekracza 75 znaków ze spacjami (`max-width: 65ch`).
- [ ] **2.7.** Kluczowe informacje i słowa kluczowe znajdują się na początku wierszy i nagłówków (F-Pattern).
- [ ] **2.8.** Strony docelowe (landing pages) prowadzą wzrok po ścieżce Z-Pattern ku wyraźnemu CTA.
- [ ] **2.9.** Zastosowano semantyczne znaczniki sekcji: `<header>`, `<nav>`, `<article>`, `<section>`, `<footer>`.
- [ ] **2.10.** Odstępy pionowe oddzielające sekcje wynoszą min. 64px na desktopie, dając oddech wizualny.

---

## 3. Treść i czytelność
- [ ] **3.1.** Kontrast tekstu podstawowego względem tła wynosi minimum **4.5:1** (WCAG 1.4.3 AA).
- [ ] **3.2.** Kontrast dużego tekstu ($\ge$ 24px lub $\ge$ 18.66px bold) wynosi minimum **3.0:1**.
- [ ] **3.3.** Kontrast ramek pól formularzy i ikon funkcyjnych wynosi minimum **3.0:1** (WCAG 1.4.11).
- [ ] **3.4.** Bazowy rozmiar czcionki tekstu akapitowego wynosi minimum **16px** (1rem).
- [ ] **3.5.** Interlinia (`line-height`) w akapitach wynosi minimum **1.5** (150%).
- [ ] **3.6.** Tekst jest wyrównany do lewej krawędzi (LTR) – brak justowania obustronnego (`text-align: justify`).
- [ ] **3.7.** Linki wewnątrz tekstu ciągłego posiadają stałe podkreślenie lub wyróżnik niezależny od koloru.
- [ ] **3.8.** Długie bloki tekstu są dzielone na akapity liczące maksymalnie 3–4 zdania.
- [ ] **3.9.** Tekst spełnia zasady Prostego Języka (Plain Language / ISO 24495-1) – brak urzędniczego żargonu.
- [ ] **3.10.** Zastosowano formatowanie skanowalne: listy wypunktowane i pogrubienia kluczowych fraz.

---

## 4. Formularze
- [ ] **4.1.** Wstępna walidacja błędów uruchamia się dopiero na zdarzeniu `onBlur` (po opuszczeniu pola).
- [ ] **4.2.** Po wystąpieniu błędu, komunikat znika natychmiast w czasie rzeczywistym (`onInput`) po poprawieniu.
- [ ] **4.3.** Każde pole posiada trwałą, widoczną etykietę `<label>` umieszczoną nad polem (top-aligned).
- [ ] **4.4.** Placeholdery nie są używane zamiast etykiet (służą jedynie jako przykłady formatu).
- [ ] **4.5.** Formularz posiada układ jedno-kolumnowy (jedno pole pod drugim).
- [ ] **4.6.** Zaimplementowano standardowe atrybuty HTML5 `autocomplete` (name, email, street-address itp.).
- [ ] **4.7.** Na urządzeniach mobilnych wywoływana jest właściwa klawiatura (`type="tel"`, `type="email"`, `inputmode="numeric"`).
- [ ] **4.8.** Pola haseł posiadają przycisk odsłonięcia znaków (Show/Hide Password toggle).
- [ ] **4.9.** Komunikaty o błędach są połączone z polami za pomocą `aria-describedby` i `aria-invalid="true"`.
- [ ] **4.10.** Wystąpienie błędu nie powoduje wyczyszczenia poprawnie wpisanych wcześniej danych.

---

## 5. Funkcjonalność i e-commerce
- [ ] **5.1.** Pole wyszukiwania jest stale wyeksponowane w nagłówku i mieści min. 27 znaków.
- [ ] **5.2.** Wyszukiwarka oferuje autouzupełnianie z podziałem na produkty, kategorie i zapytania.
- [ ] **5.3.** Wyszukiwarka posiada mechanizm tolerancji literówek (fuzzy search) i polską fleksję.
- [ ] **5.4.** Ekran braku wyników (0 results) nie jest ślepym zaułkiem – sugeruje alternatywy i bestsellery.
- [ ] **5.5.** Filtry fasetowe pozwalają na wielokrotny wybór (multi-select) i pokazują liczniki sztuk.
- [ ] **5.6.** Aktywne filtry są prezentowane jako żetony z możliwością ich szybkiego usunięcia.
- [ ] **5.7.** Dodanie do koszyka natychmiast daje feedback (slide-in cart / powiadomienie z podglądem).
- [ ] **5.8.** Zawartość koszyka jest trwale zapamiętywana (minimum 30 dni w LocalStorage/sesji).
- [ ] **5.9.** Sklep bezwzględnie umożliwia zakupy bez rejestracji (Guest Checkout).
- [ ] **5.10.** Koszyk wyraźnie prezentuje koszty dostawy i dynamiczny pasek darmowej wysyłki.

---

## 6. Dostępność cyfrowa (WCAG 2.2)
- [ ] **6.1.** 100% funkcji serwisu da się obsłużyć za pomocą samej klawiatury (WCAG 2.1.1).
- [ ] **6.2.** W kodzie CSS nie usunięto wskaźnika fokusu (`outline: none` bez stylizacji zastępczej).
- [ ] **6.3.** Wskaźnik fokusu ma min. 2px grubości i kontrast min. 3:1 (WCAG 2.4.7 / 2.4.13).
- [ ] **6.4.** Fokus nie jest zasłaniany przez sticky header lub baner cookies (WCAG 2.2 - 2.4.11).
- [ ] **6.5.** Na początku kodu znajduje się działający link "Przejdź do treści" (*Skip Link* - WCAG 2.4.1).
- [ ] **6.6.** Elementy klikalne i dotykowe mają rozmiar minimum **24x24px** (WCAG 2.5.8 AA).
- [ ] **6.7.** Przyciski na urządzeniach mobilnych spełniają zalecany rozmiar **44x44px / 48x48px**.
- [ ] **6.8.** Okna modalne zapętlają fokus klawiatury (*Focus Trap*) i zamykają się klawiszem `Esc`.
- [ ] **6.9.** Wszystkie zdjęcia informacyjne posiadają precyzyjny `alt`, a elementy ozdobne `alt=""`.
- [ ] **6.10.** Użyto natywnych znaczników HTML5 (`<button>`, `<a>`) zamiast `<div>` z onclick.

---

## 7. Estetyka i Spójność Marki
- [ ] **7.1.** W projekcie wdrożono scentralizowane zmienne projektowe (Design Tokens w CSS).
- [ ] **7.2.** Każdy widok posiada dokładnie jeden dominujący przycisk akcji pierwszego rzędu (Primary CTA).
- [ ] **7.3.** Zastosowano zasadę proporcji kolorystycznych 60-30-10.
- [ ] **7.4.** Kolor czerwony jest zarezerwowany wyłącznie dla błędów i akcji destrukcyjnych.
- [ ] **7.5.** Respektowane jest Prawo Jakoba (standardowe umiejscowienie koszyka, szukajki, konta).
- [ ] **7.6.** Liczba wariantów decyzyjnych jest zoptymalizowana zgodnie z Prawem Hicka.
- [ ] **7.7.** Wszystkie elementy interaktywne posiadają zdefiniowane stany: hover, focus, active, disabled.
- [ ] **7.8.** Zachowano zasadę bliskości Gestalt (mniejsze odstępy między elementami powiązanymi).
- [ ] **7.9.** Identyfikacja wizualna, kroje pisma i logotypy są w 100% zgodne z Brandbookiem firmy.
- [ ] **7.10.** Ikony pochodzą z jednego, spójnego zestawu (ta sama grubość linii i stylistyka).

---

## 8. Bezpieczeństwo i Zaufanie
- [ ] **8.1.** Cały ruch HTTP jest bezwzględnie przekierowywany na HTTPS (kod 301/308).
- [ ] **8.2.** Wdrożono nagłówek HSTS (*HTTP Strict Transport Security*).
- [ ] **8.3.** Wyeliminowano problem Mixed Content (brak zasobów ładowanych po nieszyfrowanym HTTP).
- [ ] **8.4.** Baner cookies zawiera przycisk "Odrzuć opcjonalne" o identycznej wadze wizualnej co "Akceptuj".
- [ ] **8.5.** Formularz rejestracji/logowania **nie blokuje wklejania haseł** ze schowka (NIST SP 800-63B).
- [ ] **8.6.** Formularze nie zdradzają istnienia użytkownika w bazie przy błędach logowania i resetu hasła.
- [ ] **8.7.** Strona błędu 500/404 nie ujawnia szczegółów technicznych serwera ani zrzutów kodu (*Stack Trace*).
- [ ] **8.8.** W stopce serwisu znajdują się pełne dane firmy (NIP, REGON, KRS, adres) oraz Polityka Prywatności.
- [ ] **8.9.** W procesie transakcyjnym wyeksponowano oficjalne logotypy certyfikowanych operatorów płatności.
- [ ] **8.10.** Użytkownik jest ostrzegany o wygaśnięciu sesji z 2-3 minutowym wyprzedzeniem z opcją przedłużenia.

---

## 9. Pozycjonowanie (SEO) i Core Web Vitals
- [ ] **9.1.** Wskaźnik LCP wynosi poniżej **2.5 sekundy** na urządzeniach mobilnych (CrUX / PageSpeed).
- [ ] **9.2.** Obraz hero posiada priorytet `fetchpriority="high"` i **nie ma** atrybutu `loading="lazy"`.
- [ ] **9.3.** Wskaźnik responsywności INP nie przekracza **200 milisekund**.
- [ ] **9.4.** Wskaźnik stabilności wizualnej CLS wynosi poniżej **0.1**.
- [ ] **9.5.** Wszystkie obrazy i tagi iframe posiadają zdefiniowane wymiary `width`/`height` lub `aspect-ratio`.
- [ ] **9.6.** Brak inwazyjnych, pełnoekranowych pop-upów zasłaniających treść po wejściu z Google.
- [ ] **9.7.** Każda podstrona posiada unikalny tag `<title>` (50-60 zn.) oraz `<meta name="description">`.
- [ ] **9.8.** Zaimplementowano ustrukturyzowane mikrodane Schema.org (JSON-LD) dla produktów i breadcrumbs.
- [ ] **9.9.** Strony z parametrami filtrów i sortowania posiadają tag kanoniczny `rel="canonical"`.
- [ ] **9.10.** Witryna jest w pełni przystosowana do indeksowania Mobile-First.
