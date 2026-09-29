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
| ewa.kowalska | GRP-Zarzad |
| adam.nowak | GRP-Sprzedaz |
| beata.nowak | GRP-Sprzedaz |
| celina.wisniewska | GRP-Ksiegowosc |
| daniel.wojcik | GRP-Recepcja |

Grupy mają zakres `Global` i typ `Security`. W kontach uzupełniłem informacje o stanowisku, dziale i przełożonym.

Dla pracowników zaznaczyłem wymóg zmiany hasła przy następnym logowaniu. Utworzyłem też osobne konto do codziennej pracy i konto administracyjne należące do `Domain Admins`.

Na potrzeby testu ustawiłem w `Default Domain Policy` próg blokady konta na 5 nieudanych prób logowania.

## Sprawdzenie działania

- Zmiana hasła przy pierwszym logowaniu:
  
 <img width="667" height="525" alt="image" src="https://github.com/user-attachments/assets/b6cb9032-bbf5-486d-9eac-fd3368129222" />

- Wynik `whoami`:
  
  <img width="705" height="335" alt="image" src="https://github.com/user-attachments/assets/29ba921d-c746-4d1e-b5b9-87078dc75f69" />

- Próba logowania na wyłączone konto:
  
  <img width="733" height="493" alt="image" src="https://github.com/user-attachments/assets/0a190d0c-b706-4d45-a630-a956fb29c584" />

- Wynik wpisania 5 razy złego hasła:
  
  <img width="642" height="512" alt="image" src="https://github.com/user-attachments/assets/44d17f5d-b6dc-41d1-8d94-0aec5fff3e7e" />




Struktura OU

<img width="781" height="472" alt="image" src="https://github.com/user-attachments/assets/2fe69035-7868-4b3f-a996-663b052ec620" />

<img width="741" height="437" alt="image" src="https://github.com/user-attachments/assets/967f2717-9e13-41cf-86bb-5f3a1957d8bf" />

<img width="748" height="357" alt="image" src="https://github.com/user-attachments/assets/87a56b22-8c5c-47ba-b604-2b365ae0d939" />

<img width="775" height="372" alt="image" src="https://github.com/user-attachments/assets/db56b8b0-1844-4fa9-b5ef-dd8e0059e508" />



