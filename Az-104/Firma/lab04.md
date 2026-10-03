# Lab 4 — Linux w domenie Active Directory

Przygotowanie w AD grupy, które zdecydują o dostępie do Linuxa.
Dołączenie LNX01 do domeny i umieszczenie w folderze Serwery.
Zmienienie pliku ustawień tak, żeby logowanie działało krótkim loginem.
Logować się tylko wybranym grupom z AD.
Sudo grupie adminów z AD, a plikom strony grupę sklepu z AD.

## Środowisko

| Element | Konfiguracja |
|---|---|
| Kontroler domeny i DNS | DC01 — `192.168.50.10` |
| Serwer Linux | LNX01 — `192.168.50.20` |
| Domena | `ad.firma.test` |
| OU komputera | `FIRMA/Serwery` |
| Integracja z AD | realmd, SSSD, adcli |
| Katalog strony | `/srv/strona` |

## Grupy i podział dostępu

| Grupa w AD | Członkowie wykorzystani w labie | Rola na LNX01 |
|---|---|---|
| `GRP-Linux-Uzytkownicy` | Anna, Tomek | Logowanie kontem domenowym |
| `GRP-Linux-Admini` | `adm-radek` | Logowanie i wykonywanie poleceń przez sudo |
| `GRP-Sklep` | Tomek| Zapis do plików strony |

<img width="498" height="40" alt="image" src="https://github.com/user-attachments/assets/66767d89-c099-4a04-8dcf-34378b7ce4d8" />

## Dołączenie do domeny

Przed dołączeniem sprawdziłem synchronizację czasu i rozwiązywanie nazwy DC01. LNX01 korzysta z DNS na kontrolerze domeny.

```bash
timedatectl
ping -c 2 dc01
sudo apt install -y sssd-ad sssd-tools realmd adcli
sudo realm discover ad.firma.test
```

<img width="583" height="247" alt="image" src="https://github.com/user-attachments/assets/c76aeea6-11e3-4cd9-896e-50e8ed38926f" />

Następnie dołączyłem serwer, wskazując docelową OU:

```bash
sudo realm join -U radek.adm \
  --computer-ou="OU=Serwery,OU=FIRMA,DC=ad,DC=firma,DC=test" \
  ad.firma.test
```

<img width="725" height="491" alt="image" src="https://github.com/user-attachments/assets/db164058-9328-498f-9254-e0bc6d49bb58" />

Stan połączenia i rozpoznawanie użytkownika sprawdziłem poleceniami:

```bash
realm list
id anna@ad.firma.test
```
<img width="817" height="82" alt="image" src="https://github.com/user-attachments/assets/e197e935-c891-40d7-bd9c-1dec0bc0c410" />


## Krótkie loginy i katalogi domowe

W sekcji domeny w `/etc/sssd/sssd.conf` ustawiłem:

```ini
use_fully_qualified_names = False
fallback_homedir = /home/%u
```

<img width="420" height="382" alt="image" src="https://github.com/user-attachments/assets/041c1819-00d0-4b4f-85d0-f1c289758d63" />

Dzięki temu mogę używać loginu `anna`, a katalog domowy ma ścieżkę `/home/anna`.

Po zmianie konfiguracji:

```bash
sudo systemctl restart sssd
systemctl status sssd
id anna.kowalska
sudo pam-auth-update --enable mkhomedir
```


## Ograniczenie logowania i sudo

Dostęp dla kont domenowych ograniczyłem do dwóch grup:

```bash
sudo realm deny --all
sudo realm permit -g grp-linux-uzytkownicy grp-linux-admini
realm list
```

<img width="848" height="331" alt="image" src="https://github.com/user-attachments/assets/4a9e9c3c-409b-48e1-a376-39a69c690b67" />

Regułę sudo przygotowałem przez:

```bash
sudo visudo -f /etc/sudoers.d/ad-admini
```

Zawartość:

```sudoers
%grp-linux-admini ALL=(ALL:ALL) ALL
```

<img width="410" height="165" alt="image" src="https://github.com/user-attachments/assets/9db2e4d7-b331-4e54-9cf7-20029e0f609b" />

Reguła pozwala członkom grupy wykonywać dowolne polecenia przez sudo na serwerze, na którym znajduje się ten plik. Nie wdraża się automatycznie na pozostałe maszyny.

## Pliki strony

Grupę katalogu i istniejącego pliku zmieniłem na domenową:

```bash
sudo chgrp grp-sklep /srv/strona /srv/strona/index.html
ls -ld /srv/strona
ls -l /srv/strona/index.html
```

Sprawdziłem również prawo zapisu grupy do `index.html`. Jeśli go brakuje, dodaje je:

```bash
sudo chmod g+w /srv/strona/index.html
```

Zmiana grupy oraz zmiana uprawnień to dwie oddzielne operacje. Nowe pliki również wymagają sprawdzenia — sama zmiana grupy katalogu nie gwarantuje dziedziczenia jej przez kolejne pliki.

## Testy dostępu

Testowałem nowe połączenia SSH z komputera gospodarza.

```bash
ssh -p 2222 tomek.lewandowski@127.0.0.1
ssh -p 2222 adm-michal.bak@127.0.0.1
ssh -p 2222 piotr.zielinski@127.0.0.1
```

<img width="642" height="97" alt="image" src="https://github.com/user-attachments/assets/c3fdfbd3-750a-485d-afbe-1dca5e8d4bb4" />

<img width="355" height="125" alt="image" src="https://github.com/user-attachments/assets/b99875c4-cf64-45bf-a435-e5a49ebf43bf" />
- Migawki DC01 i LNX01 po zakończeniu: **[wpisz nazwy wykonanych migawek]**.

[← Lista labów FIRMA](README.md)
