# Lab 8 — Goście i współpraca z klientami

W tym labie przygotowałem dostęp zewnętrzny dla klientów Rachmistrza. Skonfigurowałem zasady zapraszania, przetestowałem konto gościa i udostępnienie folderu na dokumenty klienta.

## Ustawienia współpracy
<img width="1378" height="828" alt="image" src="https://github.com/user-attachments/assets/220a9de8-f5d4-4004-97c4-c093d930457e" />
<img width="507" height="238" alt="image" src="https://github.com/user-attachments/assets/b92f64ac-f09a-4e51-9188-6d866f02f445" />
<img width="645" height="558" alt="image" src="https://github.com/user-attachments/assets/075a78a4-c43f-4c5a-9ca1-a9556ea10a00" />
<img width="613" height="606" alt="image" src="https://github.com/user-attachments/assets/b93b9deb-f773-4ac4-a21c-42a965be6db2" />
<img width="1121" height="22" alt="image" src="https://github.com/user-attachments/assets/7dd75961-0f47-44cb-8c29-837d4f32e0be" />
<img width="623" height="505" alt="image" src="https://github.com/user-attachments/assets/98b78dd3-7065-43cc-9f4d-b3f17b260705" />
<img width="557" height="456" alt="image" src="https://github.com/user-attachments/assets/4bde4445-904c-4147-a305-a23308da469e" />
<img width="312" height="225" alt="image" src="https://github.com/user-attachments/assets/dbe8ea29-5761-4c6c-b5ff-5f84dad90494" />
<img width="1302" height="372" alt="image" src="https://github.com/user-attachments/assets/662f6bb4-09cc-4920-97c1-25e9fa451a61" />
<img width="1388" height="417" alt="image" src="https://github.com/user-attachments/assets/a6579c7c-7c31-4df9-b197-cf49bd8ab7f8" />
<img width="1572" height="548" alt="image" src="https://github.com/user-attachments/assets/e31fb990-d087-4030-b64b-d0137b2d8bbd" />
<img width="667" height="411" alt="image" src="https://github.com/user-attachments/assets/1718d297-7efd-4073-897e-b6b63f062ab4" />
<img width="1287" height="476" alt="image" src="https://github.com/user-attachments/assets/d61091dc-97ca-42d8-9e70-c30c298c0f31" />
<img width="585" height="446" alt="image" src="https://github.com/user-attachments/assets/c15dfddb-9d8e-471c-be26-623771d2db66" />
<img width="531" height="417" alt="image" src="https://github.com/user-attachments/assets/af7c336d-a4bd-41b2-9d1c-afa77507aacb" />
<img width="737" height="480" alt="image" src="https://github.com/user-attachments/assets/e3946beb-2439-42bc-932e-89215727f87f" />
<img width="782" height="372" alt="image" src="https://github.com/user-attachments/assets/f92a6aba-628d-4d87-95fd-e96090bee1aa" />
<img width="556" height="465" alt="image" src="https://github.com/user-attachments/assets/29e0acd8-335c-4552-a698-c6eb80a7c1e6" />


| Ustawienie | Konfiguracja |
|---|---|
| Dostęp gości do katalogu | Najbardziej ograniczony poziom |
| Zapraszanie gości | Tylko użytkownicy z odpowiednimi rolami administracyjnymi |
| Samodzielna rejestracja przez user flows | Wyłączona |
| Samodzielne opuszczenie organizacji | Dozwolone |
| Domeny zaproszeń | Bez listy ograniczającej domeny |
| Email one-time passcode | Włączony |

Nie ograniczałem zaproszeń do wybranych domen, ponieważ klienci korzystają również z prywatnych skrzynek. Kontrolę oparłem na tym, kto może zapraszać i kto zatwierdza dostęp.

Ograniczenie widoczności katalogu Entra nie zastępuje uprawnień do plików. Dostęp klientów do dokumentów sprawdzam osobno w SharePoint.

## Rola Ewy i pierwsze zaproszenie

Kontu `adm-ewa.sowa` przypisałem rolę **Guest Inviter**. Zapraszanie klientów odbywa się z oddzielnego konta administracyjnego.

Jako pierwszą klientkę dodałem testowe konto:

| Pole | Wartość |
|---|---|
| Nazwa | Halina Kłos (Piekarnia Kłos) |
| Company name | Piekarnia Kłos |
| User type | Guest |
| Status zaproszenia po teście | [uzupełnij] |
| Sposób uwierzytelnienia | [uzupełnij] |
| Wynik rejestracji lub użycia MFA | [uzupełnij] |

