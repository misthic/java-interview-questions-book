# JAVA INTERVIEW QUESTIONS BOOK

## TABLICA HASHUJACA
Kolekcja przechowująca dane w strukturze klucz-wartość. Wykorzystuje hashCode i equals.
Podobna do HashMapy ale ZSYNCHRONIZOWANA
Nie zezwala na używanie null jako klucza i wartości
Do iteracji wykorzystuje enumerator
Wolniejsze od hashmap


## HASH CODE I EQUALS
Equals powinna służyć do porównywania obiektów, w większości przypadków domyślna metoda nie wystarczy i powinno się ją nadpisywać. Equals powinna być zwrotna, symetryczna, przechodnia, spójna i powinna zwracać false przy porównaniu z wartością null.
HashCode zwraca int, która służy do przyporządkowania danego obiektu do grupy - dzięki niej jesteśmy podzielić wszystkie możliwe instancje danej klasy na rozdzielne grupy. Zazwyczaj metodę nadpisuje się poprzez przemnożenie atrybutów klasy przez liczby pierwsze.
Jeśli obiekty A i B są równe w equals() to powinny mieć takie same hashcode'y.


## PODSTAWOWE ALGORYTMY
1. QuickSort - dzieli tablicę na 2 mniejsze, sortuje je osobno, a potem łączy ze sobą.
2. BubbleSort - prosty i wolny - porównuje każdą parę po kolei ze sobą i zamienia je miejscami jeśli trzeba.
3. InsertionSort - prosty i wolny - bierze element z nieposortowanej sekcji i wstawia go w odpowienim miejscu. 


