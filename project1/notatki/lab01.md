Scenariusz: Fikcyjne biuro nieruchomości z 12 pracownikami w jednym biurze. Wdrożenie i administracja Windows Server, Active Directory, Entra ID, Intune, Exchange, Teams, SharePoint, Copilot

# Lab 1 — pierwszy kontroler domeny

W tym labolatorium skonfigurowałem domenę `ad.zielonydom.test` i dołączyłem do niej komputer z Windows 11 Pro. Całość działa w VirtualBox, w ramach środowiska testowego fikcyjnej firmy.

## Środowisko

| Maszyna | System | Rola | Adres IP |
|---|---|---|---|
| DC01 | Windows Server 2025 | Kontroler domeny i DNS | 192.168.10.10 |
| PC01 | Windows 11 Pro | Komputer w domenie | 192.168.10.101 |

Obie maszyny korzystają z sieci NAT Network `ZielonyDom`.

## Co zrobiłem

- Zainstalowałem DC01, zmieniłem nazwę serwera i ustawiłem stały adres IP.
- Dodałem rolę AD DS i utworzyłem las `ad.zielonydom.test`.
- Na PC01 ustawiłem DNS na `192.168.10.10`.
- Dołączyłem PC01 do domeny i sprawdziłem logowanie kontem domenowym.

## Sprawdzenie

Kontroler domeny widoczny na PC01 
<img width="788" height="397" alt="image" src="https://github.com/user-attachments/assets/ede63597-75b6-4ae2-92c9-4a524002df7e" />

PC01 dostępny w kontrolerze domeny

<img width="1018" height="771" alt="image" src="https://github.com/user-attachments/assets/3ad2eefd-8696-46b9-84e5-2304c8c62aa4" />


