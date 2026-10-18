# Limity koncentracji węzłów - Egzekwowanie przeżywalności sieci
## Techniczny dodatek do Whitepapera tokenomiki EXIOM
### 07/26/2026

> **Nota o zakresie (zaktualizowana w październiku 2026).** Egzekwowaną jednostką jest *klaster bliskości* (grupa węzłów, które współdzielą infrastrukturę fizyczną lub routingową, wykrywana za pomocą bliskości routingu Lokinet, czasu dowodów uptime i ASN), a **nie kraj**. Kraj z kilkoma niezależnymi obiektami nie jest dotknięty. Dane dotyczące krajów poniżej są zgrubnym przybliżeniem geograficznym tego, gdzie obecnie leży koncentracja, a nie tym, co protokół ogranicza. Liczby węzłów w tym dodatku to zrzut z lipca 2026 (~672 węzły); zobacz whitepaper dla bieżących sum sieciowych (943 węzły na dzień 27 września 2026). Lokinet jest dostarczany w wydaniu nieegzekwującym przed HF23, a HF23 włącza egzekwowanie.

Ten dokument jest dodatkiem do Whitepapera tokenomiki EXIOM i zakłada, że został on przeczytany. Whitepaper obejmuje, czym są kontrole koncentracji i dlaczego istnieją. Ten dokument obejmuje mechaniczny szczegół tego, jak działa każda kontrola, dane walidacyjne z testnetu stojące za HF22, precyzyjną matematykę ekonomiczną stojącą za modyfikatorem zerowej nagrody, kwestię tożsamości operatora na łańcuchu prywatności oraz pozostałe ryzyka, których protokół nie rozwiązuje w pełni.

---

## Bieżące dane koncentracji

| Kraj | Aktywne węzły |
|---|---|
| France | 492 |
| Germany | 70 |
| United States | 55 |
| Canada | 18 |
| Poland | 13 |
| United Kingdom | 10 |
| Türkiye | 5 |
| Australia | 4 |
| Singapore | 2 |
| Lithuania | 2 |
| Serbia | 1 |

Francja posiada 492 z 672 węzłów w tym zrzucie (około 73% sieci), a ta koncentracja to niemal w całości pojedynczy obiekt Contabo w Grand Est, posiadający mniej więcej 426 węzłów (około 63% sieci). Suma krajowa nie jest tym, co protokół ogranicza; **klaster** Grand Est jest. Próg przeżywalności to 30% aktywnych węzłów na klaster bliskości (około 202 węzły przy 672 z tego zrzutu i około 283 przy 943 węzłach z bieżącego whitepapera), przeliczany w sposób ciągły w miarę jak sieć rośnie. Grand Est z mniej więcej 426 węzłami jest ponad dwukrotnie powyżej tego limitu.

---

## Co to oznacza dla operatorów węzłów

Ta sekcja odpowiada na pytanie wprost: jak HF23 wpływa na to, jak prowadzisz swoje węzły?

**HF23 nie ogranicza według kraju i nie wymaga jednego węzła na IP, jednego węzła na VPS ani jednego węzła na portfel.** Limit to 30% aktywnej sieci na *klaster bliskości* (węzły, które współdzielą infrastrukturę fizyczną lub routingową). Operator prowadzący 10, 50 lub nawet 100 węzłów na współdzielonej infrastrukturze jest zupełnie niedotknięty przez HF23, o ile jego klaster pozostaje poniżej tego progu. Możesz prowadzić wiele węzłów na jednej maszynie, jednym koncie VPS i jednym portfelu. Nic w HF23 tego nie zmienia.

**Modyfikator zerowej nagrody dotyczy tylko węzłów powyżej limitu na klaster (30% aktywnych węzłów).** Najstarsze zarejestrowane węzły w klastrze zarabiają pełne nagrody do tego progu. Tylko węzły rankingowane powyżej niego w nadmiernie skoncentrowanym klastrze zarabiają zero, i tylko do momentu migracji do mniej skoncentrowanego klastra.

**Deduplikacja kworum ogranicza wpływ na konsensus na rundę, a nie liczbę węzłów lub dochód.** Operator prowadzący 50 węzłów na jednym VPS zarabia nagrody blokowe na wszystkich 50 i zarządza swoją infrastrukturą dokładnie tak, jak robi to dzisiaj. Otrzymuje jedno miejsce w kworum na klaster na rundę zamiast potencjalnie wielu, co jest zamierzonym wynikiem.

