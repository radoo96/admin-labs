# Windows Server 2025 — AD, DNS i DHCP

- Utworzenie sieci biura FIRMA-net w VirtualBox, bez DHCP.
- Zainstalowane Windows Server 2025 z interfejsem graficznym.
- Przygotowanie serwera przed AD: nazwa, stały adres IP, strefa czasowa
- Zainstalowanie Active Directory i utworzenie lasu oraz domeny ad.firma.pl.
- Ustawienie DNS: przekazywanie zapytań do internetu, strefę odwrotną, adresy DNS samego serwera.
- Uruchomienie DHCP z zakresem dla biura


# Środowisko i konfiguracja 

## Sieć

| Element | Wartość |
|---|---|
| Sieć VirtualBox | `NAT-FIRMA`, NAT Network |
| Podsieć | `10.20.0.0/24` |
| Brama | `10.20.0.1` |
| DHCP VirtualBox | Wyłączony |

<img width="902" height="816" alt="image" src="https://github.com/user-attachments/assets/b7139da8-62c7-4005-94e3-7d32a765f880" />


## DC01

| Element | Wartość |
|---|---|
| Windows Server 2025 | DC01 |
| Zasoby | 4 GB RAM, 2 CPU, dysk 60 GB |
| IPv4 | `10.20.0.10/24` |
| DNS karty | `10.20.0.10`, `127.0.0.1` |
| Role | AD DS, DNS, DHCP |
| Domena | ad.firma.pl |
| NetBIOS | `FIRMA` |

<img width="602" height="593" alt="image" src="https://github.com/user-attachments/assets/4e5373af-7739-4175-8ebb-adba0a23e6a0" />

Import-Module ADDSDeployment
Install-ADDSForest `
-CreateDnsDelegation:$false `
-DatabasePath "C:\WINDOWS\NTDS" `
-DomainMode "Win2025" `
-DomainName "ad.firma.pl" `
-DomainNetbiosName "FIRMA" `
-ForestMode "Win2025" `
-InstallDns:$true `
-LogPath "C:\WINDOWS\NTDS" `
-NoRebootOnCompletion:$false `
-SysvolPath "C:\WINDOWS\SYSVOL" `
-Force:$true


## DNS i DHCP

| Element | Wartość |
|---|---|
| Forwardery | `1.1.1.1`, `8.8.8.8` |
| Strefa odwrotna | `0.20.10.in-addr.arpa` |
| Zakres DHCP | `biuro` |
| Pula DHCP | `10.20.0.100–10.20.0.199` |
| Dzierżawa | 8 dni |
| Router | `10.20.0.1` |
| DNS | `10.20.0.10` |

<img width="393" height="430" alt="image" src="https://github.com/user-attachments/assets/46695d72-ac32-4365-92bb-403dc2d66c0e" />

<img width="403" height="468" alt="image" src="https://github.com/user-attachments/assets/f8df1819-9731-402e-a5c8-dd5c0e849c13" />

<img width="498" height="411" alt="image" src="https://github.com/user-attachments/assets/9edb4896-19cb-4cbf-9508-fbd1f6fead74" />

<img width="505" height="415" alt="image" src="https://github.com/user-attachments/assets/fbb4b036-cc0e-4c97-8b0a-6c4fef90f34a" />

<img width="512" height="412" alt="image" src="https://github.com/user-attachments/assets/27cd95b8-e382-4a1d-8a8a-6a05900d8ccb" />
