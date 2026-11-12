# Oceny i opinie — skąd je brać, z przeglądarką i bez

Stan sprawdzony: listopad 2026.

Cel: przy każdym lekarzu i każdej placówce **oceny z co najmniej dwóch niezależnych źródeł**, zawsze z nazwą źródła i liczbą opinii. Google jest jednym z możliwych źródeł, nie obowiązkowym: wizytówka w Mapach Google ładuje się skryptami i zwykłe pobranie strony jej nie pokaże.

## Drabinka — użyj najwyższego szczebla, jaki masz

1. **Masz narzędzie map lub miejsc** (wyszukiwanie miejsc, dane Map Google): odczytaj z niego ocenę i liczbę opinii wizytówki.
2. **Masz przeglądarkę, którą sterujesz** — wbudowaną w asystenta albo podłączoną jako narzędzie (np. przez MCP): otwórz wizytówki Google finalnych placówek. Instrukcja niżej.
3. **Serwisy, które oddają oceny w zwykłym HTML** (tabela niżej): pobierz stronę lekarza lub placówki. To podstawowa droga dla asystenta bez przeglądarki; korzystaj z niej także wtedy, gdy masz przeglądarkę — to drugie źródło. Strona placówki w Kliniki.pl podaje też ocenę z Google, ale bywa to **starsza migawka** (w teście 451 opinii wobec 487 na wizytówce).
4. **Wynik wyszukiwania**: jeśli wyszukiwarka pokazuje ocenę z wizytówki Google, wolno ją podać, gdy nazwa i adres są jednoznaczne. Nie licz na to — w testach wyszukiwarka jej nie podawała.
5. **Link dla osoby**: gdy oceny Google nie masz, napisz „Google: nie odczytano” i daj link `https://www.google.com/maps/search/?api=1&query=<nazwa+placówki+miasto>`.

**Używasz tylko tego, co już masz.** Nie instaluj przeglądarki, rozszerzeń ani serwerów narzędzi i nie proś o to osoby w trakcie szukania. Nie pobieraj stron Map Google przez `curl` ani przeglądarką uruchamianą bez okna z wiersza poleceń — dostaniesz ekran zgody na pliki cookie, bez ocen.

## Wizytówka Google w przeglądarce

Sprawdzone w listopadzie 2026 r. Tylko dla **3–5 finalnych placówek** (do ok. 6 wizytówek na odpowiedź) — to wolne i kosztowne.

1. Otwórz `https://www.google.com/maps/search/?api=1&query=<nazwa placówki>+<ulica>+<miasto>`.
2. Jeśli pojawi się ekran „Zanim przejdziesz do Map Google”, wybierz **„Odrzuć wszystko”**. Nigdy „Zaakceptuj wszystko”. Ekran pojawia się raz na sesję.
3. Poczekaj kilka sekund, aż załaduje się panel wizytówki. Ocena stoi pod nazwą placówki: średnia, gwiazdki i liczba opinii w nawiasie, np. „4,5 (487)”.
4. **Odczytaj ją ze zrzutu ekranu albo z drzewa elementów strony** (element z opisem w rodzaju „4,5-gwiazdkowy”). Zwykłe pobranie tekstu strony zwraca tylko menu Map, bez oceny.
5. Sprawdź nazwę i adres w panelu. Jeśli zamiast jednej wizytówki jest lista wyników, wybierz ten z właściwym adresem; jeśli nie masz pewności — nie podawaj oceny.
6. Zapisz: „Google: 4,5/5 (487 opinii, placówka)”.

Granice:

- **Nie loguj się** i nie korzystaj z konta osoby, nawet jeśli przeglądarka jest zalogowana. Nie klikaj niczego poza ekranem zgody i wizytówką; nie dodawaj opinii, nie zapisuj miejsc.
- **CAPTCHA, blokada albo prośba o logowanie = koniec.** Nie obchodź zabezpieczeń; przejdź do szczebla 3 i daj link.
- Nie przeglądaj masowo: żadnego przewijania listy opinii ani odwiedzania dziesiątek wizytówek. Potrzebujesz średniej i liczby opinii; treść opinii bierz z serwisów z tabeli niżej.
- Jeśli przeglądarka należy do osoby (jej własne okno), uprzedź jednym zdaniem, co otworzysz, zanim zaczniesz.

## Serwisy z ocenami w zwykłym HTML

| Serwis | Co ocenia | Skala | Jak znaleźć stronę | Gdzie jest ocena |
|---|---|---|---|---|
| **ZnanyLekarz** | lekarze i placówki, głównie prywatne | 1–5 | [znanylekarz.md](znanylekarz.md) | blok danych strukturalnych (`aggregateRating`) i nagłówek profilu |
| **Kliniki.pl** | placówki (także szpitale) i lekarze | **1–10** | lista `https://www.kliniki.pl/<specjalizacja>/<miasto>/`; strona placówki `https://www.kliniki.pl/<nazwa-placowki>/` — adres weź z listy albo z wyszukiwarki | nagłówek strony: „9,5 / 10 • … • 2417 opinii”; niżej **rozbicie na źródła**, np. „4,6 / 5 (451 ocen placówki na Google.pl)” |
| **RankingLekarzy.pl** | lekarze | 1–5 | lista `https://www.rankinglekarzy.pl/<specjalizacja>/<miasto>/` (kolejne strony `?page=2`); profil `/lekarz/<imie-nazwisko>/<miasto-numer>` — adres weź z listy | już na liście: `data-value="4,9/5"` i „liczba opinii: 10”; na profilu `itemprop="ratingValue"` |
| **swiatprzychodni.pl** | przychodnie i poradnie, **także publiczne i na NFZ** | 1–5 | wyszukiwarka: `<nazwa przychodni> <miasto> swiatprzychodni`; strona `https://swiatprzychodni.pl/osrodki/<nazwa>/` | blok oceny zbiorczej: `itemprop="ratingValue"` obok `bestRating` i `ratingCount`. **Nie bierz** `ratingValue` z pojedynczych opinii niżej na stronie |

