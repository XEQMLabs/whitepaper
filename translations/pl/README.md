# XEQM Labs - Platforma EXIOM
## Whitepaper dotyczący tokenomiki
### Wersja robocza v12 | 09/27/2026

---

## Co działa dzisiaj a co jest planowane

| Komponent | Status |
|---|---|
| EXIOM mainnet | Działa, operacyjny od 6 maja 2026 |
| Sieć węzłów usługowych | Działa — 943 aktywne węzły usługowe na dzień 27 września 2026 |
| Lokinet (LLARP) | Dostarczany w wydaniu nieegzekwującym przed HF23 (transport działa, klastrowanie według bliskości obserwowalne); HF23 włącza egzekwowanie. Implementacja rozpoczyna się w Q4 2026 |
| Magazyn lekkich węzłów SQLite | W trakcie opracowywania; dostarczany z wydaniem Lokinet poprzedzającym HF23, dla niższego zużycia pamięci i dysku węzła, z opcjonalnymi lekkimi węzłami z ostatniego okna |
| Swap monet XEQ na XEQM | Zrealizowany i zamknięty, 35-dniowy przebieg produkcyjny, publiczny audytowalny rejestr |
| Portfel GUI | Działa, github.com/XEQMLabs/XEQMLabs-GUI |
| Eksplorator węzłów | Działa, aktywne monitorowanie węzłów usługowych |
| EXIOM Oracle | Działa na mainnecie (Robinhood Chain, chainId 4663); 12-osobowy komitet operatorów na dzień 28 września 2026 |
| EXIOM developer API | Działa w wersji beta — klucze samoobsługowe, podpisane oświadczenia zgodności i silnik weryfikacji, OpenAPI pod /docs; darmowe do budowania z przedpłaconym użyciem rozliczanym za wywołanie wdrażanym stopniowo (27 września 2026) |
| EXIOM Privacy Oracle (TLSNotary / ZK) | Fundamenty działają (silnik weryfikacji, sesje oracle); pełny oracle prywatnych danych webowych w Fazie 3 |
| Platforma handlowa EXIOM RFQ | W trakcie opracowywania, Faza 2/3, para XEQM/BTC jako pierwsza |
| HF22, deduplikacja kworum kluczy portfela, ujednolicenie unbondingu, odzyskiwanie po zawieszeniu Pulse | Aktywowane na bloku mainnetu 219120. Rewizja odzyskiwania po zawieszeniu Pulse (snode_revision 1, fallback oparty na podpisie) aktywowana na bloku 236920 w dniu 18 października 2026 |
| HF23, limit klastra bliskości i modyfikator nagród (egzekwowanie) | W projektowaniu; włącza limity koncentracji po tym, jak wydanie nieegzekwujące Lokinet + lekkie węzły zostanie wygrzane; cel Q4 2026 |
| Formalne zarządzanie on-chain | Planowane, Faza 6 |

---

## 1. Czym jest XEQM Labs

XEQM Labs to firma zajmująca się technologią prywatności. Jej flagowy produkt, EXIOM, to zachowująca prywatność sieć Proof-of-Stake Layer 1 oraz komercyjna platforma dla deweloperów, obsługiwana przez globalny zbiór węzłów usługowych. XEQM jest monetą dostępu i użytkowania dla platformy. Deweloperzy budują za darmo i płacą za użycie produkcyjne w XEQM, zużywane w miarę wywoływania API. Operatorzy węzłów usługowych zarabiają XEQM za zabezpieczanie sieci, a ci sami operatorzy mogą uzyskać dodatkowy przychód, uruchamiając sidecar oracle, który obsługuje produkty oracle platformy.

Projekt kontynuuje historię społeczności i działalności operacyjnej sięgającą ponad siedem lat wstecz. EXIOM mainnet został zbudowany, aby dać tej społeczności sieć z weryfikowalną podażą, przewidywalnym harmonogramem emisji, czystym konsensusem Proof-of-Stake bez komponentu Proof-of-Work oraz mechaniką węzłów usługowych, która szanuje czas i kapitał operatora.

XEQM jest natywną monetą Layer 1, nietokenizowaną na żadnym innym łańcuchu, nie jest to ERC-20 ani aktywo opakowane, ani nie jest mostkowana. Posiadacze wchodzą w interakcję bezpośrednio z EXIOM mainnet.

### Rodzina produktów EXIOM

**EXIOM Service Node Network.** Działa na mainnecie. Globalny zbiór węzłów usługowych zabezpiecza łańcuch, zarabia nagrody blokowe i tworzy warstwę infrastruktury, na której działają wszystkie pozostałe produkty EXIOM. 943 aktywne węzły usługowe na dzień 27 września 2026.

**EXIOM Coin Swap.** Produkt komercyjny umożliwiający projektom migrację ich społeczności posiadaczy ze starszego łańcucha na nowy łańcuch z pełną kryptograficzną audytowalnością. Pilotażem była migracja posiadaczy XEQ do XEQM na EXIOM mainnet, trwająca 35 dni, przy czym każde zgłoszenie było przetwarzane przez kryptograficznie zweryfikowany rejestr opatrzony publicznym odciskiem SHA256. Produkt jest dostępny dla innych projektów wymagających weryfikowalnej migracji łańcucha.

**EXIOM Oracle.** Działa na mainnecie. Pierwszy produkt oracle platformy: komitet operatorów węzłów usługowych XEQM — każdy uruchamiający lekki sidecar oracle — który produkuje zagregowane BLS, podpisane EIP-712 atestacje zgodności (na przykład, że adres jest uprawniony dla danej jurysdykcji), które aplikacje konsumują przez developer API. Jest wdrożony na Robinhood Chain (chainId 4663) i prowadzi 12-osobowy komitet operatorów na dzień 28 września 2026. Uruchomienie sidecara to sposób, w jaki operator węzła usługowego zarabia dodatkowy przychód oparty na użyciu, ponad nagrody blokowe.

**EXIOM Developer API.** Działa w wersji beta. Ustrukturyzowane API udostępniające możliwości zgodności i weryfikacji platformy — podpisane oświadczenia zgodności i silnik weryfikacji (mechanizmy signed-claims, TLSNotary i zero-knowledge) — z dostępem samoobsługowym (DID plus klucz API), specyfikacją OpenAPI 3.1, webhookami i żądaniami idempotentnymi. Deweloperzy budują za darmo w ramach hojnego miesięcznego limitu i płacą za użycie produkcyjne w XEQM, zużywane za wywołanie. Faza 2, aktywna.

