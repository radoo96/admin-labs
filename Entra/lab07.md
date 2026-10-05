# Lab 7 — Ryzykowne logowania i Identity Protection

W tym labie rozszerzyłem konfigurację Rachmistrza o zasady zależne od ryzyka. Sprawdziłem raporty Identity Protection, przygotowałem dwie reguły Conditional Access i przetestowałem reakcję na podejrzane logowanie oraz konto oznaczone jako przejęte.

## Licencja i przygotowanie

Reguły zależne od ryzyka wymagają Entra ID P2 dla użytkowników objętych ich działaniem. Business Premium zawiera P1, więc samo nie wystarcza do tego labu.

| Element | Stan w moim środowisku |
|---|---|
| Produkt zapewniający Entra ID P2 | [uzupełnij] |
| Użytkownicy objęci licencją | [uzupełnij] |
| Termin zakończenia triala, jeśli używany | [uzupełnij] |
| MFA Pawła zarejestrowane | [uzupełnij] |
| Paweł objęty SSPR | [uzupełnij] |
| Dostęp kontem awaryjnym sprawdzony | [uzupełnij] |

Przy zakresie `All users` sprawdziłem również licencje kont administracyjnych. Przypisanie P2 tylko grupie `DYN-Pracownicy` nie obejmuje automatycznie kont znajdujących się poza nią.

## Dwa rodzaje ryzyka

| Rodzaj | Czego dotyczy | Reakcja testowana w labie |
|---|---|---|
| Sign-in risk | Konkretnej próby logowania | Ponowne uwierzytelnienie z MFA |
| User risk | Możliwego przejęcia konta | Usunięcie ryzyka, w scenariuszu hasłowym przez bezpieczną zmianę hasła |

Przejrzałem trzy raporty:

- **Risky sign-ins** — ryzykowne logowania.
- **Risky users** — konta z podwyższonym ryzykiem.
- **Risk detections** — szczegółowe wykrycia i ich przyczyny.

Wykrycie może zostać ocenione podczas logowania albo później. Dlatego zapisywałem czas próby i sprawdzałem odpowiadające jej zdarzenie.

## Rejestracja MFA

<img width="1060" height="852" alt="image" src="https://github.com/user-attachments/assets/59488383-fb39-4776-9de6-ad0641753b73" />



W zasadzie rejestracji MFA w ID Protection ustawiłem zakres użytkowników i wykluczenie `GRP-CA-Wykluczenia`.

Stan zasady: **[uzupełnij]**.

Rejestracja metody i wymaganie jej użycia przy logowaniu to osobne zadania. Przed testami ryzyka sprawdziłem, czy Paweł ma już działającą metodę MFA oraz możliwość resetu hasła.

## Reguły Conditional Access

| Reguła | Warunek | Zasoby | Wymaganie |
|---|---|---|---|
| `CA004 - Ryzyko logowania: MFA` | Sign-in risk: Medium i High | All resources | Require multifactor authentication |
| `CA005 - Ryzyko użytkownika: zmiana hasła` | User risk: High | All resources | [wpisz faktycznie wybrane: Require risk remediation albo Require password change] |

<img width="1680" height="788" alt="image" src="https://github.com/user-attachments/assets/4402cb9c-e301-4086-989a-e114f00815fb" />

<img width="263" height="863" alt="image" src="https://github.com/user-attachments/assets/1c94d065-5e1d-4114-959f-2085c824dd4f" />
<img width="1696" height="886" alt="image" src="https://github.com/user-attachments/assets/88bc33f5-b6b0-482c-be8a-ac2ff909a23e" />

Dla obu reguł:

<img width="936" height="267" alt="image" src="https://github.com/user-attachments/assets/5ca50746-605b-41a1-b6f8-4b4fb12cb1f6" />
<img width="993" height="255" alt="image" src="https://github.com/user-attachments/assets/9390ff8e-4959-43b7-a30b-c1911ce06e8e" />

