# Projekt zaliczeniowy **ASEiED** 2021
## Wybrane zadanie 
### Zadanie 2
Dokonaj analizy danych zawierających informacje na temat poruszających się taksówek w Nowym Jorku (yellow and green taxi). Zbiór danych zawiera następujące informacje (pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts).

Zadanie wymaga przeanalizowania danych w następującym przedziale czasowym:
-   Rok 2020 / Maj 
-   Rok 2019 / Maj

## Wybrany podpunkt zadania - podpunkt c)
Wylicz średnią prędkość taksówki na podstawie informacji na temat czasu (pick-up and drop-off dates/times) oraz przebytej odległości (trip distances).

## Realizacja projektu
Projekt został opracowany w środowisku chmurowym AWS za pomocą serwisu Amazon Elastic MapReduce, dokładniej **EMR Notebook z wykorzystaniem Kernela PySpark**.

Główne etapy projektu można podzielić na:

 1. Wczytanie danych z serwisu S3 (Bucket: nyc-tlc) do pyspark DataFrame.
 2. Wybranie kolumn, które będą służyły do dalszych obliczeń oraz zunifikowanie nazw tych kolumn, aby połączyć DataFrame'y dla poszczególnych dat tj. 2019-05 oraz 2020-05.
 3. Zmiana jednostki prędkości mph na km/h, zmiana jednostki kolumn pickup_datetime oraz dropoff_datetime na unix datetime oraz obliczenie prędkości dla poszczególnych taksówek:
`trip_distance_km / (unix_dropoff_datetime - unix_pickup_datetime)`.
4. Filtrowanie niewiarygodnych rekordów (w skrajnych przypadkach prędkość taksówki wynosiła ponad 2000 km/h).
5. Wyodrębnienie danych do sporządzenia wykresów tj. średnich wartości prędkości taksówek oraz ilości taksówek (dla poszczególnych godzin oraz dni w 2019 i 2020).

## Analiza uzyskanych wyników