**EXIOM Privacy Oracle.** Zaprojektowany, fundamenty na miejscu. Szersza ewolucja oracle: dowodzenie faktów o prywatnych danych webowych (za pomocą TLSNotary i technik zero-knowledge) bez ujawniania źródła bazowego. Silnik weryfikacji i punkty końcowe sesji oracle, które go podtrzymują, już działają; pełny oracle prywatnych danych webowych jest produktem Fazy 3. Zarówno platforma EXIOM RFQ, jak i aplikacje zewnętrzne mogą konsumować wyjścia oracle.

**EXIOM RFQ Trading Platform.** W trakcie opracowywania. Platforma handlowa peer-to-peer typu over-the-counter z kryptograficznymi atestacjami rozliczenia, zbudowana na EXIOM API. Pierwsza para handlowa to XEQM/BTC, obie natywne aktywa Layer 1 bez tokenizacji, bez opakowywania i bez ryzyka mostkowego. Oracle dostarcza prywatne atestacje cenowe dla warstwy wyceny. Faza 2/3.

XEQM Labs prowadzi EXIOM jako komercyjną platformę oprogramowania. Celem jest zrównoważony przychód platformy, który z czasem zmniejsza zależność od emisji zarządczych. XEQM Labs nie zachęca do zakupu XEQM na podstawie spekulacyjnego wzrostu ceny.

---

## 2. Pochodzenie podaży

Migracja jest zakończona. 276,917,604 XEQM zostało wyemitowanych na EXIOM mainnet w zamian za starsze zasoby. Ta liczba to zweryfikowana podaż początkowa przy uruchomieniu mainnetu w dniu 6 maja 2026. Każdy starszy depozyt został zarejestrowany w publicznym rejestrze z odciskiem SHA256. Nowy łańcuch został wyemitowany jednorazowo na zakończenie swapu, aby odpowiadać dokładnie tej zweryfikowanej sumie. Klucze wydatkowania dla każdego portfela zaangażowanego w swap zostały opublikowane i każdy może zweryfikować kompletną historię transakcji od depozytu do wypłaty.

Poza podażą początkową nowy XEQM wchodzi do obiegu przez dwa strumienie emisji na poziomie protokołu: nagrody blokowe węzłów usługowych oraz emisje zarządcze. Oba działają według stałych i przewidywalnych harmonogramów zapisanych w protokole, które każdy może obliczyć z publicznych parametrów. Stawki i szczegóły operacyjne są w Sekcji 3. Całkowita podaż rośnie z czasem. XEQM jest łańcuchem o nieograniczonej podaży według tego samego modelu co emisja ogonowa Monero. Dyscyplina stałej podaży, do której projekt się zobowiązuje, odnosi się do braku uznaniowej emisji, a nie do twardego limitu emisji napędzanych przez protokół.

**Brak uznaniowych emisji.** Protokół nie dopuszcza doraźnej emisji, ręcznych korekt podaży ani emisji poza harmonogramem. Każdy nowy XEQM wchodzący do obiegu robi to poprzez dwa powyższe zaplanowane strumienie emisji.

**Brak spaleń.** Architektura kryptograficzna, na której zbudowana jest ta sieć, nie wspiera dowodliwych spaleń w sposób, w jaki ten termin jest zwykle używany. Dowolny adres, na który moneta zostaje wysłana, jest nie do wydania tylko w takim stopniu, w jakim klucz jest dowodliwie zniszczony. Nie będziemy przedstawiać żadnego portfela jako adresu spalenia. Monety niewymienione podczas okna migracji pozostają na nieaktywnym starszym łańcuchu i nie są częścią podaży XEQM.

---

## 3. Model tokenomiki

### Emisje blokowe

Sieć produkuje nowy blok co 60 sekund i przyznaje 8.25 XEQM wybranemu węzłowi usługowemu, generując 11,880 XEQM dziennie. Przy 943 aktywnych węzłach (27 września 2026) każdy węzeł zarabia około 12.6 XEQM dziennie, czyli około 380 XEQM miesięcznie.

Począwszy od HF21 nagrody blokowe są rozprowadzane według cotygodniowego harmonogramu grupowania. Przed HF21 nagrody były wydawane co 20 bloków. Nagrody teraz kumulują się w każdym oknie 10,080 bloków (około 7 dni) i są wypłacane na koniec każdego okna. Całkowita stawka emisji pozostaje bez zmian; zmienił się jedynie rytm płatności.

### Emisja zarządcza

Skarbiec otrzymuje około 17,857 XEQM dziennie, czyli mniej więcej 124,999 XEQM tygodniowo. To jest budżet operacyjny dla aktywnego komercyjnego zespołu tworzącego oprogramowanie. Inżynierowie, recenzenci bezpieczeństwa, operatorzy infrastruktury i kontrybutorzy ekosystemu są wynagradzani z tej emisji, podczas gdy platforma jest przed fazą przychodów. W miarę jak każdy produkt EXIOM osiąga status generujący przychody, emisja zarządcza jest przeglądana i odpowiednio redukowana. Długoterminowym celem jest zastąpienie emisji zarządczej przychodem platformy jako głównym mechanizmem finansowania.

### Alokacja emisji

| Alokacja | Udział | Cel |
|---|---|---|
| Nagrody węzłów usługowych | 40% | Nagrody blokowe wypłacane bezpośrednio węzłom usługowym |
| Rozwój protokołu podstawowego | 25% | Blockchain, platforma EXIOM i podstawowe usługi sieciowe |
| Marketing i świadomość | 15% | Widoczność sieci i adopcja |
| Ekosystem i społeczność | 10% | Granty, nagrody za zadania, nagrody społecznościowe, wsparcie integracji |
| Bezpieczeństwo i audyty | 5% | Audyty, przeglądy bezpieczeństwa, testy niezawodności |
| Rezerwa długoterminowa | 5% | Stabilność, potrzeby awaryjne, operacje długoterminowe |

### Przychody platformy EXIOM i dystrybucja

Poza nagrodami blokowymi platforma uzyskuje przychody z użycia przez deweloperów. Dostęp jest przedpłacony: deweloper finansuje swoje konto, deponując XEQM (bezzwrotnie), a to saldo jest pomniejszane w miarę zużywania produkcyjnego API, wycenianego za wywołanie. Rozwój i ewaluacja w ramach darmowego limitu nie są obciążane opłatami.

