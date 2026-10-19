# Limity koncentracji węzłów - egzekwowanie przeżywalności sieci
## Techniczny dodatek do whitepapera tokenomiki EXIOM
### 07/26/2026

> **Uwaga o zakresie (zaktualizowano 19 października 2026).** Egzekwowaną jednostką jest *klaster bliskości* (grupa węzłów współdzielących fizyczną lub routingową infrastrukturę, wykrywana poprzez bliskość routingu Lokinet, czasy dowodów dostępności i ASN), **a nie kraj** ani kraj rejestracji dostawcy. Kraj lub dostawca z kilkoma faktycznie niezależnymi obiektami stanowi mniejsze ryzyko niż pojedynczy obiekt posiadający duży udział. Dane o koncentracji poniżej to migawka z 19 października 2026 (893 aktywnych węzłów) pogrupowana według dostawcy hostingu, najlepszego dostępnego przybliżenia przed Lokinet. Lokinet zostaje wydany w wersji nieegzekwującej przed HF23, a HF23 włącza egzekwowanie.

Ten dokument jest dodatkiem do whitepapera tokenomiki EXIOM i zakłada, że został on przeczytany. Whitepaper opisuje, czym są mechanizmy kontroli koncentracji i dlaczego istnieją. Ten dokument opisuje mechaniczne szczegóły działania każdego mechanizmu, dane walidacyjne z testnetu stojące za HF22, dokładną matematykę ekonomiczną modyfikatora zerowej nagrody, kwestię tożsamości operatora na łańcuchu prywatności oraz ryzyka szczątkowe, których protokół nie rozwiązuje w pełni.

---

## Aktualne dane o koncentracji

Zmierzone 19 października 2026 przy 893 aktywnych węzłach, pogrupowane według dostawcy hostingu (ASN), który jest sygnałem koncentracji dostępnym dzisiaj przed Lokinet. Dostawca jest znacznie lepszym przybliżeniem współdzielonej domeny awarii niż flaga kraju, ponieważ sieć i obiekty jednej firmy mają tendencję do awarii, lub do nakazanego wyłączenia, razem.

| Dostawca (ASN) | Aktywne węzły | Udział |
|---|---|---|
| NodeHub (AS214083) | 444 | 49.7% |
| Contabo (AS51167, plus AS40021 and Contabo Asia AS141995) | ~303 | ~34% |
| OVH (AS16276) | 62 | 6.9% |
| Oracle (AS31898) | 22 | 2.5% |
| WebNX (AS18450) | 12 | 1.3% |
| wszyscy pozostali dostawcy łącznie (12 kolejnych ASN) | ~50 | ~5.6% |

Sam NodeHub posiada 49.7% sieci, znacznie powyżej 30% limitu przeżywalności (267 węzłów przy 893 aktywnych), a pojedyncza podsieć /24 posiada 41.2%. Ten jeden dostawca to koncentracja, do której rozbicia zbudowany jest HF23.

Jak do tego doszło. Pecunia, usługa hostingowa, która oferowała prowadzenie węzłów XEQM dla operatorów, umieściła większość swoich węzłów na Contabo. Wydajność Pecunii była słaba i wielu operatorów od tego czasu przeniosło się do NodeHub. Zatem dominująca domena awarii przesunęła się z Contabo, które wciąż posiada około jednej trzeciej sieci (w dużej mierze obiekt Grand Est), do NodeHub, obecnie największego pojedynczego klastra w sieci.

Uwaga o danych krajowych. Kraj rejestracji dostawcy nie jest miejscem, gdzie znajdują się jego serwery. NodeHub jest zarejestrowany w US, a Contabo w DE, więc widok według kraju oznacza ich węzły jako US i DE niezależnie od fizycznego centrum danych (największy obiekt XEQM Contabo znajduje się w Grand Est we Francji). Protokół nie ogranicza ani kraju, ani kraju rejestracji dostawcy. Ogranicza klaster bliskości, zbiór węzłów, które faktycznie współdzielą fizyczną lub routingową infrastrukturę. ASN i podsieć są dzisiejszym przybliżeniem tego, a HF23 zastępuje je bliskością routingu Lokinet, która potrafi również oddzielić odrębne obiekty w ramach jednego dostawcy. Próg wynosi 30% aktywnych węzłów na klaster (267 przy obecnych 893), przeliczany na bieżąco w miarę wzrostu sieci.