**Właściwe podejście dla nowego operatora** to sprawdzenie eksploratora węzłów, zobaczenie, gdzie istniejące klastry są skoncentrowane, i wdrożenie w słabo zaludniony klaster. Dziesięć węzłów na jednym serwerze z własnym odrębnym routingiem działa doskonale w ramach HF23, ponieważ ten klaster jest daleki od progu 30%. Pełne nagrody, pełne uczestnictwo w kworum, bez problemów.

**Dynamika działa na twoją korzyść, jeśli wdrażasz w rzadkie regiony.** Jeśli region ostatecznie się zapełni, eksplorator węzłów to pokazuje, a operatorzy mają finansową zachętę, aby przenieść się, zanim limit ich dotknie. Operatorzy, którzy dotarli tam pierwsi, zachowują pełne nagrody na swoich najstarszych węzłach do progu. Nowe rejestracje w nadmiernie skoncentrowanym klastrze zarabiają natychmiast nic, więc ekonomia naturalnie popycha nowe wdrożenia w kierunku lżejszych regionów.

**Konkretnym problemem, który HF23 rozwiązuje** jest jeden obiekt we Francji (klaster Contabo w Grand Est) hostujący mniej więcej 426 węzłów, około 63% sieci w tym zrzucie. Jeśli ten obiekt przejdzie w tryb offline, sieć się zawiesza. Celem jest sprowadzenie tego klastra poniżej limitu 30%. Każdy inny operator prowadzący odpowiedzialną konfigurację wielowęzłową w nieskoncentrowanym klastrze jest dokładnie tym, czego sieć potrzebuje więcej.

---

## Dlaczego hard forki są rozdzielone

HF22 jest dostarczany po pomyślnych testach. Deduplikacja kworum kluczy portfela i ujednolicenie okresu unbondingu nie mają zależności od Lokinet. Oba zostały zwalidowane na testnecie, a wstrzymywanie ich w czasie, gdy ocena Lokinet jest w toku, jest nieuzasadnionym opóźnieniem. Wyrafinowany aktor, który przeczyta whitepaper przed dostarczeniem HF22, mógłby podjąć próbę dzielenia portfeli, aby uprzedzić kontrolę kworum, ale zrobienie tego jest wykrywalne przez korelację czasu dowodów uptime oraz analizę IP/ASN i tworzy udokumentowany zapis do działania zarządczego.

Lokinet jest dostarczany najpierw we własnym wydaniu nieegzekwującym (wraz ze zmianą magazynu lekkich węzłów SQLite), więc nowy transport nie jest czyniony krytycznym dla konsensusu w momencie jego wprowadzenia. Podczas tego wydania klastrowanie według bliskości działa i jest obserwowalne bez konsekwencji dla nagród, co jest momentem, w którym rzeczywista liczba klastrów jest mierzona, a próg HF23 i fallback dostrajane. HF23 następnie następuje i włącza egzekwowanie. Rozdzielenie wydań daje również czyste domeny awarii: jeśli coś pójdzie nie tak po aktywacji HF23, jest mniej zmiennych do wyizolowania. Dopóki egzekwowanie HF23 nie działa, Grand Est pozostaje narażony na pełne ryzyko przeżywalności poza deduplikacją kworum z HF22.

---

## Mechanika HF22

### Deduplikacja kworum kluczy portfela

Algorytm selekcji kworum uruchamia przebieg deduplikacji na każdym zbiorze kandydatów przed sfinalizowaniem. Gdy losowanie wybiera węzeł kandydacki, algorytm sprawdza jego adres portfela operatora względem wszystkich węzłów już wybranych do rundy. Jeśli znaleziono dopasowanie, kandydat jest zastępowany przez ponowne losowanie z pozostałej uprawnionej puli, wykluczając wszystkie adresy już reprezentowane.

Losowanie zastępcze nie cykluje z powrotem przez już odrzuconych kandydatów. Losuje z pozostałej niewybranej puli w tej samej kolejności ważonej prawdopodobieństwem, używanej do losowania początkowego. To zachowuje statystyczne właściwości selekcji kworum bez wprowadzania deterministycznego ukierunkowania w stronę jakiegokolwiek konkretnego zbioru pozostałych węzłów.

