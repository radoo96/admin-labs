# Lab 2 — role administratorów

W tym ćwiczeniu rozdzieliłem zadania administracyjne w środowisku. Utworzyłem osobne konta administracyjne dla Ewy i Joanny, przetestowałem ich uprawnienia i przeniosłem rolę helpdesku z przypisania bezpośredniego na grupę.

- Przejrzenie wbudowanych ról i ich uprawnienia.
- Założenie konta admina dla Ewy i Joanny, osobne od ich kont do pracy.
- Nadanie im najmniejszych ról i sprawdzenie, czego nie mogą.
- Przeniesienie roli Ewy na grupę z możliwością przypisywania ról.
- Szukanie śladu nadania ról w dzienniku zmian.

## Konta i role

| Konto | Rola | Cel |
|---|---|---|
| adm-ewa.bak | Helpdesk Administrator | Resetowanie haseł użytkowników w dozwolonym zakresie |
| adm-ewa.bak | License Administrator | Zarządzanie przypisaniami licencji |
| adm-joanna.bak | Global Reader | Odczyt obsługiwanych ustawień administracyjnych |
| adm-joanna.bak | Billing Administrator | Obsługa rozliczeń — uprawnienia szersze niż sam odczyt |

Konta administracyjne oddzieliłem od kont używanych do codziennej pracy. Skonfigurowałem MFA i pozostawiłem puste pole Department, aby konta te nie trafiały do planowanych grup pracowników opartych na dziale.

W ramach labu przypisane jako "aktywne" jako test
<img width="567" height="592" alt="image" src="https://github.com/user-attachments/assets/4f4fe065-907d-4b87-8e3e-632c0178137f" />

<img width="1562" height="492" alt="image" src="https://github.com/user-attachments/assets/a87a7d14-3b46-4ee7-adaa-6154e15f3a2e" />

Ewa może zmieniać hasło użytkownikom (poza administratorami globalnymi) oraz dodawać licencje

<img width="237" height="166" alt="image" src="https://github.com/user-attachments/assets/693211c7-7ab9-4bc8-94b3-5f77ba2b4a09" />

<img width="867" height="728" alt="image" src="https://github.com/user-attachments/assets/4c642163-fe8b-4f83-8645-65511be39773" />

Dla admina brak opcji

<img width="261" height="137" alt="image" src="https://github.com/user-attachments/assets/cef03aee-0c7f-4a1d-96aa-6847d962b701" />

Ewa również nie może dodawać roli

<img width="710" height="122" alt="image" src="https://github.com/user-attachments/assets/d1b756ea-4000-4d01-b6fe-5293b96ca4f5" />

Role dla Joanny - Joanna może zobaczyć każde ustawienia platformy oraz rozliczenia. Nie może edytować.

<img width="1601" height="370" alt="image" src="https://github.com/user-attachments/assets/3706a56f-1e6a-4f2b-b248-6aecb8fece85" />

## Admini globalni

<img width="1602" height="457" alt="image" src="https://github.com/user-attachments/assets/dd437724-5112-414b-99c6-2a6d6a7525be" />

## Helpdesk przez grupę

Utworzyłem grupę zabezpieczeń `GRP-Rola-Helpdesk` z ustawieniami:

<img width="1640" height="605" alt="image" src="https://github.com/user-attachments/assets/c001c63d-95e0-4906-9008-a7bbbed0a5c7" />

| Ustawienie | Wartość |
|---|---|
| Microsoft Entra roles can be assigned to the group | Yes |
| Membership type | Assigned |
| Przypisana rola | Helpdesk Administrator |
| Członek | adm-ewa.sowa |

Najpierw przypisałem rolę grupie i dodałem Ewę jako członka. Następnie usunąłem jej bezpośrednie przypisanie Helpdesk Administrator.

<img width="1635" height="456" alt="image" src="https://github.com/user-attachments/assets/2298c75d-02c3-41e5-ab95-959ebe6e05e6" />

Po ponownym zalogowaniu sprawdziłem reset hasła Pawła.

<img width="240" height="161" alt="image" src="https://github.com/user-attachments/assets/538e76a0-0b53-470b-8fc4-22fea22e50e8" />

## Dziennik zmian

W Audit logs odszukałem operacje związane z nadaniem ról.

Sprawdziłem wykonawcę, obiekt docelowy, czas i wynik operacji.

<img width="858" height="26" alt="image" src="https://github.com/user-attachments/assets/61c9b896-660a-41d7-a888-0e28185009ba" />

## Moje uwagi

[Opisz napotkany problem lub obserwację, np. opóźnienie działania roli albo wynik testu odmowy dostępu.]

[← Lista labów Entra](README.md)
