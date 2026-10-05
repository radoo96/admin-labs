# Lab 1 — instalacja kontrolera domeny

W ćwiczeniu skonfigurowałem domenę `ad.zielonydom.test` i dołączyłem do niej komputer z Windows 11 Pro. Całość działa w VirtualBoxie.

- Instalacja DC01, zmienienie nazwy serwera i ustawienie stałego adresu IP.
- Dodanie roli AD DS i utworzenie lasu `ad.zielonydom.test`.
- Na PC01 ustawienie DNS na `192.168.10.10`.
- Dołączenie PC01 do domeny i sprawdzenie logowania kontem domenowym.


## Środowisko

| Maszyna | System | Rola | Adres IP |
|---|---|---|---|
| DC01 | Windows Server 2025 | Kontroler domeny i DNS | 192.168.10.10 |
| PC01 | Windows 11 Enterprise | Komputer w domenie | 192.168.10.101 |


Obie maszyny korzystają z sieci NAT Network `ZielonyDom`.

## Sprawdzenie

Kontroler domeny widoczny na PC01 
<img width="788" height="397" alt="image" src="https://github.com/user-attachments/assets/ede63597-75b6-4ae2-92c9-4a524002df7e" />

PC01 dostępny w kontrolerze domeny

<img width="1018" height="771" alt="image" src="https://github.com/user-attachments/assets/3ad2eefd-8696-46b9-84e5-2304c8c62aa4" />