**Wyniki walidacji testnetu:**
- 20 cykli zawieszenia/odzyskiwania ukończonych (20/20)
- 100% wskaźnik odzyskiwania we wszystkich cyklach
- Zero ręcznej interwencji wymaganej w jakimkolwiek cyklu (najgorsza przerwa między blokami 83 sekundy)
- Linia bazowa mainnetu przed HF22: 1,000 bloków, 100% Pulse, zero bloków GOV_SIGNED
- Analiza timeoutów R0: brak wprowadzonych timeoutów R0 w warunkach produkcyjnych. Analiza gęstości obecnego mainnetu potwierdza, że każdy klaster IP o wysokiej gęstości jest pojedynczym operatorem, co oznacza, że deduplikacja kluczy portfela już zapewnia pełną ochronę przed obecnymi wdrożeniami wielorybów. Dwa największe wdrożenia na pojedynczym IP (odpowiednio 58 węzłów i 51 węzłów) to każde jeden operator i są ograniczone do jednego miejsca w kworum na rundę w ramach HF22.

**Co jedno miejsce w kworum oznacza w praktyce:** Rozmiar kworum i częstotliwość rotacji określają, jak często węzeł uczestniczy. Przy obecnym rozmiarze sieci limit jednego miejsca oznacza, że wpływ skoncentrowanego operatora w sesjach oracle, rundach Pulse i kworach obowiązków jest identyczny z wpływem operatora z jednym węzłem. Ich dochód z nagród blokowych pozostaje bez zmian.

**Luka dzielenia portfeli i jej tymczasowe wykrywanie:** Operator, który dzieli 426 węzłów na 10 portfeli, uzyskuje do 10 miejsc w kworum na rundę zamiast jednego. To jest znana luka, którą HF23 zamyka. W międzyczasie dzielenie portfeli jest wykrywalne przez dwa sygnały już dostępne bez zmian w demonie. Po pierwsze, czas dowodów uptime: węzły na tym samym fizycznym hoście lub hypervisorze składają dowody w odstępie milisekund od siebie, niezależnie od klucza portfela. Klaster dowodów przybywających w oknach poniżej 10ms od węzłów zarejestrowanych na różnych portfelach jest silnym sygnałem współdzielonej infrastruktury. Po drugie, korelacja IP i ASN: węzły na różnych portfelach współdzielące IP, podsieć lub ASN są logowane i oznaczane do przeglądu zarządczego. Operator, który dzieli portfele, ale trzyma wszystkie węzły w tym samym obiekcie Contabo, jest identyfikowalny przez oba sygnały i podlega działaniu zarządczemu w ramach polityki listy blokującej.

### Ujednolicenie okresu unbondingu

Okres unbondingu wymuszonej deregistracji zmienia się z 10,080 bloków (około 7 dni) na 20,160 bloków (około 14 dni), zrównany z okresem dobrowolnego wycofania. To jest zmiana stałej konsensusu.

Oryginalny 7-dniowy okres wymuszony był celowym wyborem podczas stabilizacji sieci, aby ograniczyć karę dla operatorów doświadczających zdarzeń infrastrukturalnych poza ich kontrolą. To uzasadnienie już nie obowiązuje. Sieć jest stabilna, system kredytu dekomisji zapewnia bufor dla krótkich przerw, a ujednolicony 14-dniowy okres usuwa asymetrię, która nie ma pozostałego uzasadnienia.

Monety XEQM są zablokowane on-chain podczas okresu unbondingu za pośrednictwem transakcji rejestracyjnej. Nie ma mechanizmu wcześniejszego zwolnienia blokady bez zmiany protokołu. W przypadku udokumentowanych awarii infrastruktury zarządzanie może zrekompensować utracone nagrody z portfela zarządczego jako transfer XEQM, ale blokada on-chain trwa przez pełny czas niezależnie.

---

## Mechanika HF23

### Klastrowanie według bliskości Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) routuje ruch przez sieć węzłów usługowych na warstwie 3, wspierając TCP, UDP i ICMP. Każdy węzeł usługowy uczestniczy jako przekaźnik. Wyłaniający się graf routingu odzwierciedla fizyczną topologię sieci: węzły w tym samym obiekcie routują przez ten sam przełącznik nadrzędny i ten sam szkielet centrum danych, produkując skorelowane wybory ścieżek i podmilisekundowe opóźnienie międzywęzłowe. Węzły w różnych obiektach routują przez różne ścieżki z mierzalnie wyższym opóźnieniem.

