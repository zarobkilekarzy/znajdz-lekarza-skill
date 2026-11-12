# Terminy leczenia NFZ — opis API

Stan sprawdzony: listopad 2026. Oficjalne, bezpłatne API Narodowego Funduszu Zdrowia, **bez klucza i bez logowania**.

- Adres bazowy: `https://api.nfz.gov.pl/app-itl-api`
- Dokumentacja: <https://api.nfz.gov.pl/app-itl-api/> (opis maszynowy: `/swagger/v1.3/swagger.json`)
- Do każdego zapytania dopisz: `format=json&api-version=1.3`
- Tylko metoda GET. Wystarczy zwykłe narzędzie do pobierania adresów albo `curl`.
- Odstęp między zapytaniami: ok. 1 sekundy. Zbyt szybkie zapytania bywają odrzucane (pusta odpowiedź) — odczekaj i powtórz raz.

## Co te dane mówią, a czego nie

- To kolejka **do poradni lub oddziału, nie do konkretnego lekarza**.
- Dane przekazują same placówki. Statystyki są miesięczne (pole `update`, np. `2026-10`).
- Nie wszystkie poradnie są w słowniku. W listopadzie 2026 r. zapytania o poradnię kardiologiczną zwracały tylko rehabilitację kardiologiczną. Gdy czegoś nie ma — powiedz to i podaj <https://terminyleczenia.nfz.gov.pl/> oraz infolinię NFZ **800 190 590**.
- Termin zawsze trzeba potwierdzić telefonicznie w rejestracji.

## Krok 1. Znajdź nazwę świadczenia: `/benefits`

Nazwy w słowniku NFZ są nieoczywiste. **Nigdy nie zgaduj nazwy — najpierw zapytaj słownik.**

```
GET /benefits?name=<fragment>&limit=25&format=json&api-version=1.3
```

`name` to fragment nazwy (wielkość liter bez znaczenia). Odpowiedź: `data` — lista nazw, `meta.count` — ile ich jest.

Jak pytać:

| Fragment | Przykładowe wyniki |
|---|---|
| `endokrynolog` | `ŚWIADCZENIA Z ZAKRESU ENDOKRYNOLOGII`, `PORADNIA ENDOKRYNOLOGICZNA OSTEOPOROZY`, `ODDZIAŁ ENDOKRYNOLOGICZNY` |
| `ortoped` | `ŚWIADCZENIA Z ZAKRESU ORTOPEDII I TRAUMATOLOGII NARZĄDU RUCHU` |
| `okulist` | `ŚWIADCZENIA Z ZAKRESU OKULISTYKI` |
| `dermatolog` | `PORADNIA DERMATOLOGICZNA`, `PORADNIA DERMATOLOGICZNA DLA DZIECI` |
| `świadczenia z zakresu` | wszystkie świadczenia ambulatoryjne nazwane w ten sposób |
| `poradnia` | 150 poradni; kolejne strony: `&page=2`, `&page=3` |

Wskazówki:

- Używaj **rdzenia słowa** (`neurolog`, `urolog`, `alergolog`), nie pełnej nazwy specjalizacji.
- Wizyta u specjalisty to zwykle `ŚWIADCZENIA Z ZAKRESU …` albo `PORADNIA …`. `ODDZIAŁ …` oznacza leczenie szpitalne, `ZAKŁAD/OŚRODEK …` — rehabilitację.
- Dla dzieci wybierz wariant `… DLA DZIECI`, jeśli istnieje.
- Zabiegi i badania mają własne nazwy (np. fragment `zaćm`, `endoprotez`, `rezonans`, `kolonoskop`).

## Krok 2. Znajdź miejsca i kolejki: `/queues`

```
GET /queues?case=1&province=06&benefit=<NAZWA>&locality=<MIEJSCOWOŚĆ>&limit=25&format=json&api-version=1.3
```

