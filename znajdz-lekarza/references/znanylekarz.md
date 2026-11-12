# ZnanyLekarz — jak czytać

Stan sprawdzony: listopad 2026.

## Czego nie używać

- **API (`/api/v3/…`) wymaga logowania** — bez danych dostępowych odpowiada `401`. Jest przeznaczone dla placówek-partnerów serwisu. Nie próbuj go używać ani zdobywać tokenu.
- Plik `robots.txt` serwisu **zabrania** automatycznego wchodzenia na: `/api/`, `/ajax/`, `/szukaj?` (wyszukiwarka wewnętrzna), `/ranking-lekarzy`. Nie wchodź tam.
- Nie obchodź zabezpieczeń (CAPTCHA, blokady). Jeśli strona się nie otwiera — przerwij i oprzyj się na wyszukiwarce internetowej.

Czytasz wyłącznie **publiczne strony list i profili**, tak jak zwykły odwiedzający: do ok. 20 stron na jedno szukanie, z przerwą 2–3 sekund między pobraniami. Nie zapisuj ani nie kopiuj całych zbiorów danych — bierzesz tylko to, co potrzebne do odpowiedzi.

## Adresy

Fragmenty adresu (slug) pisze się małymi literami, bez polskich znaków, ze spacjami zamienionymi na myślniki: `zielona-gora`, `chirurg-naczyniowy`, `niedoczynnosc-tarczycy`.

| Co | Wzór adresu | Przykład |
|---|---|---|
| lista według **choroby** (najważniejsza) | `/choroby/<choroba>/<miasto>` | `https://www.znanylekarz.pl/choroby/niedoczynnosc-tarczycy/krakow` |
| lista według **usługi lub zabiegu** | `/uslugi-zabiegi/<usluga>/<miasto>` | `https://www.znanylekarz.pl/uslugi-zabiegi/konsultacja-endokrynologiczna/krakow` |
| lista według specjalizacji | `/<specjalizacja>/<miasto>` | `https://www.znanylekarz.pl/endokrynolog/krakow` |
| to samo, tylko przyjmujący **na NFZ** | `/<specjalizacja>/<miasto>/nfz` | `https://www.znanylekarz.pl/endokrynolog/krakow/nfz` |
| kolejna strona listy | dopisz `?page=2`, `?page=3` | `https://www.znanylekarz.pl/endokrynolog/krakow?page=2` |
| profil lekarza | `/profil/<imie-nazwisko>` albo `/<imie-nazwisko>/<specjalizacja>/<miasto>` | `https://www.znanylekarz.pl/profil/…` |
| profil placówki | `/placowki/<nazwa>` | `https://www.znanylekarz.pl/placowki/…` |

Jeśli nie znasz sluga choroby lub usługi, nie zgaduj w kółko: wejdź na listę specjalizacji, otwórz jeden profil i weź slug z sekcji „Choroby” (linki `/choroby/<slug>`), albo znajdź go wyszukiwarką internetową: `site:znanylekarz.pl/choroby <nazwa choroby>`.

Zacznij od listy według choroby. Lista według specjalizacji jest zapasowa — gdy choroby nie ma w serwisie.

## Co jest na liście

Każda strona listy ma ok. 20 wyników: lekarzy i placówki. Przy wyniku znajdziesz:

- imię, nazwisko, tytuł; specjalizacje,
- liczbę opinii i średnią ocenę,
- adres i nazwę gabinetu lub placówki,
- czy ma kalendarz z wolnymi terminami, czy przyjmuje tylko online.

Jeśli pobierasz surowy HTML (np. przez `curl`), te same dane są w atrybutach elementu `data-id="result-item"`:

| Atrybut | Znaczenie |
|---|---|
| `data-doctor-name` | nazwa (lekarz albo placówka) |
| `data-doctor-url` | adres profilu |
| `data-test-entity-type` | `doctor` albo `facility` |
| `data-eec-specialization-name` | specjalizacja, pod którą serwis pokazuje wynik (np. `endokrynolog`, `radiolog`) |
| `data-eec-stars-rating` | średnia ocena |
| `data-eec-opinions-count` | liczba opinii |
| `data-eec-address-cities` | miasta, w których przyjmuje |
| `data-is-online-only` | `true` = tylko konsultacje online |
| `data-has-calendar-with-slots` | `1` = ma rezerwację online z wolnymi terminami; brak albo `0` znaczy tylko „bez rezerwacji online”, nie „brak terminów” |
| `data-result-type` | `first-class` = **profil płatny, wyróżniony**; `organic` = zwykły |

### Kolejność na liście to nie ranking jakości

Na górze listy stoją profile płatne (`first-class`). Lekarz na 15. miejscu albo na trzeciej stronie może być lepszym wyborem niż pierwszy. Dlatego:

- przejrzyj co najmniej dwie strony listy,
- wybieraj kandydatów po dopasowaniu do problemu, nie po pozycji,
- pamiętaj, że wielu lekarzy pracujących głównie w szpitalach i na NFZ **nie ma profilu wcale** albo ma pusty — ich znajdziesz przez wyszukiwarkę internetową i strony szpitali.

### Pułapki list

