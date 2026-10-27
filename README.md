# Automatyzacja pozyskiwania, analizy i raportowania danych z teleturnieju „Milionerzy”

**Python · Web Scraping · SQLite · kontrola jakości danych · analiza statystyczna · raportowanie PDF**

## 1. Problem

Pytania i odpowiedzi z teleturnieju „Milionerzy” są publikowane w osobnych artykułach na stronie Polsatu. Każdy artykuł zawiera kilka lub kilkanaście pytań, cztery warianty odpowiedzi, poprawny wariant oraz kwotę przypisaną do danego pytania.

Ręczne zebranie tych informacji wymagałoby otwierania kolejnych artykułów, kopiowania danych i przypisywania ich do odpowiednich odcinków. Przy większej liczbie publikacji proces staje się czasochłonny i podatny na błędy.

Dodatkowym utrudnieniem są różnice w formatowaniu artykułów oraz sposobie zapisywania poprawnych odpowiedzi.

## 2. Cel

Celem było stworzenie narzędzia, które automatycznie odnajduje artykuły, wyodrębnia zawarte w nich informacje i zapisuje je w uporządkowanej bazie danych.

Rozwiązanie miało również umożliwiać kontrolę jakości zgromadzonych rekordów, wykrywanie brakujących danych, wykonywanie podstawowych analiz statystycznych oraz automatyczne generowanie raportu PDF.

## 3. Rozwiązanie

**Etap 1 — wyszukiwanie artykułów.** Program rozpoczyna pracę od wskazanej strony i automatycznie wykrywa odnośniki do kolejnych odcinków.

**Etap 2 — pobieranie i ekstrakcja danych.** Zawartość HTML jest analizowana w celu wyodrębnienia pytań, wariantów odpowiedzi, poprawnych odpowiedzi i przypisanych kwot.

**Etap 3 — porządkowanie i archiwizacja.** Dane są zapisywane w relacyjnej bazie SQLite oraz eksportowane do plików CSV, co umożliwia ich dalsze przetwarzanie.

**Etap 4 — kontrola jakości.** Osobny moduł analizuje rekordy pod kątem brakujących wartości, nieprawidłowych danych, niespójności i identycznych pytań.

**Etap 5 — analiza statystyczna.** Program oblicza podstawowe statystyki, między innymi rozkład poprawnych odpowiedzi, liczbę pytań według kwot i średnią liczbę pytań na odcinek.

**Etap 6 — raportowanie.** Na podstawie aktualnej zawartości bazy automatycznie generowany jest raport PDF z tabelami, wykresami, wynikami kontroli jakości i krótkimi wnioskami.

## 4. Rezultaty

W analizowanym zbiorze zgromadzono:

| Wskaźnik | Wynik |
|---|---:|
| Poprawnie przetworzone artykuły | 119 |
| Wyodrębnione pytania | 1 229 |
| Średnia liczba pytań na odcinek | 10,33 |
| Minimalna liczba pytań na odcinek | 4 |
| Maksymalna liczba pytań na odcinek | 14 |
| Problemy wykryte przez moduł kontroli jakości | 0 |
| Luki w numeracji odnalezionych artykułów | 1 (odcinek 81) |

![Wyniki automatycznego przetwarzania artykułów](screenshots/screenshot1.png)

*Przykładowy przebieg programu przedstawiający liczbę pytań wyodrębnionych z poszczególnych artykułów.*

Wszystkie 119 przetworzonych artykułów uzyskało status `ok`. Nie oznacza to jednak niezależnego potwierdzenia kompletności całego archiwum.

## 5. Testy i kontrola jakości danych

Do weryfikacji danych przygotowano osobny moduł analityczny, który sprawdza m.in.:

| Scenariusz | Zakres kontroli |
|---|---|
| Brakujące wartości | Wykrywanie niekompletnych rekordów |
| Nieprawidłowa odpowiedź | Sprawdzanie poprawności oznaczeń A–D |
| Nieprawidłowa kwota | Kontrola wartości przypisanych do pytań |
| Duplikaty | Wykrywanie identycznych pytań po normalizacji tekstu |
| Niespójność danych | Porównanie liczby pytań z informacjami o odcinkach |
| Brakujący artykuł | Wykrywanie luk w numeracji odnalezionych odcinków |

**Wynik kontroli:** w aktualnym zbiorze nie wykryto problemów objętych zaimplementowanymi regułami walidacji.

Kontrola nie obejmuje oceny semantycznego podobieństwa pytań ani niezależnego porównania każdego rekordu z artykułem źródłowym.

## 6. Analiza statystyczna i automatyczne raportowanie

Zgromadzone dane wykorzystano do przygotowania raportu analitycznego, generowanego automatycznie z bazy SQLite.

Raport przedstawia między innymi rozkład poprawnych odpowiedzi A–D, liczbę pytań przypadających na poszczególne kwoty oraz wyniki kontroli jakości.

W analizowanym zbiorze najczęściej występowała poprawna odpowiedź **B (359 przypadków)**, a najrzadziej **A (252 przypadki)**. Liczba zarejestrowanych pytań zmniejszała się wraz z kolejnymi progami kwotowymi.

Są to obserwacje opisowe dotyczące zgromadzonego zbioru, a nie podstawa do przewidywania przyszłych odpowiedzi.

![Automatycznie wygenerowany raport analityczny](screenshots/screenshot2.png)

*Fragment raportu PDF przedstawiający statystyki i wyniki analizy danych.*

**[Zobacz przykładowy raport analityczny PDF](reports/raport_milionerzy.pdf)**

## 7. Praktyczne wykorzystanie

Projekt pokazuje możliwość przekształcenia rozproszonych treści internetowych w uporządkowany zbiór danych, który można następnie kontrolować, analizować i prezentować w postaci raportów.

Zastosowane podejście może być wykorzystane również przy innych zadaniach wymagających automatycznego pozyskiwania informacji, porządkowania rekordów, wykrywania nieprawidłowości oraz przygotowywania cyklicznych zestawień.

Najważniejszym rezultatem jest zautomatyzowanie całego procesu — od pobrania danych źródłowych po wygenerowanie czytelnego raportu analitycznego.
