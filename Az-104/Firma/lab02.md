# Lab 2 — konta, grupy i OU w Active Directory

- Zbudowanie struktury folderów (OU)
- Założenie kont 
- Założenie dwóch konta: do pracy i do administrowania.
- Utworzenie grupy działów

## Struktura OU

Utworzyłem OU `FIRMA`, a w nim:

| OU | Przeznaczenie |
|---|---|
| Pracownicy | Konta do codziennej pracy i wyłączony szablon |
| Admini | Konta administracyjne |
| Grupy | Grupy zabezpieczeń |
| Komputery | Stacje robocze |
| Serwery | Serwery członkowskie, w tym planowany Linux |

<img width="782" height="421" alt="image" src="https://github.com/user-attachments/assets/d75c9282-e51d-4d56-9f5f-2d8761525742" />

Przy tworzeniu OU pozostawiłem ochronę przed przypadkowym usunięciem.

<img width="456" height="408" alt="image" src="https://github.com/user-attachments/assets/f517d08c-a376-44bf-8395-1d89261cf304" />

Konto kontrolera domeny DC01 pozostawiłem w istniejącym OU `Domain Controllers`.

<img width="727" height="365" alt="image" src="https://github.com/user-attachments/assets/00d56faa-de51-45c9-b3c2-7fb54905e113" />


## Oddzielne konto administracyjne

W OU `Admini` utworzyłem `radek.adm` i dodałem je do `Domain Admins`.

<img width="393" height="522" alt="image" src="https://github.com/user-attachments/assets/5d3f45c2-06fa-472f-b503-084b4debcb63" />

Zwykłe konto `radek` pozostało w OU `Pracownicy`, bez członkostwa w Domain Admins.

<img width="388" height="461" alt="image" src="https://github.com/user-attachments/assets/5f8b4970-2d51-4218-89af-aea9015e852a" />

## Grupy działowe

W OU `Grupy` utworzyłem grupy typu Security o zakresie Global.

| Grupa | Członek |
|---|---|
| GRP-Zarzad | Jan |
| GRP-Ksiegowosc | Anna |
| GRP-Sprzedaz | Piotr |
| GRP-Magazyn | Ewa |
| GRP-Sklep | Tomek |

<img width="646" height="385" alt="image" src="https://github.com/user-attachments/assets/4aea2601-a5bf-4a7f-857f-33efbb5a2b71" />

