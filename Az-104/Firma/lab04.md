# Lab 4 — serwer Linux

- Zainstalowanie Ubuntu Server ze stałym adresem IP
- Instalowanie programów i aktualizacja systemu
- Dodanie serwera do DNS na DC01.
- Połączenie się z serwerem przez SSH

## Konfiguracja maszyny

| Ustawienie | Wartość |
|---|---|
| Nazwa w VirtualBox | FIRMA-LNX01 |
| Nazwa systemowa | lnx01 |
| System | Ubuntu Server 22.10 LTS |
| Procesory | 2 |
| RAM | 2048 MB |
| Dysk | 20 GB |
| Sieć | NAT Network — NAT-Firma |
| Konto lokalne | radek |

Podczas instalacji zaznaczyłem OpenSSH Server.

<img width="761" height="695" alt="image" src="https://github.com/user-attachments/assets/ea847da1-e800-4201-bcc2-50d58883f373" />

<img width="846" height="370" alt="image" src="https://github.com/user-attachments/assets/8342db23-707e-4d87-b911-8b081b851acb" />

## Ustawienia sieci

| Parametr | Wartość |
|---|---|
| Adres IP | 192.168.50.20/24 |
| Brama | 192.168.50.1 |
| Serwer DNS | 192.168.50.10 |
| Domena wyszukiwania | ad.firma.test |

Linux korzysta z DNS na DC01. Domena wyszukiwania pozwala uzupełniać krótkie nazwy, np. `dc01`, o `ad.firma.test`.

<img width="845" height="671" alt="image" src="https://github.com/user-attachments/assets/84f889bb-c232-468f-bacc-5860a08ac7ca" />

## Uprawnienia i pakiety

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y tree htop
```

## DNS i łączność

```
Na DC01 dodałem rekord A:

```text
lnx01.ad.firma.test → 192.168.50.20
```

<img width="620" height="63" alt="image" src="https://github.com/user-attachments/assets/5111db6c-22de-4d2c-9846-b7ef42ec50a1" />

<img width="343" height="353" alt="image" src="https://github.com/user-attachments/assets/939a31fd-2059-48fc-a471-0f177e917042" />

<img width="778" height="536" alt="image" src="https://github.com/user-attachments/assets/f58fea73-7a51-4222-bf98-5521049ad977" />

<img width="1071" height="690" alt="image" src="https://github.com/user-attachments/assets/d9c9d4d1-93f7-454f-ba12-86152a5076a4" />


Przetestowałem rozwiązywanie nazw i łączność między maszynami.




Ze swojego komputera połączyłem się poleceniem:

```bash
ssh radek@192.168.50.20
```

<img width="745" height="706" alt="image" src="https://github.com/user-attachments/assets/f71b24a2-b7d6-4512-b615-e0a0699555dd" />

Przekierowanie nasłuchuje na adresie lokalnym mojego komputera. Port 2222 po stronie hosta prowadzi do portu SSH 22 na LNX01.