- **Lista według choroby miesza specjalizacje.** Przy „guzach tarczycy” obok endokrynologów są radiolodzy, patomorfolodzy i chirurdzy. Odfiltruj po specjalizacji, której szukasz.
- **Etykieta specjalizacji na liście nie jest dowodem.** Zdarza się, że pod „endokrynolog” stoi lekarz innej specjalności. Specjalizację potwierdź w profilu.
- **Lista `/nfz` jest krótka i niepełna** (bywa kilka wyników na duże miasto). To wskazówka, nie pełny obraz — poradnie na NFZ bierz z API terminów NFZ.

## Co jest w profilu lekarza

Otwórz profil każdego poważnego kandydata. Sekcje, od najważniejszej dla oceny doświadczenia:

| Sekcja na stronie | Co z niej bierzesz |
|---|---|
| **Choroby** | lista chorób, które lekarz deklaruje, że leczy — sprawdź, czy jest tam problem osoby |
| **Moje doświadczenie / O mnie** | własny opis: czym się zajmuje, gdzie pracował, szkolenia, zabiegi |
| **Doświadczenie** (miejsca pracy) | szpitale, kliniki, lata pracy — to wskazuje, czy pracuje w ośrodku zajmującym się daną chorobą |
| **Edukacja** | uczelnia, staże zagraniczne |
| **Usługi i ceny** | nazwy usług (np. „biopsja tarczycy”, „konsultacja — cukrzyca ciążowa”) i ceny wizyt prywatnych |
| **Adresy** | nazwa placówki, ulica, miasto; przy każdym adresie metody płatności i usługi |
| **Ubezpieczenia** | „przyjmuje wyłącznie pacjentów prywatnych” albo lista ubezpieczeń / NFZ |
| **Pacjenci, których przyjmuję** | dorośli, dzieci (bywa: tylko pod niektórymi adresami) |
| **Rodzaje konsultacji** | stacjonarne, online |
| **Znajomość języków** | języki obce |
| **Opinie** | treść opinii, daty, znacznik weryfikacji wizyty, najczęściej wymieniane cechy |

Uwagi do profilu:

- **Ceny nie zawsze są przypisane do adresu.** Gdy lekarz ma kilka adresów, podaj cenę jako „od … zł według profilu” i zaznacz, że trzeba potwierdzić, którego miejsca dotyczy.
- **To, czy lekarz przyjmuje na NFZ, też nie jest przypisane do adresu.** Ustal to po nazwie placówki (czy jest w danych NFZ) albo napisz, że wymaga potwierdzenia.
- Część tekstu w profilu to **opis lub ogłoszenie placówki**, nie lekarza. Usługi placówki (np. „wykonujemy biopsje”) nie znaczą, że wykonuje je ten lekarz.
- Adresy, usługi i ceny są tylko w treści strony — w bloku danych strukturalnych ich nie ma.

W surowym HTML profil ma też blok `<script type="application/ld+json">` typu `Physician` z polami `name`, `aggregateRating.ratingValue`, `aggregateRating.reviewCount` i tablicą `review` (ok. 10 najnowszych opinii: `datePublished`, `reviewRating.ratingValue`, `reviewBody`). Profil placówki ma analogiczny blok `MedicalClinic`.

## Jak czytać opinie

- Szukaj opinii, które **opisują podobny problem** („prowadzi moją cukrzycę ciążową”, „po artroskopii barku wróciłem do sportu”). Jedna taka opinia mówi więcej niż sto „miły i punktualny”.
- Średnia powyżej 4,5 jest w serwisie normą — nie różnicuje lekarzy. Zwracaj uwagę na liczbę opinii, ich daty (czy są świeże) i znacznik weryfikacji wizyty.
- Opinie krytyczne czytaj pod kątem treści: czy dotyczą leczenia, czy organizacji (kolejka, rejestracja, cena).
- Opinii nie przepisuj w całości. Streść własnymi słowami; dosłownie cytuj najwyżej krótki fragment.
- Nie podawaj imion ani pseudonimów autorów opinii.

## Opis placówki przy linku

Każdy adres z profilu opisz konkretnie, zanim podasz link:

- **pełna nazwa** placówki i adres (ulica, dzielnica, miasto),
- **rodzaj**: szpital (kliniczny, wojewódzki, powiatowy), poradnia przyszpitalna, sieciowe centrum medyczne, prywatna klinika specjalistyczna, gabinet indywidualny,
- **forma**: NFZ, prywatnie albo obie; cena wizyty, jeśli jest podana,
- co jest na miejscu, jeśli ma znaczenie (USG, rezonans, blok operacyjny, laboratorium).

Rodzaj placówki ustal ze strony placówki w serwisie (`/placowki/…`: sekcje o placówce, usługi, specjaliści, ubezpieczenia) albo z jej własnej strony internetowej. Jeśli nie da się go ustalić — napisz samą nazwę i adres, bez domysłów.

## Przykład przez curl

Gdy nie masz narzędzia do czytania stron. To samo polecenie działa w macOS, Linuksie i Windows 10/11 (w PowerShell wpisz `curl.exe` zamiast `curl`):

```
curl -s -L -A "Mozilla/5.0" -o lista.html "https://www.znanylekarz.pl/choroby/niedoczynnosc-tarczycy/krakow"
```

Plik ma ok. 1 MB — nie czytaj go w całości. Wyszukaj w nim fragmenty `data-doctor-name=` (lista) albo `application/ld+json` (profil) i czytaj tylko ich otoczenie. Po zakończeniu usuń pobrane pliki.
