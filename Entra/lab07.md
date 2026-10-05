# Lab 7 — Ryzykowne logowania i Identity Protection

- Sprawdzenie licencji P2 lub E5
- Logowania i ryzyko użytkownika oraz raporty ID Protection.
- Włączenie zasady rejestracji MFA dla nowych osób.
- Utworzenie reguły CA004 (ryzyko logowania) i CA005 (ryzyko użytkownika).
- Wywołanie wykrycia ryzyka logowaniem przez Tor i zobaczysz samodzielną naprawę.
- Oznaczenie konta jako przejęte i sprawdzenie wymuszonej zmiany hasła.

## Licencja i przygotowanie

Reguły zależne od ryzyka wymagają Entra ID P2 lub E5. Business Premium zawiera P1.

Przy zakresie `All users` sprawdziłem również licencje kont administracyjnych. Przypisanie P2 tylko grupie `DYN-Pracownicy` nie obejmuje automatycznie kont znajdujących się poza nią.

## Dwa rodzaje ryzyka

| Rodzaj | Czego dotyczy | Reakcja testowana w labie |
|---|---|---|
| Sign-in risk | Konkretnej próby logowania | Ponowne uwierzytelnienie z MFA |
| User risk | Możliwego przejęcia konta | Usunięcie ryzyka, w scenariuszu hasłowym przez bezpieczną zmianę hasła |

## Rejestracja MFA

<img width="1060" height="852" alt="image" src="https://github.com/user-attachments/assets/59488383-fb39-4776-9de6-ad0641753b73" />


W zasadzie rejestracji MFA w ID Protection ustawiłem zakres użytkowników i wykluczenie `GRP-CA-Wykluczenia`.


Rejestracja metody i wymaganie jej użycia przy logowaniu to osobne zadania. Przed testami ryzyka sprawdziłem, czy Paweł ma już działającą metodę MFA oraz możliwość resetu hasła.

## Reguły Conditional Access

| Reguła | Warunek | Zasoby | Wymaganie |
|---|---|---|---|
| `CA004 - Ryzyko logowania: MFA` | Sign-in risk: Medium i High | All resources | Require multifactor authentication |
| `CA005 - Ryzyko użytkownika: zmiana hasła` | User risk: High | All resources |Require password change] |

<img width="1680" height="788" alt="image" src="https://github.com/user-attachments/assets/4402cb9c-e301-4086-989a-e114f00815fb" />

<img width="263" height="863" alt="image" src="https://github.com/user-attachments/assets/1c94d065-5e1d-4114-959f-2085c824dd4f" />
<img width="1696" height="886" alt="image" src="https://github.com/user-attachments/assets/88bc33f5-b6b0-482c-be8a-ac2ff909a23e" />


## Testy What If

Do symulacji wybrałem Pawła i zasób, którego nie blokuje CA003, aby osobno ocenić działanie reguł ryzyka.

| Scenariusz | Oczekiwane zastosowanie reguły | Wynik |
|---|---|---|
| Sign-in risk: Medium | CA004 | 
| User risk: High | CA005 | 
| Konto awaryjne z tymi samymi warunkami | Wykluczone z CA004 i CA005 |

<img width="936" height="267" alt="image" src="https://github.com/user-attachments/assets/5ca50746-605b-41a1-b6f8-4b4fb12cb1f6" />
<img width="993" height="255" alt="image" src="https://github.com/user-attachments/assets/9390ff8e-4959-43b7-a30b-c1911ce06e8e" />

Sprawdziłem też pozostałe pasujące reguły. Nowe zasady nie zastępują CA001–CA003.

## Test logowania przez Tor

Próbę wykonałem kontem testowym Pawła na stronie `myapps.microsoft.com`.

CA001 już wymaga MFA, dlatego samo pojawienie się Authenticatora nie dowodzi działania CA004. Sprawdziłem wynik konkretnej reguły w szczegółach logowania.

Jeśli wykrycie nie pojawiło się albo zostało już oznaczone jako naprawione, odnotowuję taki wynik zamiast wpisywać oczekiwany status.

<img width="1555" height="678" alt="image" src="https://github.com/user-attachments/assets/2588d6f5-12ca-4ebf-9888-6ee8303a5a7f" />

## Test ryzyka użytkownika

W ramach symulacji oznaczyłem testowe konto Pawła przez **Confirm user compromised**. Następnie sprawdziłem nowe logowanie i reakcję CA005.

Było to ręczne oznaczenie konta na potrzeby testu, a nie dowód wykrycia rzeczywistego wycieku hasła.

<img width="1472" height="593" alt="image" src="https://github.com/user-attachments/assets/268f357a-f2b1-42fe-bdd1-e93818443ee9" />

<img width="731" height="198" alt="image" src="https://github.com/user-attachments/assets/c7710e48-5945-45ea-8def-4fe1d7296223" />

## Alerty i stan końcowy

Alerty o ryzyku High oraz cotygodniowe podsumowanie skierowałem na monitorowaną skrzynkę użytkownika, nie na konto administracyjne bez poczty.

<img width="565" height="642" alt="image" src="https://github.com/user-attachments/assets/6173c3ba-ad90-43ec-98db-8e15026416e9" />
