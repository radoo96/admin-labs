# Lab — Rejestracja urządzeń

- Trzy sposoby połączenia urządzenia z Entra ID.
- Włączenie automatycznej rejestracji w Entra ID Intune
- Ustawienie limitu urządzeń i wyglądu Portalu firmy.
- Laptop w VirtualBox i dołączenie go do Entra ID jako Marta.
- Sprawdzenie laptopa w Entra ID, w Intune

## Środowisko

| Element | Konfiguracja |
|---|---|
| Maszyna wirtualna | PC01 |
| System | Windows 11 Enterprise Evaluation |
| Pamięć | 4096 MB |
| Procesory | 2 |
| Dysk | 40 GB |
| Firmware i zabezpieczenia | EFI, Secure Boot, TPM 2.0 |
| Sieć | NAT |
| Użytkownik | Marta |

<img width="1061" height="831" alt="image" src="https://github.com/user-attachments/assets/a11e60f7-6d5d-4b90-975f-c567ba174137" />


Przed rozpoczęciem sprawdziłem licencję Intune Marty oraz jej członkostwo w `DYN-Pracownicy`.


## Sposób połączenia z Entra ID

| Stan urządzenia | Znaczenie |
|---|---|
| Entra registered | Urządzenie zarejestrowane w Entra, często używane w scenariuszu prywatnego sprzętu |
| Entra joined | Windows dołączony do Entra ID, z logowaniem kontem organizacji |
| Hybrid joined | Urządzenie dołączone do lokalnego AD i zarejestrowane w Entra ID |

Dla laptopa Marty wybrałem **Entra joined** z powodu braku AD.

Dołączenie do Entra ID i rejestracja w Intune to dwa osobne procesy. Obecność komputera w Entra nie wystarcza do potwierdzenia, że Intune nim zarządza.

## Ustawienia urządzeń w Entra ID

| Ustawienie | Wartość w labie |
|---|---|
| Users may join devices | Selected — `DYN-Pracownicy` |
| Users may register their devices | All |
| MFA przy rejestracji lub dołączeniu | Yes |
| Maximum number of devices per user | 5 |
| Dodawanie roli Global Administrator do lokalnych administratorów | Yes |
| Dodawanie użytkownika dołączającego jako lokalnego administratora | None |

<img width="678" height="853" alt="image" src="https://github.com/user-attachments/assets/749fc731-5a52-46c1-9ae0-114bd881c4c1" />


Ustawienie `None` skonfigurowałem przed dołączeniem laptopa. Marta ma pracować jako użytkownik standardowy.


## Automatyczna rejestracja w Intune

| Ustawienie | Wartość |
|---|---|
| MDM user scope | Some |
| Grupa objęta automatyczną rejestracją | `DYN-Pracownicy` |
| MAM user scope, jeśli dostępny w tym widoku | None |
| Limit urządzeń w zasadzie Intune | 5 |

<img width="985" height="722" alt="image" src="https://github.com/user-attachments/assets/79fcf6aa-b6c1-4d77-8615-6dea713ec31d" />

<img width="931" height="537" alt="image" src="https://github.com/user-attachments/assets/d7853450-b335-4a57-85f4-e5db728a338b" />


Zakres MDM decyduje, których użytkowników obejmuje automatyczna rejestracja. Nie zastępuje licencji ani pozostałych wymagań rejestracji.

## Portal firmy

<img width="862" height="800" alt="image" src="https://github.com/user-attachments/assets/4b23b2cd-5787-443a-828c-13fe6bc30c19" />

W konfiguracji Portalu firmy ustawiłem:

- nazwę organizacji: `FIRMA`;
- kontakt do IT;
- informację o sposobie zgłaszania problemów.

<img width="852" height="686" alt="image" src="https://github.com/user-attachments/assets/bfec900e-621b-41db-ada4-5079d19da125" />


## Dołączenie laptopa Marty

Podczas pierwszego uruchomienia Windows wybrałem konfigurację do pracy lub nauki i zalogowałem się kontem Marty.

<img width="832" height="585" alt="image" src="https://github.com/user-attachments/assets/415937fc-f588-405c-a875-05f687c48a43" />

<img width="983" height="735" alt="image" src="https://github.com/user-attachments/assets/f7d269cf-e0b5-40e3-91cd-55e9ea32b5cc" />

Po przygotowaniu pulpitu sprawdziłem połączenie poleceniem uruchomionym w sesji Marty:

```cmd
dsregcmd /status
```

| Pole | Oczekiwana wartość | 
|---|---|---|
| AzureAdJoined | YES | 
| DomainJoined | NO | 

<img width="895" height="283" alt="image" src="https://github.com/user-attachments/assets/0e60bc6f-b334-427c-8e2b-ba9c442ad10b" />

<img width="802" height="596" alt="image" src="https://github.com/user-attachments/assets/f811b74f-0127-41a2-a3ed-593d6c44f4c0" />


## Uprawnienia Marty

Sprawdziłem członkostwo lokalnej grupy administratorów oraz zachowanie przy próbie wykonania operacji wymagającej podniesienia uprawnień.

<img width="926" height="746" alt="image" src="https://github.com/user-attachments/assets/8882037a-ce0d-4dac-b145-8da9d4d79714" />


## Zdalna zmiana nazwy

Z Intune wysłałem polecenie **Rename device** z nazwą `PC01` i restartem.

<img width="1246" height="685" alt="image" src="https://github.com/user-attachments/assets/069792c1-4f38-4ab3-82e6-f84f8ea39423" />

<img width="822" height="132" alt="image" src="https://github.com/user-attachments/assets/3540bdff-5d30-4f93-8510-b7e7eb089827" />

<img width="275" height="76" alt="image" src="https://github.com/user-attachments/assets/230824e5-a4f3-474d-a61a-5956b85ecc93" />

<img width="1030" height="107" alt="image" src="https://github.com/user-attachments/assets/adfea8d0-0ef3-422a-8535-f258bd18c37e" />
