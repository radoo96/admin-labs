# Lab 8 — Goście i współpraca z klientami

- Ustawienie współpracy zewnętrznej: kto zaprasza, co widzą goście, jak się logują.
- Danie adm-ewa rolę Guest Inviter.
- Zaproszenie pierwszego gościa
- Zebranie gości w grupie dynamicznej.
- Ograniczenie udostępniania w SharePoint do istniejących gości.

## Ustawienia współpracy
<img width="1378" height="828" alt="image" src="https://github.com/user-attachments/assets/220a9de8-f5d4-4004-97c4-c093d930457e" />
<img width="507" height="238" alt="image" src="https://github.com/user-attachments/assets/b92f64ac-f09a-4e51-9188-6d866f02f445" />


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

Kontu `adm-ewa` przypisałem rolę **Guest Inviter**. Zapraszanie klientów odbywa się z oddzielnego konta administracyjnego.

<img width="645" height="558" alt="image" src="https://github.com/user-attachments/assets/075a78a4-c43f-4c5a-9ca1-a9556ea10a00" />

<img width="613" height="606" alt="image" src="https://github.com/user-attachments/assets/b93b9deb-f773-4ac4-a21c-42a965be6db2" />

<img width="1121" height="22" alt="image" src="https://github.com/user-attachments/assets/7dd75961-0f47-44cb-8c29-837d4f32e0be" />

<img width="623" height="505" alt="image" src="https://github.com/user-attachments/assets/98b78dd3-7065-43cc-9f4d-b3f17b260705" />

Rolę Haliny odgrywał mój dodatkowy adres e-mail. Nie publikuję go w repozytorium.

Samo zaproszenie do tenanta nie daje dostępu do dokumentów. Uprawnienie do folderu nadałem w osobnym kroku.

<img width="312" height="225" alt="image" src="https://github.com/user-attachments/assets/dbe8ea29-5761-4c6c-b5ff-5f84dad90494" />

<img width="1302" height="372" alt="image" src="https://github.com/user-attachments/assets/662f6bb4-09cc-4920-97c1-25e9fa451a61" />

### Zaufanie do MFA partnerów

<img width="557" height="456" alt="image" src="https://github.com/user-attachments/assets/4bde4445-904c-4147-a305-a23308da469e" />

<img width="1388" height="417" alt="image" src="https://github.com/user-attachments/assets/a6579c7c-7c31-4df9-b197-cf49bd8ab7f8" />

Zaufanie do MFA z innego tenanta może pozwolić uznać uwierzytelnienie wykonane w organizacji partnera. Nie jest to to samo co logowanie kodem e-mail.

# Utworzenie grupy dynamicznej `DYN-Goscie`:

```text
(user.userType -eq "Guest")
```

<img width="1572" height="548" alt="image" src="https://github.com/user-attachments/assets/e31fb990-d087-4030-b64b-d0137b2d8bbd" />
<img width="667" height="411" alt="image" src="https://github.com/user-attachments/assets/1718d297-7efd-4073-897e-b6b63f062ab4" />

Grupa służy do identyfikowania gości. Nie przyznałem jej wspólnego dostępu do dokumentów wszystkich klientów.

Ta reguła obejmuje również gości z nieprzyjętym zaproszeniem oraz konta wyłączone.

## SharePoint i folder klienta

Dla SharePoint i OneDrive ustawiłem poziom **Existing guests**. Sprawdziłem również ustawienia udostępniania konkretnej witryny.

<img width="1287" height="476" alt="image" src="https://github.com/user-attachments/assets/d61091dc-97ca-42d8-9e70-c30c298c0f31" />
<img width="585" height="446" alt="image" src="https://github.com/user-attachments/assets/c15dfddb-9d8e-471c-be26-623771d2db66" />
<img width="531" height="417" alt="image" src="https://github.com/user-attachments/assets/af7c336d-a4bd-41b2-9d1c-afa77507aacb" />
<img width="737" height="480" alt="image" src="https://github.com/user-attachments/assets/e3946beb-2439-42bc-932e-89215727f87f" />


## Zakończenie współpracy

Na jednym koncie testowym przećwiczyłem wyłączenie konta

<img width="782" height="372" alt="image" src="https://github.com/user-attachments/assets/f92a6aba-628d-4d87-95fd-e96090bee1aa" />
<img width="556" height="465" alt="image" src="https://github.com/user-attachments/assets/29e0acd8-335c-4552-a698-c6eb80a7c1e6" />