## GARBAGE COLLECTOR
(https://bulldogjob.pl/news/404-jvm-garbage-collector-wprowadzenie)
Program w JVM, który usuwa z pamięci nieużywane obiekty. Dzięki niemu memory heap nie jest zapełniany tak szybko.
Pamięć dzieli się na Young generation (YG) i Old Generation (OG):
YG obszar, do którego trafiają nowe obiekty, składa się z 3 stref - eden, survivor one i survivor two. Nowo powstały obiekt trafia do edenu, który nieustannie jest zapełniany - w momencie zapełnienia GC przenosi te obiekty do s1, jednocześnie odrzucając nieosiągalne. Cykl zaczyna się od nowa, tym razem analizuje również s1 i na koniec przenosi wszystkie obiekty do s2. W kolejnej iteracji role survivorów się odwracając, a dzięki takiemu ciągłemu czyszczeniu nie ma problemu z fragmentacją pamięci.
Obiekty ze stref s1 i s2 jeśli są w nich wystarczająco długo trafiają do OG. Obszar ten jest znacznie większy od YG i dlatego GC działa tu rzadziej.


## TYPY POLIMORFIZMU
1. Statyczny polimorfizm - compile time
np. przeciążanie method (overloading)
2. Dynamiczny polimorfizm - runtime 
np. nadpisywanie metod


## BLOKI STATYCZNE
Oznaczane i wywoływeane przy pomocy słówka static{...}. Kod zawarty w bloku statycznym wykonuje się tylko raz - przy załadowaniu danej klasy do pamięci.


## TRY WITH RESOURCES
Specjalna składnia try-catch-finally, która pozwala na uniknięcie pisania zbędnego kodu. Wykorzystuje się go zazwyczaj przy wszelkiej maści streamach/scannerach - dzięki niemu po wykonaniu kodu taki stream/scanner jest zamykany automatycznie, dzięki czemu programista nie musi robić tego ręcznie w bloku finally.


## WIELOWĄTKOWOŚĆ - JAK JA OSIĄGNĄĆ W JAVA
W Javie z wątkami możemy pracować głównie na 2 sposoby: dziedzicząc po klasie Thread lub rozszerzając interfejs Runnable. Zarówno w jednym jak i drugim przypadku musimy nadpisać metodę run(). 
Cykl życia wątków w Javie:
- NEW - nowy nieuruchomiony wątek
- RUNNABLE - wątek, który może wykonywać swój kod
- TERMINATED - wątek, który skońćzył swoją pracę
- BLOCKED - wątek zablokowany, czeka na zwolnienie współdzielonego zasobu
- WAITING - wątek uśpiony
- TIMED_WAITING - wątek uśpiony na określony czas
synchronized(){...} lub w deklaracji metody - kod może być uruchomiony tylko przez jeden wątek, rozwiązuje problem z wyścigami
volatile - oznacza, że wątek nie może odczytać wartości przed zapisem zmienianego stanu obiektu/wartości
Z wątkami dobrze działa immutable kod, ponieważ w immutable zmiennych/obiektach nie możemy zmieniać wartości, a jedynie je odczytywać.
Operacja tworzenia wątku jest bardzo kosztowna, dlatego też, gdy potrzebujemy dużej liczby predefiniowanych wątków do krótkich zadań warto skorzystać z ThreadPoola (np. ExecutorService).


## PODZIAŁ EXCEPTIONOW
1. Checked exception - jeśli w hierarchii dziedziczenia ma Exception i nie ma Runtime Exception, np IOException
2. Unchecked excpetion - pozostałe, np IllegalArgumentException


## ADNOTACJE
?? TODO


## KOLEKCJE ## 
Iterable		Map
	|
Collection
|	|	|
List / Set/ Queue
Set ma unikalne wartości - sprawdza je za pomocą hashCode i equals. Najważniejsza implementacja tego interfejsu to HashSet.
- hashset - zapewnia unikalność, nie ma gwarancji co do kolejności. Używa tablicy mieszającej
- treeset - implementacja oparta o drzewa czerwono czarne - gwarantuje to unikalność elementów oraz uporządkowanie zgodnie z naturalnym porządkiem (Comparable)
- linkedhashset - korzysta i z tablicy mieszającej i z listy podwójnie wiązanej - zachowuje kolejność zgodną z kolejnością dodawania
Map kolekcja zawiera zestaw kluczy i wartości - klucze są unikalne, wartości mogą się powtarzać. Standardowa implementacja to HashMap.
- hashmap - oparta o tablice mieszaną, nnie gwarantuje kolejności elementów. LoadFactor 0,75
- treemap - zapewnia sortowanie na podstawie naturalnego porządku kluczy wyznaczanego przez implementację interfejsu Comparable. Wykorzystuje drzewa czerwono czarne.
- linkedhashmap - zapamiętuje kolejność dodawanai elementów, wykorzystuje tablicę mieszaną i listę wiązaną.
Hashmapy wpisują elementy do tzw. bucketów - wcześniej były to po prostu linkedlisty map. Obecnie jest to albo struktura drzewa elementów albo linked lista.

## MOCKITO
Pozwala na wstrzykiwanie mockowanych instancji np serwisów. Nie są tworzone realne obiekty, tylko mocki. Tworzy się je za pomocą adnotacji @Mock.
@Spy - pozwala na tworzenie prawdziwych obiektów i pomaga w używaniu normalnych metod obiektu jednocześnie pozwalając na śledzenie każdej interakcji, jak w przypadku mocków
@Captor - tworzy ArgumentCaptora, który używany jest do przechwytywania wartości argumentów metod do assercji.


## WZORCE PROJEKTOWE
1. Kreacyjne
	Factory - udostępnia interfejs do tworzenia obiektów w ramach klasy bazowej, ale pozwala podklasom zmieniać typ tworzonych obiektów
	Builder - pozwala na budowanie obiektów etapami, nie używając rozbudowanych konstruktorów
	Prototype - polega na kopiowaniu istniejących obiektów bez tworzenia zależności miezy kodem a klasami, korzysta z clone()
	Singleton - zapewnia istnienie tylko i wyłącznie jednej instancji danej klasy.
2. Strukturalne
	Facade - odpowiada za utworzenie interfejsu, który zawierać będzie ograniczoną funkjonalność
	Proxy - tworzy obiekt zastępczy w miejsce innego obiektu
	Adapter - pozwala na kooperacje obiektów o niekompatybilnych interfejsach, np konwerter xml na json
	Decorator - wrzucanie obiektów we wrappery
3. Behawioralne
	Mediator - tworzony jest obiekt Mediatora który odpowiada za komunikacje między innymi klasami/interfejsami
	Observer - wzorzec wprowadza mechanizm, dzięki któremu obiekty zostają poinformowane o zdarzeniach na obserwowanym obiekcie
	Visitor
	Strategy - wydzielenie abstrakcji, która polega na wyborze odpowiedniego algorytmu z rodziny algorytmów odpowiedzialnych za podobną funkcjonalność


## SPRING BOOT
Ma wbudowaną bazę danych (h2) oraz wbudowany serwer aplikacji (tomcat/jetty).
Nie wymaga plików konfiguracyjnych .xml w przeciwieństwie do Springa, działa głównie na adnotacjach
Łatwa konfiguracja projektu poprzez spring initialzr


## ADNOTACJE DO TESTÓW W SPRING BOOCIE
@springboottest - informuje SB, że ma szukać klasy z główną konfiguracją (@SpringBootApplication) i użyć jej do startu application context
@AutoConfigureMockMvc - pozwala na testowanie requestów HTTP bez konieczności startowania serwera. Korzysta się z tego poprzez tworzenie instancji MockMvc, która wymaga użycia ww adnotacji nad klasą testu.


## HIBERNATE ## 
Hibernate jest najczęściej stosowanym ORMem w Javie. Służy za operacje związane z bazą danych oraz mapowanie relacyjno - obiektowe.
W Springu możliwe są transakcje, które oznaczane są adnotacją @Transactional. Polegają one na grupowym wprowadzaniu zmian w bazie danych, przy czym podzielone jest to na 3 części: rozpoczęcie, wykonanie operacji oraz jej zakończenie. Po zakończeniu operacji zmiany zostają albo zatwierdzone albo zostają wycofane (rollback). W transakcji możemy również ustawić timeout (w adnotacji @Transactional lub dla JDBC setQueryLimit). 
Możemy również konfigurować, które klasy wyjątków będą powodować rollback.
Typy:
- REQUIRED - domyslny, szuka aktywnej, jak nie ma to tworzy nowa
- SUPPORTS - szuka aktywnej, jak jest to uzywa, jak nie to non-transaction
- MANDATORY - szuka aktywnej i jej, jesli nie ma to exception
- NEVER - exception leci jak jest aktywna transakcja
- NOT_SUPPORTED - jak istnieje to logika jest wykonywana bez
- REQUIRES_NEW - zawiesza obecna jest jest i tworzy nowa
- NESTED - jesli jest aktywna to tworzymy savepoint. Jesli poleci exception w logice to robi rollback do danego miejsca. Jesli nie ma to działą jak REQUIRED.
Hibernate ma dwa poziomy cache:
1) Sposób na zbyt częste uderzanie do bazy danych
Zawsze włączony, nie da się go wyłączyć. Dzięki niemu obiekty nie muszą być za każdym razem ściągane z bazy. Sesja przechowuje wyciągane obiekty i nie wysyła SQL do bazy, jeśli obiekt jest już obecny. Po zakończeniu sesji wszystkie obiekty są kasowane.
2) Cache obiektów pomiędzy sesjami
Działa na poziomie SessionFactory, dlatego ten poziom jest wspólny dla wszystkich stworzonych sesji. Jeśli jest włączony to odpowiada za dostarczanie obiektów do L1. Wymaga dodatkowej konfiguracji oraz biblioteki zajmującej się implementacją L2.
Obiekty w Hibernate mogą posiadać 3 stany:
- transient - obiekt nie jest powiazany z sesja hibernate i nie reprezentuje wiersza w bazie. GC go zje jeśli nic innego do niego nie uderzy. Trzeba użyć save() lub persist().
- persistent - powiązany z sesją hibernate'a. Reprezentuje wiersz w bazie, posiada ID.
- detached - obiekt usunięty z sesji. Posiada ID ale nie można wykonywać na nim żadnych operacji bazodanowych - w przypadku zmian w takim obiekcie nie zostaną one zapisane w bazie danych.


