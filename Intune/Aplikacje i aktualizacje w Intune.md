# Intune aplikacje i aktualizacje


## Wdrażanie aplikacji

Dodałem aplikacje przez Microsoft Store app (new).

| Aplikacja | Przypisanie |
|---|---|
| Company Portal | Required |
| Adobe Acrobat Reader | Available for enrolled devices |

<img width="1693" height="798" alt="image" src="https://github.com/user-attachments/assets/02fdd630-4d2d-434f-ae7f-30e517b1499d" />

Company Portal miał zainstalować się automatycznie. Adobe Reader udostępniłem do samodzielnej instalacji z Portalu firmy.

<img width="797" height="621" alt="image" src="https://github.com/user-attachments/assets/02908d9f-3efc-4a33-9d94-e76674482432" />

## Test instalacji

Na PC02 uruchomiłem Company Portal jako Filip, odnalazłem Adobe Reader i wybrałem instalację.

## Pierścienie aktualizacji

Utworzyłem grupę `GRP-Komputery-Pilot` z przypisanym urządzeniem Filipa. Dodałem komputer, a nie konto użytkownika.

| Pierścień | Aktualizacje jakościowe — odroczenie | Aktualizacje funkcji — odroczenie | Przypisanie |
|---|---|---|---|
| Ring-Pilot | 0 dni | 0 dni | GRP-Komputery-Pilot |
| Ring-Wszyscy | 7 dni | 30 dni | GRP-Komputery-Windows, z wykluczeniem GRP-Komputery-Pilot |

Wykluczenie pilota z drugiego pierścienia pozwala uniknąć przypisania dwóch różnych wartości tych samych ustawień.

Odroczenia są liczone od publikacji aktualizacji. Nie oznaczają oczekiwania siedmiu dni od udanego testu na PC02 ani automatycznego zatwierdzania aktualizacji po pilotażu.

Sprawdzenie przypisań:

<img width="862" height="737" alt="image" src="https://github.com/user-attachments/assets/77f487ed-9a7d-465e-945f-09d3ebe17f79" />

<img width="807" height="757" alt="image" src="https://github.com/user-attachments/assets/416b3682-9e58-4bdb-b92c-77ff8d12191b" />

## PC03 bez lokalnych praw administratora

Przed dołączeniem PC03 zmieniłem w Entra ustawienie dodawania użytkownika dołączającego urządzenie do lokalnych administratorów na `None`.

Następnie przygotowałem Windows 11 Pro i dołączyłem komputer do Entra ID kontem Gabrieli. Sprawdziłem rejestrację w Intune oraz członkostwo w lokalnej grupie administratorów.


```cmd
net localgroup administrators
```

<img width="876" height="580" alt="image" src="https://github.com/user-attachments/assets/46a31ec8-f5c2-41e2-8e4a-594f1260878c" />

Zmiana ustawienia dołączania urządzeń nie odebrała Filipowi uprawnień nadanych wcześniej na PC02.


## Microsoft 365 Apps

Wdrożenie zainstalowania pakietu Microsoft na grupie GRP-Licencja-BusinessPremium

<img width="1695" height="492" alt="image" src="https://github.com/user-attachments/assets/3b236bd0-42b5-4fcc-808f-c19122fc75ac" />
