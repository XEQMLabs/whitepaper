# Knotenkonzentrationslimits - Netzwerk-Überlebensfähigkeit
## Technisches Begleitdokument zum EXIOM Tokenomics Whitepaper
### 26.07.2026

> *Diese Übersetzung wurde mit KI-Übersetzungstools erstellt. Im Konfliktfall gilt die englische Version: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

---

## Was Das für Node-Betreiber Bedeutet

HF23 erfordert **nicht** einen Node pro IP, einen Node pro VPS oder einen Node pro Wallet. Das Limit beträgt 30% des aktiven Netzwerks pro Proximity-Cluster, derzeit etwa 208 Nodes. Ein Betreiber mit 10, 50 oder 100 Nodes auf gemeinsamer Infrastruktur ist von HF23 nicht betroffen, solange sein Cluster unter diesem Schwellenwert bleibt.

Das spezifische Problem, das HF23 löst: Ein Rechenzentrum in Frankreich beherbergt derzeit etwa 426 Nodes, 61% des Netzwerks. Wenn dieses Rechenzentrum ausfällt, stoppt das Netzwerk.

---

## Aktuelle Konzentrationsdaten

| Land | Aktive Nodes |
|---|---|
| Frankreich | 492 |
| Deutschland | 70 |
| Vereinigte Staaten | 55 |
| Kanada | 18 |
| Polen | 13 |
| Vereinigtes Königreich | 10 |
| Türkei | 5 |
| Australien | 4 |
| Singapur | 2 |
| Litauen | 2 |
| Serbien | 1 |

---

## HF22 Kontrollen (Testnet, Validiert)

**Wallet-Schlüssel-Quorum-Deduplizierung.** Maximal ein Node pro Betreiber-Wallet-Adresse pro Runde. Validiert über neun Zyklen mit 100% Wiederherstellungsrate.

**Entsperrungszeitraum-Vereinheitlichung.** Erzwungene Deregistrierung von 7 auf 14 Tage verlängert.

---

## HF23 Kontrollen (Designphase)

**Cluster-Registrierungslimit.** Neue Registrierungen abgelehnt wenn ein Cluster 30% der aktiven Nodes überschreitet.

**Null-Belohnungsmodifikator.** Nodes über dem Clusterschwellenwert erhalten keine Blockbelohnungen bis zur Migration.

**Quorum-Fallback-Regel.** Quorum-Größe: 12 Sitze. Wenn weniger als 12 verschiedene Cluster existieren, erhalten kleinste Cluster zuerst zusätzliche Sitze.

---

*Für die vollständige technische Spezifikation siehe die englische Version: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

*Dieses Dokument stellt keine Finanz- oder Rechtsberatung dar. Im Konfliktfall gilt die englische Version.*
