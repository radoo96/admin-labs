# DHCP i DNS

W tym labie uruchomiłem DHCP na DC01 i przełączyłem PC01 z ręcznej konfiguracji sieci na automatyczną. Następnie przygotowałem rezerwację adresu, dodałem rekord DNS i sprawdziłem zachowanie komputera podczas awarii DHCP.

## Konfiguracja DHCP

Zainstalowałem rolę DHCP Server na DC01, autoryzowałem serwer w domenie i utworzyłem aktywny zakres `Biuro`.

| Ustawienie | Wartość |
|---|---|
| Serwer DHCP | DC01 — 192.168.10.10 |
| Zakres adresów | 192.168.10.100–192.168.10.200 |
| Maska | 255.255.255.0 |
| Brama | 192.168.10.1 |
| Serwer DNS | 192.168.10.10 |
| Sufiks domeny | ad.zielonydom.test |
| Czas dzierżawy | 8 dni |

DC01 zachował statyczny adres IP. DHCP w sieci NAT Network VirtualBox pozostał wyłączony.

<img width="523" height="512" alt="image" src="https://github.com/user-attachments/assets/698f4ce1-cb07-446d-801d-f457e9ae4f2c" />

<img width="947" height="257" alt="image" src="https://github.com/user-attachments/assets/64a90a9b-336f-469d-9b88-f4f1afdd0bc2" />

## PC01 i rezerwacja adresu

Na PC01 włączyłem automatyczne pobieranie adresu IP oraz DNS. Wykonałem kolejno:

```cmd
ipconfig /release
ipconfig /renew
ipconfig /all
```

Sprawdziłem otrzymane ustawienia oraz wpis PC01 w `Address Leases` na serwerze.

Następnie skonfigurowałem rezerwację `192.168.10.150` dla PC01. Po zwolnieniu i odnowieniu dzierżawy sprawdziłem, czy komputer otrzymał zarezerwowany adres.

<img width="717" height="617" alt="image" src="https://github.com/user-attachments/assets/6c5fe262-e0c0-422c-aa94-854642b9d9d9" />

## Rekord DNS drukarki

W strefie `ad.zielonydom.test` utworzyłem rekord A:

| Nazwa | Początkowy adres IP |
|---|---|
| drukarka.ad.zielonydom.test | 192.168.10.30 |

Na PC01 sprawdziłem odpowiedź poleceniem:

```cmd
nslookup drukarka.ad.zielonydom.test
```

<img width="557" height="132" alt="image" src="https://github.com/user-attachments/assets/d19bc628-bd05-46f3-8d92-143cf5e78de8" />

oraz 'ping'

<img width="718" height="101" alt="image" src="https://github.com/user-attachments/assets/ac3abdf7-454f-4a3b-bb03-43505b29faee" />

Następnie zmieniłem adres rekordu na `192.168.10.31` i sprawdziłem rozwiązywanie nazwy przed oraz po wyczyszczeniu lokalnej pamięci DNS:

```cmd
ipconfig /flushdns
```

<img width="557" height="132" alt="image" src="https://github.com/user-attachments/assets/ef3353ea-3192-4f2e-90b3-bd1e229e6073" />


## Symulacja awarii DHCP

Zatrzymałem usługę `DHCP Server` na DC01. Na PC01 zwolniłem dzierżawę i spróbowałem pobrać adres ponownie.

- Wynik `ipconfig /renew`
- Adres PC01 podczas awarii

<img width="702" height="202" alt="image" src="https://github.com/user-attachments/assets/dbacb0f8-6a8b-453e-a249-6353c685c4cc" />

<img width="677" height="183" alt="image" src="https://github.com/user-attachments/assets/32317a66-ae6d-405c-963c-ff54770fb281" />

<img width="661" height="285" alt="image" src="https://github.com/user-attachments/assets/7b11488f-bded-47f2-bb4c-20bc12d576a7" />
