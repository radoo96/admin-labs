## Intune Rejestracja, grupy dynamiczne, blokady, zgodności


PC02 korzysta z połączenia internetowego przez NAT w VirtualBox. Nie jest członkiem lokalnej domeny `ad.zielonydom.test`.

## Rejestracja urządzenia

Włączyłem automatyczną rejestrację w Intune, ustawiając `MDM user scope` na `All`. 

<img width="547" height="126" alt="image" src="https://github.com/user-attachments/assets/9e6825ca-eec8-481f-a060-7882d5ba8de6" />

Podczas konfiguracji Windows 11 Enterprise wybrałem konfigurację do pracy lub nauki i zalogowałem się kontem Filipa.

<img width="876" height="552" alt="image" src="https://github.com/user-attachments/assets/b239816d-27a8-4c5c-bb2d-3ff405855eca" />

Na PC02 uruchomiłem:

```cmd
dsregcmd /status
```

<img width="736" height="298" alt="image" src="https://github.com/user-attachments/assets/4f58b4af-ab3b-489b-b2b3-66001b1fe08a" />

## Grupa dynamiczna

Utworzyłem grupę zabezpieczeń `GRP-Komputery-Windows` z członkostwem typu `Dynamic Device`.

Reguła członkostwa:

```text
(device.deviceOSType -eq "Windows")
```

<img width="1382" height="547" alt="image" src="https://github.com/user-attachments/assets/d6180b93-6343-44df-b029-ec378f381970" />

Po przetworzeniu reguły sprawdziłem, czy komputer Filipa pojawił się w grupie. Do tej grupy przypisałem profil konfiguracji i zasadę zgodności.

<img width="1455" height="437" alt="image" src="https://github.com/user-attachments/assets/0475db90-2e54-4d4d-97c2-5922b901a8d1" />

## Profil konfiguracji

W Settings catalog utworzyłem profil `Windows-Komunikat-i-BlokadaEkranu`.

| Ustawienie | Wartość |
|---|---|
| Interactive Logon Machine Inactivity Limit | 600 sekund |
| Interactive Logon Message Title For Users Attempting To Log On | Zielony Dom |
| Interactive Logon Message Text For Users Attempting To Log On | Komputer firmowy. Korzystanie tylko do celów służbowych. |

<img width="746" height="843" alt="image" src="https://github.com/user-attachments/assets/51456e8f-c46f-4c37-a22f-aded2972f6a4" />

Uruchomiłem synchronizację urządzenia i ponownie uruchomiłem Windows. Sprawdziłem komunikat przed logowaniem, blokadę po bezczynności oraz status profilu w Intune.

<img width="737" height="467" alt="image" src="https://github.com/user-attachments/assets/c84e67c4-f866-4c55-bc24-d7550a924dae" />

## Porównanie z GPO

| Element | Lab 3 — GPO | Lab 8 — Intune |
|---|---|---|
| Komputer | PC01 w lokalnej domenie AD | PC02 dołączony do Entra ID |
| Przypisanie ustawień | Podpięcie GPO do OU | Przypisanie profilu do grupy |
| Pobieranie nowych ustawień | Łączność z kontrolerem domeny | Łączność z usługą Intune przez internet |
| Ręczne odświeżenie | gpupdate /force | Sync |
| Blokada ekranu | Wygaszacz użytkownika chroniony hasłem | Limit bezczynności komputera |

Efekt blokady jest podobny, ale w obu labach wykorzystałem inne ustawienia. Komunikat logowania skonfigurowałem przez odpowiadające sobie opcje zabezpieczeń.

## Zasada zgodności

Utworzyłem zasadę `Windows-Zgodnosc-Podstawowa` i przypisałem ją do `GRP-Komputery-Windows`.

Wymagania:

- Firewall: Require.
- Antivirus: Require.
- Microsoft Defender Antimalware: Require.

<img width="1010" height="412" alt="image" src="https://github.com/user-attachments/assets/c4dd91bd-ab93-4ba5-9510-5d4e17b9af12" />

## Test wyłączenia zapory

Na PC02 tymczasowo wyłączyłem zaporę dla aktywnego profilu sieciowego i uruchomiłem synchronizację. Następnie sprawdziłem ocenę zgodności w Intune.
Pierwsze zalogowane konto w Intune ma domyślnie administratora lokalnego

<img width="696" height="580" alt="image" src="https://github.com/user-attachments/assets/27e7ca80-c0a1-4710-9c25-5b46347d0a25" />

<img width="1292" height="372" alt="image" src="https://github.com/user-attachments/assets/650927c2-8490-46b4-b8ea-f06cc5205634" />

Po teście ponownie włączyłem zaporę i powtórzyłem synchronizację.