Algorytm klastrowania przyjmuje parami pomiary opóźnienia routingu Lokinet i nakładania się ścieżek we wszystkich aktywnych węzłach i grupuje je w klastry, używając tych pomiarów jako sygnału bliskości. Klaster nie jest stałym regionem geograficznym; jest dynamicznym grupowaniem węzłów, których zachowanie routingu wskazuje na współdzieloną infrastrukturę fizyczną. Dwa węzły w różnych obiektach Contabo w różnych krajach mogą routować przez wystarczająco dużo współdzielonej infrastruktury szkieletowej Contabo, aby pojawić się w tym samym klastrze, jeśli ich nakładanie się ścieżek jest wystarczająco wysokie. Dwa węzły w tym samym centrum danych, ale na różnych maszynach fizycznych z różnymi połączeniami nadrzędnymi, pojawią się w różnych klastrach, jeśli ich nakładanie się ścieżek jest niskie.

Sygnały uzupełniające używane obok bliskości Lokinet:

**Korelacja czasu dowodów uptime.** Sieć już otrzymuje dowody uptime od wszystkich aktywnych węzłów według regularnego harmonogramu. Rozkład czasowy przybyć dowodów od każdego węzła jest rejestrowany przez węzły odbierające. Węzły na tym samym fizycznym hoście lub hypervisorze VM składają dowody w charakterystycznym ciasnym oknie, zazwyczaj poniżej 10 milisekund. Klastrowanie tego rozkładu czasu przybycia zapewnia sygnał współzlokalizowania fizycznego, który nie wymaga zmian w demonie i działa, zanim Lokinet jest aktywny.

**Analiza ASN.** Adres IP każdego węzła mapuje się na Autonomous System Number za pomocą publicznych danych BGP. Węzły współdzielące ASN współdzielą infrastrukturę routingu na poziomie dostawcy i ekspozycję prawną na poziomie dostawcy. Dostawca, który otrzymuje nakaz na poziomie jurysdykcji dotyczący całej jego infrastruktury, wyłącza wszystkie swoje węzły ASN jednocześnie, niezależnie od tego, w ilu klastrach Lokinet się pojawiają. Koncentracja ASN jest śledzona jako sygnał uzupełniający i przyczynia się do przeglądu zarządczego operatorów blisko progu klastra.

### Limit rejestracji klastra

W czasie rejestracji protokół uruchamia ocenę bliskości względem wszystkich istniejących klastrów. Charakterystyki routingu Lokinet rejestrującego się węzła są mierzone względem centroidu każdego istniejącego klastra. Jeśli najbliższy klaster zawiera już 30% lub więcej aktywnych węzłów, rejestracja jest odrzucana z określonym kodem błędu wskazującym pojemność klastra i liczbę węzłów najbliższego klastra.

Odrzucenie jest deterministyczne: każdy węzeł, który routuje wystarczająco podobnie do nadmiernie skoncentrowanego klastra, aby zostać do niego przypisanym, jest odrzucany, niezależnie od klucza portfela operatora, historii rejestracji lub kwoty stake'u. Operator nie może odwołać się od odrzucenia przez zarządzanie. Jedyną drogą naprzód jest rejestracja na infrastrukturze, która routuje do innego klastra.

Próg jest oceniany względem liczby aktywnych węzłów w czasie rejestracji. W miarę jak sieć rośnie, próg 30% w wartościach bezwzględnych rośnie wraz z nią. Operator przy limicie dzisiaj może zarejestrować dodatkowe węzły w wcześniej ograniczonym klastrze w miarę jak sieć rośnie, a limit bezwzględny rośnie, bez migrowania jakichkolwiek istniejących węzłów.

### Modyfikator zerowej nagrody

Modyfikator zerowej nagrody jest stosowany w czasie obliczania nagrody blokowej. Obliczenie nagrody dla wybranego węzła obejmuje sprawdzenie uprawnień klastra. Jeśli klaster węzła zawiera więcej węzłów niż próg limitu, a ranking rejestracji węzła w tym klastrze jest powyżej progu (rankingowanym od najstarszego do najnowszego), obliczenie nagrody zwraca zero.

