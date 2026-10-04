# Lab 5 — Reset hasła, Temporary Access Pass i smart lockout

- Włączenie samoobsługowy reset hasła (SSPR) dla wszystkich pracowników.
- Ile metod potrzeba do resetu, i ustawienie rejestrację.
- Przetestujesz reset hasła
- Dasz Ewie rolę do wydawania kodu jednorazowego (TAP) i pomożesz Oli.
- Zablokujesz hasła z nazwą firmy.
- Ustawisz inteligentną blokadę konta i sprawdzisz, jak działa.

## Samoobsługowy reset hasła

SSPR włączyłem dla grupy `DYN-Pracownicy` z poprzedniego labu.

| Ustawienie | Wartość |
|---|---|
| Zakres SSPR | Selected — `DYN-Pracownicy` |
| Liczba metod wymaganych do resetu | 2 |
| Rejestracja przy logowaniu | Yes |
| Ponowne potwierdzanie informacji | Co 180 dni |
| Powiadomienie użytkownika o resecie | Yes |
| Powiadomienie administratorów o resecie konta administratora | Yes |

<img width="660" height="321" alt="image" src="https://github.com/user-attachments/assets/b79bb0d9-86fd-47bb-ad54-6362de2c0f5c" />

<img width="597" height="427" alt="image" src="https://github.com/user-attachments/assets/c53c5fbb-d4ca-484c-82f1-eb29595cbd91" />

<img width="510" height="302" alt="image" src="https://github.com/user-attachments/assets/f6fa0c41-15b4-4a84-9a60-228a7f0c622d" />

<img width="530" height="256" alt="image" src="https://github.com/user-attachments/assets/3a58af00-6433-4204-894a-f283c35641f5" />

<img width="492" height="252" alt="image" src="https://github.com/user-attachments/assets/b494de9d-8d56-40b5-838f-cfd52149c32e" />


Do testu wykorzystałem Microsoft Authenticator i SMS. Dwie metody zapewniają dodatkową weryfikację, ale jeśli obie są na tym samym telefonie, jego utrata może oznaczać utratę obu.

Zakres SSPR i dostępność metod to osobne ustawienia. Sprawdziłem zarówno członkostwo użytkownika w grupie, jak i dozwolone metody w Authentication methods policy.

## Test resetu hasła Kuby


Na koncie Kuby Wilka sprawdziłem zarejestrowane metody na stronie:
<img width="491" height="702" alt="image" src="https://github.com/user-attachments/assets/b1f84299-d928-4a76-ad2d-a95a7246558b" />

https://mysignins.microsoft.com/security-info

Następnie przeprowadziłem reset przez:

<img width="891" height="567" alt="image" src="https://github.com/user-attachments/assets/22920824-35db-4b88-a049-83d26d65603f" />

<img width="1547" height="320" alt="image" src="https://github.com/user-attachments/assets/fe7ad87e-338c-4a15-a509-7504cfafa13e" />

https://aka.ms/sspr

| Test | Wynik |
|---|---|
| Kuba należy do `DYN-Pracownicy` | [uzupełnij] |
| Ma dwie dostępne metody resetu | [uzupełnij] |
| Reset wymaga dwóch potwierdzeń | [uzupełnij] |
| Logowanie nowym hasłem działa | [uzupełnij] |
| Powiadomienie o resecie dotarło | [uzupełnij] |
| Operacja jest widoczna w Audit logs | [uzupełnij] |

## Temporary Access Pass

TAP wykorzystałem w scenariuszu, w którym Ola Bury straciła telefon i nie pamiętała hasła.

<img width="696" height="465" alt="image" src="https://github.com/user-attachments/assets/baaa2995-e4e0-4fab-aab9-36d463d96069" />

<img width="575" height="590" alt="image" src="https://github.com/user-attachments/assets/41f7ca3b-e261-4f97-84d0-496d2fa3a00c" />

<img width="702" height="392" alt="image" src="https://github.com/user-attachments/assets/650dd784-aba3-4759-b468-3cfcb253b0e7" />