Zużyty XEQM jest ujmowany jako przychód platformy i dystrybuowany między operatorów, którzy obsługują oracle, a operacje platformy:

| Odbiorca | Udział | Cel |
|---|---|---|
| Operatorzy sidecara oracle | 70% | Operatorzy węzłów usługowych uruchamiający sidecar oracle, nagradzani proporcjonalnie do obowiązków oracle, które pomagają obsługiwać |
| Operacje i rozwój platformy | 30% | Finansuje bieżące operacje i rozwój, zmniejszając z czasem poleganie na emisji zarządczej |

Operatorzy biorą większość, ponieważ uruchamiają infrastrukturę, która obsługuje oracle. Stosunek 70/30 jest wartością początkową i można go dostosować poprzez zarządzanie. Przychód jest ujmowany i dystrybuowany w tym samym cotygodniowym rytmie co nagrody blokowe — każde okno 10,080 bloków (około 7 dni), zgodnie z grupowaniem nagród HF21 — więc operator otrzymuje nagrody blokowe i udział w przychodach z użycia w jednym rytmie. Ten udział w przychodach jest mechanizmem, dzięki któremu nagroda sidecara operatora opisana w Sekcji 4 jest finansowana z rzeczywistego użycia, a nie z emisji.

Podstawowy sprzęt do uruchomienia węzła usługowego (i jego sidecara oracle): 4 rdzenie CPU, 8 GB RAM, 100 GB SSD, łącze 100 Mbps. Cięższe obciążenia privacy-oracle wymagają wyższych specyfikacji, omówionych w Sekcji 10.

---

## 4. Struktura węzła usługowego

### Parametry stakingu

| Parametr | Wartość |
|---|---|
| Wymóg pełnego węzła | 200,000 XEQM |
| Minimalny stake operatora | 100,000 XEQM (50% pełnego wymogu) |
| Maksymalna opłata operatora | 10% |
| Okres unbondingu, dobrowolne wycofanie | 14 dni, nagrody kontynuowane |
| Okres unbondingu, wymuszona deregistracja | 14 dni, brak nagród (ujednolicone w HF22) |
| Maksymalna liczba slotów kontrybutorów | 11 (wliczając operatora) |
| Minimalny wkład społeczności na slot | 10,000 XEQM |
| Okno stakera społeczności na węzeł | Do 100,000 XEQM w maksymalnie 10 slotach kontrybutorów |

### Ekonomia węzła

Wielu dostawców VPS w chmurze oferuje darmowy poziom usługi, który może obsłużyć działanie węzła usługowego przy zerowym koszcie miesięcznym. Płatny VPS w cenie około $5.28 miesięcznie może obsłużyć 10 węzłów usługowych, co obniża koszt hostingu na węzeł do mniej więcej $0.53 miesięcznie. Zarządzany hosting przez Pecunia jest dostępny za $1.76 na węzeł miesięcznie.

Nagrody blokowe na węzeł skalują się odwrotnie do liczby aktywnych węzłów: przy 943 aktywnych węzłach usługowych (27 września 2026) dzienna emisja sieci wynosząca 11,880 XEQM daje około 12.6 XEQM na węzeł dziennie, około 380 XEQM miesięcznie. Ponieważ zarówno nagroda, jak i stake są denominowane w XEQM, APY nagrody blokowej wynosi około 2.3% niezależnie od ceny; hosting jest jedynym istotnym kosztem cyklicznym, mniej więcej $0.53 na węzeł miesięcznie przy samodzielnym hostingu lub $1.76 przez Pecunia. Uruchomienie sidecara oracle (Sekcja 10) dodaje drugi strumień dochodu, który jest oparty na przychodach i skaluje się z rzeczywistym użyciem platformy, finansowany z konsumpcji deweloperów, a nie z emisji.

### Ekonomia kontrybutora

Operatorzy, którzy nie mogą lub nie chcą uruchamiać infrastruktury, mogą wnieść stake do istniejącego węzła w maksymalnie 10 slotach kontrybutorów. Operator może pobierać od 0% do 10% nagrody blokowej, zanim reszta zostanie podzielona proporcjonalnie między kontrybutorów. Kontrybutorzy nie ponoszą kosztu hostingu, więc w każdym punkcie cenowym zysk netto kontrybutora przewyższa zysk operatora hostującego samodzielnie lub przez Pecunia.

### Cykl życia węzła

Węzły pozostają aktywne bezterminowo przy utrzymaniu wymogów zabezpieczenia i wydajności. Węzeł, który wypada ze zgodności, może zostać naprawiony bez kary. Jeśli nie zostanie naprawiony, wymuszona deregistracja uruchamia 14-dniowy okres unbondingu bez nagród. Dobrowolne wyjście wiąże się z 14-dniowym okresem unbondingu z nagrodami kontynuowanymi przez cały czas.

---

## 5. Przeżywalność sieci i wektory ataku

### Wymóg przeżywalności

Sieć EXIOM składa deweloperom zobowiązania dotyczące niezawodności. Sieć, która może zostać wyłączona przez awarię pojedynczego centrum danych, nie może składać takich zobowiązań. Protokół egzekwuje maksymalny rozmiar domeny awarii: żaden pojedynczy obiekt fizyczny, centrum danych ani klaster routingu nie może hostować więcej niż 30% aktywnych węzłów.

Przy 943 węzłach (27 września 2026) 30% to około 283 węzły. Utrata dowolnego pojedynczego obiektu może wyłączyć jednocześnie najwyżej 283 węzły, pozostawiając co najmniej 660 węzłów operacyjnych, co wystarcza do utrzymania produkcji bloków i formowania kworum bez kaskadowych deregistracji. To jest wymóg inżynieryjny, a nie preferencja decentralizacji.

### Dwa hard forki

Egzekwowanie przeżywalności jest dostarczane w dwóch etapach, rozdzielonych w celu ograniczenia ryzyka i natychmiastowego wdrożenia zwalidowanej pracy.

