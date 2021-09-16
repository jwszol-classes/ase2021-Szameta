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
6. Przekonwertowanie danych do formatu pandas DataFrame oraz ich prezentacja z wykorzystaniem matplotlib'a.

## Analiza uzyskanych wyników

![plot](https://i.imgur.com/qzY7mrv.png)

Z wykresów można odczytać kilka wniosków:


 1. Patrząc na oba wykresy prędkości(1 i 4) można zauważyć znaczny wzrost średniej prędkości taksówek w roku 2020 względem 2019 r. Jest to najpewniej spowodowane spadkiem natężenia ruchu ulicznego spowodowanego wybuchem pandemii COVID-19. Hipotezę tą potwierdzają wykresy ilości taksówek na ulicach w korespondujących latach(2 i 5). Można zauważyć nawet ich 20-krotny spadek. 

 2. Obserwując ogólnie wszystkie wykresy można dostrzec regułę, że: im mniej taksówek na ulicy tym większa jest ich średnia prędkość. Taksówki w tym wypadku są pewnym wskaźnikiem ogólnego natężenia ruchu, a im mniejsze jest ono tym szybciej jeżdżą wszystkie pojazdy.

 3. Interesujące są również występujące co 7 dni skoki średniej prędkości zarówno w 2019 jak i 2020r(1). Pokrywają się one oczywiście ze spadkami w ilości taksówek w danych dniach(2,3). Po sprawdzeniu w kalendarzu okazuje się, że te dni to niedziele. Co sugeruje, że w weekend ruch jest mniejszy niż w dni pracujące.

 4. Z wykresów prędkości dla danych godzin(4) można zauważyć, że największa prędkość jest w godzinach od 0 do 5 kiedy to większość osób śpi. Następnie spada by potem utrzymać się na podobnym poziomie między 9 a 18, by potem znów wzrosnąć. Porównując wykresy ilości taksówek można dostrzec(5 i 6), że wykres z przed pandemii(5) ma bardziej równomiernie rozłożone wartości w godzinach 7-23 względem tego po jej wybuchu(6). Na tym drugim można dostrzec dwa szczyty jeden o 8 drugi o 16. Są to godziny w których ludzie wracają z pracy.
