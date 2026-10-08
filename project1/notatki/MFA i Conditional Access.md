# MFA i Conditional Access

W tym labie skonfigurowałem własne zasady dostępu do Microsoft 365: wymaganie MFA oraz blokowanie starszych metod uwierzytelniania. Sprawdziłem też samodzielny reset hasła i szczegóły logowań użytkowników.

## Przygotowanie

Przed zmianami przetestowałem logowanie kontem awaryjnym. Sprawdziłem również, czy Filip ma zarejestrowany Microsoft Authenticator.

Utworzyłem grupę zabezpieczeń `GRP-CA-Wykluczenia` z kontem `awaryjne` i dodałem ją do wykluczeń obu przygotowanych reguł.

Wykluczenie dotyczy tych konkretnych zasad Conditional Access. Nie znosi niezależnych wymagań MFA narzucanych przez Microsoft dla portali administracyjnych.

## Reguły Conditional Access

| Reguła | Użytkownicy | Zasoby i warunki | Działanie |
|---|---|---|---|
| CA01 - MFA dla wszystkich | Wszyscy, poza GRP-CA-Wykluczenia | All resources | Wymaganie MFA |
| CA02 - Blokuj starsze logowanie | Wszyscy, poza GRP-CA-Wykluczenia | All resources; Exchange ActiveSync clients i Other clients | Blokada dostępu |

Obie reguły przygotowałem początkowo w trybie `Report-only`.

<img width="583" height="711" alt="image" src="https://github.com/user-attachments/assets/6b149dc4-a740-465c-95b1-81642036ac39" />

<img width="280" height="882" alt="image" src="https://github.com/user-attachments/assets/b5253c96-0644-4436-83a3-dbdc9239b365" />

W ramach przejścia na własne zasady wyłączyłem Security defaults. Tryb Report-only nie egzekwuje nowych reguł, dlatego sam etap testowania nie zastępuje aktywnej ochrony.

<img width="362" height="363" alt="image" src="https://github.com/user-attachments/assets/8598aee4-5feb-42b9-be5e-ae87735f0fa5" />


## Sprawdzenie przed włączeniem

W narzędziu What If sprawdziłem konto awaryjne i konto Filipa. Dla CA02 uwzględniłem scenariusz starszego klienta — test zwykłego logowania w przeglądarce nie potwierdza zakresu tej blokady.

Konto awaryjne — CA01 | Reguła nie dotyczy konta 
Konto awaryjne — CA02 | Reguła nie dotyczy konta 
Filip — logowanie w przeglądarce | CA01 wymaga MFA 
Filip — starszy klient uwierzytelniania | CA02 blokuje dostęp 

<img width="952" height="235" alt="image" src="https://github.com/user-attachments/assets/e85df0c8-d3bf-4590-b7bb-989f8703168d" />

<img width="982" height="190" alt="image" src="https://github.com/user-attachments/assets/b181ee27-fe29-4a42-851b-5db583b40460" />

Sprawdziłem również logowanie Filipa w dzienniku i wynik oceny CA01 w zakładce po włączeniu

<img width="1412" height="58" alt="image" src="https://github.com/user-attachments/assets/d9f043cf-7ab4-43ef-815c-2ef670bc16c5" />

## Test MFA

Po włączeniu CA01 zalogowałem się jako Filip i sprawdziłem zdarzenie 

<img width="561" height="452" alt="image" src="https://github.com/user-attachments/assets/9c55378a-4389-4993-a56f-2cc8bd478deb" />

Weryfikowałem zarówno zastosowanie reguły, jak i sposób uwierzytelnienia. Wcześniejsze potwierdzenie MFA może zostać wykorzystane ponownie, bez kolejnego powiadomienia.

## Samodzielny reset hasła

Przed wdrożeniem zasady

<img width="935" height="347" alt="image" src="https://github.com/user-attachments/assets/3b3022e9-4179-46da-8317-d624e2d8c72a" />

Włączyłem SSPR dla grupy `GRP-Licencja-BusinessPremium`, do której należy Gabriela.

<img width="841" height="366" alt="image" src="https://github.com/user-attachments/assets/a915fd6f-17ce-404d-a8d8-a9cb0fdb9caa" />

Przed testem sprawdziłem dozwolone metody resetowania oraz metody zarejestrowane na jej koncie.

- Liczba metod wymaganych do resetu: 1
- Dozwolone metody:

<img width="1126" height="526" alt="image" src="https://github.com/user-attachments/assets/a687d334-e840-4028-8b2d-de407e2189c0" />

W osobnym oknie prywatnym otworzyłem stronę `https://aka.ms/sspr` i przetestowałem reset hasła Gabrieli.

Wynik resetu i późniejszego logowania nowym hasłem: 

<img width="1037" height="430" alt="image" src="https://github.com/user-attachments/assets/a7f9aec1-5d67-4c49-9d82-8c4ba9708059" />

## Diagnostyka logowania

Wykonałem próbę logowania Filipa z błędnym hasłem, a następnie odszukałem ją w dzienniku.

<img width="653" height="578" alt="image" src="https://github.com/user-attachments/assets/cf06137f-356c-49a9-97a1-77222bc958fd" />

## Blokada starych programów

Zasada CA02 zaznacza wszystkich użytkowników poza grupą wykluczenia z kontem adminina awaryjnego

<img width="670" height="342" alt="image" src="https://github.com/user-attachments/assets/78ffd2cb-67b6-4a27-90f4-8b1a2e186716" />