| Parametr | Znaczenie |
|---|---|
| `case` | podawaj zawsze: `1` — przypadek stabilny, `2` — pilny. Używaj `2` tylko wtedy, gdy osoba ma skierowanie z adnotacją „pilne”; o pilności decyduje lekarz, nie pacjent |
| `province` | kod województwa (tabela niżej) |
| `benefit` | nazwa świadczenia ze słownika; działa też fragment nazwy |
| `locality` | miejscowość; działa fragment — `KRAKÓW` obejmuje też `KRAKÓW-NOWA HUTA`. Pomiń, żeby przeszukać całe województwo |
| `benefitForChildren` | `true` — tylko miejsca przyjmujące dzieci |
| `provider` | fragment nazwy świadczeniodawcy (np. szpitala) |
| `place` | fragment nazwy miejsca (np. poradni) |
| `street` | ulica |
| `limit` | najwyżej 25 |
| `page` | numer strony; adres następnej strony jest w `links.next` |

**Polskie znaki w zapytaniu.** `benefit` i `locality` dopasowują fragment, więc najbezpieczniej podać **fragment bez polskich liter**: `ZAKRESU ENDOKRYNOLOGII` zamiast `ŚWIADCZENIA Z ZAKRESU ENDOKRYNOLOGII`, `KRAK` zamiast `KRAKÓW`, `GDA` zamiast `GDAŃSK`. Wynik jest ten sam. Jeśli fragmentu bez polskich liter nie da się ułożyć, zakoduj znaki procentowo w UTF-8 (np. `Ł` = `%C5%81`, `Ó` = `%C3%93`, `Ś` = `%C5%9A`, `Ź` = `%C5%B9`, `Ż` = `%C5%BB`, spacja = `%20`). **Nie wpisuj polskich liter wprost w poleceniu `curl`** — w Windows trafiają do API w złym kodowaniu i zapytanie zwraca zero wyników.

Po każdym zapytaniu sprawdź w odpowiedzi pole `benefit` i `locality`: jeśli fragment złapał coś innego, niż chciałeś (np. `KRAK` nie tylko Kraków), zawęź go.

**Zero wyników nie znaczy „brak poradni”.** Zanim to powiesz, powtórz zapytanie bez `locality` (całe województwo) i sprawdź nazwę w `/benefits`.

Kody województw:

| Kod | Województwo | Kod | Województwo |
|---|---|---|---|
| 01 | dolnośląskie | 09 | podkarpackie |
| 02 | kujawsko-pomorskie | 10 | podlaskie |
| 03 | lubelskie | 11 | pomorskie |
| 04 | lubuskie | 12 | śląskie |
| 05 | łódzkie | 13 | świętokrzyskie |
| 06 | małopolskie | 14 | warmińsko-mazurskie |
| 07 | mazowieckie | 15 | wielkopolskie |
| 08 | opolskie | 16 | zachodniopomorskie |

### Odpowiedź

`meta.count` — liczba wyników. `data[]` — miejsca; każde ma `id` i `attributes`:

| Pole | Znaczenie |
|---|---|
| `benefit` | nazwa świadczenia |
| `provider` | świadczeniodawca (np. szpital, spółka) |
| `place` | miejsce udzielania (np. „PORADNIA ENDOKRYNOLOGICZNA”) |
| `address`, `locality` | adres |
| `phone` | telefon do rejestracji |
| `latitude`, `longitude` | współrzędne — do policzenia odległości i linku do mapy |
| `benefits-for-children` | czy przyjmuje dzieci (bywa puste) |
| `toilet`, `ramp`, `car-park`, `elevator` | udogodnienia: `Y` / `N` |
| `statistics.provider-data.awaiting` | liczba osób oczekujących |
| `statistics.provider-data.removed` | liczba osób skreślonych z listy (przyjętych) w miesiącu |
| `statistics.provider-data.average-period` | **średni czas oczekiwania w dniach** |
| `statistics.provider-data.update` | miesiąc, którego dotyczą statystyki |
| `dates` | pierwszy wolny termin; **w testach z listopada 2026 r. pole było puste we wszystkich wynikach** |

