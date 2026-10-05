# Lab 6 — Conditional Access

- Przygotowanie grupy wykluczeń z kontami awaryjnymi.
- Utworzenie trzech reguł w trybie próbnym.
- Sprawdzenie je narzędziem What If i w dzienniku logowań.
- Przejście z security defaults na Conditional Access.

<img width="690" height="331" alt="image" src="https://github.com/user-attachments/assets/4661b319-741f-45d8-8536-bd0c1ab41869" />

Utworzyłem grupę zabezpieczeń `GRP-CA-Wykluczenia` z członkostwem Assigned. Dodałem do niej konta `awaryjne01` i `awaryjne02`.

Grupę wykluczyłem z trzech reguł tego labu. Samo utworzenie grupy nie wystarcza — jej wykluczenie trzeba sprawdzić w każdej zasadzie.


## Reguły dostępu

| Reguła | Użytkownicy | Zasoby i warunki | Decyzja | Powód |
|---|---|---|---|---|
| `CA001 - MFA dla wszystkich` | All users | All resources | Require multifactor authentication | Samo hasło nie wystarcza do uzyskania dostępu |
| `CA002 - Blokuj starsze protokoły` | All users | All resources; Exchange ActiveSync clients i Other clients | Block access | Ograniczenie starszych metod uwierzytelniania, które nie obsługują MFA |
| `CA003 - Blokuj portale admina dla pracowników` | `DYN-Pracownicy` | Microsoft Admin Portals | Block access | Oddzielenie codziennej pracy od administracji |

Wszystkie trzy reguły mają wykluczenie `GRP-CA-Wykluczenia`.

<img width="567" height="846" alt="image" src="https://github.com/user-attachments/assets/2ce518da-8f21-4dbb-8be6-ca29371358ce" />

<img width="622" height="720" alt="image" src="https://github.com/user-attachments/assets/9c9d41a1-b400-46f5-a4b7-64176ba73138" />


CA002 dotyczy starszego uwierzytelniania wskazanego w warunkach Client apps. Nie jest ogólną blokadą każdego programu pocztowego.

## Dlaczego CA003 obejmuje grupę pracowników

W tym projekcie grupa `DYN-Pracownicy` korzysta między innymi z atrybutu Department. Zwykłe konta pracowników mają go uzupełnionego, a oddzielne konta administracyjne pozostają poza grupą.

Microsoft Admin Portals obejmuje określoną grupę portali. Nie traktuję tej reguły jako blokady wszystkich API i narzędzi administracyjnych. Uprawnienia do wykonywania operacji nadal wynikają z przypisanych ról.

## Testy What If

Reguły najpierw ustawiłem w trybie Report-only.

<img width="707" height="315" alt="image" src="https://github.com/user-attachments/assets/bef295f9-4867-41ce-83e9-927ab36e53ae" />

<img width="651" height="380" alt="image" src="https://github.com/user-attachments/assets/b6934c91-7525-4b7b-9e18-4283c167d48b" />


W testach wskazywałem użytkownika, zasób i typ aplikacji klienckiej. Dla prób wejścia do portalu wybierałem Browser, a dla CA002 osobno sprawdzałem starszego klienta.

## Przejście z security defaults

<img width="357" height="612" alt="image" src="https://github.com/user-attachments/assets/01b57272-efbf-4088-8bc2-46ff53d1becc" />

<img width="877" height="852" alt="image" src="https://github.com/user-attachments/assets/7e48c652-1fd7-463c-b825-3a03a6aa4a71" />

<img width="662" height="716" alt="image" src="https://github.com/user-attachments/assets/bd9fd5f6-31eb-4947-9d0d-47bf92f31b2e" />

Przygotowałem konfigurację i testy przed przełączeniem ochrony. Po wyłączeniu security defaults włączyłem przygotowane reguły CA001 i CA002.

CA003 pozostawiłem w Report-only do sprawdzenia logowania pracownika w dzienniku. Po potwierdzeniu zakresu reguły przetestowałem jej działanie w stanie On.

Report-only nie zastępuje aktywnej ochrony — zapisuje przewidywany wynik, ale nie egzekwuje wymagań reguły.