## SQL
Indeksy to obiekty bazodane, które nie są zależne od tabeli. Pozwalają uzyskać szybszy dostęp do danych - przechowują wartości kolumn, na które są nakładane oraz ROWID wiersza.
view - wirtualne widoki które za każdym razem wykonują zapytanie
materialized view - zapisane na dysku i aktualizowane co jakiś czas, dostęp nie wymaga wykonania zapytania


## CQRS ## 
Command Query Responsibility Segregation powiązany jest z Event Sourcingiem.
ES pozwala na odtwarzanie aktualnego stanu aplikacji na podstawie odkładanych w Event Storze eventów. CQRS polega na segregowaniu polecen i zapytan w architekturze. Zapytania zwracają wyniki nie zmieniając obserwowanego stanu, polecenia zmieniają stan nie zwracając wartości.


## RABBITMQ
W skrócie kolejka, składa się z:
- publishera (np apka)
- exchange
- route
- queue
- consumer (np inna apka)
4 rodzaje exchange'y:
- direct - message trafia bezpośrednio na kolejkę, której key jest ustawiony
- topic - wysyła message na kolejki matchując między kluczem a przypisanym patternem
- fanout - wysyła message na wszystkie kolejki przypisane do niego
- headers - przydzielają kolejki na podstawie atrybutów message headera