---

## Co to oznacza dla operatorów węzłów

Ta sekcja odpowiada na pytanie wprost: jak HF23 wpływa na sposób, w jaki prowadzisz swoje węzły?

**HF23 nie ogranicza według kraju i nie wymaga jednego węzła na IP, jednego węzła na VPS ani jednego węzła na portfel.** Limit to 30% aktywnej sieci na *klaster bliskości* (węzły współdzielące fizyczną lub routingową infrastrukturę). Operator prowadzący 10, 50 lub nawet 100 węzłów na współdzielonej infrastrukturze pozostaje całkowicie nienaruszony przez HF23, dopóki jego klaster pozostaje poniżej tego progu. Możesz prowadzić wiele węzłów na jednej maszynie, jednym koncie VPS i jednym portfelu. Nic w HF23 tego nie zmienia.

**Modyfikator zerowej nagrody dotyczy wyłącznie węzłów powyżej limitu na klaster (30% aktywnych węzłów).** Najstarsze zarejestrowane węzły w klastrze zarabiają pełne nagrody aż do tego progu. Tylko węzły sklasyfikowane powyżej niego w nadmiernie skoncentrowanym klastrze zarabiają zero, i tylko do momentu przeniesienia ich do mniej skoncentrowanego klastra.

**Deduplikacja kworum ogranicza wpływ na konsensus na rundę, a nie liczbę węzłów ani dochód.** Operator prowadzący 50 węzłów na jednym VPS zarabia nagrody blokowe na wszystkich 50 i zarządza swoją infrastrukturą dokładnie tak, jak robi to dzisiaj. Otrzymuje jedno miejsce w kworum na klaster na rundę zamiast potencjalnie wielu, co jest zamierzonym wynikiem.

**Właściwe podejście dla nowego operatora** polega na sprawdzeniu eksploratora węzłów, zobaczeniu, gdzie skoncentrowane są istniejące klastry, i wdrożeniu się w słabo zaludniony klaster. Dziesięć węzłów na jednym serwerze z własnym odrębnym routingiem działa doskonale pod HF23, ponieważ ten klaster jest daleko od progu 30%. Pełne nagrody, pełny udział w kworum, żadnych problemów.

**Dynamika działa na twoją korzyść, jeśli wdrażasz się w rzadko zaludnionych regionach.** Jeśli region ostatecznie się zapełni, eksplorator węzłów to pokazuje, a operatorzy mają finansową zachętę do przeniesienia się, zanim limit ich dotknie. Operatorzy, którzy dotarli tam pierwsi, zachowują pełne nagrody na swoich najstarszych węzłach aż do progu. Nowe rejestracje w nadmiernie skoncentrowanym klastrze natychmiast zarabiają zero, więc ekonomia w naturalny sposób popycha nowe wdrożenia ku lżejszym regionom.

**Konkretnym problemem, który rozwiązuje HF23** jest pojedynczy dostawca, NodeHub, obecnie hostujący około połowy sieci (444 węzłów, 49.7%), z Contabo na drugim miejscu przy około jednej trzeciej. Jeśli infrastruktura NodeHub przejdzie w tryb offline lub zostanie nakazana do wyłączenia, sieć się zatrzymuje. Celem jest sprowadzenie dowolnego pojedynczego klastra poniżej limitu 30%. Każdy operator prowadzący odpowiedzialną konfigurację wielowęzłową u innego, nieskoncentrowanego dostawcy lub w innym obiekcie jest dokładnie tym, czego sieć potrzebuje więcej.

---

## Dlaczego hard forki są rozdzielone

HF22 zostaje wydany po pomyślnych testach. Deduplikacja kworum na podstawie klucza portfela i ujednolicenie okresu rozwiązywania (unbonding) nie mają zależności od Lokinet. Oba zostały zwalidowane na testnecie, a wstrzymywanie ich w oczekiwaniu na ocenę Lokinet to nieuzasadnione opóźnienie. Wyrafinowany aktor, który przeczyta whitepaper przed wydaniem HF22, mógłby podjąć próbę rozdzielenia portfeli, aby uprzedzić mechanizm kworum, ale czynienie tego jest wykrywalne poprzez korelację czasów dowodów dostępności oraz analizę IP/ASN i tworzy udokumentowany zapis do działań zarządczych.

