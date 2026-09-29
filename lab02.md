# Lab 2 — konta, grupy i OU w Active Directory

Kontynuacja konfiguracji domeny `ad.zielonydom.test`. W tym ćwiczeniu uporządkowałem obiekty w AD, utworzyłem konta pracowników i przypisałem je do grup działowych.

Pracowałem na maszynach DC01 i PC01 z poprzedniego labu.

## Organizacja AD

Utworzyłem OU `ZielonyDom`, a w nim:

| OU | Przeznaczenie |
|---|---|
| Uzytkownicy | Konta pracowników i moje zwykłe konto |
| Komputery | Komputery należące do domeny |
| Grupy | Grupy działowe |
| Admini | Konto administracyjne |

Przeniosłem PC01 z domyślnego kontenera `Computers` do OU `Komputery`. Przy tworzeniu OU zostawiłem włączoną ochronę przed przypadkowym usunięciem.

## Konta i grupy

Utworzyłem pięć kont pracowników:

| Login | Grupa |
|---|---|
| ewa.zielinska | GRP-Zarzad |
| adam.nowak | GRP-Sprzedaz |
| beata.kowalska | GRP-Sprzedaz |
| celina.wisniewska | GRP-Ksiegowosc |
| daniel.wojcik | GRP-Recepcja |

Grupy mają zakres `Global` i typ `Security`. W kontach uzupełniłem informacje o stanowisku, dziale i przełożonym.

Dla pracowników zaznaczyłem wymóg zmiany hasła przy następnym logowaniu. Utworzyłem też osobne konto do codziennej pracy i konto administracyjne należące do `Domain Admins`.

Na potrzeby testu ustawiłem w `Default Domain Policy` próg blokady konta na 5 nieudanych prób logowania.

## Sprawdzenie działania

- Zmiana hasła przy pierwszym logowaniu: <img width="667" height="525" alt="image" src="https://github.com/user-attachments/assets/b6cb9032-bbf5-486d-9eac-fd3368129222" />

- Wynik `whoami`: <img width="705" height="335" alt="image" src="https://github.com/user-attachments/assets/29ba921d-c746-4d1e-b5b9-87078dc75f69" />

- Próba logowania na wyłączone konto: <img width="733" height="493" alt="image" src="https://github.com/user-attachments/assets/0a190d0c-b706-4d45-a630-a956fb29c584" />

- Wynik wpisania 5 razy złego hasła: <img width="642" height="512" alt="image" src="https://github.com/user-attachments/assets/44d17f5d-b6dc-41d1-8d94-0aec5fff3e7e" />


Struktura OU

<img width="772" height="541" alt="image" src="https://github.com/user-attachments/assets/9b776cbd-9f54-44ea-9b67-f5c873a2f573" />