<img width="697" height="557" alt="image" src="https://github.com/user-attachments/assets/b3050cc4-11c1-4a21-84d7-21c047502b65" />

<img width="580" height="300" alt="image" src="https://github.com/user-attachments/assets/e095117a-262d-49bc-bff5-d6b98534d87d" />



| Ustawienie | Wartość |
|---|---|
| Temporary Access Pass | Enabled |
| Zakres w labie | All users |
| Domyślna ważność | 1 godzina |
| Jednorazowe użycie | Yes |
| Konto obsługujące zgłoszenie | `adm-ewa.sowa` |
| Dodana rola | Authentication Administrator |

TAP może być jednorazowy albo wielokrotny. W tym ćwiczeniu wybrałem kod jednorazowy.

Ewie nadałem rolę umożliwiającą zarządzanie metodami zwykłych pracowników. Sama rola Helpdesk Administrator z wcześniejszego labu nie wystarczała do wydania TAP.

### Procedura odzyskania dostępu

1. Potwierdzenie tożsamości Oli niezależnie od utraconego telefonu.
2. Wydanie jednorazowego TAP z ograniczonym czasem ważności.
3. Bezpieczne przekazanie kodu Oli.
4. Logowanie kodem TAP i rejestracja nowych metod.
5. Reset zapomnianego hasła przez SSPR.
6. Sprawdzenie logowania i usunięcie nieaktualnych metod związanych ze zgubionym urządzeniem.

TAP umożliwia odzyskanie dostępu i rejestrację metod. Samo jego wydanie nie zmienia hasła użytkownika.

| Test | Wynik |
|---|---|
| Ewa może wydać TAP Oli | [uzupełnij] |
| Pierwsze logowanie kodem działa | [uzupełnij] |
| Rejestracja nowych metod działa | [uzupełnij] |
| Ponowne użycie kodu w nowym logowaniu jest odrzucone | [uzupełnij] |
| Ola może zresetować hasło i zalogować się | [uzupełnij] |

Kodu TAP, haseł i kodów QR nie zapisuję w dokumentacji repozytorium.

## Ochrona haseł


<img width="691" height="518" alt="image" src="https://github.com/user-attachments/assets/26ef2f5b-821c-4bdf-b206-37a366b76233" />


Włączyłem własną listę zakazanych haseł i dodałem:

```text
Rachmistrz
rachunkowosc
ksiegowosc
faktura
Joanna
```

Lista uzupełnia globalną ochronę Microsoftu. Mechanizm uwzględnia normalizację znaków oraz ocenę punktową hasła, więc nie działa jak prosty zakaz wystąpienia danego słowa.

| Test | Wynik |
|---|---|
| Enforce custom list | [uzupełnij] |
| Próba ustawienia hasła z instrukcji | [zaakceptowane / odrzucone] |
| Treść komunikatu | [uzupełnij] |

Samo przyjęcie hasła zawierającego nazwę firmy nie wystarcza, żeby uznać konfigurację za błędną. Trzeba uwzględnić sposób oceny całego hasła.

<img width="473" height="420" alt="image" src="https://github.com/user-attachments/assets/d609c1e1-c769-409c-aa10-da69de96cbda" />


## Inteligentna blokada
<img width="715" height="501" alt="image" src="https://github.com/user-attachments/assets/e2b0cc07-f01a-44ca-9746-dbb3ad5ede4d" />

<img width="568" height="535" alt="image" src="https://github.com/user-attachments/assets/fe729fe7-31ec-4ebb-8cfc-979811456cdf" />


Ustawiłem:

| Parametr | Wartość |
|---|---|
| Lockout threshold | 8 |
| Lockout duration in seconds | 120 |

Test przeprowadziłem na koncie Pawła Gila.

Smart lockout nie jest prostym licznikiem każdego wpisania złego hasła. Uwzględnia między innymi powtarzające się błędne hasła oraz znane i nieznane miejsca logowania. Dlatego nie zakładam, że blokada pojawi się dokładnie po ósmym kliknięciu.
 |