Lokinet zostaje wydany najpierw we własnej wersji nieegzekwującej (wraz ze zmianą przechowywania lekkiego węzła SQLite), więc nowy transport nie staje się krytyczny dla konsensusu w momencie jego wprowadzenia. Podczas tego wydania klasterowanie bliskości działa na żywo i jest obserwowalne bez konsekwencji dla nagród, co jest momentem, w którym mierzona jest rzeczywista liczba klastrów oraz strojony jest próg HF23 i mechanizm awaryjny (fallback). HF23 następuje potem i włącza egzekwowanie. Rozdzielenie wydań daje również czyste domeny awarii: jeśli coś pójdzie nie tak po aktywacji HF23, jest mniej zmiennych do izolowania. Dopóki egzekwowanie HF23 nie jest aktywne, Grand Est pozostaje narażony na pełne ryzyko przeżywalności poza deduplikacją kworum z HF22.

---

## Mechanika HF22

### Deduplikacja kworum na podstawie klucza portfela

Algorytm selekcji kworum uruchamia przebieg deduplikacji na każdym zbiorze kandydatów przed sfinalizowaniem. Gdy losowanie wybiera węzeł kandydujący, algorytm sprawdza adres portfela jego operatora względem wszystkich węzłów już wybranych do rundy. Jeśli zostanie znalezione dopasowanie, kandydat jest zastępowany przez ponowne losowanie z pozostałej kwalifikującej się puli, z wyłączeniem wszystkich adresów już reprezentowanych.

Zastępcze losowanie nie cofa się przez już odrzuconych kandydatów. Losuje z pozostałej niewybranej puli w tej samej kolejności ważonej prawdopodobieństwem, jaka została użyta w pierwotnym losowaniu. Zachowuje to właściwości statystyczne selekcji kworum bez wprowadzania deterministycznego obciążenia w kierunku jakiegokolwiek konkretnego zbioru pozostałych węzłów.

**Wyniki walidacji na testnecie:**
- 20 ukończonych cykli zatrzymania/odzyskania (20/20)
- 100% wskaźnik odzyskania we wszystkich cyklach
- Zero wymaganej ręcznej interwencji w jakimkolwiek cyklu (najgorsza przerwa między blokami 83 sekundy)
- Poziom bazowy mainnetu przed HF22: 1,000 bloków, 100% Pulse, zero bloków GOV_SIGNED
- Analiza przekroczeń czasu R0: brak wprowadzonych przekroczeń czasu R0 w warunkach produkcyjnych. Analiza gęstości obecnego mainnetu potwierdza, że każdy klaster IP o wysokiej gęstości to pojedynczy operator, co oznacza, że deduplikacja na podstawie klucza portfela już zapewnia pełną ochronę przed obecnymi wdrożeniami wielorybów. Dwa największe wdrożenia na pojedynczym IP (odpowiednio 58 węzłów i 51 węzłów) to każde jeden operator i są ograniczone do jednego miejsca w kworum na rundę pod HF22.

**Co jedno miejsce w kworum oznacza w praktyce:** Rozmiar kworum i częstotliwość rotacji determinują, jak często węzeł uczestniczy. Przy obecnym rozmiarze sieci limit jednego miejsca oznacza, że wpływ skoncentrowanego operatora w sesjach oracle, rundach Pulse i kworum zobowiązań jest identyczny z wpływem operatora posiadającego jeden węzeł. Ich dochód z nagród blokowych pozostaje niezmieniony.

