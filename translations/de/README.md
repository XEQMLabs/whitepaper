# XEQM Labs - EXIOM Plattform
## Tokenomics Whitepaper
### Entwurf v11 | 26.07.2026

> *Diese Übersetzung wurde mit KI-Übersetzungstools erstellt. Sie dient nur zu Informationszwecken. Im Falle eines Konflikts oder einer Mehrdeutigkeit zwischen dieser Übersetzung und dem englischen Original gilt die englische Version. Die englische Version ist unter [github.com/XEQMLabs/whitepaper](https://github.com/XEQMLabs/whitepaper) verfügbar.*

---

## Was Heute Aktiv Ist vs. Was Geplant Ist

| Komponente | Status |
|---|---|
| EXIOM Mainnet | Aktiv, in Betrieb seit 6. Mai 2026 |
| Service-Node-Netzwerk | Aktiv, 693 aktive Nodes, 184 Betreiber (Juli 2026) |
| Lokinet (LLARP) | Im Code vorhanden, Aktivierungsstatus in technischer Bewertung |
| XEQ zu XEQM Coin-Tausch | Abgeschlossen, 35-tägiger Produktionsbetrieb, öffentlich prüfbares Ledger |
| GUI Wallet | Aktiv, github.com/XEQMLabs/XEQMLabs-GUI |
| Node-Explorer | Aktiv, aktive Service-Node-Überwachung |
| EXIOM Entwickler-API | In Entwicklung, Phase 2 (AKTIV) |
| EXIOM Privacy Oracle | Entworfen, vor der Implementierung, Phase 3 |
| EXIOM RFQ Handelsplattform | In Entwicklung, Phase 2/3, erstes Paar XEQM/BTC |
| HF22, Quorum-Deduplizierung und Entsperrungsvereinheitlichung | Betritt Testnet, validiert, keine Lokinet-Abhängigkeit |
| HF23, Proximity-Cluster-Limit, Belohnungsmodifikator, Lokinet-Transport | Designphase, ausstehende Lokinet-Technikbewertung |
| Formale On-Chain-Governance | Geplant, Phase 6 |

---

## 1. Was Ist XEQM Labs

XEQM Labs ist ein Datenschutztechnologieunternehmen. Sein Flaggschiffprodukt EXIOM ist ein datenschutzerhaltendes Proof-of-Stake Layer-1-Netzwerk und eine kommerzielle Entwicklerplattform, die von einem globalen Satz von Service-Nodes betrieben wird. XEQM ist die Zugangs- und Nutzungsmünze der Plattform.

Das Projekt trägt eine Gemeinschaft und Betriebsgeschichte von mehr als sieben Jahren fort. Das EXIOM Mainnet wurde gebaut, um dieser Gemeinschaft ein Netzwerk mit einem nachprüfbaren Angebot, einem vorhersehbaren Emissionsplan, reinem Proof-of-Stake-Konsens ohne Proof-of-Work-Komponente zu geben.

XEQM ist eine native Layer-1-Münze, nicht tokenisiert auf einer anderen Chain, kein ERC-20 oder verpacktes Asset, und nicht gebrückt. Inhaber interagieren direkt mit dem EXIOM Mainnet.

### Die EXIOM Produktfamilie

**EXIOM Service-Node-Netzwerk.** Aktiv im Mainnet. 693 aktive Nodes über 184 unabhängige Betreiber im Juli 2026.

**EXIOM Coin-Tausch.** Ein kommerzielles Produkt, das Projekten ermöglicht, ihre Inhaber-Community von einer Legacy-Chain auf eine neue Chain mit vollständiger kryptografischer Prüfbarkeit zu migrieren. Der Pilotversuch war die Migration von XEQ-Inhabern zu XEQM über 35 Tage.

**EXIOM Private Entwickler-API.** In Entwicklung. Eine Entwicklerplattform, die die Datenschutzfähigkeiten des Netzwerks über eine strukturierte API zugänglich macht. Phase 2, aktiv.

**EXIOM Privacy Oracle.** Entworfen, vor der Implementierung. Ein datenschutzorientiertes Oracle, das Fakten über private Webdaten beweist, ohne die zugrunde liegende Quelle preiszugeben. Phase 3.

**EXIOM RFQ Handelsplattform.** In Entwicklung. Eine Peer-to-Peer-OTC-Handelsplattform mit kryptografischen Abrechnungsbestätigungen. Das erste Handelspaar ist XEQM/BTC. Phase 2/3.

XEQM Labs ermutigt nicht zum Kauf von XEQM auf der Grundlage spekulativer Preissteigerungen.

---

## 2. Herkunft des Angebots

Die Migration ist abgeschlossen. 276.917.604 XEQM wurden im EXIOM Mainnet gegen Legacy-Bestände ausgegeben. Das Angebot zu Beginn beim Mainnet-Launch am 6. Mai 2026 ist damit verifiziert. Jede Legacy-Einzahlung wurde in einem öffentlichen Ledger mit einem SHA256-Fingerabdruck aufgezeichnet.

**Keine diskretionären Prägungen.** Das Protokoll erlaubt keine Ad-hoc-Ausgabe oder außerplanmäßige Prägungen.

**Kein Burning.** Die kryptografische Architektur dieses Netzwerks unterstützt keine nachweisbaren Burns. Wir werden keine Wallet als Burn-Adresse darstellen.

---

## 3. Tokenomics-Modell

Das Netzwerk produziert alle 60 Sekunden einen neuen Block und vergibt 8,25 XEQM an den ausgewählten Service-Node, was 11.880 XEQM pro Tag generiert. Mit 700 aktiven Nodes verdient jeder Node ungefähr 17,0 XEQM pro Tag oder 516 XEQM pro Monat.

Das Schatzamt erhält täglich ungefähr 17.857 XEQM. Dies ist das Betriebsbudget für das aktive Softwareentwicklungsteam während der Pre-Einnahmen-Phase.

### Emissionsaufteilung

| Zuweisung | Anteil | Zweck |
|---|---|---|
| Service-Node-Belohnungen | 40% | Block-Belohnungen direkt an Service-Nodes |
| Kern-Protokoll-Entwicklung | 25% | Blockchain, EXIOM-Plattform und Kernnetzwerkdienste |
| Marketing und Bekanntheit | 15% | Netzwerksichtbarkeit und Adoption |
| Ökosystem und Community | 10% | Zuschüsse, Prämien, Community-Belohnungen |
| Sicherheit und Audits | 5% | Audits und Sicherheitsüberprüfungen |
| Langfristige Reserve | 5% | Stabilität und Notfallbedarf |

### EXIOM Plattformgebühren-Verteilung

| Empfänger | Anteil |
|---|---|
| API-Node-Betreiber | 35% |
| XEQM Labs Schatzamt | 35% |
| Community-Governance | 30% |

---

## 4. Service-Node-Struktur

| Parameter | Wert |
|---|---|
| Vollständige Node-Anforderung | 200.000 XEQM |
| Mindest-Betreiber-Stake | 100.000 XEQM (50%) |
| Maximale Betreibergebühr | 10% |
| Entsperrungszeitraum, freiwilliger Rückzug | 14 Tage, Belohnungen laufen weiter |
| Entsperrungszeitraum, erzwungene Deregistrierung | 14 Tage, keine Belohnungen (HF22) |
| Maximale Beitrags-Slots | 11 (einschließlich Betreiber) |
| Mindestbeitrag pro Slot | 10.000 XEQM |

### Node-Wirtschaft

Ein bezahlter VPS für ca. 5,28 USD pro Monat kann 10 Service-Nodes betreiben, was die Kosten pro Node auf ca. 0,53 USD pro Monat bringt. Verwaltetes Hosting über Pecunia ist für 1,76 USD pro Node pro Monat verfügbar.

| Preis | Brutto/Monat | Netto: selbst gehostet ($0,53) | Netto: Pecunia ($1,76) | APY auf 200k Stake |
|---|---|---|---|---|
| $0,01547 (heute) | $0,008 | -$0,52 | -$1,75 | 3,1% |
| $0,05 | $0,026 | -$0,50 | -$1,73 | 3,1% |
| $0,10 | $0,052 | -$0,48 | -$1,71 | 3,1% |
| $0,25 | $0,129 | -$0,40 | -$1,63 | 3,1% |
| $0,50 | $0,258 | -$0,27 | -$1,50 | 3,1% |
| $1,00 | $0,516 | -$0,01 | -$1,24 | 3,1% |
| $2,00 | $1,032 | +$0,50 | -$0,73 | 3,1% |
| $5,00 | $2,580 | +$2,05 | +$0,82 | 3,1% |

---

## 6. XEQM als Nutzungsmünze

| Stufe | Erforderlicher Stake | Eingeschlossene Aufrufe |
|---|---|---|
| Kostenlos | Keiner | 10.000 Testnet-Aufrufe pro Monat |
| Builder | 1.000 XEQM | 100.000 Mainnet-Aufrufe pro Monat |
| Produktion | 10.000 XEQM | 1.000.000 Aufrufe pro Monat, Webhooks, Prioritätssupport |
| Enterprise | 50.000 XEQM | Unbegrenzte Aufrufe, benutzerdefinierte Ratenlimits, SLA |

---

## 8. Parameterübersicht

| Parameter | Wert |
|---|---|
| Konsensmechanismus | 100% Proof-of-Stake |
| Blockzeit | 60 Sekunden |
| Blockbelohnung | 8,25 XEQM pro Block |
| Tägliche Block-Emissionen | 11.880 XEQM |
| Governance-Emission | ~17.857 XEQM pro Tag |
| Vollständige Node-Anforderung | 200.000 XEQM |
| Quorum-Größe | 12 Sitze pro Runde |
| Nakamoto-Koeffizient (Juli 2026) | 7 (Ziel: 8) |
| Kern-Repositories | github.com/XEQMLabs |

---

## Verfügbare Sprachen

| Sprache | Whitepaper |
|---|---|
| English | [README.md](../../README.md) |
| Español | [../es/README.md](../es/README.md) |
| Français | [../fr/README.md](../fr/README.md) |
| 中文 | [../zh/README.md](../zh/README.md) |
| Português | [../pt/README.md](../pt/README.md) |
| Türkçe | [../tr/README.md](../tr/README.md) |
| Polski | [../pl/README.md](../pl/README.md) |
| Bahasa Indonesia | [../id/README.md](../id/README.md) |

---

*Dies ist ein Entwurfsdokument. Die hier beschriebenen Parameter, Emissionspläne und Roadmap-Phasen sind das beabsichtigte Design.*

*Dieses Dokument stellt keine Finanz- oder Rechtsberatung dar. XEQM ist eine Nutzungsmünze für die EXIOM-Plattform, kein Anlageprodukt. Token-Klassifizierung, Wertpapierstatus und anwendbare Vorschriften variieren je nach Gerichtsbarkeit. Teilnehmer sollten ihren lokalen Rechts- und Regulierungsrahmen konsultieren, bevor sie XEQM erwerben oder damit operieren. XEQM Labs ermutigt nicht zum Kauf von XEQM auf der Grundlage spekulativer Preissteigerungen.*
