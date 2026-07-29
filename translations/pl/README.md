# XEQM Labs - Platforma EXIOM
## Biała Księga Tokenomii
### Wersja robocza v11 | 26.07.2026

> *To tłumaczenie zostało wykonane przy użyciu narzędzi do tłumaczenia AI. Jest udostępnione wyłącznie w celach informacyjnych. W przypadku jakiegokolwiek konfliktu lub niejednoznaczności między tym tłumaczeniem a angielskim oryginałem, wersja angielska jest wiążąca. Angielska wersja jest dostępna na [github.com/XEQMLabs/whitepaper](https://github.com/XEQMLabs/whitepaper).*

---

## Co Jest Aktywne Dziś vs. Co Jest Planowane

| Komponent | Status |
|---|---|
| Sieć główna EXIOM | Aktywna, działa od 6 maja 2026 |
| Sieć węzłów usługowych | Aktywna, 693 aktywne węzły, 184 operatorów (lipiec 2026) |
| Lokinet (LLARP) | Obecny w bazie kodu, status aktywacji w ocenie inżynieryjnej |
| Wymiana monet XEQ na XEQM | Dostarczona i zamknięta, 35-dniowe działanie produkcyjne, publiczna audytowalna księga |
| Portfel GUI | Aktywny, github.com/XEQMLabs/XEQMLabs-GUI |
| Eksplorator węzłów | Aktywny, aktywne monitorowanie węzłów usługowych |
| API programisty EXIOM | W trakcie rozwoju, Faza 2 (AKTYWNA) |
| Wyrocznia prywatności EXIOM | Zaprojektowana, przed implementacją, Faza 3 |
| Platforma handlowa RFQ EXIOM | W trakcie rozwoju, Faza 2/3, pierwsza para XEQM/BTC |
| HF22, deduplikacja kworum i unifikacja odblokowania | Wchodzi do testnetu, zatwierdzone, brak zależności od Lokinetu |
| HF23, limit klastra zbliżeniowego, modyfikator nagrody, transport Lokinet | Faza projektowania, oczekiwanie na ocenę inżynieryjną Lokinetu |
| Formalne zarządzanie on-chain | Planowane, Faza 6 |

---

## 1. Czym Jest XEQM Labs

XEQM Labs to firma zajmująca się technologią prywatności. Jej flagowy produkt, EXIOM, to sieć Layer 1 Proof-of-Stake zachowująca prywatność i komercyjna platforma programistyczna obsługiwana przez globalny zestaw węzłów usługowych. XEQM jest monetą dostępu i użytkowania platformy.

Projekt kontynuuje ponad siedmioletnią historię społeczności i działalności. Sieć główna EXIOM została zbudowana, aby dać tej społeczności sieć z weryfikowalną podażą, przewidywalnym harmonogramem emisji i czystym konsensusem Proof-of-Stake bez komponentu Proof-of-Work.

XEQM jest natywną monetą Layer 1, nieztokenizowaną w żadnej innej sieci, nie jest ERC-20 ani opakowanym aktywem i nie ma mostu. Posiadacze wchodzą w interakcję bezpośrednio z siecią główną EXIOM.

### Rodzina Produktów EXIOM

**Sieć Węzłów Usługowych EXIOM.** Aktywna w sieci głównej. 693 aktywne węzły u 184 niezależnych operatorów w lipcu 2026.

**Wymiana Monet EXIOM.** Komercyjny produkt umożliwiający projektom migrację ich społeczności posiadaczy ze starszej sieci do nowej sieci z pełną kryptograficzną audytowalnością. Pilotażem była migracja posiadaczy XEQ do XEQM, trwająca 35 dni z każdym zgłoszeniem przetworzonym przez kryptograficznie zweryfikowaną księgę z publicznym odciskiem SHA256.

**Prywatne API Programisty EXIOM.** W trakcie rozwoju. Platforma programistyczna udostępniająca możliwości prywatności sieci przez ustrukturyzowane API. Faza 2, aktywna.

**Wyrocznia Prywatności EXIOM.** Zaprojektowana, przed implementacją. Wyrocznia skupiona na prywatności, udowadniająca fakty dotyczące prywatnych danych internetowych bez ujawniania źródłowego. Faza 3.

**Platforma Handlowa RFQ EXIOM.** W trakcie rozwoju. Platforma handlu OTC peer-to-peer z kryptograficznymi potwierdzeniami rozliczenia, zbudowana na API EXIOM. Pierwsza para handlowa to XEQM/BTC. Faza 2/3.

XEQM Labs nie zachęca do kupowania XEQM na podstawie spekulacyjnego wzrostu cen.

---

## 2. Pochodzenie Podaży

Migracja jest zakończona. 276 917 604 XEQM zostało wyemitowanych w sieci głównej EXIOM w zamian za starsze zasoby. Ta liczba stanowi zweryfikowaną początkową podaż przy uruchomieniu sieci głównej 6 maja 2026. Każdy starszy depozyt został zarejestrowany w publicznej księdze z odciskiem SHA256. Klucze wydatkowania dla każdego portfela zaangażowanego w wymianę zostały opublikowane.

**Brak uznaniowych emisji.** Protokół nie zezwala na emisje ad hoc ani bicie poza harmonogramem.

**Brak palenia.** Architektura kryptograficzna tej sieci nie obsługuje udowodnialnego palenia. Nie będziemy przedstawiać żadnego portfela jako adresu do palenia.

---

## 3. Model Tokenomii

Sieć produkuje nowy blok co 60 sekund i przyznaje 8,25 XEQM wybranemu węzłowi usługowemu, generując 11 880 XEQM dziennie. Przy 700 aktywnych węzłach każdy węzeł zarabia około 17,0 XEQM dziennie lub 516 XEQM miesięcznie.

Skarbiec otrzymuje około 17 857 XEQM dziennie. To budżet operacyjny dla aktywnego zespołu zajmującego się tworzeniem oprogramowania komercyjnego w fazie przed przychodami.

### Alokacja Emisji

| Alokacja | Udział | Cel |
|---|---|---|
| Nagrody Węzłów Usługowych | 40% | Nagrody blokowe wypłacane bezpośrednio węzłom |
| Rozwój Głównego Protokołu | 25% | Blockchain, platforma EXIOM i usługi sieciowe |
| Marketing i Świadomość | 15% | Widoczność sieci i adopcja |
| Ekosystem i Społeczność | 10% | Dotacje, nagrody, premie społeczności |
| Bezpieczeństwo i Audyty | 5% | Audyty i przeglądy bezpieczeństwa |
| Długoterminowa Rezerwa | 5% | Stabilność i potrzeby awaryjne |

### Dystrybucja Opłat Platformy EXIOM

| Odbiorca | Udział |
|---|---|
| Operatorzy Węzłów API | 35% |
| Skarbiec XEQM Labs | 35% |
| Zarządzanie Społecznością | 30% |

---

## 4. Struktura Węzła Usługowego

| Parametr | Wartość |
|---|---|
| Wymaganie pełnego węzła | 200 000 XEQM |
| Minimalny stake operatora | 100 000 XEQM (50%) |
| Maksymalna opłata operatora | 10% |
| Okres odblokowania, dobrowolne wycofanie | 14 dni, nagrody kontynuowane |
| Okres odblokowania, wymuszone wyrejestrowanie | 14 dni, bez nagród (HF22) |
| Maksymalna liczba slotów dla uczestników | 11 (w tym operator) |
| Minimalny wkład na slot | 10 000 XEQM |

### Ekonomia Węzła

Płatny VPS za około 5,28 USD miesięcznie może obsługiwać 10 węzłów usługowych, obniżając koszt na węzeł do około 0,53 USD miesięcznie. Zarządzany hosting przez Pecunia jest dostępny za 1,76 USD na węzeł miesięcznie.

| Cena | Brutto/miesiąc | Netto: samodzielny ($0,53) | Netto: Pecunia ($1,76) | APY na 200k stake |
|---|---|---|---|---|
| $0,01547 (dziś) | $0,008 | -$0,52 | -$1,75 | 3,1% |
| $0,05 | $0,026 | -$0,50 | -$1,73 | 3,1% |
| $0,10 | $0,052 | -$0,48 | -$1,71 | 3,1% |
| $0,25 | $0,129 | -$0,40 | -$1,63 | 3,1% |
| $0,50 | $0,258 | -$0,27 | -$1,50 | 3,1% |
| $1,00 | $0,516 | -$0,01 | -$1,24 | 3,1% |
| $2,00 | $1,032 | +$0,50 | -$0,73 | 3,1% |
| $5,00 | $2,580 | +$2,05 | +$0,82 | 3,1% |

---

## 6. XEQM jako Moneta Użytkowa

| Poziom | Wymagany Stake | Wliczone Wywołania |
|---|---|---|
| Darmowy | Brak | 10 000 wywołań testnet miesięcznie |
| Builder | 1 000 XEQM | 100 000 wywołań mainnet miesięcznie |
| Produkcja | 10 000 XEQM | 1 000 000 wywołań miesięcznie, webhooki, wsparcie priorytetowe |
| Enterprise | 50 000 XEQM | Nieograniczone wywołania, niestandardowe limity szybkości, SLA |

---

## 8. Podsumowanie Parametrów

| Parametr | Wartość |
|---|---|
| Mechanizm konsensusu | 100% Proof-of-Stake |
| Czas bloku | 60 sekund |
| Nagroda za blok | 8,25 XEQM na blok |
| Dzienne emisje bloków | 11 880 XEQM |
| Emisja zarządzania | ~17 857 XEQM dziennie |
| Wymaganie pełnego węzła | 200 000 XEQM |
| Rozmiar kworum | 12 miejsc na rundę |
| Współczynnik Nakamoto (lipiec 2026) | 7 (cel: 8) |
| Główne repozytoria | github.com/XEQMLabs |

---

## Dostępne Języki

| Język | Biała Księga |
|---|---|
| English | [README.md](../../README.md) |
| Español | [../es/README.md](../es/README.md) |
| Français | [../fr/README.md](../fr/README.md) |
| Deutsch | [../de/README.md](../de/README.md) |
| 中文 | [../zh/README.md](../zh/README.md) |
| Português | [../pt/README.md](../pt/README.md) |
| Türkçe | [../tr/README.md](../tr/README.md) |
| Bahasa Indonesia | [../id/README.md](../id/README.md) |


---

*To jest dokument roboczy. Opisane tutaj parametry, harmonogramy emisji i fazy planu działania stanowią zamierzony projekt.*

*Ten dokument nie stanowi porady finansowej ani prawnej. XEQM jest monetą użytkową platformy EXIOM, a nie produktem inwestycyjnym. Klasyfikacja tokenów, status papierów wartościowych i obowiązujące przepisy różnią się w zależności od jurysdykcji. Uczestnicy powinni skonsultować się z lokalnym środowiskiem prawnym i regulacyjnym przed nabyciem lub obsługą XEQM. XEQM Labs nie zachęca do kupowania XEQM na podstawie spekulacyjnego wzrostu cen.*
