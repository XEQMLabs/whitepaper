# Limity Koncentracji Węzłów - Egzekwowanie Odporności Sieci
## Techniczny Dokument Uzupełniający Białą Księgę Tokenomii EXIOM
### 26.07.2026

> *To tłumaczenie zostało wykonane przy użyciu narzędzi do tłumaczenia AI. W przypadku konfliktu wersja angielska jest wiążąca: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

---

## Co To Oznacza dla Operatorów Węzłów

HF23 **nie wymaga** jednego węzła na IP, jednego węzła na VPS ani jednego węzła na portfel. Limit wynosi 30% aktywnej sieci na klaster zbliżeniowy, obecnie około 208 węzłów. Operator prowadzący 10, 50 lub 100 węzłów na wspólnej infrastrukturze nie jest dotknięty przez HF23, o ile jego klaster pozostaje poniżej tego progu.

Konkretny problem, który HF23 rozwiązuje: jedna instalacja we Francji aktualnie obsługuje około 426 węzłów, stanowiących 61% sieci. Jeśli ta instalacja przejdzie w tryb offline, sieć zatrzyma się.

---

## Aktualne Dane Koncentracji

| Kraj | Aktywne węzły |
|---|---|
| Francja | 492 |
| Niemcy | 70 |
| Stany Zjednoczone | 55 |
| Kanada | 18 |
| Polska | 13 |
| Wielka Brytania | 10 |
| Turcja | 5 |
| Australia | 4 |
| Singapur | 2 |
| Litwa | 2 |
| Serbia | 1 |

---

## Kontrole HF22 (Wchodzi do Testnetu, Zatwierdzone)

**Deduplikacja kworum według klucza portfela operatora.** Co najwyżej jeden węzeł na adres portfela operatora na rundę. Zatwierdzone w dziewięciu cyklach ze 100% wskaźnikiem odzyskiwania.

**Unifikacja okresu odblokowania.** Wymuszone wyrejestrowanie przedłużone z 7 do 14 dni.

---

## Kontrole HF23 (Faza Projektowania)

**Limit rejestracji klastra.** Nowe rejestracje odrzucane gdy klaster przekracza 30% aktywnych węzłów.

**Modyfikator zerowej nagrody.** Węzły powyżej progu klastra otrzymują zerowe nagrody blokowe do czasu migracji.

**Reguła awaryjnego kworum.** Rozmiar kworum: 12 miejsc. Jeśli istnieje mniej niż 12 odrębnych klastrów, algorytm przyznaje dodatkowe miejsca zaczynając od najmniejszych klastrów.

---

*Pełną specyfikację techniczną znajdziesz w wersji angielskiej: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

*Ten dokument nie stanowi porady finansowej ani prawnej. W przypadku konfliktu wersja angielska jest wiążąca.*