**HF22, aktywowany:** Deduplikacja kworum kluczy portfela operatora i ujednolicenie okresu unbondingu, plus rewizja odzyskiwania po zawieszeniu Pulse (snode_revision 1), która zastępuje wcześniejszy fallback odzyskiwania Proof-of-Work fallbackiem opartym na podpisie. Brak zależności od Lokinet. Zwalidowane przez 20 cykli zawieszenia/odzyskiwania ze 100% wskaźnikiem odzyskiwania, zerową interwencją i najgorszą przerwą między blokami wynoszącą 83 sekundy. HF22 aktywowany na bloku mainnetu 219120; rewizja odzyskiwania po zawieszeniu aktywowana na bloku 236920 w dniu 18 października 2026.

**HF23, w projektowaniu, cel Q4 2026:** Limit rejestracji w klastrze bliskości, modyfikator zerowej nagrody dla nadmiarowych węzłów oraz uaktualnienie deduplikacji kworum z klucza portfela na klaster bliskości. Wszystkie trzy opierają się na grafie routingu Lokinet jako sygnale bliskości. Aby nie czynić nowego transportu krytycznym dla konsensusu w momencie jego wprowadzenia, Lokinet jest dostarczany najpierw w osobnym wydaniu nieegzekwującym (wraz ze zmianą magazynu lekkich węzłów SQLite), gdzie klastrowanie według bliskości działa i jest obserwowalne, ale nie ma konsekwencji dla nagród. HF23 następnie włącza egzekwowanie, po tym jak to wydanie zostanie wygrzane, a rzeczywista liczba klastrów zmierzona oraz próg i fallback dostrojone.

### Kontrole HF22

**Deduplikacja kworum kluczy portfela operatora.** Co najwyżej jeden węzeł na adres portfela operatora może zajmować miejsce walidatora w danej rundzie Pulse, sesji oracle lub kworum obowiązków. Jeśli losowe losowanie wybierze dwa węzły z tego samego adresu operatora, drugi jest zastępowany węzłem od innego operatora. Nagrody blokowe pozostają bez zmian; są przydzielane według kolejności czasu oczekiwania, niezależnie od uczestnictwa w kworum.

Znane ograniczenie: pokonywane przez dzielenie portfeli. Operator używający wielu adresów portfeli prezentuje protokołowi wiele kluczy operatora. HF23 zamyka tę lukę poprzez deduplikację klastra bliskości.

**Ujednolicenie okresu unbondingu.** Unbonding wymuszonej deregistracji wydłużony z 7 dni do 14 dni, zrównany z dobrowolnym wycofaniem. Oba przypadki wynoszą teraz 14 dni.

### Kontrole HF23

Gdy Lokinet jest aktywny jako transport sieciowy, węzły fizycznie współzlokalizowane wykażą charakterystyczne sygnatury routingu: podmilisekundowe wzajemne opóźnienie i wysokie nakładanie się ścieżek przez graf routingu Lokinet. Węzły w rzeczywiście różnych obiektach wykażą wyższe opóźnienie i niższe nakładanie się ścieżek. Ten sygnał klastrowania jest wyprowadzany z obserwowalnego zachowania sieci, bez wymogu, aby operatorzy ujawniali swojego dostawcę lub lokalizację.

**Limit rejestracji klastra.** Rejestracje nowych węzłów oceniane są względem bliskości routingu Lokinet do istniejących klastrów. Jeśli docelowy klaster zawiera już 30% lub więcej aktywnych węzłów, rejestracja jest odrzucana przez protokół.

**Modyfikator zerowej nagrody.** Węzły powyżej progu limitu klastra zarabiają zero nagród blokowych do momentu migracji do nieskoncentrowanego klastra. Węzły są rankingowane w każdym klastrze według wieku rejestracji; najstarsze węzły do progu limitu zarabiają pełne nagrody. Każdy węzeł powyżej tego progu zarabia zero. Obniżoną stawkę można racjonalnie uzasadnić względem kosztów VPS; zera nie można.

30-dniowy okres karencji obowiązuje przy aktywacji HF23. Wszystkie węzły zarabiają pełne nagrody podczas okresu karencji. Po jego wygaśnięciu modyfikator zerowej nagrody aktywuje się na nadmiarowych węzłach.

**Deduplikacja kworum klastra bliskości.** Uaktualnia deduplikację kluczy portfela z HF22 do deduplikacji klastra bliskości. Co najwyżej jeden węzeł na klaster bliskości na rundę, niezależnie od struktury portfeli. Zamyka lukę dzielenia portfeli.

Rozmiar kworum to 12 miejsc na rundę. Deduplikacja wymaga zatem co najmniej 12 odrębnych klastrów bliskości, aby działać bez fallbacku. Biorąc pod uwagę obecną topologię sieci, liczba klastrów przy aktywacji HF23 może być bliska temu minimum. Algorytm implementuje obowiązkowy fallback: jeśli wszystkie odrębne klastry zostaną wyczerpane przed wypełnieniem 12 miejsc, dodatkowe miejsca są przydzielane począwszy od najmniejszych (najmniej skoncentrowanych) klastrów, zanim najbardziej skoncentrowany klaster otrzyma drugie miejsce. Częstotliwość fallbacku jest logowana i publikowana w eksploratorze węzłów jako wskaźnik ryzyka koncentracji w czasie rzeczywistym. Sieć, która nigdy nie uruchamia fallbacku, osiągnęła odpowiednią różnorodność fizyczną.

### Dodatkowe kontrole

**Bariera kosztu kapitałowego.** Minimalny stake operatora wynoszący 100,000 XEQM zapewnia, że każdy operator angażuje realny kapitał w każdy węzeł. Uruchomienie N węzłów wymaga co najmniej N x 100,000 XEQM zastakowanych.

**Ochrona przed przechwyceniem opłaty operatora.** EXIOM nie podlega atakowi przechwycenia opłaty operatora obecnemu w niektórych sieciach węzłów usługowych, gdzie operator rejestruje węzeł z minimalnym kapitałem i ustawia opłatę 100%, aby przechwycić całą nagrodę blokową niezależnie od stake'u kontrybutora. Maksymalna opłata jest ograniczona do 10%, a 50% minimalny stake operatora czyni to ekonomicznie nieracjonalnym.

**Analiza czasowa dowodów uptime.** Węzły na tym samym fizycznym hoście składają dowody uptime w ciasno skorelowanych klastrach, wykrywalne z istniejących danych odbioru dowodów bez zmian w demonie.

**Analiza ASN.** Węzły za tym samym Autonomous System Number dzielą infrastrukturę na poziomie dostawcy i ekspozycję prawną. Koncentracja ASN przyczynia się do przypisania klastra i przeglądu zarządczego.