**Luka rozdzielania portfeli i jej tymczasowe wykrywanie:** Operator, który rozdziela 426 węzłów na 10 portfeli, uzyskuje do 10 miejsc w kworum na rundę zamiast jednego. To jest znana luka, którą zamyka HF23. W międzyczasie rozdzielanie portfeli jest wykrywalne poprzez dwa sygnały już dostępne bez zmian w daemonie. Po pierwsze, czasy dowodów dostępności: węzły na tym samym fizycznym hoście lub hypervisorze przesyłają dowody w odstępie milisekund od siebie, niezależnie od klucza portfela. Klaster dowodów przybywających w oknach poniżej 10ms od węzłów zarejestrowanych na różne portfele jest silnym sygnałem współdzielonej infrastruktury. Po drugie, korelacja IP i ASN: węzły na różnych portfelach współdzielące IP, podsieć lub ASN są logowane i oznaczane do przeglądu zarządczego. Operator, który rozdziela portfele, ale trzyma wszystkie węzły w tym samym obiekcie Contabo, jest identyfikowalny poprzez oba sygnały i podlega działaniom zarządczym w ramach polityki listy blokad.

### Ujednolicenie okresu rozwiązywania (unbonding)

Okres rozwiązywania przy wymuszonej deregistracji zmienia się z 10,080 bloków (około 7 dni) na 20,160 bloków (około 14 dni), odpowiadając okresowi dobrowolnego wycofania. Jest to zmiana stałej konsensusu.

Pierwotny 7-dniowy okres wymuszony był świadomym wyborem podczas stabilizacji sieci, aby ograniczyć karę dla operatorów doświadczających zdarzeń infrastrukturalnych poza ich kontrolą. To uzasadnienie już nie obowiązuje. Sieć jest stabilna, system kredytu za wycofanie z eksploatacji (decommission credit) zapewnia bufor dla krótkich przerw, a ujednolicony 14-dniowy okres usuwa asymetrię, która nie ma już żadnego uzasadnienia.

Monety XEQM są zablokowane on-chain podczas okresu rozwiązywania poprzez transakcję rejestracyjną. Nie ma mechanizmu wcześniejszego zwolnienia blokady bez zmiany protokołu. W przypadku udokumentowanych awarii infrastruktury zarząd może zrekompensować utracone nagrody z portfela zarządczego jako transfer XEQM, ale blokada on-chain trwa przez swój pełny czas niezależnie.

---

## Mechanika HF23

### Klasterowanie bliskości Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) kieruje ruch przez sieć węzłów usługowych na warstwie 3, obsługując TCP, UDP i ICMP. Każdy węzeł usługowy uczestniczy jako przekaźnik. Powstający graf routingu odzwierciedla fizyczną topologię sieci: węzły w tym samym obiekcie kierują ruch przez ten sam przełącznik nadrzędny i tę samą sieć szkieletową centrum danych, produkując skorelowane wybory ścieżek i sub-milisekundowe opóźnienie między węzłami. Węzły w różnych obiektach kierują ruch przez różne ścieżki z mierzalnie wyższym opóźnieniem.

Algorytm klasterowania pobiera parami pomiary opóźnienia routingu Lokinet i nakładania się ścieżek we wszystkich aktywnych węzłach i grupuje je w klastry, używając tych pomiarów jako sygnału bliskości. Klaster nie jest stałym regionem geograficznym; jest dynamicznym grupowaniem węzłów, których zachowanie routingu wskazuje na współdzieloną fizyczną infrastrukturę. Dwa węzły w różnych obiektach Contabo w różnych krajach mogą kierować ruch przez wystarczająco dużo współdzielonej infrastruktury szkieletowej Contabo, aby pojawić się w tym samym klastrze, jeśli ich nakładanie się ścieżek jest wystarczająco wysokie. Dwa węzły w tym samym centrum danych, ale na różnych fizycznych maszynach z różnymi połączeniami nadrzędnymi, pojawią się w różnych klastrach, jeśli ich nakładanie się ścieżek jest niskie.

Sygnały uzupełniające używane wraz z bliskością Lokinet:

**Korelacja czasów dowodów dostępności.** Sieć już otrzymuje dowody dostępności od wszystkich aktywnych węzłów według regularnego harmonogramu. Rozkład znaczników czasu przybycia dowodów od każdego węzła jest rejestrowany przez węzły odbierające. Węzły na tym samym fizycznym hoście lub hypervisorze VM przesyłają dowody w charakterystycznym wąskim oknie, zazwyczaj poniżej 10 milisekund. Klasterowanie tego rozkładu czasów przybycia zapewnia sygnał fizycznej kolokacji, który nie wymaga zmian w daemonie i działa, zanim Lokinet jest aktywny.