## CI/CD
CI - continous integration
Wprowadzane zmiany w kodzie są okresowo sprawdzane w repozytorium wersji kodu. Celem CI jest stworzenie spójnego i zautomatyzowanego środowiska budowania i testowania aplikacji.
CD - continous delivery
Polega na automatyzacji wdrażania aplikacji i wprowadzanych zmian w kodzie oraz dostarczania ich do odpowiednich środowisk (developerskie, testowe, produkcyjne)


## HTTP
Kody i przykłady:
- informacyjne 100-199
	100 - wszystko spoko i należy kontynuować
- sukces 200-299
	200 OK
	201 CREATED - zwracamy np po POST requeście
	202 ACCEPTED - przyjęto request ale jeszcze nic się nie wydarzyło
- przekierowanie 300-399
	300 MULTIPLE CHOICES 0 rquest ma wiecej niz jedną prawdopodobną odpowiedź
- błędy klienta 400-499
	400 BAD REQUEST - błędny request 
	401 UNAUTHORIZED - brak autentykacji
	403 FORBIDDEN - klient nie ma dostępu do danej zawartości / brak autoryzacji
	404 NOT FOUND - nie znaleziono
- błędy serwera - 500-599
	500 INTERNAL - coś się popsuło i nie wiadomo czemu
	503 SERVICE UNAVAILABLE - serwer/apka nie jest w stanie obsłużyć requesta
	Metody:
- GET - pobieranie danych
- POST - tworzenie danych
- PUT - aktualizacja całej danej lub jej stworzenie | idempotentny
- DELETE - usunięcie danych
- PATCH - częściowa aktualizacja danych  | częściowo idempotentny
Odpowiedniki CRUD:
- Read
- Create
- Update/replace
- Delete
- Update/modify


## GIT ## 
1. Merge vs Rebase
Merge tworzy dodatkowe rozgałęzienie oraz commity na głównym branchu po marge'u
Rebase "wypłaszcza" drzewo, tworzy liniową strukturę, ale modyfikuje historie zmian
2. Cherry pick - pozwala dołączać wybrane commity do obecnego HEADa


