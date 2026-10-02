# Lab 3 — licencje i grupy dynamiczne

W tym ćwiczeniu zautomatyzowałem przypisywanie licencji pracownikom. Utworzyłem grupę dynamiczną, przeniosłem licencje z przypisań bezpośrednich na grupowe i sprawdziłem działanie na nowym koncie.

- Utworzenie grupy dynamicznej wszystkich pracowników i przetestowanie jej reguły.
- Przypisanie licencji grupie i usuniecie przypisania ręcznie.
- Zmiana grupy działów na dynamiczną.
- Założenie konta nowej pracownicy i sprawdzenie automatycznego przypisania.
- Sprawdzenie, co się dzieje z licencją po wyłączeniu konta.

## Grupa pracowników

Utworzyłem grupę zabezpieczeń `DYN-Pracownicy` z członkostwem typu Dynamic User.

Reguła:

```text
(user.userType -eq "Member") and (user.accountEnabled -eq true) and (user.department -ne null)
```

Reguła wybiera aktywne konta typu Member z uzupełnionym działem. W tym laboratorium konta administracyjne i awaryjne mają puste Department, dlatego pozostają poza grupą.

<img width="1606" height="567" alt="image" src="https://github.com/user-attachments/assets/bd728cef-bf0e-4231-80ca-a919a40f4d8f" />

„pracownik, a nie gość”, „konto włączone”, „ma wpisany dział”. Konta admina i konta awaryjne nie mają działu (lab 2), więc licencji nie dostaną.

Przed zapisaniem sprawdziłem regułę w Validate Rules.

| Konto | Oczekiwany wynik |
|---|---|---|
| Marta | Spełnia regułę | 
| Kuba | Spełnia regułę | 
| adm-ewa.sowa | Nie spełnia reguły | 

<img width="1642" height="466" alt="image" src="https://github.com/user-attachments/assets/339112bd-742f-4c55-9136-bc677d249f9d" />

<img width="677" height="586" alt="image" src="https://github.com/user-attachments/assets/824a5f98-7302-4d76-96f6-658af2ea5988" />

## Licencja przez grupę

W Microsoft 365 admin center przypisałem produkt do `DYN-Pracownicy`.

Dopiero po potwierdzeniu działającej licencji grupowej usunąłem zbędne przypisania bezpośrednie u Kuby i na moim zwykłym koncie.

<img width="887" height="823" alt="image" src="https://github.com/user-attachments/assets/5a56b272-e1a6-4577-a818-bb6ebbe44265" />

<img width="967" height="282" alt="image" src="https://github.com/user-attachments/assets/41b7ad9e-8d4b-49ed-9339-7753d26f4886" />

## Dynamiczne grupy działów

Zmieniłem członkostwo pięciu grup działowych z Assigned na Dynamic User.

| Grupa | Wartość Department |
|---|---|
| GRP-Zarzad | Zarzad |
| GRP-Ksiegowosc | Ksiegowosc |
| GRP-Kadry | Kadry |
| GRP-Obsluga | ObslugaKlienta |
| GRP-Biuro | Biuro |

Początkowo reguły sprawdzały tylko dział. Po teście wyłączenia konta dodałem warunek aktywności. W końcowej wersji uwzględniłem również typ Member.

Przykład dla kadr:

```text
(user.department -eq "Kadry")
```

<img width="1382" height="276" alt="image" src="https://github.com/user-attachments/assets/b087dd51-dc49-4b82-921c-7273c121db7a" />

<img width="1571" height="243" alt="image" src="https://github.com/user-attachments/assets/bb62fe16-c319-4337-b93b-d0acc7653d65" />

Pozostałe grupy otrzymały analogiczne reguły z odpowiednią nazwą działu.

## Test nowej pracownicy

Utworzyłem konto Leny Bąk:

| Właściwość | Wartość |
|---|---|
| Login bez domeny | lena.bak |
| Department | Kadry |
| Job title | Specjalistka ds. płac |
| Usage location | Poland |

Nie dodawałem jej ręcznie do grup ani nie przypisywałem licencji bezpośrednio.

Sprawdzenie

<img width="1552" height="223" alt="image" src="https://github.com/user-attachments/assets/a4af5eb1-5579-41fe-812f-b27bb12b3ea5" />

<img width="1108" height="257" alt="image" src="https://github.com/user-attachments/assets/f8d14e21-cd5b-449f-b6b2-bc3969d3e5a7" />


## Test wyłączenia konta

Tymczasowo wyłączyłem konto Leny i sprawdziłem skutki po przetworzeniu zmian.

<img width="937" height="371" alt="image" src="https://github.com/user-attachments/assets/f7684db3-143f-4eaf-acf2-807004f130fd" />

<img width="1280" height="320" alt="image" src="https://github.com/user-attachments/assets/fa0cbfcf-854d-4f90-b849-1d0d60f9452b" />

<img width="1560" height="277" alt="image" src="https://github.com/user-attachments/assets/9ac36a72-95db-40f7-917b-47db00c629e4" />

Na końcu ponownie włączyłem konto i sprawdziłem powrót członkostwa oraz licencji.