**Analiza ASN.** Adres IP każdego węzła mapuje się na numer systemu autonomicznego (Autonomous System Number) poprzez publiczne dane BGP. Węzły współdzielące ASN współdzielą infrastrukturę routingu na poziomie dostawcy oraz ekspozycję prawną na poziomie dostawcy. Dostawca, który otrzymuje nakaz na poziomie jurysdykcji dotykający całej jego infrastruktury, wyłącza wszystkie swoje węzły ASN jednocześnie, niezależnie od tego, w ilu klastrach Lokinet się pojawiają. Koncentracja ASN jest śledzona jako sygnał uzupełniający i przyczynia się do przeglądu zarządczego operatorów bliskich progu klastra.

### Limit rejestracji klastra

W czasie rejestracji protokół uruchamia ocenę bliskości względem wszystkich istniejących klastrów. Charakterystyki routingu Lokinet rejestrującego się węzła są mierzone względem centroidu każdego istniejącego klastra. Jeśli najbliższy klaster zawiera już 30% lub więcej aktywnych węzłów, rejestracja jest odrzucana z konkretnym kodem błędu wskazującym pojemność klastra i liczbę węzłów najbliższego klastra.

Odrzucenie jest deterministyczne: każdy węzeł, który kieruje ruch wystarczająco podobnie do nadmiernie skoncentrowanego klastra, aby zostać do niego przypisanym, zostaje odrzucony, niezależnie od klucza portfela operatora, historii rejestracji czy wysokości stawki. Operator nie może odwołać się od odrzucenia przez zarząd. Jedyną drogą naprzód jest rejestracja na infrastrukturze, która kieruje ruch do innego klastra.

Próg jest oceniany względem liczby aktywnych węzłów w momencie rejestracji. W miarę wzrostu sieci próg 30% w kategoriach bezwzględnych rośnie wraz z nią. Operator przy limicie dzisiaj może zarejestrować dodatkowe węzły w wcześniej ograniczonym klastrze w miarę wzrostu sieci i wzrostu bezwzględnego limitu, bez przenoszenia jakichkolwiek istniejących węzłów.

### Modyfikator zerowej nagrody

Modyfikator zerowej nagrody jest stosowany w czasie obliczania nagrody blokowej. Obliczenie nagrody dla wybranego węzła obejmuje sprawdzenie kwalifikowalności klastra. Jeśli klaster węzła zawiera więcej węzłów niż próg limitu, a ranga rejestracji węzła w tym klastrze jest powyżej progu (uszeregowana od najstarszego do najnowszego), obliczenie nagrody zwraca zero.

Ranking jest obliczany na podstawie wysokości bloku rejestracji węzła w ramach przypisania do klastra. Najstarszy zarejestrowany węzeł w klastrze otrzymuje rangę 1, najnowszy otrzymuje rangę N. Węzły z rangą większą niż próg limitu zarabiają zero. Węzły z rangą na poziomie progu limitu lub poniżej zarabiają pełną standardową nagrodę. Ranking jest przeliczany za każdym razem, gdy zmienia się przypisanie klastra, co następuje, gdy węzły migrują poza klaster, gdy dołączają nowe węzły lub gdy granica klastra przesuwa się z powodu zmian topologii sieci.

**Matematyka ekonomiczna dla Grand Est:** Przy 426 węzłach z limitem 208 węzłów, 218 węzłów zarabia zero nagród blokowych. Przy cenie własnego hostingu 0,53 USD za węzeł miesięcznie te 218 węzłów kosztuje 115,54 USD miesięcznie przy zerowym dochodzie. Przy cenie Pecunii 1,76 USD za węzeł miesięcznie koszt wynosi 383,68 USD miesięcznie. Operator ma dwie racjonalne reakcje: przenieść nadmiarowe węzły do nieskoncentrowanych klastrów, przywracając ich nagrody natychmiast po zaakceptowaniu nowej rejestracji, albo wyrejestrować nadmiarowe węzły i odzyskać zastawione XEQM poprzez proces rozwiązywania. Każda z reakcji zmniejsza koncentrację. Nie ma racjonalnej podstawy do utrzymywania nadmiarowych węzłów przy zerowej nagrodzie.

