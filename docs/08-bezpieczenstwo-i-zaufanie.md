# 08. Bezpieczeństwo i Zaufanie (Security, Privacy & Trust UX)

> **Pytanie kontrolne z audytu:** *Czy strona działa na HTTPS i chroni dane?*

---

## 1. Wprowadzenie i znaczenie biznesowe

Bezpieczeństwo w wymiarze technologicznym (cybersecurity) oraz w wymiarze doświadczenia użytkownika (**Security UX / Trust UX**) to dwie strony tego samego medalu. Użytkownik może nie znać niuansów szyfrowania AES-256 czy nagłówków CSP, ale natychmiast rejestruje sygnały ostrzegawcze wysyłane przez przeglądarkę (*"Niezabezpieczona"*) lub podejrzanie wyglądający proces wprowadzania danych karty.

Według badań Baymard Institute aż **25% kupujących porzuca koszyk wyłącznie z powodu braku zaufania do bezpieczeństwa strony w momencie płatności**. Co więcej, naruszenia przepisów o ochronie danych osobowych (RODO / GDPR) grożą karami sięgającymi 20 milionów euro lub 4% rocznego światowego obrotu przedsiębiorstwa.

---

## 2. Kluczowe wytyczne techniczne i projektowe

### 2.1. Certyfikat SSL/TLS i Wymuszenie HTTPS
* **Całkowite przejście na HTTPS (Zero-tolerance for HTTP):**
  * Każde wywołanie protokołu `http://` musi automatycznie i bez wyjątków przekierowywać statusem **301 Moved Permanently** lub **308** na bezpieczną wersję `https://`.
  * Wdrożenie nagłówka **HSTS (HTTP Strict Transport Security)**:
    ```http
    Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
    ```
* **Brak ostrzeżeń o mieszanej zawartości (Mixed Content Warning):**
  * Żadne zasoby (skrypty JS, style CSS, obrazki, fonty) nie mogą być pobierane z nieszyfrowanych adresów `http://`. Obecność mieszanej zawartości powoduje, że przeglądarki Chrome, Firefox i Safari usuwają symbol kłódki lub blokują ładowanie strony.

### 2.2. Uwierzytelnianie przyjazne użytkownikowi (Authentication UX)
Zgodnie z najnowszymi wytycznymi **NIST SP 800-63B (Digital Identity Guidelines)** oraz OWASP:
* **Koniec ze sztucznymi i sprzecznymi regułami haseł:**
  * Nie twórz absurdalnych wymagań (np. *"dokładnie jeden znak specjalny z wykluczeniem znaku zapytania, nie dłuższe niż 12 znaków"*).
  * Promuj **długość ponad złożoność**: minimalna rekomendowana długość to 10–12 znaków.
  * Zezwalaj na używanie menedżerów haseł (nie blokuj wklejania do pól hasła – atrybut `onpaste="return false;"` jest poważnym antywzorcem obniżającym bezpieczeństwo!).
* **Zapobieganie enumeracji użytkowników (User Enumeration Protection):**
  * Podczas resetu hasła lub błędnego logowania nie zdradzaj, czy dane konto istnieje w bazie.
  * *Poprawny komunikat:* *"Jeśli konto z podanym adresem e-mail istnieje, wysłaliśmy link do zresetowania hasła"*.
* **Limitowanie zapytań (Rate Limiting) z przyjaznym feedbackiem:**
  * Zamiast blokować konto bez słowa, wyświetl czytelny komunikat: *"Zbyt wiele nieudanych prób logowania. Spróbuj ponownie za 5 minut"*.

### 2.3. Zgody, RODO i zakaz Dark Patterns (Deceptive Design)
* **Baner cookies (Zgoda zgodna z wyrokami TSUE i RODO):**
  * Zgoda na pliki cookies marketingowe i analityczne musi być **świadoma, dobrowolna i jednoznaczna**.
  * Przycisk *"Odrzuć wszystkie"* musi być **tak samo łatwo dostępny i widoczny** jak *"Zaakceptuj wszystkie"* (równy rozmiar, czytelny kontrast).
  * Zabronione są ciemne wzorce (Dark Patterns): ukrywanie opcji odrzucenia w głębi podmenu, fałszywa hierarchia przycisków czy domyślnie zaznaczone checkboxy.
* **Polityka prywatności i dane kontaktowe:**
  * W stopce każdej podstrony musi znajdować się bezpośredni link do aktualnej Polityki Prywatności, Regulaminu oraz pełnych danych rejestrowych firmy (NIP, REGON, KRS, fizyczny adres siedziby).

### 2.4. Bezpieczna obsługa błędów i transakcji
* **Brak wycieków technicznych (Information Disclosure):**
  * W razie błędu serwera (HTTP 500) użytkownik **nigdy nie może zobaczyć zrzutu kodu źródłowego (Stack Trace)**, zapytań SQL czy wersji frameworka. Strona błędu musi być przyjazna i bezpieczna.
* **Symbole zaufania przy płatnościach (Trust Badges):**
  * Umieszczenie oficjalnych logotypów certyfikowanych bramek płatniczych (Visa, Mastercard, BLIK, Apple Pay, PayPal). Badania laboratoryjne dowodzą, że znane logotypy bankowe i płatnicze w pobliżu przycisku "Kupuję i płacę" obniżają lęk transakcyjny o 35%.

---

## 3. Sprawdzone źródła i autorytety

1. **OWASP (Open Web Application Security Project):**
   * [*OWASP Application Security Verification Standard (ASVS)*](https://owasp.org/www-project-application-security-verification-standard/)
   * [*OWASP Authentication & Password UX Cheat Sheet*](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)
2. **NIST (National Institute of Standards and Technology):**
   * [*NIST SP 800-63B: Digital Identity Guidelines – Authentication and Lifecycle*](https://pages.nist.gov/800-63-3/sp800-63b.html)
3. **Baymard Institute:**
   * [*Perceived Security in Checkout: How Badges Influence Trust*](https://baymard.com/blog/perceived-security-checkout)
4. **Europejska Rada Ochrony Danych (EDPB):**
   * [*Guidelines 03/2022 on Deceptive Design Patterns (Dark Patterns)*](https://edpb.europa.eu/our-work-tools/our-documents/guidelines/guidelines-032022-deceptive-design-patterns-social-media_en)

---

## 4. Typowe błędy i antywzorce (Anti-patterns)

| Błąd | Skutek | Rozwiązanie |
|---|---|---|
| **Brak przekierowania z HTTP na HTTPS** | Ostrzeżenie w przeglądarce o braku bezpieczeństwa, utrata ruchu | Konfiguracja reguły 301 na poziomie serwera Nginx/Apache/Cloudflare |
| **Blokowanie wklejania haseł (`onpaste="return false"`)** | Zniechęcanie do korzystania z menedżerów haseł (1Password, Bitwarden) | Pełne odblokowanie możliwości wklejania w polach formularza |
| **Dark pattern w banerze cookies (brak opcji "Odrzuć")** | Ryzyko wielomilionowych kar od UODO/TSUE i utrata zaufania | Przycisk "Odrzuć" na tym samym poziomie wizualnym co "Akceptuj" |
| **Wyciek ścieżek serwera w komunikatach błędów 500** | Ułatwienie ataku hakerskiego (*reconnaissance*) | Własna, estetyczna i bezpieczna strona 500/404 |
| **Niejasne lub ukryte dane firmy w stopce** | Poczucie, że serwis jest fikcyjnym sklepem wyłudzającym pieniądze | Transparentna sekcja stopki z danymi rejestrowymi i kontaktem |


