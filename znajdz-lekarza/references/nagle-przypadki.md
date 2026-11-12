# Nagłe przypadki

## Kolejność odpowiedzi

1. **Pierwsze zdanie** (dokładne brzmienie możesz dopasować, sens nie może się zmienić): „To może być stan nagły. Zadzwoń teraz pod 112 albo jedź na najbliższy SOR.” Bez wstępu i bez pytań przed tym zdaniem.
2. Jeśli osoba jest sama, źle się czuje albo ma objawy udaru lub zawału — **112, nie własny samochód**.
3. Podaj mapę SOR: <https://zarobkilekarzy.pl/prawa-pacjenta/sor/> — pokazuje wszystkie szpitalne oddziały ratunkowe w Polsce i bieżące kolejki.
4. Zaproponuj: „Podaj miejscowość, wskażę najbliższe SOR-y”.
5. Nie pobieraj żadnych danych przed wysłaniem tej odpowiedzi. Szukanie SOR zaczynasz dopiero po niej.

Nie oceniaj, czy „to na pewno nic poważnego”. W razie wątpliwości traktuj sytuację jako nagłą.

## Jak znaleźć najbliższy SOR

**Sposób 1 — lista SOR dołączona do skilla (zalecany).** Plik [assets/sor.csv](../assets/sor.csv) zawiera wszystkie 250 szpitalnych oddziałów ratunkowych w Polsce (źródło: pacjent.gov.pl, stan na 24.09.2026). Kolumny rozdzielone średnikiem: `id`, `wojewodztwo`, `miasto`, `szpital`, `adres`, `lat`, `lng`. Nie wymaga internetu.

Postępowanie:

1. Znajdź wiersze, w których `miasto` jest **dokładnie** miejscowością osoby („Radom” to nie „Radomsko”). Jeśli są — to najbliższe oddziały; podaj wszystkie.
2. Jeśli miejscowość nie ma SOR, porównaj odległości po współrzędnych. Weź współrzędne miejscowości osoby (jeśli ich nie znasz na pewno — zapytaj o najbliższe większe miasto albo powiat) i dla oddziałów z tego **i sąsiednich województw** policz przybliżoną odległość: różnica `lat` × 111 km oraz różnica `lng` × 68 km, z obu pierwiastek sumy kwadratów. Granica województwa nie ma znaczenia — liczy się odległość.
3. Podaj **2–3 najbliższe** oddziały: nazwę szpitala (pisaną normalnie, nie wielkimi literami), adres, miasto i przybliżoną odległość w linii prostej. Zaznacz, że to odległość w linii prostej, a dojazd pokaże mapa.
4. Link do nawigacji zbuduj ze współrzędnych: `https://www.google.com/maps/search/?api=1&query=<lat>,<lng>`.

Jeśli nie możesz pewnie ustalić położenia osoby, nie zgaduj: powiedz, że **dyspozytor numeru 112 wskaże i wyśle pomoc**, i podaj mapę SOR.

**Bieżąca kolejka (opcjonalnie, najwyżej jedno pobranie na rozmowę).** Tylko gdy dwa oddziały są podobnie blisko i osoba pyta, gdzie krócej się czeka. Plik `https://dane.zarobkilekarzy.pl/sor/teraz.json` (dane państwowego systemu TOPSOR, odświeżane co ok. 10 minut) ma pod kluczem `sor["<id>"]` (to samo `id` co w liście):

- `w` — liczba wszystkich pacjentów na oddziale,
- `e` — 7 par `[liczba osób, "czas oczekiwania"]`; priorytet średni to `e[4]`, niski `e[5]` (licząc od zera). Czas jest tekstem („32 min”, „powyżej 2 godzin”); „-” przy zerze osób znaczy, że nikt w tej grupie nie czeka,
- zamiast tego może być `blad` — wtedy napisz „brak bieżących danych”.

Nie pobieraj tego pliku wielokrotnie ani „na zapas”. Jeśli jest niedostępny, odeślij do mapy — pokazuje te same dane.

**Sposób 2 — wyszukiwarka internetowa.** `SOR <miejscowość>` albo `szpitalny oddział ratunkowy <powiat>`. Sprawdź, czy wynik to SOR, a nie izba przyjęć.

**Ważne przy wyborze**: przy zagrożeniu życia liczy się najbliższy SOR, nie najkrótsza kolejka. O kolejności przyjęcia decyduje triaż (ocena pilności), nie kolejność zgłoszeń — pacjent w ciężkim stanie jest przyjmowany od razu. Kolejkę porównuj tylko wtedy, gdy dwa oddziały są podobnie blisko.

Lista w `assets/sor.csv` ma datę — oddziały rzadko, ale się zmieniają. Przy wątpliwości (np. osoba mówi, że SOR zamknięto) zaufaj osobie i mapie.

Dzieci: jeśli w okolicy jest SOR dziecięcy albo szpital dziecięcy, wskaż go w pierwszej kolejności.

## Gdy to pilne, ale nie zagraża życiu

| Sytuacja | Gdzie |
|---|---|
| Wieczór, noc, weekend, święto; gorączka, infekcja, ból, którego nie da się odłożyć do rana | **nocna i świąteczna opieka zdrowotna** — bez skierowania, bezpłatnie dla ubezpieczonych; lista punktów: wyszukiwarka `nocna i świąteczna opieka zdrowotna <miejscowość>` |
| Potrzebna porada lekarska przez telefon poza godzinami pracy przychodni | **Teleplatforma Pierwszego Kontaktu: 800 137 200** |
| Dzień roboczy | lekarz podstawowej opieki zdrowotnej (POZ), wizyta w dniu zgłoszenia przy nagłym pogorszeniu |

## Kryzys psychiczny

Przy myślach samobójczych lub zamiarze zrobienia sobie krzywdy: **112**, a jeśli osoba chce porozmawiać:

- **800 70 2222** — Centrum Wsparcia dla osób dorosłych w kryzysie psychicznym, całą dobę, bezpłatnie,
- **116 123** — telefon zaufania dla dorosłych,
- **116 111** — telefon zaufania dla dzieci i młodzieży, całą dobę.

Nie zostawiaj takiej osoby z samą listą lekarzy. Najpierw pomoc natychmiastowa, potem — jeśli zechce — szukanie psychiatry lub psychoterapeuty.
