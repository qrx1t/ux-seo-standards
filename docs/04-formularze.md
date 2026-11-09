# 04. Formularze (Form UX & Inline Validation)

> **Pytanie kontrolne z audytu:** *Czy walidacja działa w czasie rzeczywistym?*

---

## 1. Wprowadzenie i znaczenie biznesowe

Formularze to moment prawdy w cyklu życia klienta – to tutaj następuje rejestracja, logowanie, zapytanie ofertowe (lead) oraz płatność. Z badań **Baymard Institute** wynika, że aż **17% do 22% użytkowników porzuca proces zamówienia z powodu zbyt długich lub skomplikowanych formularzy**.

Największym punktem tarcia (*friction point*) w formularzach jest **nieprawidłowy moment i sposób walidacji danych**. Użytkownik, który po wypełnieniu 10 pól klika "Dalej" i zostaje ukarany ścianą czerwonych komunikatów o błędach, czuje frustrację i często bezpowrotnie opuszcza serwis.

---

## 2. Kluczowe wytyczne techniczne i projektowe

### 2.1. Złota reguła walidacji w czasie rzeczywistym (Inline Validation)
Badania laboratoryjne Baymard Institute jednoznacznie określają idealną architekturę walidacji w locie:
* **Krok 1: Wstępna weryfikacja na zdarzenie `blur` (opuszczenie pola):**
  * **Nigdy nie waliduj błędu przy pierwszych wpisywanych znakach (`onKeyUp` / `onInput`).** Jeśli użytkownik zaczyna wpisywać adres e-mail (`j...`), wyświetlenie natychmiastowego komunikatu *"Niepoprawny e-mail"* powoduje lęk i rozdrażnienie, ponieważ użytkownik jeszcze nie skończył pisać.
  * Walidacja powinna uruchomić się w momencie, gdy użytkownik skończy wpisywać i przejdzie do następnego pola (`onBlur`) LUB gdy pole o stałej długości osiągnie maksymalną liczbę znaków (np. 16 cyfr karty płatniczej czy 5 cyfr kodu pocztowego).
* **Krok 2: Czyszczenie błędu w czasie rzeczywistym na każde naciśnięcie klawisza (`onInput`):**
  * Jeśli pole zostało oznaczone jako błędne, mechanizm musi natychmiast zmienić logikę: błąd powinien zniknąć **w ułamku sekundy, gdy użytkownik poprawi wartość na prawidłową** (bez konieczności ponownego opuszczania pola).
* **Krok 3: Wskaźnik sukcesu (Green Checkmark):**
  * Zielony "ptaszek" potwierdzający poprawność powinien pojawiać się wyłącznie w polach, które niosą ze sobą ryzyko niepewności (np. dostępność unikalnego loginu, silne hasło, poprawny NIP z bazy GUS). Stosowanie zielonych ikon przy każdym banalnym polu (np. imię) wywołuje zbędny szum wizualny.

### 2.2. Konstrukcja komunikatów o błędach
Komunikat o błędzie musi spełniać regułę **3P (Precyzja, Położenie, Pomoc)**:
1. **Precyzja:** Nie pisz ogólników typu *"Błędna wartość"*. Napisz: *"Wprowadź 9-cyfrowy numer telefonu bez spacji i myślników"*.
2. **Położenie:** Komunikat błędu musi znajdować się **bezpośrednio pod polem**, którego dotyczy (nie w osobnym powiadomieniu na samej górze ekranu).
3. **Pomoc:** Wyjaśnij, jak błąd naprawić.
4. **Dostępność ARIA:** Pole musi mieć atrybut powiązania `aria-describedby="error-message-id"` oraz `aria-invalid="true"`, aby użytkownik czytnika ekranu usłyszał komunikat błędu.

### 2.3. Układ pól (Form Layout) i etykiety
* **Układ jednokolumnowy (Single Column):**
  * Wszystkie pytania powinny układać się w jedną pionową linię. Układy wielokolumnowe powodują zaburzenie naturalnego wzorca skanowania wzrokiem (użytkownik nie wie, czy czytać wierszami czy kolumnami).
  * Wyjątki: Pola ściśle powiązane (np. Imię i Nazwisko, Kod pocztowy i Miasto, Data ważności karty i CVV).
