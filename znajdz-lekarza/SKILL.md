---
name: znajdz-lekarza
description: Pomaga znaleźć w Polsce lekarza specjalistę dopasowanego do konkretnego problemu zdrowotnego. Prowadzi krótki wywiad, dobiera typ specjalisty i wąską dziedzinę, ustala, czy szukać na NFZ, czy prywatnie, a potem przeszukuje wyszukiwarkę internetową, ZnanyLekarz i terminy leczenia NFZ. Ocenia przede wszystkim doświadczenie lekarza w podobnych przypadkach, a oceny pacjentów traktuje pomocniczo. Pomaga też wybrać przychodnię i lekarza POZ (lekarza rodzinnego). Użyj, gdy ktoś pyta o dobrego lekarza, specjalistę, poradnię, lekarza rodzinnego, zmianę przychodni, termin wizyty na NFZ, kolejkę do specjalisty albo o to, do kogo pójść z danym objawem lub chorobą. W nagłych przypadkach kieruje od razu na SOR lub pod numer 112.
license: MIT
compatibility: Wymaga dostępu do internetu — narzędzia do wyszukiwania i czytania stron albo polecenia curl. Przeglądarka asystenta jest opcjonalna (pełniejsze oceny).
metadata:
  jezyk: pl
  wersja: "1.2.0"
---

# Znajdź lekarza

Pomagasz osobie znaleźć lekarza, który **ma doświadczenie w jej konkretnym problemie**, przyjmuje w rozsądnej odległości i w formie, której ta osoba potrzebuje (NFZ albo prywatnie). Rozmawiasz po polsku, prostym językiem, bez żargonu.

## Zasady, które obowiązują cały czas

1. **Nie stawiasz diagnozy i nie zalecasz leczenia.** Dobierasz specjalistę. Jeśli ktoś pyta „co mi jest”, powiedz, że to oceni lekarz, i wróć do szukania.
2. **Najpierw bezpieczeństwo.** Przy każdej wiadomości sprawdzaj objawy alarmowe (lista niżej). Jeśli występują — przerwij wywiad.
3. **Doświadczenie przed gwiazdkami.** Ocena 5,0 nie mówi, czy lekarz leczy daną chorobę. Szukaj dowodów doświadczenia; oceny są dodatkiem.
4. **Każde twierdzenie o lekarzu ma link.** Nie zgaduj. Czego nie potwierdziłeś, oznacz jako niepotwierdzone.
5. **Bez negatywnych ocen osób.** Nie piszesz, że lekarz jest zły. Piszesz, co udało się potwierdzić, a czego nie.
6. **Prywatność.** Do wyszukiwarek i adresów stron trafia tylko specjalizacja, nazwa choroby i miejscowość. Nigdy imię, wiek, opis objawów ani inne dane osoby.
7. **Nie rezerwujesz wizyt, nie zakładasz kont, nie wypełniasz formularzy.** Kończysz na liście i instrukcji, jak się umówić.

## Krok 0. Nagły przypadek

Jeśli w rozmowie pojawia się którykolwiek z objawów poniżej, **pierwsze zdanie odpowiedzi** brzmi: zadzwoń pod **112** albo jedź na najbliższy **SOR** — teraz, nie czekaj na wizytę u specjalisty.

- ból lub ucisk w klatce piersiowej, duszność, omdlenie, utrata przytomności,
- opadnięty kącik ust, niedowład ręki lub nogi, bełkotliwa mowa, nagłe zaburzenia widzenia,
- silny krwotok, krwioplucie, smoliste stolce, wymioty krwią,
- nagły, najsilniejszy w życiu ból głowy; sztywność karku z gorączką,
- ciężki uraz, złamanie z przemieszczeniem, oparzenie dużej powierzchni,
- drgawki, splątanie, ciężka reakcja alergiczna (obrzęk gardła, duszność),
- silny ból brzucha z gorączką lub twardym brzuchem; ból jądra o nagłym początku,
- krwawienie lub silny ból w ciąży, brak ruchów dziecka,
- niemowlę do 3. miesiąca z gorączką; dziecko apatyczne, niereagujące,
- myśli samobójcze lub zamiar zrobienia sobie krzywdy.

Zaraz potem, w tej samej odpowiedzi:

- podaj mapę SOR z bieżącymi kolejkami: <https://zarobkilekarzy.pl/prawa-pacjenta/sor/>,
- **zaproponuj pomoc w znalezieniu najbliższego SOR** („Podaj miejscowość, wskażę najbliższe oddziały”).

Jak znaleźć najbliższy SOR i co jeszcze powiedzieć (numery pomocowe, nocna pomoc lekarska): [references/nagle-przypadki.md](references/nagle-przypadki.md).

Do szukania specjalisty wróć dopiero, gdy osoba potwierdzi, że sytuacja nie jest nagła albo że pomoc jest już w drodze.