## ONION ARCHITECTURE
Architektura tworzenia systemu, która gwarantuje:
- niezależność od frameworka / bibliotek 
- testowalność z wykluczeniem bazy danych i UI
- niezależność względem UI
- niezależność względem wybranego rodzaju bazy danych
- odseparowanie modelu biznesowego
Składa się z 4 warstw (licząc od zewnętrznej):
1. Frameworki i sterowniki
2. Adaptery interfejsu
3. Reguły biznesowej logiki
4. Warstwa entities
Dzięki OA zapewniona jest IoC


## IoC i DI
Inversion of Control, czyli odwrócenie sterowania
DI - dependency injection


## SOLID
- Single Responsobility - klasa powinna mieć wyłącznie jeden powód do zmiany -> klasa powinna mieć jeden główny cel
- Open/Closed - otwarty na rozszerzenia, zamknięty na modyfikacje. Dotyczy używania kompozycji, dziedziczenia i modyfikatorów dostępu
- Liskov Substitution - kod powinien pracować poprawnie z klasą, jak i jej podklasami
- Interface Segregation - rozdzielanie interfejsów klasy
- Dependency Inversion - wysokopoziomowe klasy nie powinny zależeć od niskopziomowych detali. Powinno to być odwrócone poprzez wprowadzenie dodatkowych warstw abstrakcji.


## ACID
Związane z bazami danych
- Atomicity - niepodzielność; każda transakcja wykonywana jest albo w całości albo wcale 
- Consistency - spójność; integralność danych - zapewnia spójność danych 
- Isolation - izolacja; związane ze współbieżnością, przykładowo kilka osób może korzystać z bazy w tej samej chwili
- Durability - trwałość; w przypadku awarii jesteśmy w stanie odtworzyć


## REST
Główne sposoby autentykacji:
1. HTTP schematy
	basic auth - nie zalecana, wymaga loginu i hasła, kodowane przy użyciu Base64
	digest - wysyłany w plaintexcie, klucz jednorazowy. Łączy się z kilkoma rzeczami, np loginem, hasłem, URI requestem a potem się szyfruje przy użyciu MD5
2. API Keys
	Autentykacja poprzez użycie klucza dostępu, którego możemy np wrzucić w header, w basic authu, w body itd.
3. OAuth 2.0
	Najczęściej do autentykacji osób, które logują się do systemu. Wymaga access tokenu lub/i refresh tokenu. Access token może wygasnąć. 


## JWT
JSON Web Token, sposób autentykacji API. Składa się z:
- header - informacje na temat algorytmu szyfrowania oraz typie tokena
- payload - dowolny ładunek, najczęściej info na temat roli i praw usera / długość zycia tokena
- verify - podpis cyfrowy, stanowi sumę kontrolną


## PIRAMIDA TESTÓW
Od dołu:
1. Jednostkowe - testują małe fragmentu kodu, np pojedyncze klasy czy metody
2. Integracyjne - testują interfejsy i interakcje, np między modułami tworzonego systemu
3. Systemowe/e2e - na docelowym środowisku produkcyjnym. Mają na celu przejście przez wszystkie warstwy aplikacji.


## SWAGGER
Pozwala wygenerować dokumentację API na podstawie kodu.
Przyspiesza tworzenie dokumentacji oraz prace w różnych zespołach pracujących nad jednym produktem.


## JDK
Java development kit, zawiera:
- JRE 
	class loader - odnajduje binarne reprezentacje klasy w classpathie aplikacji, po czym wczytuje ją do odpowiedniego segmentu pamięci
	byte code verifier - sprawdza poprawność strukturalna klasy czy interfejsu
	java api
- JVM 
	java interpreter
	JIT - kompilator, który optymalizuje i kompiluje tylko wybrane fragmenty kodu bajtowego będącego wynikiem wstępnej kompilacji dokonanej przez kompilator Javy
	GC - było wyżej
	
	