Ranking jest obliczany z wysokości bloku rejestracji węzła w ramach jego przypisania do klastra. Najstarszy zarejestrowany węzeł w klastrze otrzymuje rangę 1, najnowszy zarejestrowany otrzymuje rangę N. Węzły z rangą większą niż próg limitu zarabiają zero. Węzły z rangą na poziomie lub poniżej progu limitu zarabiają pełną standardową nagrodę. Ranking jest przeliczany za każdym razem, gdy zmienia się przypisanie klastra, co następuje, gdy węzły migrują poza klaster, gdy dołączają nowe węzły lub gdy granica klastra przesuwa się z powodu zmian topologii sieci.

**Matematyka ekonomiczna dla Grand Est:** Przy 426 węzłach z limitem 208 węzłów, 218 węzłów zarabia zero nagród blokowych. Przy cenie samodzielnego hostingu $0.53 na węzeł miesięcznie te 218 węzłów kosztuje $115.54 miesięcznie przy zerowym dochodzie. Przy cenie Pecunia $1.76 na węzeł miesięcznie koszt wynosi $383.68 miesięcznie. Operator ma dwie racjonalne reakcje: zmigrować nadmiarowe węzły do nieskoncentrowanych klastrów, przywracając ich nagrody natychmiast po zaakceptowaniu nowej rejestracji, lub zderegistrować nadmiarowe węzły i odzyskać zastakowany XEQM przez proces unbondingu. Każda z reakcji zmniejsza koncentrację. Nie ma racjonalnej podstawy do utrzymywania nadmiarowych węzłów przy zerowej nagrodzie.

**Mechanika okresu karencji:** Na bloku aktywacji HF23 protokół wykonuje zrzut wszystkich aktywnych klastrów i ich liczby węzłów. Każdy klaster przekraczający próg 30% jest oznaczany jako nadmiernie skoncentrowany. Przez 30 dni po bloku aktywacji modyfikator zerowej nagrody jest zawieszony dla wszystkich węzłów, włącznie z tymi powyżej progu limitu. Podczas okresu karencji właściciele węzłów mogą obserwować przypisania klastrów w eksploratorze węzłów, planować migracje i zacząć je wykonywać. Na bloku wygaśnięcia okresu karencji modyfikator się aktywuje. Węzły, które do tego bloku zmigrowały poza nadmiernie skoncentrowany klaster, zarabiają pełne nagrody od tego bloku naprzód. Węzły wciąż powyżej progu zarabiają zero od tego bloku naprzód do momentu migracji.

### Deduplikacja kworum klastra bliskości

Uaktualnienie deduplikacji kworum HF23 zastępuje sprawdzenie adresu portfela sprawdzeniem przynależności do klastra. Gdy losowanie wybiera węzeł kandydacki, algorytm sprawdza jego przypisanie do klastra względem wszystkich węzłów już wybranych do rundy. Jeśli dwa węzły współdzielą przypisanie do klastra, drugi jest zastępowany losowaniem z pozostałej puli, wykluczając wszystkie klastry już reprezentowane.

Praktyczny efekt dla operatora dzielącego portfele: 10 adresów portfeli na 426 węzłach, wszystkie w tym samym obiekcie Contabo, pojawia się w tym samym klastrze bliskości. Sprawdzenie klastra łapie je wszystkie jako jedną jednostkę. Jeden węzeł z tego klastra zajmuje miejsce. Pozostałe 425 węzłów z tego klastra nie, niezależnie od tego, pod iloma odrębnymi adresami portfeli są zarejestrowane.

### Wymóg minimalnej liczby klastrów i reguła fallbacku

Rozmiar kworum sieci EXIOM to 12 miejsc na rundę. Deduplikacja klastra bliskości wymaga zatem co najmniej 12 odrębnych klastrów bliskości w zbiorze aktywnych węzłów, aby zagwarantować formowanie kworum. Jeśli sieć produkuje mniej niż 12 odrębnych klastrów, algorytm nie może spełnić ograniczenia jednego miejsca na klaster i formowanie kworum zawodzi.