**Mechanika okresu karencji:** W bloku aktywacji HF23 protokół wykonuje migawkę wszystkich aktywnych klastrów i ich liczby węzłów. Każdy klaster przekraczający próg 30% jest oznaczany jako nadmiernie skoncentrowany. Przez 30 dni po bloku aktywacji modyfikator zerowej nagrody jest zawieszony dla wszystkich węzłów, w tym tych powyżej progu limitu. Podczas okresu karencji właściciele węzłów mogą obserwować przypisania klastrów w eksploratorze węzłów, planować migracje i rozpocząć ich realizację. W bloku wygaśnięcia okresu karencji modyfikator się aktywuje. Węzły, które do tego bloku przeniosły się poza nadmiernie skoncentrowany klaster, zarabiają pełne nagrody od tego bloku wprzód. Węzły wciąż powyżej progu zarabiają zero od tego bloku wprzód, dopóki się nie przeniosą.

### Deduplikacja kworum na podstawie klastra bliskości

Aktualizacja deduplikacji kworum w HF23 zastępuje sprawdzenie adresu portfela sprawdzeniem członkostwa w klastrze. Gdy losowanie wybiera węzeł kandydujący, algorytm sprawdza jego przypisanie do klastra względem wszystkich węzłów już wybranych do rundy. Jeśli dwa węzły współdzielą przypisanie do klastra, drugi jest zastępowany losowaniem z pozostałej puli, z wyłączeniem wszystkich klastrów już reprezentowanych.

Praktyczny efekt dla operatora rozdzielającego portfele: 10 adresów portfeli na 426 węzłach, wszystkie w tym samym obiekcie Contabo, pojawia się w tym samym klastrze bliskości. Sprawdzenie klastra łapie je wszystkie jako jedną jednostkę. Jeden węzeł z tego klastra zajmuje miejsce. Pozostałe 425 węzłów z tego klastra nie, niezależnie od tego, pod iloma odrębnymi adresami portfeli są zarejestrowane.

### Wymóg minimalnej liczby klastrów i reguła awaryjna (fallback)

Rozmiar kworum sieci EXIOM to 12 miejsc na rundę. Deduplikacja klastra bliskości wymaga zatem co najmniej 12 odrębnych klastrów bliskości w zbiorze aktywnych węzłów, aby zagwarantować uformowanie kworum. Jeśli sieć produkuje mniej niż 12 odrębnych klastrów, algorytm nie może spełnić ograniczenia jednego miejsca na klaster i uformowanie kworum się nie udaje.

Szacuje się, że obecny rozkład sieci, po zastosowaniu klasterowania bliskości Lokinet, produkuje między 12 a 18 odrębnych klastrów. Jest to niekomfortowo blisko minimum 12 miejsc. Współdzielona infrastruktura szkieletowa dostawcy między nominalnie oddzielnymi obiektami może spowodować połączenie dwóch odrębnych lokalizacji IP w jeden klaster bliskości w grafie routingu Lokinet. Każde takie połączenie, które redukuje liczbę klastrów poniżej 12, całkowicie łamie uformowanie kworum.

Algorytm wdraża zatem obowiązkową regułę awaryjną:

1. Algorytm próbuje wypełnić wszystkie 12 miejsc jednym węzłem na odrębny klaster, przechodząc przez dostępne klastry w losowej kolejności.
2. Jeśli wszystkie odrębne klastry zostaną wyczerpane przed wypełnieniem 12 miejsc, algorytm wchodzi w przebieg awaryjny.
3. W przebiegu awaryjnym zezwala na drugi węzeł z każdego klastra, zaczynając najpierw od najmniejszych klastrów. Najmniej skoncentrowane klastry otrzymują drugie miejsce przed najbardziej skoncentrowanymi.
4. Algorytm kontynuuje przebiegi awaryjne, zwiększając maksymalną liczbę miejsc na klaster o jedno w każdym przebiegu, aż 12 miejsc zostanie wypełnionych.
5. Najbardziej skoncentrowany klaster, taki jak Grand Est w obecnych warunkach, otrzymuje dodatkowe miejsca dopiero po tym, jak wszystkie mniejsze klastry otrzymają swoją alokację awaryjną.