## ZAKRESY BEANOW
1. Singleton - istnieje tylko jedna instancja beana
2. Prototype - przy każdym wywołaniu beana dostajemy jego nową instancję
3. Request - cykl życia beana powiązany z pojedynczym żądaniem http
4. Session - zakres beana równa się zakresowi sesji http
5. Global session - jak wyżej ale globalnemu zakresowi sesji http


## RODZAJE AUTOWIRING
Beany Springa możemy autowiringować poprzez:
1. Typ danych - jeśli typ danych peirwszego beana jest zgodny z typem danych pola drugiego beana, to pierwszego podpinamy pod pole drugiego
2. Nazwę - bierze pod uwagę nazwę beana i nazwę pola w drugim beanie, a jeśli się zgada to Spring automatycznie podpina go pod to pole
3. Konstruktor - jak (1), ale nie patrzy na typ danych pola, tylko na konstruktor
4. Autodetekcję - jeśli do beana dorzucimy konstruktor to próbuje przez (3), jeśli nie występuje w beanie kontruktor to (1)


## FINAL/-LY/-IZE
final - keyword, po inicjalizacji zmiennej/obiektu nie można w nim nic zmieniać
finally - działa z try-catchem, oznacza blok kodu, któy zawsze się wykona
finalize - metoda klasy Object, wywoływana tylko i wyłącznie raz - przez usunięciem z pamięci przez GB


## PROBLEM N+1
Problem polegający na wysłaniu n+1 małych zapytań do bazy o dane z powiązanych tabel, zamiast wysłania jednego zapytania, który pobierze wszystkie dane.
Przykład:
Mamy encje User i Message, przy czym Message ma 1 autora, 1 user może mieć wiele message'y. Wrzucamy nad polem author @ManyToOne z typem fetchowania LAZY - przez to powstaje problem N+1. Pobieramy listę wszystkich wiadomości i robiąc getAuthor() za każdym razem uderzamy do bazy danych.
Rozwiązanie - EAGER jest zbyt obciążąjący, więc:
1) w JPA EntityGraph
2) w JPQL LEFT JOIN FETCH
3) w CRITERIA fetch


DODATKOWO:
## cache w rescie - czyli cachecontrol


## synchronized kolekcje java
Collections.synchronized  - List/Map/Set


## threadlocal


## kiedy baza nie uzywa indeksu mimo ze jest poprawnie zalozony
Kiedy jest mało danych


--jak dziala @transactional pod spodem


## interrupted exception w javie
Thrown when a thread is waiting, sleeping, or otherwise occupied, and the thread is interrupted, either before or during the activity


## plusy minusy mikroserwisow


## oauth 2


##  pull vs fetch w gicie
pull robi merge, fetch nie i aktualizuje tylko lokalne repo .git


## tdd 


## jak sie nazywa polaczenie commitow w jeden 
squosh czy jak to sie pisze


## roznica miedzy having a where
Having przy zagregowanych danych (np sumy) + używa się go z GRUOP BY


## typy generyczne


## interfejs funkcyjny
https://javastart.pl/baza-wiedzy/slownik/interfejs-funkcyjny


## modyfikatory dostepu i czym rozni sie default od protected
Default nie jest widoczny w subclassie, protected jest
private - default - protected - public


## czy overridujac klase mozemy zmienic jej modyfikator dostepu
Tak, ale nie może być bardziej restrykcyjny


## roznica miedzy jpa vs springdata - DAO vs repo w sumie
DAO (Data Access Object) jak Repository dostarczają interfejs umożliwiający komunikacje ze źródłem danych. Rozwiązania takie nazywane są Data Access Layer (DAL). Przy czym DAO jest rozwiązaniem bardziej elastycznym, natomiast Reposiotry nowszym i preferowanym do wykorzystania przez twórców wielu frameworków


## sposób pisania własnych zapytań w SpringBoocie - czyli Query i NativeQuery
Query - JPQL/HQL    ;   NativeQuery - SQL


## lockowanie - optimistic pesimistic