Wyniki są ułożone rosnąco według `average-period` (sprawdzone na trzech kolejnych stronach w listopadzie 2026 r.); wpisy bez statystyk stoją w dowolnym miejscu. Nie zakładaj tej kolejności na ślepo — przy wyborze porównaj `average-period` sam. `meta.count` to łączna liczba wyników; gdy jest większa niż 25, kolejne strony pobieraj tylko wtedy, gdy na pierwszej nie ma miejsc w zasięgu osoby.

Jeśli `dates` jest puste, opieraj się na `average-period` i `awaiting` i napisz wprost, że to średnia z danego miesiąca, a nie data pierwszego wolnego terminu. Jeśli `dates` ma wartość, podaj ją razem z dniem, z którego pochodzi.

Na co uważać w wynikach:

- **Poradnie dziecięce są wymieszane z dorosłymi** i nie ma filtra „tylko dorośli”. Dla osoby dorosłej pomiń miejsca, które w `provider` lub `place` mają „dziecięcy”, „dzieci”, „pediatryczny”.
- `statistics` bywa `null` — takie miejsce nie ma danych o kolejce i stoi w dowolnym miejscu listy. Nie podawaj go jako „krótkiej kolejki”.
- To samo miejsce może wystąpić **dwa razy** z różnymi danymi. Podaj wpis ze statystykami.
- `latitude` i `longitude` bywają `null` — wtedy link do mapy zbuduj z adresu: `https://www.google.com/maps/search/?api=1&query=<ulica+numer+miasto>`.
- Bardzo długie kolejki (setki dni) są częste w dużych szpitalach klinicznych. Podaj je, jeśli tam przyjmuje wybrany lekarz, ale zawsze z liczbą dni.

Wartości `0` w `awaiting` i `average-period` mogą oznaczać zarówno brak kolejki, jak i brak sprawozdania — podaj je z zastrzeżeniem i poleć telefon do rejestracji.

### Szczegóły jednego miejsca

```
GET /queues/<id>?format=json&api-version=1.3
```

Zwraca te same pola dla jednego miejsca. `GET /many-places/<id>` — inne miejsca tego samego świadczeniodawcy z tym samym świadczeniem.

## Słowniki pomocnicze

Wszystkie przyjmują `name` (fragment) i opcjonalnie `province`:

- `/localities` — nazwy miejscowości tak, jak zapisuje je NFZ (przydatne, gdy `locality` nic nie znajduje),
- `/providers` — świadczeniodawcy,
- `/places` — miejsca udzielania świadczeń,
- `/streets` — ulice.

## Jak przedstawić wynik

Wybierz 2–3 miejsca z najkrótszym czasem oczekiwania w zasięgu osoby. Dla każdego podaj:

- nazwę poradni (`place`) i świadczeniodawcy (`provider`) — pisane normalnie, nie wielkimi literami; formy prawne skróć („sp. z o.o.”, „SP ZOZ”),
- adres i telefon,
- średni czas oczekiwania w dniach, liczbę oczekujących i miesiąc danych,
- datę pierwszego wolnego terminu, jeśli jest,
- link do mapy: `https://www.google.com/maps/search/?api=1&query=<latitude>,<longitude>`.

Potem sprawdź na stronie placówki albo wyszukiwarką internetową, **którzy lekarze przyjmują w tej poradni**, i połącz to z oceną doświadczenia. Poradnia z krótką kolejką, w której przyjmuje lekarz z listy kandydatów, to najlepszy wynik na ścieżce NFZ.

## Przykłady przez curl

Działają tak samo w macOS, Linuksie i Windows 10/11 (w PowerShell wpisz `curl.exe` zamiast `curl`). Nic nie trzeba instalować. Adresy zawierają wyłącznie znaki ASCII.

Słownik:

```
curl -s "https://api.nfz.gov.pl/app-itl-api/benefits?name=endokrynolog&limit=25&format=json&api-version=1.3"
```

Kolejki w Krakowie, przypadek stabilny:

```
curl -s "https://api.nfz.gov.pl/app-itl-api/queues?case=1&province=06&benefit=ZAKRESU%20ENDOKRYNOLOGII&locality=KRAK&limit=25&format=json&api-version=1.3"
```