Każda runda, która wyzwala przebieg awaryjny, jest logowana z liczbą klastrów, która ją spowodowała. Zarząd monitoruje częstotliwość przebiegów awaryjnych jako bezpośredni wskaźnik ryzyka koncentracji. Sieć z 12 lub więcej odrębnymi klastrami nigdy nie wyzwala przebiegu awaryjnego. Sieć konsekwentnie wyzwalająca przebieg awaryjny sygnalizuje, że egzekwowanie koncentracji HF23 nie osiąga jeszcze odpowiedniej fizycznej różnorodności i że limit klastra lub egzekwowanie okresu karencji wymaga uwagi zarządu.

Log przebiegów awaryjnych jest publikowany w eksploratorze węzłów obok przypisań klastrów, aby społeczność operatorów mogła obserwować ryzyko koncentracji w czasie rzeczywistym.

---

## Tożsamość operatora na łańcuchu prywatności

Protokół nie musi identyfikować, który ludzki operator posiada które węzły, aby egzekwować limit klastra i modyfikator zerowej nagrody. Oba mechanizmy działają na poziomie klastra. To, co można i czego nie można ustalić, jest użytecznym kontekstem dla monitorowania zarządczego, ale nie jest wymagane do egzekwowania protokołu.

**Co jest deterministyczne z danych on-chain:** węzły zarejestrowane pod tym samym kluczem portfela operatora są definitywnie tym samym operatorem. Jest to informacja publiczna w transakcji rejestracyjnej.

**Co jest wywnioskowalne z wysoką pewnością z danych Lokinet i czasowych:** liczba odrębnych fizycznych hostów leżących u podstaw klastra węzłów, niezależnie od tego, ilu kluczy portfeli używają. Pięć kluczy portfeli, każdy prowadzący 85 węzłów, wszystkie na tych samych dwóch fizycznych serwerach, produkuje dwie odrębne sygnatury czasowe i dwa centroidy bliskości Lokinet, a nie pięć.

**Czego nie można ustalić na łańcuchu prywatności:** czy dwa różne klucze portfeli z odrębną infrastrukturą należą do tego samego ludzkiego operatora. Źródło finansowania każdego klucza portfela jest prywatne z założenia. Wyrafinowany operator używający pięciu portfeli finansowanych z pięciu różnych źródeł poprzez warstwę transakcyjną łańcucha prywatności przedstawia pięć odrębnych tożsamości na poziomie protokołu.

Dla egzekwowania przeżywalności to nie ma znaczenia. Klaster zawiera 426 węzłów. Najstarsze 208 zarabia nagrody. Najnowsze 218 zarabia zero. Tożsamość operatora jest nieistotna dla tego obliczenia.

---

## Status implementacji

| Mechanizm | Status |
|---|---|
| Deduplikacja kworum na podstawie klucza portfela operatora | HF22, aktywowano w bloku 219120 |
| Ujednolicenie okresu rozwiązywania, 7 do 14 dni | HF22, aktywowano |
| Odzyskiwanie po zatrzymaniu Pulse (fallback podpisów, snode_revision 1) | Aktywowano w bloku 236920, 18 października 2026 |
| Aktywacja Lokinet jako transportu sieci | W rozwoju; wydanie w wersji nieegzekwującej przed HF23 |
| Przechowywanie lekkiego węzła SQLite | W rozwoju; wydanie wraz z wersją Lokinet przed HF23 |
| Algorytm klasterowania bliskości | Faza projektowa, w oczekiwaniu na ocenę Lokinet |
| Limit rejestracji klastra, próg 30% | HF23, faza projektowa |
| Modyfikator zerowej nagrody dla nadmiarowych węzłów | HF23, faza projektowa |
| Mechanizm okresu karencji | HF23, faza projektowa |
| Deduplikacja kworum klastra bliskości z regułą awaryjną | HF23, faza projektowa |
| Monitorowanie minimalnej liczby klastrów i logowanie przebiegów awaryjnych | HF23, faza projektowa |
| Narzędzia do korelacji czasów dowodów dostępności | Brak wymaganych zmian w daemonie, narzędzia w rozwoju |
| Uzupełnienie klasterowania ASN | Brak wymaganych zmian w daemonie, narzędzia w rozwoju |