Obecny rozkład sieci, po zastosowaniu klastrowania według bliskości Lokinet, szacuje się, że produkuje od 12 do 18 odrębnych klastrów. To jest niepokojąco blisko minimum 12 miejsc. Współdzielona infrastruktura szkieletowa dostawcy między nominalnie oddzielnymi obiektami może spowodować, że dwie odrębne lokalizacje IP połączą się w jeden klaster bliskości w grafie routingu Lokinet. Każde takie połączenie, które zmniejsza liczbę klastrów poniżej 12, całkowicie łamie formowanie kworum.

Algorytm implementuje zatem obowiązkową regułę fallbacku:

1. Algorytm próbuje wypełnić wszystkie 12 miejsc jednym węzłem na odrębny klaster, przechodząc przez dostępne klastry w losowej kolejności.
2. Jeśli wszystkie odrębne klastry zostaną wyczerpane przed wypełnieniem 12 miejsc, algorytm wchodzi w przebieg fallbacku.
3. W przebiegu fallbacku dopuszcza drugi węzeł z każdego klastra, zaczynając od najmniejszych klastrów. Najmniej skoncentrowane klastry otrzymują drugie miejsce przed najbardziej skoncentrowanymi.
4. Algorytm kontynuuje przebiegi fallbacku, zwiększając maksymalną liczbę miejsc na klaster o jeden w każdym przebiegu, aż 12 miejsc zostanie wypełnionych.
5. Najbardziej skoncentrowany klaster, taki jak Grand Est w obecnych warunkach, otrzymuje dodatkowe miejsca dopiero po tym, jak wszystkim mniejszym klastrom przyznano ich alokację fallbacku.

Każda runda, która uruchamia fallback, jest logowana z liczbą klastrów, która to spowodowała. Zarządzanie monitoruje częstotliwość fallbacku jako bezpośredni wskaźnik ryzyka koncentracji. Sieć z 12 lub więcej odrębnymi klastrami nigdy nie uruchamia fallbacku. Sieć konsekwentnie uruchamiająca fallback sygnalizuje, że egzekwowanie koncentracji HF23 nie osiąga jeszcze odpowiedniej różnorodności fizycznej i że limit klastra lub egzekwowanie okresu karencji wymaga uwagi zarządczej.

Log fallbacku jest publikowany w eksploratorze węzłów obok przypisań klastrów, aby społeczność operatorów mogła obserwować ryzyko koncentracji w czasie rzeczywistym.

---

## Tożsamość operatora na łańcuchu prywatności

Protokół nie musi identyfikować, który ludzki operator jest właścicielem których węzłów, aby egzekwować limit klastra i modyfikator zerowej nagrody. Obie kontrole działają na poziomie klastra. To, co można i czego nie można ustalić, jest użytecznym kontekstem dla monitorowania zarządczego, ale nie jest wymagane do egzekwowania protokołu.

**Co jest deterministyczne z danych on-chain:** węzły zarejestrowane pod tym samym kluczem portfela operatora są definitywnie tym samym operatorem. To jest publiczna informacja w transakcji rejestracyjnej.

**Co można wnioskować z wysoką pewnością z danych Lokinet i czasowych:** liczba odrębnych fizycznych hostów stojących za klastrem węzłów, niezależnie od tego, ilu kluczy portfela używają. Pięć kluczy portfela, każdy prowadzący 85 węzłów, wszystkie na tych samych dwóch fizycznych serwerach, produkuje dwie odrębne sygnatury czasowe i dwa centroidy bliskości Lokinet, a nie pięć.

**Czego nie można ustalić na łańcuchu prywatności:** czy dwa różne klucze portfela z odrębną infrastrukturą należą do tego samego ludzkiego operatora. Źródło finansowania każdego klucza portfela jest prywatne z założenia. Wyrafinowany operator używający pięciu portfeli finansowanych z pięciu różnych źródeł przez warstwę transakcyjną łańcucha prywatności prezentuje pięć odrębnych tożsamości na poziomie protokołu.

Dla egzekwowania przeżywalności to nie ma znaczenia. Klaster zawiera 426 węzłów. Najstarsze 208 zarabia nagrody. Najnowsze 218 zarabia zero. Tożsamość operatora jest nieistotna dla tego obliczenia.

---

## Status implementacji

