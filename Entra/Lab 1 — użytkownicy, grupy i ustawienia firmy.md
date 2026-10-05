# Lab 1 — użytkownicy, grupy i ustawienia firmy

- Utworzenie jednej osoby ręcznie i pięć z pliku CSV.
- Utworzenie grupy działów 
- Ustawienie wyglądu strony logowania firmy.
- Ograniczenie pracownikom zakładanie grup, aplikacji i wchodzenie do portalu admina.

## Konta pracowników

| Osoba | Login bez domeny | Dział | Stanowisko |
|---|---|---|---|
| Joanna Bąk | joanna.bak | Zarzad | Właścicielka |
| Marta Bąk | marta.bak | Ksiegowosc | Główna księgowa |
| Paweł Bąk | pawel.bak | Ksiegowosc | Księgowy |
| Ola Bąk | ola.bak | Kadry | Specjalistka ds. kadr i płac |
| Kuba Bąk | kuba.bak | ObslugaKlienta | Opiekun klienta |
| Ewa Bąk | ewa.bak | Biuro | Asystentka biura |

Dla pracowników ustawiłem Usage location na Polskę.


## Import CSV

Joannę utworzyłem przez formularz New user. Pozostałych pięć osób dodałem przez `Bulk create`.

Pobrałem szablon z portalu, a plik zapisałem jako CSV UTF-8.

<img width="1800" height="252" alt="image" src="https://github.com/user-attachments/assets/a5d8752e-2c85-4218-afad-6d56f814eb9a" />

<img width="1651" height="617" alt="image" src="https://github.com/user-attachments/assets/4667d875-c09d-4611-b060-e8aba48f0e9c" />

## Grupy

Utworzyłem grupy z członkostwem typu Assigned.

| Grupa | Typ | Członkowie |
|---|---|---|
| GRP-Ksiegowosc | Security | Marta, Paweł |
| GRP-Zarzad | Security | Joanna |
| GRP-Kadry | Security | Ola |
| GRP-Obsluga | Security | Kuba |
| GRP-Biuro | Security | Ewa |
| Zespół Księgowości | Microsoft 365 | Marta, Paweł |

Grupy zabezpieczeń przygotowałem do przypisywania uprawnień, licencji i zasad. Grupę Microsoft 365 utworzyłem do współpracy zespołu.

<img width="1173" height="617" alt="image" src="https://github.com/user-attachments/assets/e9709c3a-b8bf-4c3c-a5be-d506a7aed231" />

<img width="418" height="730" alt="image" src="https://github.com/user-attachments/assets/945baef0-3954-44b6-b00b-0c65053cc72b" />

## Wygląd logowania

Skonfigurowałem wygląd strony logowania oraz tekst informacyjny dla pracowników. Następnie sprawdziłem efekt po wpisaniu loginu Marty w nowej sesji przeglądarki.

<img width="1858" height="683" alt="image" src="https://github.com/user-attachments/assets/6281be48-ef8d-44df-825b-e542023ab463" />

## Ustawienia użytkowników

| Ustawienie | Wartość |
|---|---|
| Users can register applications | No |
| Restrict non-admin users from creating tenants | Yes |
| Restrict access to Microsoft Entra admin center | Yes |
| LinkedIn account connections | No |
| Users can create security groups | No |

W scenariuszu przyjąłem, że nowe grupy i zespoły tworzy administrator na prośbę pracowników.

<img width="690" height="831" alt="image" src="https://github.com/user-attachments/assets/00078def-ca5a-45e9-8a5d-549e5d58c482" />

Na koncie Pawła sprawdziłem dostęp do portalu Entra.

<img width="895" height="556" alt="image" src="https://github.com/user-attachments/assets/f96df6a2-6782-46f7-a576-b95e0a19e5f9" />

<img width="807" height="662" alt="image" src="https://github.com/user-attachments/assets/c9fd05b7-9106-47d6-89cb-6b35b061eaae" />

Ograniczenie portalu administracyjnego nie odbiera automatycznie dostępu do katalogu przez Microsoft Graph lub PowerShell. Nie traktuję go jako granicy bezpieczeństwa.
