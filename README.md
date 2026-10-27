# Automatyzacja pozyskiwania i porządkowania danych z teleturnieju „Milionerzy”

**Python · Web Scraping · SQLite · przetwarzanie danych · kontrola jakości**

## 1. Problem

Pytania i odpowiedzi z kolejnych odcinków teleturnieju „Milionerzy” są publikowane w osobnych artykułach na stronie Polsatu. Każdy artykuł zawiera informacje, które można wykorzystać do stworzenia uporządkowanej bazy pytań: ich treść, cztery warianty odpowiedzi, poprawny wariant oraz przypisaną kwotę.

Ręczne zebranie tych informacji wymagałoby otwierania kolejnych artykułów, kopiowania danych i przypisywania ich do odpowiednich odcinków. Przy większej liczbie publikacji proces staje się czasochłonny i podatny na pomyłki.

Dodatkowym utrudnieniem są różnice w sposobie zapisywania odpowiedzi pomiędzy artykułami.

## 2. Cel

Celem było stworzenie narzędzia, które automatycznie odnajduje artykuły, wyodrębnia zawarte w nich pytania i odpowiedzi, a następnie zapisuje je w jednolitym formacie.

Program miał również umożliwiać identyfikowanie niekompletnych danych oraz ponowne przetwarzanie artykułów wymagających weryfikacji.

## 3. Rozwiązanie

**Etap 1 — wyszukiwanie artykułów.** Program rozpoczyna pracę od wskazanej strony i automatycznie wykrywa odnośniki do kolejnych odcinków.

**Etap 2 — pobieranie i analiza.** Artykuły są pobierane, a ich zawartość HTML analizowana w celu odnalezienia pytań, wariantów odpowiedzi i przypisanych kwot.

**Etap 3 — porządkowanie danych.** Wyodrębnione informacje są przekształcane w rekordy o jednakowej strukturze, niezależnie od różnic w formatowaniu artykułów.

**Etap 4 — zapis i kontrola.** Dane trafiają do bazy SQLite i plików CSV. Program rejestruje wyniki przetwarzania oraz sygnalizuje artykuły wymagające dodatkowej weryfikacji.

## 4. Rezultaty pierwszego przebiegu

Podczas pierwszego pełnego przebiegu program sprawdził **119 artykułów**, z których **114 zostało poprawnie przetworzonych**. W bazie zapisano **1173 pytania**.

Pozostałych pięć artykułów pozwoliło wykryć dodatkowy wariant zapisu poprawnych odpowiedzi, który wymagał rozszerzenia parsera.

![Wyniki automatycznego przetwarzania artykułów](screenshots/screenshot1.png)

*Zrzut ekranu przedstawiający wyniki automatycznego wykrywania pytań w kolejnych odcinkach.*

Wyniki dotyczą konkretnego przebiegu programu przed ponownym przetworzeniem pięciu problematycznych artykułów.
