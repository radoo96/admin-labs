# Lab 13 — SharePoint i OneDrive

W tym ćwiczeniu przygotowałem wspólne miejsce na dokumenty sprzedaży w SharePoint. Sprawdziłem dostęp pracowników, udostępnianie plików oraz odzyskiwanie usuniętego dokumentu i jego wcześniejszej wersji.

## OneDrive

Na koncie Filipa przesłałem plik `Moje-notatki.txt` do OneDrive i udostępniłem go Beacie.

W `Manage access` sprawdziłem, kto ma dostęp i z jakimi uprawnieniami.

<img width="952" height="662" alt="image" src="https://github.com/user-attachments/assets/6ccaec62-8626-48ed-9ac2-d7d915255820" />

OneDrive wykorzystałem do dokumentu roboczego jednej osoby. Dokumenty wspólne dla działu umieściłem na witrynie SharePoint.

## Witryna sprzedaży

Utworzyłem prywatną witrynę zespołu `Sprzedaz`. W bibliotece Documents umieściłem dwa dokumenty testowe:


<img width="1357" height="692" alt="image" src="https://github.com/user-attachments/assets/01cdc284-4d5f-4819-90fc-bf0792bfa20c" />

## Uprawnienia

| Osoba | Rola lub grupa | Dostęp |
|---|---|---|
| Ewa | Owners | Pełna kontrola nad witryną |
| Adam, Beata, Filip, Hanna | Members | Edycja dokumentów |
| Celina | Visitors | Odczyt |

Celinie nadałem dostęp do odczytu witryny, bez dodawania jej do członków grupy Microsoft 365.

<img width="410" height="856" alt="image" src="https://github.com/user-attachments/assets/b9c700cd-2935-4673-b7e3-90d07b28ec68" />

Sprawdziłem dostęp na osobnych kontach. Sam widok administratora nie wystarcza do potwierdzenia uprawnień pracowników.

| Test | Mój wynik |
|---|---|
| Filip otwiera cennik | [uzupełnij] |
| Filip może edytować dokument | [uzupełnij] |
| Celina otwiera cennik | [uzupełnij] |
| Celina nie może zapisać zmian w oryginale | [uzupełnij] |

## Domyślne udostępnianie

W SharePoint admin center ustawiłem:

| Ustawienie | Wartość |
|---|---|
| Domyślny rodzaj linku | Specific people |
| Domyślne uprawnienie linku | View |

<img width="1218" height="616" alt="image" src="https://github.com/user-attachments/assets/cc176189-245f-43fd-8811-1774d66368ee" />

Następnie na koncie Adama otworzyłem okno udostępniania cennika i sprawdziłem proponowany rodzaj linku.

<img width="542" height="676" alt="image" src="https://github.com/user-attachments/assets/ff9fbeaa-e810-440f-9ae5-0ea56f97cd97" />

To ustawienie ogranicza ryzyko przypadkowego utworzenia zbyt szerokiego linku. Nie zmienia jednak istniejących uprawnień: osoba należąca do Members nadal może edytować dokument, nawet jeśli otrzyma link z prawem View.

## Przywrócenie usuniętego pliku

Na koncie Filipa usunąłem testowy plik `Umowa-wzor.docx`. Następnie otworzyłem kosz witryny i wybrałem Restore.

<img width="1047" height="762" alt="image" src="https://github.com/user-attachments/assets/3c7b48cd-1c78-40da-a5ef-6bc15b06e0d9" />

## Historia wersji

W cenniku zapisałem początkową zawartość, a następnie zmieniłem ją na `wersja 2`. Po zapisaniu zmiany otworzyłem historię wersji i przywróciłem wcześniejszą wersję.

<img width="792" height="380" alt="image" src="https://github.com/user-attachments/assets/f3b35171-3e92-43ec-b3ad-f2ca1458c67d" />


## Pliki witryny na komputerze Filipa

<img width="1437" height="437" alt="image" src="https://github.com/user-attachments/assets/a3e0ec0a-2839-4dbb-b4a7-8d059790d289" />

<img width="282" height="237" alt="image" src="https://github.com/user-attachments/assets/25df2076-df4a-4c04-a827-ff5cfe252d57" />

## Wnioski

Dokumenty wspólne dla działu powinny znajdować się w miejscu zarządzanym przez zespół. Dzięki witrynie SharePoint dostęp do cennika nie zależy od przesyłania kopii mailem przez jednego pracownika.

Uprawnienia do witryny i uprawnienia nadawane linkami trzeba rozpatrywać razem. Link do odczytu nie odbiera dostępu do edycji przyznanego inną drogą.

Kosz pomaga odzyskać usunięty plik, a historia wersji — wcześniejszą zawartość dokumentu. W obu przypadkach warto po przywróceniu otworzyć plik i sprawdzić rezultat.
