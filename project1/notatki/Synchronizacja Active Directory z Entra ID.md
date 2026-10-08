# Synchronizacja Active Directory z Entra ID

## Przygotowanie kont

Dodałem w Active Directory alternatywny sufiks UPN odpowiadający domenie tenanta i ustawiłem go dla kont pracowników objętych ćwiczeniem.

Przykładowy format loginu po zmianie:

```text
adam.nowak@<tenant>.onmicrosoft.com
```

Rzeczywistą nazwę tenanta pomijam w publicznej dokumentacji.

## Agent Cloud Sync

Na DC01 zainstalowałem agenta Microsoft Entra Cloud Sync i skonfigurowałem jego połączenie z tenantem oraz lokalną domeną.

<img width="850" height="512" alt="image" src="https://github.com/user-attachments/assets/e79b7aec-ed4a-46da-905d-89a1551f06df" />

Dla usługi utworzyłem konto gMSA. Agent korzysta z konta usługi, którego hasłem zarządza Active Directory.

<img width="1235" height="262" alt="image" src="https://github.com/user-attachments/assets/7042e697-60bf-49cd-a998-e037fa9f1f6c" />

## Zakres synchronizacji

W konfiguracji AD → Microsoft Entra ID włączyłem synchronizację skrótów haseł i ograniczyłem zakres do OU:

```text
OU=Uzytkownicy,OU=ZielonyDom,DC=ad,DC=zielonydom,DC=test
```

Sprawdziłem zawartość OU przed uruchomieniem synchronizacji. Filtr obejmuje znajdujące się tam obiekty, a nie wyłącznie osoby wymienione w instrukcji.

Konta administracyjne pozostawiłem poza zakresem, aby rozdzielić zarządzanie lokalną domeną i chmurą.

## Test na jednym koncie

Najpierw uruchomiłem `Provision on demand` dla Adama, podając jego rzeczywisty Distinguished Name z AD.

Po sprawdzeniu wyniku włączyłem konfigurację i zweryfikowałem pozostałe konta.

<img width="1017" height="652" alt="image" src="https://github.com/user-attachments/assets/1de57de3-222d-4c10-a7ea-24a681f657be" />

<img width="1323" height="447" alt="image" src="https://github.com/user-attachments/assets/0aee1803-1666-4889-acb4-1126aa80c1df" />

<img width="1432" height="551" alt="image" src="https://github.com/user-attachments/assets/55496444-57a9-4612-a468-eb8e220127b8" />

## Licencje i logowanie

Dodałem pracowników biura do chmurowej grupy `GRP-Licencja-BusinessPremium`. Sprawdziłem lokalizację korzystania z usług, dostępność licencji oraz wynik ich przypisania.

<img width="1390" height="533" alt="image" src="https://github.com/user-attachments/assets/a520f5d6-8664-434c-98b4-95f08d03202b" />

Następnie zalogowałem się jako Adam do Microsoft 365, używając jego UPN i hasła z lokalnego AD.

<img width="1561" height="701" alt="image" src="https://github.com/user-attachments/assets/b92fd28d-8520-4d72-b702-6516ff48eab3" />

Synchronizacja hasła nie zastępuje MFA. Dostęp do usług nadal podlega regułom z labu 7.

## Zmiana danych i hasła

W lokalnym AD zmieniłem stanowisko Adama na `Starszy agent`. Następnie sprawdziłem, czy zmiana pojawiła się w Entra.

<img width="458" height="542" alt="image" src="https://github.com/user-attachments/assets/4ec38784-8fb3-4ccb-9504-ea95efc6dbef" />

<img width="512" height="647" alt="image" src="https://github.com/user-attachments/assets/169f1b96-b63a-4e36-adfd-970e9c2c24dc" />

<img width="383" height="325" alt="image" src="https://github.com/user-attachments/assets/cbd6fee8-8ad9-4bf4-8edc-a7db35b4eef8" />

Na PC01 zmieniłem hasło Adama i po synchronizacji sprawdziłem logowanie do Microsoft 365 nowym hasłem.

<img width="1033" height="241" alt="image" src="https://github.com/user-attachments/assets/14a51d72-6d6e-40f1-978b-9c494305e5ba" />

Dla atrybutów synchronizowanych z AD w tej konfiguracji zmiany wykonuję lokalnie. Licencjami i przypisaniami do grup chmurowych nadal zarządzam w chmurze.
