# Ryzyko Sybil i model łagodzenia EXIOM
## Techniczny dodatek do Whitepapera tokenomiki EXIOM
### 07/26/2026

> **Nota (zaktualizowana w październiku 2026).** Koncentracja jest egzekwowana na *klaster bliskości* (współdzielona infrastruktura fizyczna lub routingowa), a **nie na kraj**. Liczby węzłów tutaj to zrzut z lipca 2026; zobacz whitepaper dla bieżących sum. Lokinet jest dostarczany w wydaniu nieegzekwującym przed HF23, a HF23 włącza egzekwowanie.

Ten dokument jest dodatkiem do Whitepapera tokenomiki EXIOM oraz propozycji Limitów koncentracji węzłów i zakłada, że oba zostały przeczytane. Whitepaper obejmuje, czym są kontrole. Propozycja concentration-limits-proposal obejmuje mechanikę tego, jak działa każda kontrola. Ten dokument obejmuje model zagrożenia: jak faktycznie wygląda atak Sybil na łańcuchu prywatności, co czyni architekturę EXIOM konkretnie odporną lub podatną oraz jak bieżąca metodologia monitorowania identyfikuje koncentrację w praktyce.

---

## Zagrożenie Sybil na łańcuchu prywatności

Atak Sybil na sieć węzłów usługowych oznacza pojedynczego aktora operującego wieloma węzłami pod odrębnymi pozornymi tożsamościami, aby zyskać nieproporcjonalny wpływ. Na przejrzystym blockchainie analiza grafu portfeli często może ujawnić, że wiele adresów operatora węzła jest finansowanych ze wspólnego źródła, demaskując Sybil. Na łańcuchu prywatności to narzędzie jest niedostępne z założenia. Gwarancja prywatności, która chroni transakcje użytkowników, usuwa również najczęstszą metodę wykrywania Sybil.

Powierzchnia Sybil EXIOM różni się zatem od przejrzystego łańcucha w konkretny sposób: operator, który poprawnie używa funkcji prywatności, może prezentować wiele adresów portfeli, które wydają się niepowiązane na poziomie protokołu, niezależnie od tego, jak dużym kapitałem kontrolują. To nie jest wada w projekcie prywatności. Jest to nieodłączna właściwość każdego łańcucha prywatności, którą trzeba zaadresować za pomocą mechanizmów innych niż analiza grafu transakcji.

Dwie powierzchnie ataku Sybil na EXIOM są odrębne i wymagają osobnych kontroli:

**Atak wpływu na konsensus.** Operator akumuluje wystarczająco wiele węzłów, przez dowolną strukturę portfeli, aby posiadać jednocześnie nieproporcjonalną liczbę miejsc w kworum. To pozwala mu wpływać na wyniki sesji oracle, rundy Pulse i kwora obowiązków ponad to, co sugerowałaby sprawiedliwość jego indywidualnej proporcji stake'u. Szkoda dotyczy integralności konsensusu, niekoniecznie uptime sieci.

**Atak domeny awarii.** Operator koncentruje węzły w pojedynczym obiekcie fizycznym. To może, ale nie musi być zamierzone jako atak; może wynikać z optymalizacji kosztów. Szkoda dotyczy przeżywalności sieci: jedna awaria obiektu wyłącza węzły operatora jednocześnie, potencjalnie zawieszając produkcję bloków, jeśli koncentracja jest wystarczająco duża.

---

## Co czyni EXIOM strukturalnie odpornym

**Koszt kapitałowy na tożsamość.** W przeciwieństwie do czystych ataków Sybil, gdzie tożsamości są darmowe, każdy węzeł usługowy EXIOM wymaga 200,000 XEQM zastakowanych, przy czym operator osobiście stakuje co najmniej 100,000 XEQM. Operator prowadzący 100 węzłów ma 10,000,000 XEQM kapitału zastakowanego i zablokowanego. Tworzenie dodatkowych pozornych tożsamości przez dzielenie portfeli nie redukuje tego kosztu -- każdy węzeł wciąż wymaga 100,000 XEQM stake'u operatora. Atak Sybil jest kosztowny na każdej skali.