* **Etykiety nad polem (Top-Aligned Labels):**
  * Etykiety umieszczone na górze nad polem umożliwiają najszybsze wypełnianie formularza przy najmniejszej liczbie fiksacji wzroku.
* **Zakaz używania placeholderów jako etykiet:**
  * Placeholder znika po rozpoczęciu pisania, co powoduje, że użytkownik traci kontekst i nie może sprawdzić, co właściwie wpisał. Placeholder może służyć jedynie jako przykład formatu (np. `np. Jan Kowalski`).

### 2.4. Ułatwienia wprowadzania danych (Autofill & Input Types)
* **Atrybuty `autocomplete`:**
  * Zawsze deklaruj standardowe wartości HTML5, np. `autocomplete="name"`, `autocomplete="email"`, `autocomplete="street-address"`, `autocomplete="postal-code"`. Pozwala to przeglądarkom wypełnić formularz jednym kliknięciem (skracając czas o 70%).
* **Odpowiednie typy pól na urządzeniach mobilnych:**
  * `type="tel"` – wywołuje klawiaturę numeryczną dla numerów telefonów.
  * `type="email"` – wywołuje klawiaturę z widocznym symbolem `@` i `.`.
  * `inputmode="numeric"` – wywołuje dużą klawiaturę numeryczną dla kodu PIN/kodu BLIK.
* **Podgląd hasła (Show/Hide Password Toggle):**
  * Zawsze udostępniaj ikonę oka pozwalającą podejrzeć wpisywane hasło, szczególnie na smartfonach. Redukuje to liczbę błędnych logowań o ponad 30%.

---

## 3. Sprawdzone źródła i autorytety

1. **Baymard Institute:**
   * [*Checkout Form Usability: 43 Design Guidelines*](https://baymard.com/research/checkout-usability)
   * [*The Current State of Checkout UX (Over 70% Cart Abandonment)*](https://baymard.com/cart-abandonment)
   * [*Usability Testing of Inline Form Validation Timing (Blur vs. Keystroke)*](https://baymard.com/blog/inline-form-validation)
2. **Nielsen Norman Group (NN/g):**
   * [*Website Forms Usability: Top 10 Recommendations*](https://www.nngroup.com/articles/web-form-design/)
   * [*Placeholders in Form Fields Are Harmful*](https://www.nngroup.com/articles/form-design-placeholders/)
   * [*Error-Message Guidelines*](https://www.nngroup.com/articles/error-message-guidelines/)
3. **Luke Wroblewski:**
   * [*Web Form Design: Filling in the Blanks* (A Book Apart / Rosenfeld Media)](https://www.lukew.com/resources/web_form_design.asp)
4. **W3C WAI:**
   * [*WAI-ARIA Authoring Practices: Form Controls & Validation*](https://www.w3.org/WAI/ARIA/apg/practices/structural-roles/)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **Walidacja na pierwsze naciśnięcie klawisza** | Użytkownik widzi błąd zanim zdąży wpisać poprawny tekst; wysoki stres | Opóźnienie walidacji do zdarzenia `blur` |
| **Znikający placeholder zamiast stałej etykiety** | Brak możliwości weryfikacji zawartości pola po wypełnieniu | Stałe etykiety umieszczone trwale nad polem |
| **Czyszczenie wpisanych danych po błędzie** | Użytkownik musi wpisywać całe hasło lub adres od nowa | Bezwzględne zachowanie wszystkich wprowadzonych poprawnie danych |
| **Domyślne zaznaczanie zgód marketingowych** | Łamanie RODO/GDPR i dark pattern niszczący zaufanie | Wymóg świadomej, dobrowolnej zgody (opt-in) |
| **Brak grupowania pól (zbyt długi formularz)** | Wrażenie przytłoczenia (*information overload*) | Podział na kroki (Multi-step form) z paskiem postępu |



