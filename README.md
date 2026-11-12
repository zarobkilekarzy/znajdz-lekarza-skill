# Znajdź lekarza — skill dla asystentów AI

Zestaw instrukcji (skill), dzięki któremu asystent AI pomaga znaleźć w Polsce lekarza specjalistę dopasowanego do konkretnego problemu zdrowotnego.

Asystent z tym skillem:

1. **Sprawdza, czy to nie nagły przypadek.** Jeśli tak — od razu kieruje pod 112 lub na SOR, podaje [mapę SOR z bieżącymi kolejkami](https://zarobkilekarzy.pl/prawa-pacjenta/sor/) i pomaga znaleźć najbliższy oddział.
2. **Prowadzi krótki wywiad** — problem, miejscowość, pilność, NFZ czy prywatnie.
3. **Dobiera typ specjalisty i wąską dziedzinę**, w której lekarz powinien mieć doświadczenie.
4. **Szuka kandydatów** w wyszukiwarce internetowej, na publicznych stronach ZnanyLekarz i w oficjalnych danych NFZ o terminach leczenia.
5. **Ocenia przede wszystkim doświadczenie** w podobnych przypadkach. Oceny pacjentów bierze pod uwagę, ale nie są najważniejsze.
6. **Podaje 3–5 lekarzy** z uzasadnieniem, linkami do źródeł, opisem każdej placówki i informacją, czego nie udało się potwierdzić.

Skill nie stawia diagnozy, nie zaleca leczenia i nie rezerwuje wizyt.

## Instalacja

Skill to zwykły folder z plikami tekstowymi. **Nie wymaga instalowania żadnych programów** — działa tak samo w Windows, macOS i Linuksie.

1. Pobierz to repozytorium (zielony przycisk **Code → Download ZIP**) i rozpakuj.
2. Skopiuj folder `znajdz-lekarza` do katalogu skilli swojego asystenta:

| Asystent | Katalog |
|---|---|
| Claude Code | `~/.claude/skills/` |
| Claude (aplikacja i claude.ai) | Ustawienia → Możliwości → Skille → prześlij folder `znajdz-lekarza` spakowany do ZIP |
| Codex | `~/.agents/skills/` |
| inne narzędzia zgodne z [Agent Skills](https://agentskills.io) (m.in. Gemini CLI, Cursor) | według dokumentacji narzędzia — szukaj hasła „skills” |

W Windows znak `~` oznacza folder użytkownika, np. `C:\Users\Anna`. Katalogi mogą się zmieniać między wersjami narzędzi. Po skopiowaniu zapytaj asystenta: „Jakie masz skille?” — jeśli nie wymieni `znajdz-lekarza`, sprawdź w jego dokumentacji, gdzie trzyma skille.

3. Napisz do asystenta zwykłym zdaniem, np. „Szukam dobrego endokrynologa w Krakowie, mam guzek tarczycy”.

Asystent musi mieć dostęp do internetu (wyszukiwanie i czytanie stron).

## Co jest w środku

```
znajdz-lekarza/
├── SKILL.md                      przebieg rozmowy i zasady
├── assets/
│   └── sor.csv                   lista SOR w Polsce ze współrzędnymi
└── references/
    ├── nagle-przypadki.md        112, SOR, nocna pomoc, telefony wsparcia
    ├── wywiad.md                 pytania, dobór specjalisty, skierowania
    ├── znanylekarz.md            jak czytać publiczne strony ZnanyLekarz
    ├── nfz-terminy.md            opis API terminów leczenia NFZ
    └── ocena.md                  kryteria oceny i format odpowiedzi
```

## Dlaczego bez skryptów

Żeby skill działał u każdego, także u osób nietechnicznych, nie zawiera programów do uruchomienia. Asystent pobiera dane swoim własnym narzędziem do czytania stron. Gdy go nie ma, używa polecenia `curl`, które jest wbudowane w Windows 10 i 11, macOS i Linuksa. Lista SOR jest w pliku dołączonym do skilla, więc najbliższy oddział da się wskazać także bez internetu.

## Źródła danych i ograniczenia

- **Terminy leczenia NFZ** — oficjalne, otwarte API (`api.nfz.gov.pl/app-itl-api`). Pokazuje kolejkę do poradni, nie do konkretnego lekarza; statystyki są miesięczne.
- **ZnanyLekarz** — tylko publiczne strony list i profili, w niewielkiej liczbie, z poszanowaniem pliku `robots.txt`. API serwisu wymaga logowania i nie jest używane. Asystent nie udaje przeglądarki. Kolejność na listach ustala serwis i nie jest ona oceną doświadczenia, a wielu lekarzy nie ma tam profilu — dlatego to jedno z trzech źródeł, nie jedyne. Korzystając ze skilla, przestrzegaj regulaminu serwisu.
- **Lista SOR** — plik `assets/sor.csv` dołączony do skilla (250 oddziałów ze współrzędnymi; źródło: pacjent.gov.pl, stan na 24.09.2026). Bieżące kolejki pokazuje [mapa SOR na zarobkilekarzy.pl](https://zarobkilekarzy.pl/prawa-pacjenta/sor/) na danych państwowego systemu TOPSOR.

Wynik zależy od tego, co jest publicznie dostępne w internecie. Lista lekarzy **nie jest poradą medyczną ani rankingiem**; terminy, ceny i zakres leczenia trzeba potwierdzić w rejestracji. Dane o zdrowiu podane w rozmowie nie trafiają do zapytań — asystent wyszukuje po specjalizacji, nazwie choroby i miejscowości.

## Zgłaszanie błędów

Adresy stron i odpowiedzi API się zmieniają. Jeśli coś przestało działać, zgłoś to w zakładce **Issues**.

## Licencja

[MIT](LICENSE)
