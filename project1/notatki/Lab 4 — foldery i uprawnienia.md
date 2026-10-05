# Lab 4 — foldery i uprawnienia

W labie utworzyłem wspólne foldery dla Zielonego Domu. Dostęp przypisałem grupom utworzonym w labie 2, a mapowanie dysku S: skonfigurowałem przez GPO.

Jeden serwer pełni rolę kontrolera domeny i serwera plików.

## Foldery i dostęp

Utworzyłem katalog `C:\Dane` z trzema podfolderami i udostępniłem go jako `\\DC01\Dane`.

Docelowe uprawnienia pracowników:

| Folder | Grupa | Uprawnienia NTFS |
|---|---|---|
| Ksiegowosc | GRP-Ksiegowosc | Modify |
| Ksiegowosc | GRP-Zarzad | Read & execute |
| Sprzedaz | GRP-Sprzedaz | Modify |
| Sprzedaz | GRP-Zarzad | Read & execute |
| Wspolne | Domain Users | Modify |

## Konfiguracja udziału i NTFS

Na poziomie udziału usunąłem `Everyone` i nadałem `Authenticated Users` uprawnienie `Full Control`. Szczegółowy dostęp do folderów ustawiłem przez NTFS.

W katalogu `C:\Dane` wyłączyłem dziedziczenie, przekształcając odziedziczone wpisy w jawne. Usunąłem wpisy `Users` i `Authenticated Users`, pozostawiając wpisy administracyjne, `SYSTEM` oraz `CREATOR OWNER`.

Grupie `Domain Users` nadałem `Read & execute` z zakresem `This folder only`. Dzięki temu użytkownicy mogą otworzyć katalog główny udziału, ale ten wpis nie daje im dostępu do zawartości wszystkich podfolderów.

Na podfolderach dodałem uprawnienia zgodnie z tabelą.

<img width="520" height="515" alt="image" src="https://github.com/user-attachments/assets/5a37368d-6342-4fe4-8c37-2bba035d7a63" />

<img width="382" height="497" alt="image" src="https://github.com/user-attachments/assets/bf3485b1-331c-430e-9ec9-467707d6be7e" />

<img width="362" height="485" alt="image" src="https://github.com/user-attachments/assets/6e7a0e85-0fc7-470d-9d35-29f8b75679a1" />

<img width="476" height="553" alt="image" src="https://github.com/user-attachments/assets/17b21e68-ec3e-40c3-a469-f2aa47906ea3" />

## Ukrywanie folderów

Włączyłem Access-Based Enumeration (ABE) dla udziału `Dane`. Ukrywa ono podczas przeglądania udziału foldery, do których użytkownik nie ma dostępu. Sam dostęp nadal kontrolują uprawnienia.

## Mapowanie dysku S:

Utworzyłem GPO `U-Uzytkownicy-DyskS` i podpiąłem je do OU `ZielonyDom/Uzytkownicy`.

W `User Configuration → Preferences → Windows Settings → Drive Maps` dodałem:

| Ustawienie | Wartość |
|---|---|
| Action | Update |
| Location | `\\DC01\Dane` |
| Label as | Dane firmy |
| Drive Letter | S: |

## Sprawdzenie dostępu

Konto Adama 

<img width="527" height="216" alt="image" src="https://github.com/user-attachments/assets/2947d825-6327-4e33-a5bd-e75dbf3f2592" />

<img width="788" height="577" alt="image" src="https://github.com/user-attachments/assets/718d5227-becc-4088-8bb8-728d9626717c" />


