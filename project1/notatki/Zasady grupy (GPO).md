# Zasady grupy (GPO)

Zostały skonfigurowane trzy zasady grupy w domenie `ad.zielonydom.test`. Ustawienia przygotowałem na DC01 w konsoli Group Policy Management, a ich działanie sprawdzałem na PC01.

## Skonfigurowane zasady

Wszystkie poniższe ścieżki OU znajdują się pod `ZielonyDom`.

| GPO | Podpięcie do OU | Działanie |
|---|---|---|
| C-Komputery-Komunikat | Komputery | Komunikat o komputerze firmowym przed logowaniem |
| U-Uzytkownicy-BlokadaEkranu | Uzytkownicy | Wygaszacz po 60 sekundach i wymagane hasło przy powrocie |
| U-Recepcja-BezPanelu | Uzytkownicy/Recepcja | Zablokowany dostęp do Panelu sterowania i Ustawień |

## Co zrobiłem oraz wyniki

W konsoli `gpmc.msc` sprawdziłem ustawienia istniejącej `Default Domain Policy`, a następnie utworzyłem osobne GPO dla poszczególnych ustawień.

Komunikat logowania skonfigurowałem w części `Computer Configuration` i podpiąłem do OU z komputerem PC01. Ustawiłem tytuł „Zielony Dom” i informację o służbowym przeznaczeniu komputera.

<img width="700" height="642" alt="image" src="https://github.com/user-attachments/assets/60e7073d-7bc5-41be-a228-520e48246ce6" />

Zasadę wygaszacza skonfigurowałem w `User Configuration`. Włączyłem wygaszacz, ochronę hasłem i limit bezczynności wynoszący 60 sekund.

<img width="1615" height="835" alt="image" src="https://github.com/user-attachments/assets/13f5016c-27eb-4865-90b8-169e94abf922" />

Dla recepcji utworzyłem OU `Recepcja` wewnątrz `Uzytkownicy` i przeniosłem tam konto Daniela. Do tego OU podpiąłem zasadę blokującą Panel sterowania i Ustawienia.

<img width="1521" height="126" alt="image" src="https://github.com/user-attachments/assets/51f5db1f-bb56-45ac-92f4-8fa621918673" />
<img width="1346" height="196" alt="image" src="https://github.com/user-attachments/assets/d21d8930-22ee-4018-bb20-4ee8a5723115" />

Komunikat przed logowaniem po restarcie PC01 

<img width="683" height="370" alt="image" src="https://github.com/user-attachments/assets/9c7b4011-36ba-4fef-afd1-5e41371c01e0" />

Panel sterowania na koncie Daniela 

<img width="781" height="276" alt="image" src="https://github.com/user-attachments/assets/14940849-42f4-4bdc-b09d-ef13a814b91e" />

Weryfikacja w konsoli 'gpresult /r'

<img width="752" height="612" alt="image" src="https://github.com/user-attachments/assets/61e5e9e1-dc81-4687-924c-a14ddd6e43b9" />

Panel sterowania na koncie Adama 

<img width="787" height="618" alt="image" src="https://github.com/user-attachments/assets/ffe6aea7-3103-4536-9ad4-e17a50170d4d" />

<img width="731" height="501" alt="image" src="https://github.com/user-attachments/assets/84ee3e85-35bc-484f-9601-318cdea2be58" />



