# Lab 6 — Microsoft 365 i Entra ID

W tym labie przygotowałem środowisko Microsoft 365 dla fikcyjnej firmy Zielony Dom. Utworzyłem konta dwóch pracowników i porównałem bezpośrednie przypisanie licencji z przypisaniem przez grupę.

Wszystkie czynności wykonywałem w przeglądarce. Na tym etapie konta chmurowe są niezależne od lokalnego Active Directory z poprzednich labów.

## Środowisko

| Element | Zastosowanie |
|---|---|
| Microsoft 365 Business Premium | Subskrypcja testowa |
| Microsoft 365 admin center | Użytkownicy, licencje i usługi |
| Microsoft Entra admin center | Grupy, role i logowania |
| Microsoft Authenticator | MFA dla kont używanych w ćwiczeniu |

W dokumentacji nie podaję rzeczywistej nazwy tenanta ani danych logowania.

## Konto awaryjne

Przed dalszą konfiguracją utworzyłem konto `awaryjne` z rolą `Global Administrator`, bez licencji produktowej.

Skonfigurowałem MFA i sprawdziłem logowanie do panelu administracyjnego w osobnym oknie prywatnym. Konto pozostawiłem wyłącznie do odzyskiwania dostępu, bez używania go do codziennej pracy.

<img width="757" height="311" alt="image" src="https://github.com/user-attachments/assets/60867e2c-add3-499b-b73f-5549d42a3e88" />

<img width="545" height="370" alt="image" src="https://github.com/user-attachments/assets/d4228aad-d7e1-41a4-95ba-28fa471236fc" />

<img width="586" height="513" alt="image" src="https://github.com/user-attachments/assets/2f0baed6-a6ef-45e4-9abe-1a349e77a037" />


W labie zastosowałem jedno konto awaryjne. Docelowa konfiguracja wymaga dodatkowej niezależności od zwykłego konta administratora — samo drugie konto w Authenticatorze na tym samym telefonie nie zabezpiecza przed utratą telefonu.

## Konta pracowników

Utworzyłem dwa konta chmurowe:

| Użytkownik | Login | Dział | Przypisanie Business Premium |
|---|---|---|---|
| Filip Mazur | filip.mazur | Sprzedaz | Bezpośrednio |
| Gabriela Lis | gabriela.lis | Ksiegowosc | Przez grupę |

Ustawiłem lokalizację korzystania z usług na Polskę oraz wymóg zmiany hasła początkowego.

## Licencja przez grupę

Utworzyłem grupę zabezpieczeń `GRP-Licencja-BusinessPremium` i dodałem do niej Gabrielę.

W Microsoft 365 admin center przypisałem licencję Business Premium do grupy. Następnie sprawdziłem, czy przypisanie zostało przetworzone i czy Gabriela otrzymała licencję z tego źródła.

- Źródło licencji Filipa:


- Źródło licencji Gabrieli:

<img width="942" height="828" alt="image" src="https://github.com/user-attachments/assets/0c54c955-2b7a-4fab-9951-3156b1fa2b9e" />

<img width="1310" height="65" alt="image" src="https://github.com/user-attachments/assets/43c86fd7-5080-4d73-ae63-0630df83a683" />

<img width="1036" height="172" alt="image" src="https://github.com/user-attachments/assets/9ba6abd2-401d-4777-b68a-5bfa544a8433" />

Członkostwo w grupie ustawiłem ręcznie. Automatyczne jest przypisywanie licencji jej członkom.

## Role administracyjne

Sprawdziłem przypisania roli `Global Administrator`. W konfiguracji z tego ćwiczenia rolę mają moje konto administracyjne i konto awaryjne.

Filip i Gabriela pozostali zwykłymi użytkownikami, bez ról administracyjnych.

## Test usług

W osobnym oknie prywatnym zalogowałem się jako Filip. Sprawdziłem zmianę hasła początkowego, konfigurację MFA oraz dostęp do Outlooka.

<img width="1917" height="462" alt="image" src="https://github.com/user-attachments/assets/591a047a-f39a-4af9-8968-562eed095129" />

