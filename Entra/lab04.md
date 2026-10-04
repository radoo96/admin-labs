# Lab 4 — MFA i metody logowania

- Ustawienie Microsoft Authenticator tak, żeby pokazywał nazwę aplikacji i miejsce logowania.
- Przeprowadzenie rejestracji metod
- Sprawdzenie w raporcie, kto zarejestrował MFA, a kto nie.
- Obsłużyć zgubiony telefon: wylogowanie i ponowna rejestracja.

## Sposób wymuszania MFA

Na tym etapie pozostawiłem włączone security defaults. Conditional Access będzie wdrażany w kolejnym labie.

<img width="1670" height="178" alt="image" src="https://github.com/user-attachments/assets/e1c70929-76c0-40c6-9955-2a788e1da315" />

| Mechanizm | Zastosowanie w projekcie |
|---|---|
| Security defaults | Obecna ochrona logowania |
| Per-user MFA | Nie włączam osobno dla użytkowników |
| Conditional Access | Planowane reguły z warunkami i wykluczeniami |

Status `Disabled` na stronie per-user MFA nie oznacza, że konto nie jest chronione przez MFA. Wymóg może pochodzić z security defaults albo Conditional Access.

<img width="782" height="646" alt="image" src="https://github.com/user-attachments/assets/6eba57f5-c0f9-4591-a1d8-ef81fcf05fd3" />

<img width="1313" height="576" alt="image" src="https://github.com/user-attachments/assets/27c17b5e-3e3f-466e-b39e-b3d19a1fc378" />

## Microsoft Authenticator

W Authentication methods policy skonfigurowałem:

| Ustawienie | Wartość |
|---|---|
| Microsoft Authenticator | Enabled |
| Grupa docelowa | All users |
| Nazwa aplikacji w powiadomieniu | Enabled |
| Lokalizacja w powiadomieniu | Enabled |

<img width="790" height="388" alt="image" src="https://github.com/user-attachments/assets/071cfe1a-e1ff-4248-a1f8-de963a5b28b3" />

<img width="1442" height="476" alt="image" src="https://github.com/user-attachments/assets/665e0622-79aa-4a6d-9b53-6b66a6941159" />

Dopasowanie liczb pomaga ograniczyć przypadkowe zatwierdzanie powiadomień. Nazwa aplikacji i lokalizacja dostarczają dodatkowego kontekstu. Lokalizacja wynika z adresu IP, więc nie traktuję jej jako dokładnego położenia telefonu.

## Rejestracja pracowników

Rejestrację przećwiczyłem na koncie i Pawła. Konta testowe dodałem do aplikacji Authenticator na swoim telefonie.

<img width="1282" height="602" alt="image" src="https://github.com/user-attachments/assets/605f7d3b-4ab8-46ae-8b59-6dc1b68dc28e" />

<img width="1542" height="692" alt="image" src="https://github.com/user-attachments/assets/7b2a5057-91d9-44ec-b47b-ed8991732baf" />

Przebieg:

1. Logowanie na konto pracownika.
2. Dodanie konta służbowego w Authenticatorze przez kod QR.
3. Potwierdzenie testowego powiadomienia.
4. Sprawdzenie metod na stronie [Security info](https://mysignins.microsoft.com/security-info).

Przećwiczyłem procedurę odzyskania dostępu:

<img width="1560" height="693" alt="image" src="https://github.com/user-attachments/assets/b0f365d6-949f-454b-997d-3a4c3fb18a0a" />

<img width="522" height="645" alt="image" src="https://github.com/user-attachments/assets/4ed127c3-ef38-4a87-b6fb-eb077c88f3bf" />

- Najważniejsza obserwacja: **[uzupełnij]**.
- Problem podczas ćwiczenia: **[uzupełnij albo wpisz „brak”]**.
- Rozwiązanie: **[uzupełnij]**.

[← Lista labów Entra ID](README.md)