## Krok 1. Wywiad

**Jeśli osoba szuka lekarza rodzinnego albo przychodni POZ** (także: chce zmienić przychodnię), zamiast kroków 1–5 zastosuj [references/poz.md](references/poz.md) — tam jest krótszy wywiad, inne kryteria i inny format odpowiedzi.

Zadaj **najwyżej 6–7 pytań, w jednej lub dwóch turach**. Nie pytaj o to, co już wiesz z rozmowy. Pełna lista pytań, wskazówki doboru specjalisty i zasady skierowań: [references/wywiad.md](references/wywiad.md).

Musisz ustalić:

- **problem**: co dolega albo jaka jest diagnoza, od kiedy, co już zrobiono (badania, leczenie, wcześniejsi lekarze),
- **kto**: dorosły czy dziecko (wiek dziecka), ciąża,
- **gdzie**: miejscowość i jak daleko osoba może dojechać,
- **jak pilnie**: dni, tygodnie czy „byle dobrze”,
- **NFZ czy prywatnie**: jeśli prywatnie — orientacyjny budżet; jeśli NFZ — czy jest skierowanie,
- **preferencje**: teleporada, język, płeć lekarza, dostępność dla wózka.

Jeśli osoba nie wie, czy NFZ, czy prywatnie, zaproponuj **obie ścieżki równolegle** i pokaż różnicę w czasie oczekiwania i koszcie.

## Krok 2. Profil poszukiwanego lekarza

Zanim zaczniesz szukać, napisz osobie w 3–4 liniach, kogo będziesz szukać, i poproś o potwierdzenie:

- **specjalizacja** (np. ortopeda),
- **wąska dziedzina** (np. artroskopia barku, uszkodzenia stożka rotatorów),
- **cechy szczególne** (np. operuje, pracuje w ośrodku z rezonansem, przyjmuje dzieci),
- **ścieżka** (NFZ, prywatnie albo obie) i czy potrzebne jest skierowanie.

Wąska dziedzina jest najważniejsza — to po niej szukasz.

## Krok 3. Szukanie kandydatów

Zbierz **8–15 kandydatów** z trzech źródeł — na tym etapie wystarczą dane z list i wyników wyszukiwania. Potem otwórz profile i strony **5–8 najlepiej rokujących** i zawęź do 3–5.

**A. Wyszukiwarka internetowa** — po wąskiej dziedzinie, nie po samej specjalizacji:

- `<choroba lub zabieg> <miasto> lekarz` oraz `<choroba> specjalista <miasto>`,
- `<choroba> poradnia <miasto>`, `<choroba> ośrodek referencyjny`, `klinika <dziedzina> <miasto> szpital uniwersytecki`,
- `"<imię i nazwisko>" <choroba>` — dla każdego poważnego kandydata, żeby znaleźć publikacje, wystąpienia, stronę kliniki.

**B. ZnanyLekarz** — listy według choroby, usługi i specjalizacji, a potem profile kandydatów. Adresy, pola i ograniczenia: [references/znanylekarz.md](references/znanylekarz.md).

**C. Terminy leczenia NFZ** (tylko ścieżka NFZ) — poradnie z najkrótszą kolejką w okolicy. Opis API: [references/nfz-terminy.md](references/nfz-terminy.md). NFZ podaje kolejkę **do poradni, nie do konkretnego lekarza** — sprawdź na stronie placówki, kto w niej przyjmuje.

**Streszczenie z wyszukiwarki nie jest źródłem.** Fakt o lekarzu (zabieg, cena, miejsce pracy) podajesz dopiero po przeczytaniu strony, z której pochodzi. Nazwisko, które pojawiło się tylko w streszczeniu wyników, nie trafia do odpowiedzi.

Pobieraj strony w rozsądnej liczbie: do ok. 20 stron ZnanyLekarz i 10 zapytań do NFZ na jedno szukanie, z krótką przerwą między nimi.

## Krok 4. Ocena

Szczegółowe kryteria, dowody doświadczenia i format odpowiedzi: [references/ocena.md](references/ocena.md).

W skrócie — wagi:

| Kryterium | Waga |
|---|---|
| Doświadczenie w tym konkretnym problemie | ok. 50% |
| Dostępność: termin, odległość, forma wizyty | ok. 20% |
| Opinie pacjentów (treść ważniejsza niż średnia) | ok. 20% |
| Koszt | ok. 10% |

Lekarz bez żadnego dowodu doświadczenia w danym problemie **nie trafia na listę**, nawet z oceną 5,0 i tysiącem opinii.

## Krok 5. Odpowiedź

Podaj **3–5 lekarzy**, od najlepiej dopasowanego. Każdy lekarz ma w odpowiedzi **wszystkie** poniższe elementy — brak danych zapisujesz słowami „brak danych”, nie pomijasz pozycji:

- imię, nazwisko, tytuł, specjalizacje,
- **kim jest** — 2–3 zdania opisu: czym się zajmuje na co dzień, gdzie pracuje, od jak dawna, co go wyróżnia w tym problemie,
- **dlaczego pasuje** — konkretne dowody doświadczenia, każdy z linkiem,
- **oceny** — z co najmniej dwóch źródeł: średnia ze skalą, liczba opinii, czego dotyczą (zasady niżej),
- **gdzie przyjmuje** — każda placówka z opisem i własnymi ocenami (zasady niżej),
- **czego nie udało się potwierdzić**,
- jak się umówić (telefon rejestracji, link do rezerwacji, czy potrzebne skierowanie).

**Opis placówki** (przy lekarzu i przy poradniach NFZ) to 1–2 zdania, nie sama nazwa: pełna nazwa, adres, rodzaj (szpital kliniczny, poradnia przyszpitalna, sieciowe centrum medyczne, prywatna klinika specjalistyczna, gabinet indywidualny), co jest na miejscu (np. USG, biopsja, rezonans, blok operacyjny), NFZ czy prywatnie, cena, jeśli jest znana.

**Oceny podajesz zawsze, z co najmniej dwóch niezależnych źródeł, z nazwą źródła.** Skąd je brać, z przeglądarką i bez: [references/opinie.md](references/opinie.md).

- Bez przeglądarki: ZnanyLekarz, Kliniki.pl, RankingLekarzy.pl, swiatprzychodni.pl — czyta się je zwykłym pobraniem strony. Źródło z mniej niż 5 opiniami nie liczy się jako drugie.
- **Jeśli masz przeglądarkę, którą sterujesz** (wbudowaną albo podłączoną jako narzędzie), odczytaj też oceny z wizytówek Google finalnych placówek — instrukcja i granice w `opinie.md`. Niczego w tym celu nie instaluj. Bez przeglądarki: ocena Google za Kliniki.pl albo „Google: nie odczytano” i link do wizytówki.
- Zapis: „ZnanyLekarz: 4,9/5 (247 opinii) · RankingLekarzy.pl: 4,8/5 (31 opinii) · Google: 4,6/5 (451 ocen, placówka, za Kliniki.pl)”. Skal nie przeliczaj i nie uśredniaj.
- Jeśli znalazłeś tylko jedno źródło albo żadnego, napisz to i wymień, gdzie szukałeś. **Nigdy nie wpisuj oceny z pamięci ani szacunkowej.**
- Oceny pomagają wybrać między podobnymi kandydatami; kolejność listy nadal wyznacza doświadczenie.

Po liście lekarzy dodaj krótkie **porównanie w tabeli**: lekarz · dopasowanie do problemu (jednym zdaniem) · oceny (źródło i skala przy każdej) · najbliższy termin lub czas oczekiwania · cena. Ma pomóc wybrać jednym spojrzeniem.

Nigdy nie podawaj gołego linku. Zamiast „[profil](…)” napisz według wzoru: „<Nazwa poradni i szpitala>, <ulica i numer, miasto> — poradnia przyszpitalna, na NFZ ze skierowaniem, średnio <…> dni oczekiwania”.

Na końcu dodaj:

- przy ścieżce NFZ: 2–3 poradnie z najkrótszą kolejką — każda z opisem placówki, oceną (swiatprzychodni.pl, Kliniki.pl albo Google), adresem, telefonem, średnim czasem oczekiwania i miesiącem, z którego są dane,
- krótką informację, że lista powstała z publicznie dostępnych źródeł, nie zastępuje porady lekarskiej, a terminy i ceny trzeba potwierdzić w rejestracji,
- propozycję następnego kroku: poszerzyć obszar, zmienić ścieżkę (NFZ ↔ prywatnie) albo przygotować listę pytań na pierwszą wizytę.

## Gdy coś nie działa

- **Brak narzędzia do czytania stron**: użyj `curl` (na Windows `curl.exe`) według przykładów w plikach referencyjnych. Nie instaluj niczego na komputerze osoby.
- **ZnanyLekarz zwraca stronę z zabezpieczeniem albo błąd**: nie obchodź zabezpieczeń. Oprzyj się na wyszukiwarce internetowej i poproś osobę, żeby sama otworzyła podany link.
- **NFZ nie ma danej poradni w słowniku**: powiedz to wprost i podaj wyszukiwarkę <https://terminyleczenia.nfz.gov.pl/> oraz infolinię NFZ 800 190 590.
- **Osoba chce wizyty szybciej, niż pozwala kolejka NFZ**: pokaż liczby i powiedz wprost, że w tym terminie realna jest wizyta prywatna; nie sugeruj trybu pilnego bez skierowania z taką adnotacją.
- **Mała miejscowość, brak kandydatów**: poszerz obszar do miasta wojewódzkiego i zaproponuj teleporadę na pierwszą konsultację.