<img width="1555" height="678" alt="image" src="https://github.com/user-attachments/assets/2588d6f5-12ca-4ebf-9888-6ee8303a5a7f" />

- zakres użytkowników: **[uzupełnij]**;
- wykluczenie: `GRP-CA-Wykluczenia`;
- Sign-in frequency: `Every time`;
- początkowy stan: `Report-only`.

Progi Medium/High dla logowania i High dla użytkownika przyjąłem jako punkt wyjścia do ćwiczenia. Pozwalają sprawdzić reakcję na wyraźniejsze sygnały ryzyka bez obejmowania wszystkich zdarzeń Low.

`Require risk remediation` dobiera sposób naprawy do zagrożenia i metody logowania. Nie zakładam, że zawsze wyświetli ekran zmiany hasła.

## Testy What If

Do symulacji wybrałem Pawła i zasób, którego nie blokuje CA003, aby osobno ocenić działanie reguł ryzyka.

| Scenariusz | Oczekiwane zastosowanie reguły | Wynik |
|---|---|---|
| Sign-in risk: Medium | CA004 | [uzupełnij] |
| User risk: High | CA005 | [uzupełnij] |
| Konto awaryjne z tymi samymi warunkami | Wykluczone z CA004 i CA005 | [uzupełnij] |

Sprawdziłem też pozostałe pasujące reguły. Nowe zasady nie zastępują CA001–CA003.

## Test logowania przez Tor

Próbę wykonałem kontem testowym Pawła na stronie `myapps.microsoft.com`.

| Obserwacja | Wynik |
|---|---|
| Data i godzina próby | [uzupełnij] |
| Wynik logowania | [uzupełnij] |
| Nazwa wykrycia | [uzupełnij albo „brak wykrycia”] |
| Poziom ryzyka | [uzupełnij] |
| Wynik CA004 w Report-only | [uzupełnij] |
| Wynik po włączeniu CA004 | [uzupełnij] |
| Stan ryzyka po uwierzytelnieniu | [uzupełnij] |

CA001 już wymaga MFA, dlatego samo pojawienie się Authenticatora nie dowodzi działania CA004. Sprawdziłem wynik konkretnej reguły w szczegółach logowania.

Jeśli wykrycie nie pojawiło się albo zostało już oznaczone jako naprawione, odnotowuję taki wynik zamiast wpisywać oczekiwany status.

![Wynik testu Identity Protection](zrzuty/lab07.png)

## Test ryzyka użytkownika

W ramach symulacji oznaczyłem testowe konto Pawła przez **Confirm user compromised**. Następnie sprawdziłem nowe logowanie i reakcję CA005.

| Test | Wynik |
|---|---|
| Ryzyko użytkownika po oznaczeniu konta | [uzupełnij] |
| Wymagane czynności podczas logowania | [uzupełnij] |
| Czy wymuszono zmianę hasła | [uzupełnij] |
| Stan ryzyka po zakończeniu | [uzupełnij] |
| Logowanie po naprawie | [uzupełnij] |

Było to ręczne oznaczenie konta na potrzeby testu, a nie dowód wykrycia rzeczywistego wycieku hasła.

## Alerty i stan końcowy

Alerty o ryzyku High oraz cotygodniowe podsumowanie skierowałem na monitorowaną skrzynkę użytkownika, nie na konto administracyjne bez poczty.

| Element | Stan |
|---|---|
| CA004 | [Report-only / On] |
| CA005 | [Report-only / On] |
| Alerty High | [uzupełnij] |
| Weekly digest | [uzupełnij] |
| Końcowy stan konta Pawła | [uzupełnij] |

## Moje uwagi

- Najważniejsza obserwacja: **[uzupełnij]**.
- Problem podczas testów: **[uzupełnij albo wpisz „brak”]**.
- Rozwiązanie: **[uzupełnij]**.

[← Lista labów Entra ID](README.md)