Zasady czytania są takie same jak dla ZnanyLekarz: tylko publiczne strony list i profili, w niewielkiej liczbie (łącznie do ok. 15 stron z tych trzech serwisów na całą odpowiedź, nie na każdego lekarza — sprawdzaj oceny tylko dla 3–5 finalnych kandydatów i ich placówek), z przerwą 2–3 sekund, bez wyszukiwarek wewnętrznych serwisów i bez udawania przeglądarki. Jeśli serwis odmawia albo pokazuje zabezpieczenie — pomiń go.

- **swiatprzychodni.pl** w pliku `robots.txt` zabrania wstępu botowi GPTBot. Jeśli działasz jako asystent OpenAI albo pobierasz strony pod tą nazwą, **nie pobieraj tego serwisu** — podaj tylko link.
- **Kliniki.pl** łączy w ocenie placówki opinie własne, z Google i ze ZnanyLekarz, i pokazuje na stronie rozbicie na te źródła. Podaj więc składniki osobno: „Kliniki.pl: 4,7/5 (195 ocen) · Google: 4,6/5 (451 ocen, za Kliniki.pl)”. Ocena łączona (np. 9,5/10) **nie jest niezależna** od ZnanyLekarz ani Google — nie licz jej jako osobnego źródła obok nich.
- **Znajdowanie konkretnej osoby lub placówki.** Lista specjalizacji rzadko wystarcza. Wyszukaj: `<imię nazwisko> <miasto> znanylekarz`, `<imię nazwisko> <miasto> rankinglekarzy`, `<nazwa placówki> <miasto> kliniki.pl`. Adresy profili ZnanyLekarz z wyszukiwarki mają też postać `/<imie-nazwisko>/<specjalizacja>/<miasto>` — to te same profile.
- **Liczby bierz ze strony, którą sam pobrałeś.** Streszczenia wyszukiwarki pokazują stare migawki (w teście różniły się o kilka–kilkanaście opinii).
- Adresu strony nie składaj z nazwy — weź go z listy albo z wyniku wyszukiwania i sprawdź nazwę oraz adres placówki po otwarciu.

## Pułapki

- **Mniej niż 5 opinii nie liczy się jako drugie źródło.** Podaj taką ocenę z liczbą opinii, ale szukaj dalej albo napisz, że rzetelne jest tylko jedno źródło.
- **Sieć z wieloma oddziałami.** ZnanyLekarz podaje zwykle ocenę całej sieci, a Kliniki.pl i Google — jednego oddziału. Napisz przy każdej, czego dotyczy („cała sieć”, „oddział przy ul. …”), i szukaj oceny oddziału, w którym lekarz przyjmuje.
- **Dwa podmioty pod jednym adresem** (częste w przychodniach przyszpitalnych i dawnych zespołach przychodni). Porównaj pełną nazwę, nie sam adres. Jeśli nie masz pewności, który podmiot jest właściwy, podaj oba z nazwami i zaznacz wątpliwość.
- **Nazwa z NFZ a nazwa w serwisie mogą się różnić** (skróty, dawne nazwy, forma prawna). Szukaj po ulicy i najbardziej charakterystycznym członie nazwy.

## Które źródło do czego

| Szukasz ocen… | Najpierw | Potem |
|---|---|---|
| lekarza przyjmującego prywatnie | ZnanyLekarz | RankingLekarzy.pl |
| prywatnej kliniki lub szpitala | Kliniki.pl (z rozbiciem: własne, Google, ZnanyLekarz) | ZnanyLekarz (strona placówki) |
| poradni lub przychodni na NFZ, POZ | swiatprzychodni.pl | Kliniki.pl (często bez opinii); Google przez link |
| dużego szpitala publicznego | Kliniki.pl | Google przez link |

Lekarze pracujący wyłącznie w szpitalach publicznych często nie mają ocen nigdzie. To nie obniża ich pozycji na liście — napisz „ocen nie znaleziono” i wymień, gdzie szukałeś.

## Jak zapisać

- Zawsze: źródło, średnia **ze skalą**, liczba opinii, czego dotyczy. Przykład: „ZnanyLekarz: 4,9/5 (247 opinii) · RankingLekarzy.pl: 4,8/5 (31 opinii) · Google: 4,5/5 (487 opinii, placówka)”; ocenę Google wziętą z Kliniki.pl oznacz „za Kliniki.pl, może być nieaktualna”; gdy Google brak: „Google: nie odczytano — [wizytówka](…)”.
- **Nie przeliczaj skal i nie uśredniaj między serwisami.** 9,5/10 i 4,7/5 podaj obok siebie tak, jak są.
- Ocena z kilku opinii znaczy niewiele — liczba opinii zawsze stoi obok średniej.
- Duża różnica między źródłami to informacja: powiedz o niej i sprawdź, czego dotyczą niskie oceny (często rejestracja i kolejka, nie leczenie).
- Nigdy nie wpisuj oceny z pamięci ani szacunkowej.

## Na końcu odpowiedzi

Jeśli dla wybranych lekarzy lub placówek nie masz oceny Google (nie masz przeglądarki albo wizytówka się nie otworzyła), dodaj jedno zdanie: „Ocen Google nie mogę odczytać. Jeśli chcesz je uwzględnić, otwórz linki do wizytówek i wklej mi oceny — dopiszę je do porównania.” Nie powtarzaj tej prośby przy każdym lekarzu.