**Lista blokująca zarządzania.** Zarządzana przez governance publiczna lista blokująca kluczy uniemożliwia zablokowanym kluczom rejestracyjnym rejestrowanie nowych węzłów.

**Cel współczynnika Nakamoto.** Sieć celuje we współczynnik operatorów wynoszący co najmniej 8. Na dzień 27 września 2026, w ramach 943 aktywnych węzłów usługowych i 204 operatorów, współczynnik Nakamoto operatorów — minimalna liczba operatorów kontrolujących większość aktywnych węzłów — wynosi 9, spełniając cel (wzrost z 7 w ramach 184 operatorów w lipcu 2026). Koncentracja obiektów fizycznych to osobny i bardziej dotkliwy problem: pojedynczy region centrum danych nadal hostuje większość węzłów, co jest dokładnie tą koncentracją, którą limit klastra bliskości HF23 ma przełamać.

Pełna propozycja limitów koncentracji znajduje się pod [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). Metodologia odporności na Sybil znajduje się pod [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Lokinet jako przyszły transport sieciowy

Infrastruktura adresowania sieci EXIOM będzie migrować z publicznie ogłaszanych adresów IP na adresowanie Lokinet. Lokinet jest dostarczany najpierw w wydaniu nieegzekwującym przed HF23 (cel Q4 2026); HF23 następnie dodaje egzekwowanie koncentracji, które wykorzystuje graf routingu Lokinet. Lokinet (Low Latency Anonymous Routing Protocol, LLARP) to protokół routingu cebulowego warstwy 3 routujący dowolny ruch oparty na IP przez wiele węzłów usługowych za pomocą wieloskokowego routingu cebulowego, przy czym żaden pojedynczy węzeł na ścieżce nie zna jednocześnie źródła i miejsca docelowego.

Gdy Lokinet jest aktywny:

- Węzły usługowe będą adresowane przez swój kryptograficzny identyfikator Lokinet, a nie przez publicznie ogłaszany adres IP
- EXIOM developer API będzie dostępne jako usługa ukryta pod adresem `.loki`, ukrywając źródłowy adres IP dewelopera przed węzłem API
- Platforma handlowa RFQ będzie dostępna jako usługa ukryta, ukrywając adresy IP zgłaszającego i LP przed platformą
- Komunikacja sesji oracle między dowodzącym a kworum weryfikującym będzie routowana przez Lokinet, eliminując założenie zaufania do scentralizowanego koordynatora

Lokinet jest dostarczany w wydaniu nieegzekwującym przed HF23, z celem Q4 2026, przy czym HF23 następuje po tym, jak zostanie wygrzane. Baza kodu LLARP jest obecna w repozytorium EXIOM; implementacja Lokinet jako podstawowego transportu sieciowego rozpoczyna się w Q4 2026.

---

## 6. XEQM jako moneta użytkowa

Popyt na XEQM pochodzi z trzech źródeł. Staking węzłów blokuje największy udział podaży, około 68% przy obecnych 943 aktywnych węzłach (27 września 2026). Konsumpcja deweloperów tworzy ciągłą warstwę prędkości obiegu: aplikacje płacą za produkcyjne użycie API w XEQM, więc adopcja platformy przekłada się bezpośrednio na cykliczny popyt na monetę. Dostęp do oracle dodaje trzecią warstwę dla konsumentów o większym wolumenie.

Dostęp podąża za modelem przedpłaconym, opartym na użyciu, a nie bramką stake-to-unlock — deweloperzy nie muszą nabywać i blokować stałego stake'u, aby budować:

| Poziom | Model dostępu |
|---|---|
| Free | Buduj i ewaluuj bez kosztu: hojny miesięczny limit wywołań, brak wymaganego depozytu |
| Production | Przedpłacone użycie: zdeponuj XEQM i płać za wywołanie; webhooki i wyższe limity |
| Enterprise | Niestandardowe limity, SLA i wsparcie; warunki wolumenowe |

Użycie produkcyjne jest mierzone za wywołanie API i pobierane z przedpłaconego salda XEQM dewelopera. Depozyty są bezzwrotne i są ujmowane jako przychód platformy w miarę ich zużywania (patrz Sekcja 3). Wcześniejszy projekt bramkował poziomy za stałym stakiem XEQM; zostało to zastąpione tym przedpłaconym modelem, który jest prostszy dla deweloperów i standardowy dla komercyjnych API.

---

## 7. Zarządzanie i skarbiec

Adres portfela zarządczego i klucz podglądu są opublikowane. Każdy może w dowolnym momencie zweryfikować saldo. Zarządzanie obecnie odbywa się przez zespół założycielski z udziałem społeczności za pośrednictwem otwartych kanałów Telegram i dyskusji na GitHubie.

Alokacje skarbca, pobierane z emisji zarządczej opisanej w Sekcji 3:

- Rozwój podstawowy (25%): inżynieria dla EXIOM API, oracle i platformy RFQ
- Marketing i świadomość (15%): listingi na giełdach, treści, wzrost społeczności
- Ekosystem i społeczność (10%): granty, nagrody za zadania, wsparcie integracji
- Bezpieczeństwo i audyty (5%): audyty kodu, przeglądy bezpieczeństwa, testy penetracyjne
- Rezerwa długoterminowa (5%): stabilność operacyjna i rezerwy awaryjne

Faza 3 wprowadza formalny proces propozycji i komentarzy. Faza 6 wprowadza głosowanie ważone, w którym operatorzy węzłów usługowych i węzłów API posiadają formalne prawa proporcjonalne do stake'u i stażu.

---

## 8. Podsumowanie parametrów

| Parametr | Wartość |
|---|---|
| Mechanizm konsensusu | 100% Proof-of-Stake |
| Czas bloku | 60 sekund |
| Nagroda blokowa | 8.25 XEQM na blok |
| Dzienne emisje blokowe | 11,880 XEQM |
| Emisja zarządcza | ~17,857 XEQM dziennie |
| Wymóg pełnego węzła | 200,000 XEQM |
| Minimalny stake operatora | 100,000 XEQM (50%) |
| Maksymalna opłata operatora | 10% |
| Maksymalna liczba slotów kontrybutorów | 11 (wliczając operatora) |
| Minimalny wkład społeczności | 10,000 XEQM na slot |
| Okno stakera społeczności na węzeł | Do 100,000 XEQM w 10 slotach |
| Okres unbondingu, dobrowolne wycofanie | 14 dni, nagrody kontynuowane |
| Okres unbondingu, wymuszona deregistracja | 14 dni, brak nagród (HF22) |
| Całkowita podaż | 276,917,604 XEQM przy uruchomieniu, rosnąca przez zaplanowane emisje |
| Podaż zablokowana przy 943 węzłach (Sep 27, 2026) | ~188,600,000 XEQM (~68% podaży początkowej) |
| Swobodnie krążące przy 943 węzłach | ~88,300,000 XEQM przy podaży początkowej, rosnące wraz z emisjami |
| APY solo operatora przy 943 węzłach | ~2.3% (tylko nagrody blokowe, wypłacane cotygodniowo przez HF21) |
| Koszt na węzeł przy samodzielnym hostingu | ~$0.53/miesiąc ($5.28/mo VPS, 10 węzłów) |
| Koszt zarządzanego hostingu (Pecunia) | $1.76/węzeł/miesiąc |
| Aktywne węzły usługowe (27 września 2026) | 943 |
| Współczynnik Nakamoto operatorów (Sep 27, 2026) | 9 — kontrola większościowa; cel >= 8; 943 węzły, 204 operatorów |
| Zewnętrzna aktywacja oracle | Nakamoto >= 6 osiągnięte; uzależnione od ukończenia Fazy 3 |
| Rozmiar kworum | 12 miejsc na rundę |
| Deduplikacja kworum, HF22 | Jeden adres portfela operatora na miejsce w kworum na rundę |
| Deduplikacja kworum, HF23 | Jeden klaster bliskości na miejsce w kworum na rundę (wymaga Lokinet) |
| Fallback deduplikacji kworum, HF23 | Jeśli istnieje mniej niż 12 odrębnych klastrów, najmniejsze klastry otrzymują dodatkowe miejsca jako pierwsze przed najbardziej skoncentrowanymi klastrami; częstotliwość fallbacku logowana i publikowana |
| Limit przeżywalności sieci, HF23 | 30% aktywnych węzłów na klaster bliskości (~283 węzły przy obecnej liczbie) |
| Modyfikator zerowej nagrody, HF23 | Zero nagród blokowych dla węzłów powyżej limitu klastra, rankingowanych według wieku rejestracji |
| Repozytoria podstawowe | github.com/XEQMLabs |

---

## 9. Roadmapa

**Faza 1, Stabilizacja sieci. UKOŃCZONA.** Sieć węzłów usługowych wzrosła do 943 aktywnych węzłów usługowych na dzień 27 września 2026 (z 693 w ramach 184 operatorów w lipcu 2026, współczynnik Nakamoto 7). Swap monet XEQ na XEQM przebiegł i zamknął się pomyślnie.

**Faza 2, EXIOM developer API i EXIOM Oracle. AKTYWNA.** EXIOM Oracle działa na mainnecie z komitetem operatorów, a developer API działa w wersji beta (poświadczenia samoobsługowe, punkty końcowe zgodności i weryfikacji, OpenAPI). Pozostałe prace Fazy 2: rozliczanie konsumpcji przedpłaconej, udział operatorów w przychodach oraz pierwsze integracje produkcyjne. Rozwój platformy handlowej EXIOM RFQ przebiega równolegle, z XEQM/BTC jako pierwszą parą handlową.

**Faza 3, EXIOM Privacy Oracle i platforma RFQ.** Oracle jest wdrażany etapami: wewnętrzny proof of concept, federacyjny testnet, następnie mainnet z wewnętrznymi konsumentami. Platforma handlowa RFQ osiąga produkcję w tej fazie, używając oracle do prywatnej atestacji cenowej na parze XEQM/BTC. Oba są zbudowane na EXIOM API.

**Faza 4, Zewnętrzny dostęp konsumenta oracle.** Wyjścia oracle dostępne dla deweloperów poziomu Production i Enterprise oraz konsumentów zewnętrznych. Próg współczynnika Nakamoto wynoszący 6 już osiągnięty; aktywacja uzależniona od ukończenia Fazy 3.

**HF22, aktywowany (blok mainnetu 219120).** Dwie zmiany konsensusu bez zależności od Lokinet, deduplikacja kworum kluczy portfela operatora (jeden adres operatora na miejsce w kworum na rundę) i ujednolicenie okresu unbondingu (wymuszona deregistracja wydłużona z 7 do 14 dni), plus rewizja odzyskiwania po zawieszeniu Pulse (snode_revision 1), która aktywowała się na bloku 236920 w dniu 18 października 2026, zastępując odzyskiwanie Proof-of-Work fallbackiem opartym na podpisie. Zwalidowane przez 20 cykli zawieszenia/odzyskiwania (100% odzyskiwania, najgorsza przerwa między blokami 83 sekundy).

**Wydanie Lokinet i lekkich węzłów, przed HF23.** Wydanie nieegzekwujące, które uruchamia Lokinet jako transport sieciowy (klastrowanie według bliskości działa i jest obserwowalne w eksploratorze węzłów, bez konsekwencji dla nagród) i wprowadza magazyn lekkich węzłów SQLite (niższa pamięć i dysk na węzeł, z opcjonalnymi lekkimi węzłami z ostatniego okna). To wydanie jest wygrzewane, aby rzeczywista liczba klastrów bliskości mogła być zmierzona, a próg HF23 i fallback dostrojone, zanim jakiekolwiek egzekwowanie wejdzie w życie.

**HF23, w projektowaniu, cel Q4 2026.** Włącza egzekwowanie po tym, jak powyższe wydanie nieegzekwujące Lokinet i lekkich węzłów zostanie wygrzane: limit rejestracji w klastrze bliskości (rejestracje odrzucane, gdy klaster przekracza 30% aktywnych węzłów); modyfikator zerowej nagrody dla węzłów powyżej progu limitu rankingowanych według wieku rejestracji; uaktualnienie deduplikacji kworum z klucza portfela na klaster bliskości, z obowiązkową regułą fallbacku zapewniającą, że formowanie kworum jest zawsze możliwe nawet gdy istnieje mniej niż 12 odrębnych klastrów (najmniejsze klastry otrzymują dodatkowe miejsca jako pierwsze przed najbardziej skoncentrowanymi klastrami, z częstotliwością fallbacku logowaną i publikowaną jako wskaźnik ryzyka koncentracji). 30-dniowy okres karencji obowiązuje przy aktywacji, zanim modyfikator zerowej nagrody wejdzie w życie.

**Faza 6, Formalne zarządzanie.** Ustrukturyzowany proces propozycji, głosowanie ważone dla operatorów, długoterminowe przejście od zarządzania przez zespół założycielski.

---

## 10. EXIOM Oracle

### Pierwszy działający oracle: EXIOM Oracle

Pierwszy produkt oracle platformy działa na mainnecie. EXIOM Oracle to komitet operatorów węzłów usługowych XEQM — każdy uruchamiający lekki sidecar oracle obok swojego węzła — którzy wspólnie produkują zagregowane BLS, podpisane EIP-712 atestacje o faktach zgodności, najbardziej bezpośrednio o tym, czy dany adres jest uprawniony dla danej jurysdykcji. Aplikacje konsumują te atestacje przez developer API i mogą przesłać podpisany wynik on-chain. Komitet jest wdrożony na Robinhood Chain (chainId 4663) i prowadzi 12-osobowy komitet operatorów na dzień 28 września 2026, z progiem podpisu dwóch trzecich (8-z-12).

**Model bezpieczeństwa: zbiór zarejestrowany kontra próg.** EXIOM Oracle nie próbkuje komitetu na rundę. Ponieważ agregat BLS kosztuje bramkę tyle samo do weryfikacji, czy podpisało ośmiu członków czy osiemset, każdy zarejestrowany członek podpisuje każdą rundę; próbkowanie podzbioru nie przyniosłoby nic i ponownie wprowadziłoby ryzyko, że pechowe losowanie akurat obejmie wystarczająco wielu zmawiających się członków, by sfałszować. Bezpieczeństwo sprowadza się zatem do dwóch właściwości zbioru zarejestrowanych członków o rozmiarze N, przy progu dwóch trzecich k = ceil(2N/3), który bramka egzekwuje:

- **Fałszerstwo** wymaga, aby przeciwnik kontrolował co najmniej k zarejestrowanych członków — zmowa, a zatem kwestia koncentracji **operatorów**.
- **Zatrzymanie** (awaria żywotności) wymaga, aby co najmniej N - k + 1 = floor(N/3) + 1 zarejestrowanych członków zgasło naraz — skorelowana awaria, a zatem kwestia koncentracji **infrastruktury**.

To są dwa współczynniki Nakamoto i są one właściwościami zbioru zarejestrowanego, a nie szerszej floty węzłów usługowych: rozkład floty ogranicza konsensus, podczas gdy odporność oracle na fałszerstwo i żywotność zależy tylko od tego, kto zajmuje zarejestrowane miejsca.

**Obecna realizacja.** Na dzień 28 września 2026 wszyscy zarejestrowani członkowie są obsługiwani przez operatora projektu, więc współczynnik operatorów oracle wynosi 1: dziś jego odporność na fałszerstwo opiera się na zaufaniu do pojedynczego operatora, a nie na rozproszonej kryptografii. To jest uczciwy stan początkowy. Model bezpieczeństwa to k-z-N wśród niezależnych operatorów; realizacja twardnieje w miarę jak niezależni się zapisują, co jest celem wdrażania dodatkowych operatorów węzłów usługowych jako członków sidecara. Sama liczba węzłów nie pomaga — dodatkowi członkowie podnoszą oba współczynniki tylko o tyle, o ile są niezależnymi operatorami w odrębnych obiektach.

**Jak egzekwowana jest różnorodność.** Ponieważ nie ma selekcji na rundę, różnorodność jest decydowana przy **przyjęciu**: członek jest rejestrowany tylko wtedy, gdy utrzymuje udział każdego operatora poniżej k i udział każdego obiektu na poziomie lub poniżej floor(N/3), a k jest podnoszone, aby śledzić ceil(2N/3) w miarę rośnięcia zbioru. Koncentracja zbioru zarejestrowanego jest monitorowana w sposób ciągły i publikowana jako margines fałszerstwa (k minus udział największego operatora) oraz margines żywotności (floor(N/3) + 1 minus udział największego obiektu); niedodatni margines jest alarmem. Sygnałem obiektu jest dziś ASN i czas przybycia dowodów uptime, wyostrzony przy HF23 do bliskości routingu Lokinet, która wykrywa współzlokalizowanie fizyczne nawet w ramach odrębnych ASN. Te fakty o rozkładzie są same w sobie atestowalne przez typowany interfejs faktów oracle, więc metryka koncentracji jest wartością podpisaną przez komitet, a nie wynikiem pojedynczego zaufanego skryptu.

Sidecar jest celowo lekki: przechowuje tylko swój własny klucz podpisu, czyta tożsamość swojego węzła lokalnie i nigdy nie obsługuje kluczy wydatkowania operatora. Jego uruchomienie to mechanizm, dzięki któremu operator węzła usługowego zarabia dodatkowy, finansowany z użycia przychód opisany w Sekcjach 3 i 4.

### Szersza wizja: EXIOM Privacy Oracle

EXIOM Privacy Oracle pozwala aplikacjom konsumować uwierzytelnione prywatne strumienie danych bez ujawniania bazowych danych źródłowych. Wykorzystuje techniki dowodów zero-knowledge do udowodnienia pochodzenia danych ze standardowych punktów końcowych HTTPS, nie wymagając współpracy po stronie serwera ani zaufanego sprzętu. Jest produktem Fazy 3, następującym po stabilizacji platformy API z Fazy 2 oraz konsultacji kryptograficznej, zanim rozpocznie się pełna budowa.

Oracle nie jest strumieniem danych ogólnego przeznaczenia. Jest to oracle stawiający prywatność na pierwszym miejscu, dla przypadków użycia, w których same dane muszą pozostać poufne: progi cenowe bez ujawniania dokładnych cen, salda kont bez ujawniania poświadczeń, atestacje zgodności bez ujawniania bazowego rekordu. Platforma EXIOM RFQ jest pierwszym wewnętrznym konsumentem, używając jej do udowodnienia, że realizacja XEQM/BTC nastąpiła po cenie referencyjnej lub lepszej, bez ujawniania dokładnej ceny platformie lub drugiej stronie.

Gdy Lokinet jest aktywny jako transport sieciowy, komunikacja sesji oracle między dowodzącym a kworum weryfikującym będzie routowana cebulowo przez sieć węzłów usługowych. Ani źródło dowodzącego, ani adresy sieciowe węzłów kworum nie będą widoczne dla żadnego pojedynczego węzła przekazującego, eliminując założenie zaufania do scentralizowanego koordynatora.

### Architektura

**Warstwa dowodząca.** Aplikacja lub użytkownik posiadający dostęp do prywatnego źródła danych uczestniczy w protokole kryptograficznym, który zobowiązuje się do odpowiedzi TLS bez jej ujawniania. Poświadczenia i surowe dane nigdy nie opuszczają kontroli dowodzącego.

**Warstwa weryfikująca.** Rotujące kworum węzłów usługowych weryfikuje, że zobowiązane dane spełniają żądany warunek. Węzły weryfikujące poznają tylko wynik (prawda lub fałsz, powyżej lub poniżej progu) i nigdy nie widzą bazowych danych ani poświadczeń.

**Warstwa konsumenta.** Konsumenci otrzymują tylko minimalne wyjście: wynik boolean, porównanie z progiem, podpisaną atestację lub małą wartość pochodną. Surowe dane źródłowe nigdy nie są publikowane.

### Etapowy plan budowy

**Faza 1, Wewnętrzny proof of concept.** Zespół założycielski waliduje pełny protokół kryptograficzny od początku do końca względem małego zbioru źródeł na białej liście, bez konsumentów zewnętrznych ani uczestnictwa węzłów usługowych.

**Faza 2, Federacyjny testnet oracle.** Operatorzy węzłów usługowych wolontariusze z silną historią uptime dołączają do puli weryfikującej na testnecie. Testowanie adwersaryjne integralności atestacji przed jakimkolwiek wdrożeniem na mainnecie.

**Faza 3, Oracle mainnet z wewnętrznymi konsumentami.** Obowiązek weryfikatora oracle otwiera się dla kwalifikujących się węzłów mainnetu. Wyjścia zasilają wewnętrzne kontrakty EXIOM i platformę RFQ. Opłaty oracle zaczynają płynąć do uczestniczących węzłów weryfikujących.

**Faza 4, Zewnętrzny dostęp konsumenta.** Wyjścia oracle dostępne dla deweloperów poziomu Production i Enterprise oraz konsumentów zewnętrznych. Uzależnione od ukończenia Fazy 3.

### Wymagania sprzętowe weryfikatora

Orientacyjne wymagania: 8 rdzeni CPU, 16 GB RAM, 200 GB SSD, 500 Mbps z niskim opóźnieniem. Standardowy podstawowy sprzęt węzła API nie jest wystarczający do obowiązku weryfikatora oracle.

### Nagrody weryfikatora

| Źródło przychodu | Opis |
|---|---|
| Nagrody blokowe | Standardowa nagroda blokowa węzła usługowego, bez zmian |
| Udział w przychodach platformy | Proporcjonalny udział w przychodach z konsumpcji deweloperów dla operatorów uruchamiających sidecar oracle |
| Opłaty sesji oracle | Opłata za sesję od konsumentów oracle, dystrybuowana do kworum weryfikującego |
| Bonus za obowiązek oracle | Uzupełniająca emisja zarządcza w okresach niskiego wolumenu, redukowana w miarę jak opłaty za sesje stają się samowystarczalne |

---

## 11. EXIOM RFQ Trading Platform

Platforma EXIOM RFQ to system handlowy peer-to-peer typu over-the-counter z kryptograficznymi atestacjami rozliczenia, zbudowany na EXIOM API. Pierwsza para handlowa to XEQM/BTC, obie natywne aktywa Layer 1 bez tokenizacji, bez opakowywania i bez ryzyka mostkowego.

Gdy Lokinet jest aktywny, platforma RFQ będzie dostępna jako usługa ukryta Lokinet. Ani adres IP zgłaszającego, ani LP nie będzie widoczny dla platformy. Warstwa wyceny oracle pozwala kontrahentowi udowodnić, że realizacja nastąpiła po cenie referencyjnej lub lepszej ze źródła z białej listy, bez ujawniania dokładnej ceny realizacji platformie lub drugiej stronie.

Specyfikacja aplikacji RFQ i model danych są ukończone. Aktywny rozwój przebiega w Fazie 2 na warstwie API. Pełna produkcja platformy handlowej jest produktem Fazy 3, zależnym od osiągnięcia produkcji przez EXIOM API i ukończenia przez MVP oracle jego wewnętrznego proof of concept.

---

---

## Dostępne języki

Tłumaczenia społecznościowe tego whitepapera są utrzymywane w folderze translations dla wygody. **Wersja angielska jest jedynym autorytatywnym dokumentem przez cały czas.** Tłumaczenia mogą pozostawać w tyle za bieżącą wersją angielską i nie ma gwarancji, że są aktualne; w przypadku jakiegokolwiek konfliktu, niejednoznaczności lub różnicy jakiegokolwiek rodzaju, wersja angielska jest rozstrzygająca.

| Language | Whitepaper |
|---|---|
| Español | [translations/es/README.md](./translations/es/README.md) |
| Français | [translations/fr/README.md](./translations/fr/README.md) |
| Deutsch | [translations/de/README.md](./translations/de/README.md) |
| 中文 | [translations/zh/README.md](./translations/zh/README.md) |
| Português | [translations/pt/README.md](./translations/pt/README.md) |
| Türkçe | [translations/tr/README.md](./translations/tr/README.md) |
| Polski | [translations/pl/README.md](./translations/pl/README.md) |
| Bahasa Indonesia | [translations/id/README.md](./translations/id/README.md)

---

*To jest dokument roboczy. Parametry, harmonogramy emisji i fazy roadmapy opisane tutaj są zamierzonym projektem. Aktualizacje będą publikowane w miarę ewolucji sieci i platformy.*

*Ten dokument nie stanowi porady finansowej ani prawnej. XEQM jest monetą użytkową dla platformy EXIOM, a nie produktem inwestycyjnym. Klasyfikacja tokena, status papierów wartościowych i obowiązujące regulacje różnią się w zależności od jurysdykcji. Uczestnicy powinni skonsultować się ze swoim lokalnym otoczeniem prawnym i regulacyjnym przed nabyciem lub operowaniem z XEQM. XEQM Labs nie zachęca do zakupu XEQM na podstawie spekulacyjnego wzrostu ceny.*
