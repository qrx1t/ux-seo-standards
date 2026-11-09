# 05. Funkcjonalność i e-commerce (Search, Cart & Checkout UX)

> **Pytanie kontrolne z audytu:** *Czy koszyk i wyszukiwarka działają bezbłędnie?*

---

## 1. Wprowadzenie i znaczenie biznesowe

Dwa najważniejsze filary funkcjonalne każdego sklepu internetowego i zaawansowanego serwisu to **wyszukiwarka wewnętrzna** (Site Search) oraz **mechanizm koszyka i finalizacji zamówienia** (Cart & Checkout).

* **Wyszukiwarka:** Użytkownicy korzystający z wyszukiwarki mają nawet **2x do 3x wyższy współczynnik konwersji** niż osoby przeglądające kategorie, ponieważ wchodzą z precyzyjną intencją zakupu. Awaria wyszukiwarki to bezpośrednia strata przychodów.
* **Koszyk i Checkout:** Według badań Baymard Institute średni globalny wskaźnik porzucania koszyków wynosi aż **70.19%**. Głównymi powodami są:
  1. Zbyt wysokie dodatkowe koszty (dostawa, opłaty manipulacyjne) ujawnione dopiero na końcu (48%).
  2. Wymóg założenia konta (26%).
  3. Zbyt skomplikowany lub długi proces checkoutu (22%).
  4. Brak zaufania do bezpieczeństwa płatności (25%).

---

## 2. Kluczowe wytyczne techniczne i projektowe

### 2.1. Wyszukiwarka wewnętrzna (Site Search UX)
* **Widoczność pola wyszukiwania:**
  * Wyszukiwarka nie powinna być ukryta pod pojedynczą ikoną lupy na desktopie. Pole powinno być otwarte i widoczne w stałym miejscu nagłówka.
  * **Szerokość pola:** Pole wyszukiwania powinno mieścić minimum **27 znaków** bez przewijania wpisanego tekstu.
* **Autosugestie i autouzupełnianie (Autocomplete):**
  * Uruchamianie po wpisaniu min. 2–3 znaków z debounce'em (ok. 250–300 ms).
  * Wyniki w podpowiedzi powinny być podzielone na sekcje: *Sugerowane kategorie*, *Konkretne produkty ze zdjęciem i ceną*, *Ostatnio wyszukiwane frazy*.
* **Tolerancja błędów i literówek (Typo Tolerance / Fuzzy Search):**
  * Wyszukiwarka musi radzić sobie z literówkami, odmianą fleksyjną w języku polskim oraz fonetycznymi zapisami (np. odnalezienie "smartfon" przy wpisaniu "smartfone" lub "samrtfon").
* **Strona braku wyników (Zero-Results Page):**
  * **Zabroniony jest pusty biały ekran z lakonicznym "Brak wyników".**
  * Ekran musi zawierać:
    1. Informację o braku wyników dla danej frazy z propozycją sprawdzenia pisowni.
    2. Sugestię powiązanych haseł lub kategorii.
    3. Listę bestsellerów / produktów polecanych.
    4. Szybki kontakt do obsługi klienta.
* **Filtrowanie fasetowe (Faceted Navigation):**
  * Filtry muszą pokazywać liczbę dopasowanych produktów w nawiasie obok opcji (np. *Czarne (14)*).
  * Opcje dające 0 wyników powinny być wygaszone lub ukryte.
  * Zastosowanie natychmiastowej aktualizacji AJAX z zachowaniem stanu URL (Search Params).

### 2.2. Koszyk zakupowy (Shopping Cart UX)
* **Mechanizm dodawania do koszyka:**
  * Natychmiastowe potwierdzenie akcji bez przeładowania całej strony (np. wysuwany boczny panel *Slide-out / Drawer Cart* lub powiadomienie toast ze stanem koszyka).
  * Panel koszyka musi pokazywać: miniaturę zdjęcia, pełną nazwę, wybrany wariant (rozmiar/kolor), aktualną cenę jednostkową, selektor ilości oraz sumę całkowitą.
* **Pasek postępu darmowej dostawy (Free Shipping Threshold Bar):**
  * Dynamiczny wskaźnik informujący: *"Brakuje Ci tylko 24,00 zł do darmowej dostawy!"*. Zwiększa średnią wartość koszyka (AOV) o 15–20%.
* **Przejrzystość kosztów:**
  * Podawanie cen brutto, szacowanego kosztu dostawy i przewidywanego terminu doręczenia już w widoku koszyka (przed przejściem do logowania).

### 2.3. Tunel zakupowy (Checkout Flow)
* **Zakupy bez rejestracji (Guest Checkout):**
  * Bezwzględny wymóg nowoczesnego e-commerce. Opcja zakupu jako gość musi być tak samo wyeksponowana jak logowanie.
  * Zaoferuj utworzenie konta **po złożeniu zamówienia** (na stronie Thank You Page), umożliwiając ustawienie hasła jednym kliknięciem.
* **Wskaźnik kroków (Linear Stepper):**
  * Czytelny, 3-krokowy proces: 1. Adres dostawy ➔ 2. Metoda wysyłki i płatność ➔ 3. Podsumowanie.
* **Bezpieczeństwo i zaufanie:**
  * Wyeksponowanie znanych i bezpiecznych metod płatności (BLIK, Apple Pay, Google Pay, szybkie przelewy PayU/Przelewy24, karty płatnicze).
  * Wyświetlenie ikon bezpieczeństwa (SSL, ochrona kupujących).

---

## 3. Sprawdzone źródła i autorytety

1. **Baymard Institute:**
   * [*E-Commerce Search Usability: 60+ Design Guidelines*](https://baymard.com/research/ecommerce-search)
   * [*Cart & Checkout UX Benchmark*](https://baymard.com/research/checkout-usability)
   * [*Reasons for Cart Abandonment and How to Prevent Them*](https://baymard.com/cart-abandonment)
2. **Nielsen Norman Group (NN/g):**
   * [*Search: Visible and Immediate* (Jakob Nielsen)](https://www.nngroup.com/articles/search-visible-and-immediate/)
   * [*E-Commerce Checkout: Never Force Registration*](https://www.nngroup.com/articles/checkout-registration/)
   * [*Faceted Navigation: Best Practices for Filtering and Sorting*](https://www.nngroup.com/articles/faceted-navigation/)
3. **Google Merchant Center:**
   * [*Google Merchant Center: Best Practices for Checkout & Transparency*](https://support.google.com/merchants/answer/6363310)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **Przymusowa rejestracja przed zakupem** | 26% natychmiastowych porzuceń koszyka | Wprowadzenie łatwego Guest Checkout z samym e-mailem |
| **Ukryte koszty dostawy do ostatniego kroku** | 48% porzuceń z powodu rozczarowania ostateczną ceną | Kalkulator dostawy w koszyku przed formularzem |
| **Pusta strona "0 wyników" wyszukiwania** | Użytkownik uznaje, że sklep nie ma towaru i idzie do konkurencji | Propozycje alternatyw, bestsellery, tolerancja literówek |
| **Trudna zmiana ilości lub usunięcie z koszyka** | Użytkownik nie może skorygować zamówienia i rezygnuje | Wygodne kontrolki `+` / `-` oraz czytelny przycisk "Usuń" |
| **Brak walidacji dostępności magazynowej w locie** | Frustracja, gdy produkt okazuje się niedostępny po zapłacie | Rezerwacja stanu i weryfikacja w czasie rzeczywistym |