---

## Czego te mechanizmy nie rozwiązują

**Koncentracja prawna na poziomie dostawcy.** Dostawca otrzymujący nakaz prawny na poziomie jurysdykcji dotykający całej jego globalnej infrastruktury wyłącza wszystkie swoje węzły jednocześnie, nawet jeśli te węzły pojawiają się w wielu klastrach bliskości Lokinet. Analiza ASN uwidacznia to ryzyko, ale protokół nie może egzekwować różnorodności dostawców bez wymagania ujawnienia przez operatora tożsamości jego dostawcy. Rozproszenie geograficzne naturalnie produkowane przez limit klastra zasadniczo łagodzi to ryzyko w praktyce, ponieważ operatorzy zmuszeni do rozproszenia się między klastry w praktyce użyją wielu dostawców.

**Ustalenie tożsamości ludzkiego operatora w ramach rozdziału portfeli na łańcuchu prywatności.** Jak opisano powyżej, wyrafinowany operator używający wielu portfeli finansowanych poprzez łańcuch prywatności nie może zostać zidentyfikowany na poziomie protokołu. Limit klastra i modyfikator zerowej nagrody adresują ryzyko domeny awarii niezależnie od tożsamości. Deduplikacja kworum zamyka lukę wpływu na konsensus w HF23. Ryzyko szczątkowe polega na tym, że wyrafinowany operator prowadzi wiele węzłów w wielu faktycznie odrębnych klastrach, akumulując dochód z nagród blokowych proporcjonalny do liczby swoich węzłów, jednocześnie przyczyniając się proporcjonalnie do zdrowia sieci. Jest to akceptowalny wynik: skoncentrowany wpływ na konsensus jest ograniczony; rozproszony udział kapitałowy jest nagradzany.

Operatorzy z pytaniami o przypisanie do klastra, planowanie migracji lub harmonogram HF22/HF23 są zachęcani do publikowania na kanale Node Operators Telegram lub otwarcia zgłoszenia (issue) w tym repozytorium.

---

## Dostępne języki

Tłumaczenia społecznościowe tego dokumentu są utrzymywane w repozytorium whitepapera. W przypadku jakiegokolwiek konfliktu między tłumaczeniem a wersją angielską, wersja angielska jest rozstrzygająca.

| Język | Dokument |
|---|---|
| Español | [translations/es/concentration-limits-proposal.md](./translations/es/concentration-limits-proposal.md) |
| Français | [translations/fr/concentration-limits-proposal.md](./translations/fr/concentration-limits-proposal.md) |
| Deutsch | [translations/de/concentration-limits-proposal.md](./translations/de/concentration-limits-proposal.md) |
| 中文 | [translations/zh/concentration-limits-proposal.md](./translations/zh/concentration-limits-proposal.md) |
| Português | [translations/pt/concentration-limits-proposal.md](./translations/pt/concentration-limits-proposal.md) |
| Türkçe | [translations/tr/concentration-limits-proposal.md](./translations/tr/concentration-limits-proposal.md) |
| Polski | [translations/pl/concentration-limits-proposal.md](./translations/pl/concentration-limits-proposal.md) |
| Bahasa Indonesia | [translations/id/concentration-limits-proposal.md](./translations/id/concentration-limits-proposal.md) |

---

*Ten dokument nie stanowi porady finansowej ani prawnej. XEQM jest monetą użytkową dla platformy EXIOM, a nie produktem inwestycyjnym. Klasyfikacja tokenów, status papierów wartościowych i obowiązujące przepisy różnią się w zależności od jurysdykcji. Uczestnicy powinni skonsultować się ze swoimi lokalnymi ramami prawnymi i regulacyjnymi przed nabyciem lub prowadzeniem działalności z użyciem XEQM. XEQM Labs nie zachęca do zakupu XEQM na podstawie spekulacyjnego wzrostu ceny.*