| Kontrola | Status |
|---|---|
| Deduplikacja kworum kluczy portfela operatora | HF22, aktywowana na bloku 219120 |
| Ujednolicenie okresu unbondingu, 7 do 14 dni | HF22, aktywowana |
| Odzyskiwanie po zawieszeniu Pulse (fallback oparty na podpisie, snode_revision 1) | Aktywowane na bloku 236920, 18 października 2026 |
| Aktywacja Lokinet jako transportu sieciowego | W trakcie opracowywania; dostarczane w wydaniu nieegzekwującym przed HF23 |
| Magazyn lekkich węzłów SQLite | W trakcie opracowywania; dostarczane z wydaniem Lokinet poprzedzającym HF23 |
| Algorytm klastrowania według bliskości | Faza projektowania, oczekuje na ocenę Lokinet |
| Limit rejestracji klastra, próg 30% | HF23, faza projektowania |
| Modyfikator zerowej nagrody dla nadmiarowych węzłów | HF23, faza projektowania |
| Mechanizm okresu karencji | HF23, faza projektowania |
| Deduplikacja kworum klastra bliskości z regułą fallbacku | HF23, faza projektowania |
| Monitorowanie minimalnej liczby klastrów i logowanie fallbacku | HF23, faza projektowania |
| Narzędzia korelacji czasu dowodów uptime | Brak wymaganych zmian w demonie, narzędzia w trakcie opracowywania |
| Uzupełnienie klastrowania ASN | Brak wymaganych zmian w demonie, narzędzia w trakcie opracowywania |

---

## Czego te kontrole nie rozwiązują

**Koncentracja prawna na poziomie dostawcy.** Dostawca otrzymujący nakaz prawny na poziomie jurysdykcji dotyczący całej jego globalnej infrastruktury wyłącza wszystkie swoje węzły jednocześnie, nawet jeśli te węzły pojawiają się w wielu klastrach bliskości Lokinet. Analiza ASN uwidacznia to ryzyko, ale protokół nie może egzekwować różnorodności dostawców bez wymogu ujawnienia przez operatora tożsamości jego dostawcy. Rozprzestrzenienie geograficzne naturalnie produkowane przez limit klastra w praktyce znacznie łagodzi to ryzyko, ponieważ operatorzy zmuszeni do rozproszenia się po klastrach w praktyce użyją wielu dostawców.

**Ustalenie tożsamości ludzkiego operatora w podziałach portfeli na łańcuchu prywatności.** Jak opisano powyżej, wyrafinowany operator używający wielu portfeli finansowanych przez łańcuch prywatności nie może być zidentyfikowany na poziomie protokołu. Limit klastra i modyfikator zerowej nagrody adresują ryzyko domeny awarii niezależnie od tożsamości. Deduplikacja kworum zamyka lukę wpływu na konsensus w HF23. Pozostałe ryzyko polega na tym, że wyrafinowany operator prowadzi wiele węzłów w wielu rzeczywiście odrębnych klastrach, akumulując dochód z nagród blokowych proporcjonalny do liczby swoich węzłów, przy jednoczesnym proporcjonalnym wkładzie w zdrowie sieci. To jest akceptowalny wynik: skoncentrowany wpływ na konsensus jest ograniczony; rozproszone uczestnictwo kapitałowe jest nagradzane.

Operatorzy z pytaniami dotyczącymi przypisania klastra, planowania migracji lub harmonogramu HF22/HF23 są zachęcani do publikowania na kanale Telegram Node Operators lub otwarcia zgłoszenia w tym repozytorium.

---

## Dostępne języki

Tłumaczenia społecznościowe tego dokumentu są utrzymywane w repozytorium whitepapera. W przypadku jakiegokolwiek konfliktu między tłumaczeniem a wersją angielską, wersja angielska jest rozstrzygająca.

| Language | Document |
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

*Ten dokument nie stanowi porady finansowej ani prawnej. XEQM jest monetą użytkową dla platformy EXIOM, a nie produktem inwestycyjnym. Klasyfikacja tokena, status papierów wartościowych i obowiązujące regulacje różnią się w zależności od jurysdykcji. Uczestnicy powinni skonsultować się ze swoim lokalnym otoczeniem prawnym i regulacyjnym przed nabyciem lub operowaniem z XEQM. XEQM Labs nie zachęca do zakupu XEQM na podstawie spekulacyjnego wzrostu ceny.*