**Tarcie unbondingu.** 14-dniowy okres unbondingu zarówno przy dobrowolnym wycofaniu, jak i wymuszonej deregistracji oznacza, że kapitał zaangażowany w węzły Sybil nie może być szybko wyciągnięty. Atakujący, który zdecyduje się wyjść, nie może zrobić tego szybciej niż jakikolwiek inny operator.

**Publiczny rejestr węzłów.** Klucz rejestracyjny każdego węzła usługowego i adres portfela operatora są publiczne. Węzeł nie może uczestniczyć w konsensusie anonimowo. Choć ludzka tożsamość stojąca za adresem portfela jest prywatna, operacyjny odcisk węzła akumuluje się z czasem przez wzorce rejestracji, czas dowodów uptime i zachowanie routingu.

---

## Jak koncentracja jest identyfikowana bez analizy grafu transakcji

Ponieważ analiza na poziomie transakcji jest niedostępna, wykrywanie koncentracji EXIOM opiera się na czterech sygnałach, które są obserwowalne z zachowania węzła, a nie z historii finansowania.

**Klastrowanie kluczy rejestracyjnych.** Węzły zarejestrowane pod tym samym kluczem portfela operatora są definitywnie tym samym operatorem. To jest deterministyczne z danych on-chain. Duży operator, który nie dzieli portfeli, jest w pełni widoczny przez sam ten sygnał. Obecne największe wdrożenia w sieci, włącznie z węzłami prowadzącymi odpowiednio 58 i 51 węzłów z pojedynczych adresów IP, to każde pojedynczy operatorzy potwierdzeni przez analizę klucza rejestracyjnego.

**Klastrowanie adresów IP i podsieci.** Obecnie podstawowy sygnał współzlokalizowania fizycznego. Wiele węzłów z tego samego adresu IP jest niemal na pewno na tym samym serwerze. Wiele węzłów z tej samej podsieci sugeruje to samo konto hostingowe lub blok centrum danych. Ten sygnał jest dostępny dzisiaj bez jakichkolwiek zmian w demonie i pozostanie jako sygnał uzupełniający po aktywacji Lokinet.

**Korelacja czasu dowodów uptime.** Sieć otrzymuje dowody uptime od każdego aktywnego węzła według regularnego harmonogramu. Rozkład czasowy przybyć tych dowodów jest rejestrowany przez węzły odbierające. Węzły działające na tym samym fizycznym hoście lub hypervisorze VM składają dowody w charakterystycznym ciasnym oknie, zazwyczaj poniżej 10 milisekund, ponieważ współdzielą ten sam zegar systemowy i interfejs sieciowy. Klaster węzłów z różnych kluczy portfela, których dowody konsekwentnie przybywają w tym oknie, jest silnym sygnałem współdzielonej infrastruktury fizycznej, wykrywalnym bez jakichkolwiek zmian w demonie i bez aktywnego Lokinet.

Ten sygnał jest szczególnie użyteczny do identyfikacji operatorów dzielących portfele, którzy trzymają swoje węzły na współdzielonej infrastrukturze. Klucze portfeli się różnią; czas dowodów nie.

**Bliskość routingu Lokinet (dostarczana nieegzekwująca przed HF23; egzekwowana przy HF23).** Gdy Lokinet jest aktywny jako transport sieciowy, graf routingu zapewnia ciągłą mapę topologii fizycznej sieci węzłów. Węzły w tym samym obiekcie routują przez tę samą infrastrukturę nadrzędną, produkując skorelowane wybory ścieżek i podmilisekundowe opóźnienie międzywęzłowe niezależnie od ich kluczy portfela lub ogłaszanych adresów IP. To jest najbardziej solidny sygnał, ponieważ odzwierciedla fizyczną rzeczywistość sieci, której nie można zmienić konfiguracją oprogramowania bez faktycznego przeniesienia infrastruktury.

---

## Atak dzielenia portfeli w szczegółach

Najbardziej wyrafinowane podejście Sybil dostępne na EXIOM to dzielenie portfeli: rejestrowanie węzłów pod wieloma adresami portfeli finansowanymi przez warstwę transakcyjną łańcucha prywatności, aby wspólne źródło finansowania nie było widoczne. To pokonuje sygnał klastrowania kluczy rejestracyjnych, ale nie pozostałe.