Rolę Haliny odgrywał mój dodatkowy adres e-mail. Nie publikuję go w repozytorium.

Samo zaproszenie do tenanta nie daje dostępu do dokumentów. Uprawnienie do folderu nadałem w osobnym kroku.

## Conditional Access i MFA

CA001 obejmuje `All users`, więc uwzględnia także gości, o ile nie zostali wykluczeni.

W What If sprawdziłem Halinę dla konkretnego zasobu i typu klienta Browser. Przy testowaniu reguł ryzyka podawałem również odpowiedni poziom ryzyka — samo wskazanie gościa nie powoduje zastosowania CA004 i CA005.

| Sprawdzenie | Wynik |
|---|---|
| CA001 — wymóg MFA | [uzupełnij] |
| CA003 — brak członkostwa w DYN-Pracownicy | [uzupełnij] |
| CA004 — test z ryzykiem logowania | [uzupełnij] |
| CA005 — ocena wpływu na gości | [uzupełnij] |

Gość nie trafia do `DYN-Pracownicy`, ponieważ reguła tej grupy wymaga `userType = Member`. Nie otrzymuje więc automatycznie przypisanych do niej licencji pracowniczych. Nie oznacza to, że wszystkie funkcje External ID są bezpłatne.

### Zaufanie do MFA partnerów

Sprawdziłem ustawienia **Cross-tenant access → Inbound → Trust settings**.

Zaufanie do MFA z innego tenanta może pozwolić uznać uwierzytelnienie wykonane w organizacji partnera. Nie jest to to samo co logowanie kodem e-mail.

Zakres zastosowanego zaufania: **[ustawienia domyślne / konkretna organizacja / bez zmian]**.

Uzasadnienie: **[uzupełnij]**.

Włączenie zaufania w ustawieniach domyślnych ma szerszy zakres niż ustawienie go dla jednego sprawdzonego partnera.

## Zaproszenia zbiorcze i grupa gości

Do zaproszeń zbiorczych wykorzystałem szablon pobrany z portalu. Zachowałem jego nagłówki i użyłem wyłącznie kontrolowanych przeze mnie adresów testowych.

| Operacja | Wynik |
|---|---|
| Liczba zaproszeń w CSV | [uzupełnij] |
| Liczba poprawnie przetworzonych zaproszeń | [uzupełnij] |
| Liczba przyjętych zaproszeń | [uzupełnij] |

Status `Succeeded` operacji zbiorczej nie oznacza jeszcze przyjęcia zaproszenia przez odbiorcę.

Utworzyłem grupę dynamiczną `DYN-Goscie`:

```text
(user.userType -eq "Guest")
```

Grupa służy do identyfikowania gości. Nie przyznałem jej wspólnego dostępu do dokumentów wszystkich klientów.

Ta reguła obejmuje również gości z nieprzyjętym zaproszeniem oraz konta wyłączone.

## SharePoint i folder klienta

Dla SharePoint i OneDrive ustawiłem poziom **Existing guests**. Sprawdziłem również ustawienia udostępniania konkretnej witryny.

Na witrynie księgowości przygotowałem folder `Piekarnia Klos`. Halinie nadałem dostęp do tego folderu z prawem edycji, bez dodawania jej do całego zespołu księgowości.

| Test | Wynik |
|---|---|
| Halina otwiera folder | [uzupełnij] |
| Halina wgrywa dokument testowy | [uzupełnij] |
| Halina nie ma dostępu do folderu innego klienta | [uzupełnij] |
| Udostępnienie nowemu adresowi spoza katalogu | [uzupełnij] |

Existing guests ogranicza udostępnianie do osób już obecnych w katalogu. Nadal trzeba sprawdzać, czy wybrany gość jest właściwym odbiorcą danych.

![Goście w środowisku Rachmistrz](zrzuty/lab08.png)

## Zakończenie współpracy

Na jednym koncie testowym przećwiczyłem wyłączenie i ponowne włączenie logowania.

Wynik: **[uzupełnij]**.

Przy zakończeniu rzeczywistej współpracy trzeba również odebrać uprawnienia do zasobów i uwzględnić aktywne sesje. Samo opuszczenie organizacji przez gościa nie oznacza usunięcia wszystkich dokumentów i danych dotyczących tej osoby.

## Moje uwagi

- Najważniejsza obserwacja: **[uzupełnij]**.
- Problem podczas testów: **[uzupełnij albo wpisz „brak”]**.
- Rozwiązanie: **[uzupełnij]**.

[Procedura: nowy klient](procedury/nowy-klient.md)

[← Lista labów Entra ID](README.md)
