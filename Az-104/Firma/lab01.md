# Lab 1 — kontroler domeny: AD DS i DNS

- Ułożenie planu adresów biura i sieci w Azure.
- Utworzenie sieć biuro w VirtualBox.
- Zainstalowanie Windows Server 2025, AD oraz utworzenie kontrolera domeny ad.firma.test.

## Plan adresów

| Sieć lub urządzenie | Adres | Przeznaczenie |
|---|---|---|
| Biuro — NAT-Firma | 192.168.50.0/24 | Sieć lokalnego laboratorium |
| Brama | 192.168.50.1 | Wyjście przez NAT VirtualBox |
| DC01 | 192.168.50.10 | Active Directory i DNS |
| LNX01 | 192.168.50.20 | Adres zarezerwowany dla serwera Linux |
| vnet-firma-sklep | 10.20.0.0/16 | Planowana sieć Azure |
| vnet-firma-zaplecze | 10.30.0.0/16 | Planowana sieć Azure |

Wybrałem niepokrywające się zakresy, aby przygotować środowisko do późniejszych połączeń sieciowych.

## Maszyna wirtualna

| Ustawienie | Wartość |
|---|---|
| Nazwa w VirtualBox | FIRMA-DC01 |
| Nazwa systemowa Windows | DC01 |
| System | Windows Server 2025 Standard Evaluation — Desktop Experience |
| Procesory | 2 |
| RAM | 4096 MB |
| Dysk | 50 GB |
| Sieć | NAT Network — NAT-Firma |

W sieci NAT-Firma wyłączyłem DHCP. Przed promocją serwera ustawiłem nazwę komputera, strefę czasową i statyczną konfigurację IPv4.

## Konfiguracja sieci DC01

| Parametr | Wartość |
|---|---|
| Adres IP | 192.168.50.10 |
| Maska | 255.255.255.0 |
| Brama | 192.168.50.1 |
| Preferowany DNS | 127.0.0.1 |

Adres DNS wskazuje na sam serwer. Po instalacji roli DNS DC01 obsługuje zapytania dotyczące domeny.

<img width="547" height="565" alt="image" src="https://github.com/user-attachments/assets/f9973efa-0c43-4a5a-950f-a37237088587" />

```
Microsoft Windows [Version 10.0.26100.32230]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Administrator>systeminfo

Host Name:                     DC01
OS Name:                       Microsoft Windows Server 2025 Standard Evaluation
OS Version:                    10.0.26100 N/A Build 26100
OS Manufacturer:               Microsoft Corporation
OS Configuration:              Standalone Server
OS Build Type:                 Multiprocessor Free
Registered Owner:              N/A
Registered Organization:       N/A
Product ID:                    00493-20000-00001-AA588
Original Install Date:         3.10.2026, 21:09:18
System Boot Time:              3.10.2026, 12:32:37
System Manufacturer:           innotek GmbH
System Model:                  VirtualBox
System Type:                   x64-based PC
Processor(s):                  1 Processor(s) Installed.
                               [01]: Intel64 Family 6 Model 140 Stepping 1 GenuineIntel ~2419 Mhz
BIOS Version:                  innotek GmbH VirtualBox, 1.12.2006
Windows Directory:             C:\WINDOWS
System Directory:              C:\WINDOWS\system32
Boot Device:                   \Device\HarddiskVolume1
System Locale:                 en-us;English (United States)
Input Locale:                  pl;Polish
Time Zone:                     (UTC+01:00) Sarajevo, Skopje, Warsaw, Zagreb
Total Physical Memory:         4 077 MB
Available Physical Memory:     2 070 MB
Virtual Memory: Max Size:      5 485 MB
Virtual Memory: Available:     3 999 MB
Virtual Memory: In Use:        1 486 MB
Page File Location(s):         C:\pagefile.sys
Domain:                        WORKGROUP
Logon Server:                  \\DC01
Hotfix(s):                     3 Hotfix(s) Installed.
                               [01]: KB5066131
                               [02]: KB5073379
                               [03]: KB5072725
Network Card(s):               1 NIC(s) Installed.
                               [01]: Intel(R) PRO/1000 MT Desktop Adapter
                                     Connection Name: Ethernet
                                     DHCP Enabled:    No
                                     IP address(es)
                                     [01]: 192.168.50.10
                                     [02]: fe80::6113:b6da:72a1:2ce6
Virtualization-based security: Status: Not enabled
                               App Control for Business policy: Enforced
                               App Control for Business user mode policy: Off
                               Security Features Enabled:
Hyper-V Requirements:          A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```

## Utworzenie domeny

Zainstalowałem rolę Active Directory Domain Services i uruchomiłem kreator promocji kontrolera domeny.

<img width="367" height="397" alt="image" src="https://github.com/user-attachments/assets/13d842a5-1ce4-48f9-99b5-b1befd373672" />

<img width="697" height="332" alt="image" src="https://github.com/user-attachments/assets/504b61c2-3114-4cfc-b936-cca2f8d82a50" />

Utworzyłem nowy las z ustawieniami:

| Parametr | Wartość |
|---|---|
| Domena główna lasu | ad.firma.test |
| Nazwa NetBIOS | FIRMA |
| Serwer DNS | Włączony |
| Global Catalog | Włączony |
| Poziom funkcjonalności lasu i domeny |

<img width="1466" height="391" alt="image" src="https://github.com/user-attachments/assets/572a79c3-83c2-4b35-a109-7dee240af466" />

## Konfiguracja DNS

W `dnsmgmt.msc` sprawdziłem strefę `ad.firma.test`, rekord hosta DC01 i rekordy usług używane do odnajdywania kontrolera domeny.

Dodałem forwardery:

- 1.1.1.1
- 8.8.8.8

<img width="755" height="480" alt="image" src="https://github.com/user-attachments/assets/eb3a3a2b-0a5a-4ba4-b97e-8c15502e553f" />

<img width="1752" height="627" alt="image" src="https://github.com/user-attachments/assets/bfc451fe-2dc0-4ae9-abfa-d54769dec78b" />

Są to serwery, do których DC01 może przekazywać zapytania o nazwy spoza obsługiwanych stref. Nie wpisałem ich jako alternatywnego DNS na karcie sieciowej DC01.