Operator prowadzący 426 węzłów na 10 portfelach, wszystkie hostowane w tym samym obiekcie Contabo, jest zdemaskowany przez:

- Czas dowodów uptime: dowody ze wszystkich 426 węzłów przybywają w charakterystycznym oknie poniżej 10ms współdzielonej infrastruktury
- Analiza IP i podsieci: nawet przy wielu IP, przypisanie bloku centrum danych i ASN są współdzielone
- Bliskość Lokinet (po HF23): wszystkie 426 węzłów routuje przez ten sam szkielet Contabo niezależnie od klucza portfela

Operator prowadzący 426 węzłów na 10 portfelach, rzeczywiście rozproszonych po 10 różnych dostawcach w 10 różnych krajach, nie jest znacząco zdemaskowany przez żaden obecny sygnał. Klucze rejestracyjne się różnią, czas dowodów się różni, ponieważ infrastruktura się różni, ASN się różnią, a ścieżki Lokinet się różnią. Na poziomie protokołu wygląda to jak 10 różnych operatorów.

To jest pozostałe ryzyko Sybil na EXIOM po zastosowaniu wszystkich kontroli. Jest ograniczone w swoich konsekwencjach: deduplikacja kworum HF23 ogranicza każdy klaster bliskości do jednego miejsca w kworum na rundę niezależnie od struktury portfeli, więc nawet rozproszony operator dzielący portfele nie zyskuje nieograniczonego wpływu na konsensus. Ich dochód z nagród blokowych skaluje się z liczbą ich węzłów, co jest sprawiedliwe, ponieważ zastakowali proporcjonalny kapitał. Ich wpływ na konsensus na rundę jest ograniczony przez deduplikację klastra niezależnie od tego, ilu portfeli używają.

---

## Bieżąca metodologia monitorowania

**Lista blokująca zarządzania.** Zarządzana przez governance publiczna lista blokująca kluczy uniemożliwia zablokowanym kluczom rejestracyjnym rejestrowanie nowych węzłów. Operator, który przenosi się na nowy klucz portfela, podczas gdy oryginalny jest zablokowany, tworzy udokumentowany zapis uchylania się, a czas dowodów i zachowanie routingu nowego klucza są korelowane względem historycznego profilu zablokowanego klucza.

**Analiza grafu slotów kontrybutorów.** Sloty kontrybutorów węzła usługowego są drugorzędnym sygnałem tożsamości. Operator, który finansuje sloty kontrybutorów przez wiele własnych kluczy portfela, tworzy obserwowalny graf relacji nawet na łańcuchu prywatności, ponieważ transakcje rejestracji kontrybutorów niosą obserwowalne dane o tym, do których węzłów się przyczyniają. Operator, który konsekwentnie przyczynia się do węzłów zarejestrowanych pod portfelem A z portfeli B i C, podczas gdy te same portfele B i C rejestrują własne węzły, tworzy graf korelacji, który uzupełnia bezpośredni sygnał klastrowania kluczy rejestracyjnych.

**Monitorowanie ASN.** IP każdego aktywnego węzła mapuje się na Autonomous System Number przez publiczne dane BGP. Sieć śledzi koncentrację ASN w zbiorze aktywnych węzłów. Węzły współdzielące ASN współdzielą infrastrukturę na poziomie dostawcy i ekspozycję prawną. Wysoka koncentracja ASN jest oznaczana do przeglądu zarządczego, nawet gdy indywidualne rejestracje węzłów wydają się niepowiązane. Sygnał ASN nie identyfikuje ludzkiego operatora, ale identyfikuje domenę awarii.

Bieżący status implementacji dla wszystkich kontroli opisanych w tym dokumencie jest utrzymywany w [propozycji Limitów koncentracji węzłów](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md).

---

*Ten dokument nie stanowi porady finansowej ani prawnej. XEQM jest monetą użytkową dla platformy EXIOM, a nie produktem inwestycyjnym. Klasyfikacja tokena, status papierów wartościowych i obowiązujące regulacje różnią się w zależności od jurysdykcji. Uczestnicy powinni skonsultować się ze swoim lokalnym otoczeniem prawnym i regulacyjnym przed nabyciem lub operowaniem z XEQM. XEQM Labs nie zachęca do zakupu XEQM na podstawie spekulacyjnego wzrostu ceny.*
