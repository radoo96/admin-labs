# Windows Autopilot

W tym labie przygotowałem automatyczną konfigurację komputera dla pracownika zdalnego. Wykorzystałem Windows Autopilot device preparation, Intune i konto Hanny.

Scenariusz przetestowałem na maszynie PC04 w VirtualBox. Symulowała nowy laptop uruchamiany przez pracownika.

## Przygotowanie

Sprawdziłem konto Hanny, jej licencję oraz objęcie automatyczną rejestracją w Intune.

PC04 przygotowałem z Windows 11 Enterprise i połączeniem internetowym przez NAT.

- Pamięć RAM i rozmiar dysku:
  
<img width="790" height="127" alt="image" src="https://github.com/user-attachments/assets/68e1e280-28aa-42a9-ac31-5dd0482e0810" />

<img width="470" height="432" alt="image" src="https://github.com/user-attachments/assets/6d0b15df-a64c-4e75-beef-abb691bccb4d" />

## Grupy

Utworzyłem dwie grupy zabezpieczeń z członkostwem typu Assigned:

| Grupa | Przeznaczenie |
|---|---|
| GRP-Autopilot-Uzytkownicy | Użytkownicy objęci zasadą przygotowania, w tym Hanna |
| GRP-Autopilot-Urzadzenia | Urządzenia dodawane podczas przygotowania |

Właścicielem grupy urządzeń ustawiłem usługę `Intune Provisioning Client`.

<img width="1426" height="342" alt="image" src="https://github.com/user-attachments/assets/23b51284-cf05-4138-a658-ae85982cb0c1" />

Zasadę przygotowania przypisałem grupie użytkowników. Grupę urządzeń wykorzystałem do przypisania aplikacji instalowanej podczas wdrożenia.

## Aplikacja

Dla Company Portal dodałem przypisanie `Required` do `GRP-Autopilot-Urzadzenia`.

<img width="1475" height="727" alt="image" src="https://github.com/user-attachments/assets/73d0824e-f381-4cb4-aa06-21f5e79d3bbf" />

Sprawdziłem kontekst instalacji aplikacji i wybrałem ją również w zasadzie device preparation jako aplikację do zainstalowania podczas przygotowania.

## Zasada przygotowania

Utworzyłem zasadę `Autopilot-Praca-Zdalna`.

| Ustawienie | Wartość |
|---|---|
| Deployment mode | User-driven |
| Deployment type | Single user |
| Join type | Microsoft Entra joined |
| User account type | Standard User |
| Grupa urządzeń | GRP-Autopilot-Urzadzenia |
| Przypisanie do użytkowników | GRP-Autopilot-Uzytkownicy |
| Aplikacja podczas przygotowania | Company Portal |

<img width="661" height="782" alt="image" src="https://github.com/user-attachments/assets/a60c216a-1a22-4ef2-8b21-a9ab50434494" />

<img width="740" height="327" alt="image" src="https://github.com/user-attachments/assets/3e85a3d1-d2d8-4f40-8d22-0303694cce11" />

## Pierwsze uruchomienie PC04

Podczas konfiguracji Windows wybrałem konfigurację do pracy lub nauki i zalogowałem się kontem Hanny.

Sprawdziłem, czy przed wyświetleniem pulpitu pojawił się ekran przygotowania urządzenia i czy instalacja Company Portal zakończyła się poprawnie.

Komunikat o MFA


<img width="1001" height="776" alt="image" src="https://github.com/user-attachments/assets/ddaf8ed2-0a2d-422d-830d-da784ad56e49" />

<img width="992" height="793" alt="image" src="https://github.com/user-attachments/assets/7d9f8a52-18ab-4f9d-a54f-875a55a4145f" />

## Sprawdzenie uprawnień

Po zalogowaniu sprawdziłem lokalną grupę administratorów.

```cmd
net localgroup administrators
```

<img width="692" height="506" alt="image" src="https://github.com/user-attachments/assets/218c4010-6012-4c92-86d8-8664dfc8221f" />

Sprawdziłem też, czy czynność wymagająca uprawnień administratora prosi o dane innego konta.

<img width="635" height="735" alt="image" src="https://github.com/user-attachments/assets/b29179fd-df86-4a1a-8454-922f3e4ec76f" />

<img width="666" height="668" alt="image" src="https://github.com/user-attachments/assets/2f778e47-ab89-4910-b059-99837eab72b0" />

## Raport wdrożenia

W Intune otworzyłem raport Windows Autopilot device preparation deployments i sprawdziłem wpis dotyczący PC04.

<img width="1681" height="493" alt="image" src="https://github.com/user-attachments/assets/105600ef-4509-428f-8f8a-d8a5f2881b18" />

<img width="1445" height="502" alt="image" src="https://github.com/user-attachments/assets/28ef4de2-368f-4e0c-9764-6498c0b86a58" />

## Wnioski

Device preparation pozwala skonfigurować urządzenie podczas pierwszego uruchomienia przez pracownika. Administrator wcześniej przygotowuje zasady, grupy i przypisania aplikacji.

Grupa użytkowników określa, kogo obejmuje zasada. Grupa urządzeń zbiera komputery podczas wdrożenia i służy do przypisania wymaganych aplikacji.
