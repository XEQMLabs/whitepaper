# XEQM Labs - EXIOM-Plattform
## Tokenomics-Whitepaper
### Entwurf v12 | 09/27/2026

---

## Was heute live ist vs. was geplant ist

| Komponente | Status |
|---|---|
| EXIOM-Mainnet | Live, in Betrieb seit 6. Mai 2026 |
| Service-Node-Netzwerk | Live — 943 aktive Service Nodes mit Stand vom 27. September 2026 |
| Lokinet (LLARP) | Wird in einer nicht durchsetzenden Version vor HF23 ausgeliefert (Transport live, Proximity-Clustering beobachtbar); HF23 aktiviert die Durchsetzung. Implementierung beginnt Q4 2026 |
| SQLite-Light-Node-Speicher | In Entwicklung; wird mit der Lokinet-Version vor HF23 ausgeliefert, für geringeren Node-Speicher und -Festplattenbedarf, mit optionalen Light Nodes für aktuelle Zeitfenster |
| XEQ-zu-XEQM-Coin-Swap | Ausgeliefert und abgeschlossen, 35-tägiger Produktionslauf, öffentlich prüfbares Ledger |
| GUI-Wallet | Live, github.com/XEQMLabs/XEQMLabs-GUI |
| Node-Explorer | Live, aktive Überwachung der Service Nodes |
| EXIOM Oracle | Live im Mainnet (Robinhood Chain, chainId 4663); 12-köpfiges Betreiber-Komitee mit Stand vom 28. September 2026 |
| EXIOM Developer API | Live in der Beta — Self-Service-Schlüssel, signierte Compliance-Claims und eine Verifizierungs-Engine, OpenAPI unter /docs; kostenlos zum Entwickeln mit vorausbezahlter Nutzung pro Aufruf im Rollout (27. September 2026) |
| EXIOM Privacy Oracle (TLSNotary / ZK) | Grundlagen live (Verifizierungs-Engine, Oracle-Sessions); vollständiges Oracle für private Webdaten in Phase 3 |
| EXIOM RFQ-Handelsplattform | In Entwicklung, Phase 2/3, XEQM/BTC als erstes Paar |
| HF22, Wallet-Key-Quorum-Dedup, Vereinheitlichung des Unbonding, Pulse-Stall-Recovery | Aktiviert bei Mainnet-Block 219120. Die Pulse-Stall-Recovery-Revision (snode_revision 1, signaturbasierter Fallback) wurde bei Block 236920 am 18. Oktober 2026 aktiviert |
| HF23, Proximity-Cluster-Cap und Reward-Modifier (Durchsetzung) | In der Entwurfsphase; aktiviert die Konzentrationsgrenzen, sobald die nicht durchsetzende Lokinet- + Light-Node-Version eingelaufen ist; angepeilt für Q4 2026 |
| Formale On-Chain-Governance | Geplant, Phase 6 |

---

## 1. Was XEQM Labs ist

XEQM Labs ist ein Unternehmen für Privacy-Technologie. Sein Flaggschiff-Produkt EXIOM ist ein datenschutzwahrendes Proof-of-Stake-Layer-1-Netzwerk und eine kommerzielle Entwicklerplattform, die von einer globalen Gruppe von Service Nodes betrieben wird. XEQM ist der Zugangs- und Nutzungs-Coin für die Plattform. Entwickler bauen kostenlos und bezahlen die Produktionsnutzung in XEQM, der verbraucht wird, während sie die API aufrufen. Service-Node-Betreiber verdienen XEQM für die Absicherung des Netzwerks, und dieselben Betreiber können zusätzliche Einnahmen erzielen, indem sie einen Oracle-Sidecar betreiben, der die Oracle-Produkte der Plattform bedient.

Das Projekt führt eine Community- und Betriebsgeschichte fort, die mehr als sieben Jahre zurückreicht. Das EXIOM-Mainnet wurde gebaut, um dieser Community ein Netzwerk mit einem verifizierbaren Angebot, einem vorhersehbaren Emissionsplan, reinem Proof-of-Stake-Konsens ohne Proof-of-Work-Komponente und Service-Node-Mechanismen zu geben, die die Zeit und das Kapital der Betreiber respektieren.

XEQM ist ein nativer Layer-1-Coin, nicht auf einer anderen Chain tokenisiert, kein ERC-20 oder Wrapped Asset und nicht gebrückt. Inhaber interagieren direkt mit dem EXIOM-Mainnet.

### Die EXIOM-Produktfamilie

**EXIOM-Service-Node-Netzwerk.** Live im Mainnet. Eine globale Gruppe von Service Nodes sichert die Chain, verdient Blockbelohnungen und bildet die Infrastrukturschicht, auf der alle anderen EXIOM-Produkte laufen. 943 aktive Service Nodes mit Stand vom 27. September 2026.

**EXIOM Coin Swap.** Ein kommerzielles Produkt, das es Projekten ermöglicht, ihre Inhaber-Community mit voller kryptografischer Prüfbarkeit von einer Legacy-Chain auf eine neue Chain zu migrieren. Der Pilot war die Migration der XEQ-Inhaber zu XEQM im EXIOM-Mainnet, die 35 Tage lief, wobei jede Einreichung über ein kryptografisch verifiziertes Ledger mit einem öffentlichen SHA256-Fingerabdruck verarbeitet wurde. Das Produkt steht anderen Projekten zur Verfügung, die eine verifizierbare Chain-Migration benötigen.

**EXIOM Oracle.** Live im Mainnet. Das erste Oracle-Produkt der Plattform: ein Komitee von XEQM-Service-Node-Betreibern — jeder betreibt einen leichtgewichtigen Oracle-Sidecar — das BLS-aggregierte, EIP-712-signierte Compliance-Attestierungen erzeugt (zum Beispiel, dass eine Adresse für eine bestimmte Jurisdiktion berechtigt ist), die Anwendungen über die Developer API konsumieren. Es ist auf der Robinhood Chain (chainId 4663) deployt und betreibt mit Stand vom 28. September 2026 ein 12-köpfiges Betreiber-Komitee. Der Betrieb des Sidecars ist die Art und Weise, wie ein Service-Node-Betreiber zusätzliche, nutzungsbasierte Einnahmen über die Blockbelohnungen hinaus erzielt.

**EXIOM Developer API.** Live in der Beta. Eine strukturierte API, die die Compliance- und Verifizierungsfähigkeiten der Plattform offenlegt — signierte Compliance-Claims und eine Verifizierungs-Engine (signierte Claims, TLSNotary und Zero-Knowledge-Mechanismen) — mit Self-Service-Zugang (eine DID plus API-Schlüssel), einer OpenAPI-3.1-Spezifikation, Webhooks und idempotenten Anfragen. Entwickler bauen kostenlos mit einem großzügigen monatlichen Kontingent und bezahlen die Produktionsnutzung in XEQM, der pro Aufruf verbraucht wird. Phase 2, aktiv.

**EXIOM Privacy Oracle.** Entworfen, Grundlagen vorhanden. Die breitere Weiterentwicklung des Oracles: das Nachweisen von Fakten über private Webdaten (via TLSNotary und Zero-Knowledge-Techniken), ohne die zugrunde liegende Quelle offenzulegen. Die Verifizierungs-Engine und die Oracle-Session-Endpunkte, die es untermauern, sind bereits live; das vollständige Oracle für private Webdaten ist ein Liefergegenstand der Phase 3. Sowohl die EXIOM-RFQ-Plattform als auch Drittanwendungen können Oracle-Outputs konsumieren.

**EXIOM RFQ-Handelsplattform.** In Entwicklung. Eine Peer-to-Peer-Over-the-Counter-Handelsplattform mit kryptografischen Settlement-Attestierungen, aufgebaut auf der EXIOM API. Das erste Handelspaar ist XEQM/BTC, beides native Layer-1-Assets ohne Tokenisierung, ohne Wrapping und ohne Bridge-Risiko. Das Oracle liefert private Preis-Attestierungen für die Preisschicht. Phase 2/3.

XEQM Labs betreibt EXIOM als kommerzielle Softwareplattform. Das Ziel sind nachhaltige Plattformeinnahmen, die die Abhängigkeit von Governance-Emissionen im Laufe der Zeit verringern. XEQM Labs ermutigt nicht zum Kauf von XEQM auf Basis spekulativer Preissteigerungen.

---

## 2. Herkunft des Angebots

Die Migration ist abgeschlossen. 276.917.604 XEQM wurden im EXIOM-Mainnet im Austausch gegen Legacy-Bestände ausgegeben. Diese Zahl ist das verifizierte Startangebot beim Mainnet-Launch am 6. Mai 2026. Jede Legacy-Einzahlung wurde in einem öffentlichen Ledger mit einem SHA256-Fingerabdruck erfasst. Die neue Chain wurde am Ende des Swaps einmalig geprägt, um genau diese verifizierte Gesamtsumme zu erreichen. Die Spend Keys für jede am Swap beteiligte Wallet wurden veröffentlicht, und jeder kann die vollständige Transaktionshistorie von der Einzahlung bis zur Auszahlung verifizieren.

Über das Startangebot hinaus gelangt neues XEQM durch zwei Emissionsströme auf Protokollebene in den Umlauf: Service-Node-Blockbelohnungen und Governance-Emissionen. Beide laufen nach festen und vorhersehbaren Plänen, die ins Protokoll geschrieben sind und die jeder aus öffentlichen Parametern berechnen kann. Raten und operative Details stehen in Abschnitt 3. Das Gesamtangebot wächst mit der Zeit. XEQM ist eine Chain mit unbegrenztem Angebot nach demselben Modell wie Moneros Tail Emission. Die Fixed-Supply-Disziplin, zu der sich das Projekt verpflichtet, bezieht sich auf das Fehlen diskretionärer Ausgaben, nicht auf eine harte Obergrenze für protokollgesteuerte Emissionen.

**Keine diskretionären Prägungen.** Das Protokoll erlaubt keine Ad-hoc-Ausgaben, manuellen Angebotsanpassungen oder planabweichenden Prägungen. Jedes neue XEQM, das in den Umlauf gelangt, tut dies über die beiden oben genannten planmäßigen Emissionsströme.

**Keine Burns.** Die kryptografische Architektur, auf der dieses Netzwerk aufbaut, unterstützt keine nachweisbaren Burns in der Weise, wie dieser Begriff üblicherweise verwendet wird. Jede Adresse, an die ein Coin gesendet wird, ist nur so unausgebbar, wie der Schlüssel nachweislich zerstört ist. Wir werden keine Wallet als Burn-Adresse darstellen. Coins, die während des Migrationsfensters nicht geswappt wurden, verbleiben auf der inaktiven Legacy-Chain und sind nicht Teil des XEQM-Angebots.

---

## 3. Tokenomics-Modell

### Block-Emissionen

Das Netzwerk produziert alle 60 Sekunden einen neuen Block und vergibt 8,25 XEQM an den ausgewählten Service Node, wodurch 11.880 XEQM pro Tag erzeugt werden. Bei 943 aktiven Nodes (27. September 2026) verdient jeder Node ungefähr 12,6 XEQM pro Tag oder etwa 380 XEQM pro Monat.

Ab HF21 werden Blockbelohnungen nach einem wöchentlichen Batching-Plan verteilt. Vor HF21 wurden Belohnungen alle 20 Blöcke ausgegeben. Belohnungen akkumulieren jetzt über jedes 10.080-Block-Fenster (ungefähr 7 Tage) und werden am Ende jedes Fensters ausgezahlt. Die Gesamtemissionsrate ist unverändert; nur die Zahlungsfrequenz hat sich verschoben.

### Governance-Emission

Die Treasury erhält ungefähr 17.857 XEQM pro Tag oder grob 124.999 XEQM pro Woche. Dies ist das Betriebsbudget für ein aktives kommerzielles Softwareentwicklungsteam. Ingenieure, Security-Reviewer, Infrastrukturbetreiber und Ökosystem-Beitragende werden aus dieser Emission vergütet, während die Plattform noch keine Einnahmen erzielt. Sobald jedes EXIOM-Produkt einen umsatzgenerierenden Status erreicht, wird die Governance-Emission überprüft und entsprechend reduziert. Das langfristige Ziel ist, dass Plattformeinnahmen die Governance-Emission als primären Finanzierungsmechanismus ersetzen.

### Emissions-Allokation

| Allokation | Anteil | Zweck |
|---|---|---|
| Service-Node-Belohnungen | 40% | Blockbelohnungen, die direkt an Service Nodes gezahlt werden |
| Kern-Protokollentwicklung | 25% | Blockchain, EXIOM-Plattform und Kern-Netzwerkdienste |
| Marketing und Bekanntheit | 15% | Netzwerksichtbarkeit und -adoption |
| Ökosystem und Community | 10% | Grants, Bounties, Community-Belohnungen, Integrationsunterstützung |
| Sicherheit und Audits | 5% | Audits, Security-Reviews, Zuverlässigkeitstests |
| Langfristige Reserve | 5% | Stabilität, Notfallbedarf, langfristiger Betrieb |

### EXIOM-Plattformeinnahmen und -verteilung

Über die Blockbelohnungen hinaus erzielt die Plattform Einnahmen aus der Entwicklernutzung. Der Zugang ist vorausbezahlt: Ein Entwickler füllt sein Konto auf, indem er XEQM einzahlt (nicht erstattungsfähig), und dieses Guthaben wird abgebaut, während er die Produktions-API nutzt, abgerechnet pro Aufruf. Entwicklung und Evaluierung auf dem kostenlosen Kontingent werden nicht berechnet.

Verbrauchtes XEQM wird als Plattformeinnahme erfasst und zwischen den Betreibern, die das Oracle bedienen, und dem Plattformbetrieb verteilt:

| Empfänger | Anteil | Zweck |
|---|---|---|
| Oracle-Sidecar-Betreiber | 70% | Service-Node-Betreiber, die den Oracle-Sidecar betreiben, belohnt im Verhältnis zu den Oracle-Aufgaben, bei deren Erfüllung sie helfen |
| Plattformbetrieb und -entwicklung | 30% | Finanziert den laufenden Betrieb und die Entwicklung und verringert im Laufe der Zeit die Abhängigkeit von Governance-Emissionen |

Betreiber nehmen den Großteil, weil sie die Infrastruktur betreiben, die das Oracle bedient. Das 70/30-Verhältnis ist der Ausgangswert und kann über Governance angepasst werden. Einnahmen werden in derselben wöchentlichen Frequenz wie Blockbelohnungen erfasst und verteilt — jedes 10.080-Block-Fenster (ungefähr 7 Tage), ausgerichtet am HF21-Reward-Batching — sodass ein Betreiber Blockbelohnungen und den Anteil an den Nutzungseinnahmen in einem Rhythmus erhält. Dieser Einnahmenanteil ist der Mechanismus, durch den die in Abschnitt 4 beschriebene Betreiber-Sidecar-Belohnung aus tatsächlicher Nutzung statt aus Emission finanziert wird.

Basis-Hardware zum Betrieb eines Service Nodes (und seines Oracle-Sidecars): 4 CPU-Kerne, 8 GB RAM, 100 GB SSD, 100-Mbps-Verbindung. Schwerere Privacy-Oracle-Workloads erfordern höhere Spezifikationen, behandelt in Abschnitt 10.

---

## 4. Service-Node-Struktur

### Staking-Parameter

| Parameter | Wert |
|---|---|
| Full-Node-Anforderung | 200.000 XEQM |
| Mindest-Betreiber-Stake | 100.000 XEQM (50% der vollen Anforderung) |
| Maximale Betreibergebühr | 10% |
| Unbonding-Periode, freiwilliger Abzug | 14 Tage, Belohnungen laufen weiter |
| Unbonding-Periode, erzwungene Deregistrierung | 14 Tage, keine Belohnungen (in HF22 vereinheitlicht) |
| Maximale Beitragenden-Slots | 11 (einschließlich des Betreibers) |
| Mindest-Community-Beitrag pro Slot | 10.000 XEQM |
| Community-Staker-Fenster pro Node | Bis zu 100.000 XEQM über bis zu 10 Beitragenden-Slots |

### Node-Ökonomie

Viele Cloud-VPS-Anbieter bieten eine kostenlose Service-Stufe, die den Betrieb eines Service Nodes zu null monatlichen Kosten unterstützen kann. Ein kostenpflichtiger VPS zu ungefähr 5,28 $ pro Monat kann 10 Service Nodes betreiben, wodurch die Hosting-Kosten pro Node auf grob 0,53 $ pro Monat sinken. Managed Hosting über Pecunia ist für 1,76 $ pro Node pro Monat verfügbar.

Blockbelohnungen pro Node skalieren umgekehrt zur Anzahl der aktiven Nodes: Bei 943 aktiven Service Nodes (27. September 2026) ergibt die tägliche Emission des Netzwerks von 11.880 XEQM grob 12,6 XEQM pro Node pro Tag, etwa 380 XEQM pro Monat. Da sowohl die Belohnung als auch der Stake in XEQM denominiert sind, beträgt die Blockbelohnungs-APY ungefähr 2,3% unabhängig vom Preis; Hosting ist die einzige nennenswerte wiederkehrende Kostenstelle, bei grob 0,53 $ pro Node pro Monat selbst gehostet oder 1,76 $ über Pecunia. Der Betrieb des Oracle-Sidecars (Abschnitt 10) fügt einen zweiten Einkommensstrom hinzu, der umsatzbasiert ist und mit der tatsächlichen Plattformnutzung skaliert, finanziert aus dem Entwicklerverbrauch statt aus Emission.

### Beitragenden-Ökonomie

Betreiber, die keine Infrastruktur betreiben können oder wollen, können Stake zu einem bestehenden Node über bis zu 10 Beitragenden-Slots beisteuern. Der Betreiber kann 0% bis 10% der Blockbelohnung erheben, bevor der Rest proportional unter den Beitragenden aufgeteilt wird. Beitragende tragen keine Hosting-Kosten, sodass die Nettorendite eines Beitragenden bei jedem Preispunkt die eines selbst gehosteten oder Pecunia-gehosteten Betreibers übersteigt.

### Node-Lebenszyklus

Nodes bleiben bei aufrechterhaltenem Collateral und erfüllten Leistungsanforderungen unbegrenzt aktiv. Ein Node, der aus der Compliance fällt, kann ohne Strafe behoben werden. Wird er nicht behoben, löst die erzwungene Deregistrierung eine 14-tägige Unbonding-Periode ohne Belohnungen aus. Der freiwillige Ausstieg trägt eine 14-tägige Unbonding-Periode, wobei die Belohnungen durchgehend weiterlaufen.

---

## 5. Netzwerk-Überlebensfähigkeit und Angriffsvektoren

### Überlebensfähigkeits-Anforderung

Das EXIOM-Netzwerk gibt Entwicklern Zuverlässigkeitszusagen. Ein Netzwerk, das durch einen einzigen Rechenzentrumsausfall offline genommen werden kann, kann diese Zusagen nicht machen. Das Protokoll erzwingt eine maximale Failure-Domain-Größe: Keine einzelne physische Einrichtung, kein Rechenzentrum und kein Routing-Cluster darf mehr als 30% der aktiven Nodes hosten.

Bei 943 Nodes (27. September 2026) sind 30% ungefähr 283 Nodes. Der Verlust einer einzigen Einrichtung kann höchstens 283 Nodes gleichzeitig offline nehmen und lässt mindestens 660 Nodes betriebsbereit, ausreichend, um die Blockproduktion und Quorum-Bildung ohne kaskadierende Deregistrierungen aufrechtzuerhalten. Dies ist eine technische Anforderung, keine Dezentralisierungs-Präferenz.

### Zwei Hard Forks

Die Durchsetzung der Überlebensfähigkeit wird in zwei Stufen geliefert, getrennt, um das Risiko zu reduzieren und validierte Arbeit sofort auszuliefern.

**HF22, aktiviert:** Betreiber-Wallet-Key-Quorum-Deduplizierung und Vereinheitlichung der Unbonding-Periode, plus eine Pulse-Stall-Recovery-Revision (snode_revision 1), die den früheren Proof-of-Work-Recovery-Fallback durch einen signaturbasierten ersetzt. Keine Lokinet-Abhängigkeit. Validiert durch 20 Stall-/Recovery-Zyklen mit einer 100%igen Recovery-Rate, null Eingriffen und einer schlechtesten Blocklücke von 83 Sekunden. HF22 wurde bei Mainnet-Block 219120 aktiviert; die Stall-Recovery-Revision wurde bei Block 236920 am 18. Oktober 2026 aktiviert.

**HF23, in der Entwurfsphase, angepeilt für Q4 2026:** Proximity-Cluster-Registrierungs-Cap, Zero-Reward-Modifier für überschüssige Nodes und Upgrade der Quorum-Deduplizierung von Wallet-Key auf Proximity-Cluster. Alle drei stützen sich auf den Lokinet-Routing-Graphen als Proximity-Signal. Um zu vermeiden, dass ein neuer Transport im Moment seiner Einführung konsenskritisch gemacht wird, wird Lokinet zuerst in einer separaten nicht durchsetzenden Version ausgeliefert (zusammen mit der SQLite-Light-Node-Speicheränderung), bei der das Proximity-Clustering live und beobachtbar ist, aber keine Belohnungskonsequenzen hat. HF23 aktiviert dann die Durchsetzung, nachdem diese Version eingelaufen ist und die reale Cluster-Anzahl gemessen sowie der Schwellenwert und Fallback abgestimmt wurden.

### HF22-Kontrollen

**Betreiber-Wallet-Key-Quorum-Deduplizierung.** Höchstens ein Node pro Betreiber-Wallet-Adresse darf in einer gegebenen Pulse-Runde, Oracle-Session oder einem Obligations-Quorum einen Validator-Sitz halten. Wenn eine Zufallsziehung zwei Nodes von derselben Betreiberadresse auswählt, wird der zweite durch einen Node von einem anderen Betreiber ersetzt. Blockbelohnungen sind nicht betroffen; sie werden nach Wartezeit-Reihenfolge unabhängig von der Quorum-Teilnahme zugewiesen.

Bekannte Einschränkung: wird durch Wallet-Splitting ausgehebelt. Ein Betreiber, der mehrere Wallet-Adressen verwendet, präsentiert dem Protokoll mehrere Betreiberschlüssel. HF23 schließt diese Lücke durch Proximity-Cluster-Deduplizierung.

**Vereinheitlichung der Unbonding-Periode.** Das Unbonding bei erzwungener Deregistrierung wurde von 7 Tagen auf 14 Tage verlängert und entspricht dem freiwilligen Abzug. Beide Fälle betragen nun 14 Tage.

### HF23-Kontrollen

Sobald Lokinet als Netzwerktransport aktiv ist, zeigen physisch am selben Ort befindliche Nodes charakteristische Routing-Signaturen: Sub-Millisekunden-Latenz untereinander und hohe Pfadüberlappung durch den Lokinet-Routing-Graphen. Nodes an wirklich unterschiedlichen Einrichtungen zeigen höhere Latenz und geringere Pfadüberlappung. Dieses Clustering-Signal wird aus beobachtbarem Netzwerkverhalten abgeleitet, ohne dass Betreiber ihren Anbieter oder Standort offenlegen müssen.

**Cluster-Registrierungs-Cap.** Neue Node-Registrierungen werden anhand der Lokinet-Routing-Proximity zu bestehenden Clustern bewertet. Wenn das Ziel-Cluster bereits 30% oder mehr der aktiven Nodes enthält, wird die Registrierung vom Protokoll abgelehnt.

**Zero-Reward-Modifier.** Nodes oberhalb des Cluster-Cap-Schwellenwerts verdienen null Blockbelohnungen, bis sie in ein nicht konzentriertes Cluster migriert werden. Nodes werden innerhalb jedes Clusters nach Registrierungsalter geordnet; die ältesten Nodes bis zum Cap-Schwellenwert verdienen volle Belohnungen. Jeder Node oberhalb dieses Schwellenwerts verdient null. Eine reduzierte Rate kann gegenüber VPS-Kosten gerechtfertigt werden; null kann es nicht.

Bei der HF23-Aktivierung gilt eine 30-tägige Schonfrist. Alle Nodes verdienen während der Schonfrist volle Belohnungen. Bei Ablauf aktiviert sich der Zero-Reward-Modifier auf überschüssigen Nodes.

**Proximity-Cluster-Quorum-Deduplizierung.** Hebt die HF22-Wallet-Key-Dedup auf Proximity-Cluster-Dedup an. Höchstens ein Node pro Proximity-Cluster pro Runde, unabhängig von der Wallet-Struktur. Schließt die Wallet-Splitting-Lücke.

Die Quorum-Größe beträgt 12 Sitze pro Runde. Die Dedup erfordert daher mindestens 12 verschiedene Proximity-Cluster, um ohne Fallback zu funktionieren. Angesichts der aktuellen Netzwerktopologie kann die Cluster-Anzahl bei der HF23-Aktivierung nahe an diesem Minimum liegen. Der Algorithmus implementiert einen verpflichtenden Fallback: Wenn alle verschiedenen Cluster erschöpft sind, bevor 12 Sitze gefüllt sind, werden zusätzliche Sitze zugewiesen, beginnend mit den kleinsten (am wenigsten konzentrierten) Clustern, bevor das am stärksten konzentrierte Cluster einen zweiten Sitz erhält. Die Fallback-Häufigkeit wird protokolliert und im Node-Explorer als Echtzeit-Indikator für Konzentrationsrisiken veröffentlicht. Ein Netzwerk, das den Fallback nie auslöst, hat eine ausreichende physische Diversität erreicht.

### Zusätzliche Kontrollen

**Kapitalkosten-Barriere.** Der Mindest-Betreiber-Stake von 100.000 XEQM stellt sicher, dass jeder Betreiber echtes Kapital für jeden Node einsetzt. Der Betrieb von N Nodes erfordert mindestens N x 100.000 XEQM gestakt.

**Schutz gegen Betreibergebühren-Abschöpfung.** EXIOM ist nicht dem Betreibergebühren-Abschöpfungsangriff ausgesetzt, der in einigen Service-Node-Netzwerken vorkommt, bei dem ein Betreiber einen Node mit minimalem Kapital registriert und eine 100%-Gebühr setzt, um die gesamte Blockbelohnung unabhängig vom Beitragenden-Stake abzuschöpfen. Die maximale Gebühr ist auf 10% gedeckelt, und der Mindest-Betreiber-Stake von 50% macht dies wirtschaftlich irrational.

**Timing-Analyse von Uptime-Proofs.** Nodes auf demselben physischen Host reichen Uptime-Proofs in eng korrelierten Clustern ein, erkennbar aus bestehenden Proof-Empfangsdaten ohne Daemon-Änderungen.

**ASN-Analyse.** Nodes hinter derselben Autonomous System Number teilen sich Infrastruktur auf Anbieterebene und rechtliche Exposition. ASN-Konzentration trägt zur Cluster-Zuweisung und zur Governance-Überprüfung bei.

**Governance-Blocklist.** Eine von der Governance verwaltete öffentliche Schlüssel-Blocklist verhindert, dass auf der Blocklist stehende Registrierungsschlüssel neue Nodes registrieren.

**Nakamoto-Koeffizient-Ziel.** Das Netzwerk zielt auf einen Betreiber-Koeffizienten von mindestens 8 ab. Mit Stand vom 27. September 2026 beträgt über 943 aktive Service Nodes und 204 Betreiber der Betreiber-Nakamoto-Koeffizient — die Mindestanzahl der Betreiber, die eine Mehrheit der aktiven Nodes kontrollieren — 9 und erfüllt damit das Ziel (gegenüber 7 über 184 Betreiber im Juli 2026). Die Konzentration physischer Einrichtungen ist ein separates und akuteres Problem: Eine einzelne Rechenzentrumsregion hostet nach wie vor eine Mehrheit der Nodes, was genau die Konzentration ist, die der Proximity-Cluster-Cap von HF23 aufbrechen soll.

Der vollständige Vorschlag zu Konzentrationsgrenzen befindet sich unter [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). Die Methodik zur Sybil-Resistenz befindet sich unter [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Lokinet als zukünftiger Netzwerktransport

Die Adressierungs-Infrastruktur des EXIOM-Netzwerks wird von öffentlich angekündigten IP-Adressen auf Lokinet-Adressierung migrieren. Lokinet wird zuerst in einer nicht durchsetzenden Version vor HF23 ausgeliefert (angepeilt für Q4 2026); HF23 fügt dann die Konzentrationsdurchsetzung hinzu, die den Lokinet-Routing-Graphen verwendet. Lokinet (Low Latency Anonymous Routing Protocol, LLARP) ist ein Layer-3-Onion-Routing-Protokoll, das jeglichen IP-basierten Verkehr über mehrere Service Nodes mittels Multi-Hop-Onion-Routing leitet, wobei kein einzelner Node im Pfad sowohl Ursprung als auch Ziel kennt.

Sobald Lokinet aktiv ist:

- Service Nodes werden durch ihren kryptografischen Lokinet-Identifikator statt durch eine öffentlich angekündigte IP-Adresse adressiert
- Die EXIOM Developer API wird als Hidden Service unter einer `.loki`-Adresse erreichbar sein und die Ursprungs-IP des Entwicklers vor dem API-Node verbergen
- Die RFQ-Handelsplattform wird als Hidden Service erreichbar sein und die IP-Adressen von Anforderer und LP vor der Plattform verbergen
- Die Oracle-Session-Kommunikation zwischen Prover und Verifier-Quorum wird über Lokinet geleitet, wodurch die zentralisierte Koordinator-Vertrauensannahme eliminiert wird

Lokinet wird in einer nicht durchsetzenden Version vor HF23 ausgeliefert, angepeilt für Q4 2026, wobei HF23 folgt, sobald es eingelaufen ist. Die LLARP-Codebasis ist im EXIOM-Repository vorhanden; die Implementierung von Lokinet als primärem Netzwerktransport beginnt in Q4 2026.

---

## 6. XEQM als Utility-Coin

Die Nachfrage nach XEQM kommt aus drei Quellen. Node-Staking bindet den größten Anteil des Angebots, ungefähr 68% bei den aktuellen 943 aktiven Nodes (27. September 2026). Der Entwicklerverbrauch schafft eine kontinuierliche Velocity-Schicht: Anwendungen bezahlen die Produktions-API-Nutzung in XEQM, sodass die Plattformadoption sich direkt in wiederkehrende Nachfrage nach dem Coin umsetzt. Oracle-Zugang fügt eine dritte Schicht für Konsumenten mit höherem Volumen hinzu.

Der Zugang folgt einem vorausbezahlten, nutzungsbasierten Modell statt einem Stake-to-Unlock-Gate — Entwickler müssen keinen festen Stake erwerben und sperren, um zu bauen:

| Stufe | Zugangsmodell |
|---|---|
| Free | Bauen und evaluieren kostenlos: ein großzügiges monatliches Aufruf-Kontingent, keine Einzahlung erforderlich |
| Production | Vorausbezahlte Nutzung: XEQM einzahlen und pro Aufruf bezahlen; Webhooks und höhere Limits |
| Enterprise | Individuelle Limits, SLA und Support; Volumenkonditionen |

Die Produktionsnutzung wird pro API-Aufruf gemessen und vom vorausbezahlten XEQM-Guthaben des Entwicklers abgezogen. Einzahlungen sind nicht erstattungsfähig und werden als Plattformeinnahme erfasst, während sie verbraucht werden (siehe Abschnitt 3). Ein früheres Design gatete Stufen hinter einem festen XEQM-Stake; dies wurde durch dieses vorausbezahlte Modell ersetzt, das für Entwickler einfacher und für kommerzielle APIs Standard ist.

---

## 7. Governance und Treasury

Die Governance-Wallet-Adresse und der View Key sind veröffentlicht. Jeder kann das Guthaben jederzeit verifizieren. Governance läuft derzeit über das Gründungsteam mit Community-Input über offene Telegram-Kanäle und GitHub-Diskussionen.

Treasury-Allokationen, entnommen aus der in Abschnitt 3 beschriebenen Governance-Emission:

- Kernentwicklung (25%): Engineering für die EXIOM API, das Oracle und die RFQ-Plattform
- Marketing und Bekanntheit (15%): Börsen-Listings, Content, Community-Wachstum
- Ökosystem und Community (10%): Grants, Bounties, Integrationsunterstützung
- Sicherheit und Audits (5%): Code-Audits, Security-Reviews, Penetrationstests
- Langfristige Reserve (5%): operative Stabilität und Notfallreserven

Phase 3 führt einen formalen Vorschlags- und Kommentarprozess ein. Phase 6 führt gewichtete Abstimmungen ein, bei denen Service-Node- und API-Node-Betreiber formale Rechte proportional zu Stake und Dauer der Zugehörigkeit halten.

---

## 8. Parameter-Zusammenfassung

| Parameter | Wert |
|---|---|
| Konsensmechanismus | 100% Proof-of-Stake |
| Blockzeit | 60 Sekunden |
| Blockbelohnung | 8,25 XEQM pro Block |
| Tägliche Block-Emissionen | 11.880 XEQM |
| Governance-Emission | ~17.857 XEQM pro Tag |
| Full-Node-Anforderung | 200.000 XEQM |
| Mindest-Betreiber-Stake | 100.000 XEQM (50%) |
| Maximale Betreibergebühr | 10% |
| Maximale Beitragenden-Slots | 11 (einschließlich Betreiber) |
| Mindest-Community-Beitrag | 10.000 XEQM pro Slot |
| Community-Staker-Fenster pro Node | Bis zu 100.000 XEQM über 10 Slots |
| Unbonding-Periode, freiwilliger Abzug | 14 Tage, Belohnungen laufen weiter |
| Unbonding-Periode, erzwungene Deregistrierung | 14 Tage, keine Belohnungen (HF22) |
| Gesamtangebot | 276.917.604 XEQM beim Launch, wachsend durch planmäßige Emissionen |
| Gesperrtes Angebot bei 943 Nodes (27. Sep. 2026) | ~188.600.000 XEQM (~68% des Startangebots) |
| Frei zirkulierend bei 943 Nodes | ~88.300.000 XEQM beim Startangebot, wachsend mit Emissionen |
| Solo-Betreiber-APY bei 943 Nodes | ~2,3% (nur Blockbelohnungen, wöchentlich via HF21 ausgezahlt) |
| Selbst gehostete Kosten pro Node | ~0,53 $/Monat (5,28 $/Mon. VPS, 10 Nodes) |
| Managed-Hosting-Kosten (Pecunia) | 1,76 $/Node/Monat |
| Aktive Service Nodes (27. September 2026) | 943 |
| Betreiber-Nakamoto-Koeffizient (27. Sep. 2026) | 9 — Mehrheitskontrolle; Ziel >= 8; 943 Nodes, 204 Betreiber |
| Oracle-Externaktivierung | Nakamoto >= 6 erreicht; abhängig vom Abschluss der Phase 3 |
| Quorum-Größe | 12 Sitze pro Runde |
| Quorum-Dedup, HF22 | Eine Betreiber-Wallet-Adresse pro Quorum-Sitz pro Runde |
| Quorum-Dedup, HF23 | Ein Proximity-Cluster pro Quorum-Sitz pro Runde (erfordert Lokinet) |
| Quorum-Dedup-Fallback, HF23 | Wenn weniger als 12 verschiedene Cluster existieren, erhalten die kleinsten Cluster zuerst zusätzliche Sitze vor den am stärksten konzentrierten Clustern; Fallback-Häufigkeit protokolliert und veröffentlicht |
| Netzwerk-Überlebensfähigkeits-Cap, HF23 | 30% der aktiven Nodes pro Proximity-Cluster (~283 Nodes bei aktueller Anzahl) |
| Zero-Reward-Modifier, HF23 | Null Blockbelohnungen für Nodes oberhalb des Cluster-Caps, geordnet nach Registrierungsalter |
| Kern-Repos | github.com/XEQMLabs |

---

## 9. Roadmap

**Phase 1, Netzwerkstabilisierung. ABGESCHLOSSEN.** Das Service-Node-Netzwerk wuchs auf 943 aktive Service Nodes mit Stand vom 27. September 2026 (von 693 über 184 Betreiber im Juli 2026, Nakamoto-Koeffizient 7). Der XEQ-zu-XEQM-Coin-Swap lief und wurde erfolgreich abgeschlossen.

**Phase 2, EXIOM Developer API und EXIOM Oracle. AKTIV.** Das EXIOM Oracle ist mit einem Betreiber-Komitee im Mainnet live, und die Developer API ist live in der Beta (Self-Service-Zugangsdaten, Compliance- und Verifizierungsendpunkte, OpenAPI). Verbleibende Phase-2-Arbeit: vorausbezahlte Verbrauchsabrechnung, der Betreiber-Einnahmenanteil und erste Produktionsintegrationen. Die Entwicklung der EXIOM-RFQ-Handelsplattform verläuft parallel, XEQM/BTC als erstes Handelspaar.

**Phase 3, EXIOM Privacy Oracle und RFQ-Plattform.** Das Oracle wird in Phasen ausgerollt: interner Proof of Concept, föderiertes Testnet, dann Mainnet mit internen Konsumenten. Die RFQ-Handelsplattform erreicht in dieser Phase die Produktion und verwendet das Oracle für private Preis-Attestierung auf dem XEQM/BTC-Paar. Beide sind auf der EXIOM API aufgebaut.

**Phase 4, Externer Oracle-Konsumentenzugang.** Oracle-Outputs stehen Entwicklern der Stufen Production und Enterprise sowie externen Konsumenten zur Verfügung. Der Nakamoto-Koeffizient-Schwellenwert von 6 ist bereits erreicht; die Aktivierung ist abhängig vom Abschluss der Phase 3.

**HF22, aktiviert (Mainnet-Block 219120).** Zwei Konsensänderungen ohne Lokinet-Abhängigkeit, Betreiber-Wallet-Key-Quorum-Deduplizierung (eine Betreiberadresse pro Quorum-Sitz pro Runde) und Vereinheitlichung der Unbonding-Periode (erzwungene Deregistrierung von 7 auf 14 Tage verlängert), plus eine Pulse-Stall-Recovery-Revision (snode_revision 1), die bei Block 236920 am 18. Oktober 2026 aktiviert wurde und Proof-of-Work-Recovery durch einen signaturbasierten Fallback ersetzt. Validiert über 20 Stall-/Recovery-Zyklen (100% Recovery, schlechteste Blocklücke 83 Sekunden).

**Lokinet- und Light-Node-Version, vor HF23.** Eine nicht durchsetzende Version, die Lokinet als Netzwerktransport online bringt (Proximity-Clustering live und im Node-Explorer beobachtbar, ohne Belohnungskonsequenzen) und SQLite-Light-Node-Speicher einführt (geringerer Speicher- und Festplattenbedarf pro Node, mit optionalen Light Nodes für aktuelle Zeitfenster). Diese Version läuft ein, sodass die reale Proximity-Cluster-Anzahl gemessen und der HF23-Schwellenwert und -Fallback abgestimmt werden können, bevor eine Durchsetzung in Kraft tritt.

**HF23, in der Entwurfsphase, angepeilt für Q4 2026.** Aktiviert die Durchsetzung, sobald die obige nicht durchsetzende Lokinet- und Light-Node-Version eingelaufen ist: Proximity-Cluster-Registrierungs-Cap (Registrierungen werden abgelehnt, wenn ein Cluster 30% der aktiven Nodes überschreitet); Zero-Reward-Modifier für Nodes oberhalb des Cap-Schwellenwerts, geordnet nach Registrierungsalter; Upgrade der Quorum-Deduplizierung von Wallet-Key auf Proximity-Cluster, mit einer verpflichtenden Fallback-Regel, die sicherstellt, dass die Quorum-Bildung immer möglich ist, selbst wenn weniger als 12 verschiedene Cluster existieren (die kleinsten Cluster erhalten zuerst zusätzliche Sitze vor den am stärksten konzentrierten Clustern, wobei die Fallback-Häufigkeit als Konzentrationsrisiko-Indikator protokolliert und veröffentlicht wird). Bei der Aktivierung gilt eine 30-tägige Schonfrist, bevor der Zero-Reward-Modifier in Kraft tritt.

**Phase 6, Formale Governance.** Strukturierter Vorschlagsprozess, gewichtete Abstimmungen für Betreiber, langfristiger Übergang weg von der Governance durch das Gründungsteam.

---

## 10. EXIOM Oracle

### Das erste Live-Oracle: EXIOM Oracle

Das erste Oracle-Produkt der Plattform ist im Mainnet live. Das EXIOM Oracle ist ein Komitee von XEQM-Service-Node-Betreibern — jeder betreibt einen leichtgewichtigen Oracle-Sidecar neben seinem Node — das gemeinsam BLS-aggregierte, EIP-712-signierte Attestierungen über Compliance-Fakten erzeugt, am unmittelbarsten, ob eine gegebene Adresse für eine gegebene Jurisdiktion berechtigt ist. Anwendungen konsumieren diese Attestierungen über die Developer API und können das signierte Ergebnis on-chain einreichen. Das Komitee ist auf der Robinhood Chain (chainId 4663) deployt und betreibt mit Stand vom 28. September 2026 ein 12-köpfiges Betreiber-Komitee mit einem Zweidrittel-Signierschwellenwert (8-von-12).

**Sicherheitsmodell: registrierte Menge vs. Schwellenwert.** Das EXIOM Oracle sampelt kein Komitee pro Runde. Da ein BLS-Aggregat das Gate gleich viel kostet, egal ob acht Mitglieder oder achthundert signiert haben, signiert jedes registrierte Mitglied jede Runde; das Sampeln einer Teilmenge würde nichts bringen und würde das Risiko wieder einführen, dass eine unglückliche Ziehung zufällig genug kolludierende Mitglieder enthält, um zu fälschen. Die Sicherheit reduziert sich daher auf zwei Eigenschaften der registrierten Mitgliedermenge der Größe N, beim Zweidrittel-Schwellenwert k = ceil(2N/3), den das Gate durchsetzt:

- **Fälschung** erfordert, dass ein Angreifer mindestens k registrierte Mitglieder kontrolliert — eine Kollusion und damit eine Frage der **Betreiber**-Konzentration.
- **Halt** (ein Liveness-Ausfall) erfordert, dass mindestens N - k + 1 = floor(N/3) + 1 registrierte Mitglieder gleichzeitig ausfallen — ein korrelierter Ausfall und damit eine Frage der **Infrastruktur**-Konzentration.

Dies sind die zwei Nakamoto-Koeffizienten, und sie sind Eigenschaften der registrierten Menge, nicht der breiteren Service-Node-Flotte: Die Verteilung der Flotte begrenzt den Konsens, während die Fälschungs- und Liveness-Resistenz des Oracles nur davon abhängt, wer die registrierten Sitze hält.

**Gegenwärtige Realisierung.** Mit Stand vom 28. September 2026 werden die registrierten Mitglieder alle vom Projektbetreiber betrieben, sodass der Betreiber-Koeffizient des Oracles 1 beträgt: Heute ruht seine Fälschungsresistenz auf dem Vertrauen in einen einzelnen Betreiber, nicht auf verteilter Kryptografie. Dies ist der ehrliche Ausgangszustand. Das Sicherheitsmodell ist k-von-N über unabhängige Betreiber; die Realisierung härtet sich, während sich Unabhängige einschreiben, was der Zweck des Onboardings zusätzlicher Service-Node-Betreiber als Sidecar-Mitglieder ist. Die Node-Anzahl allein hilft nicht — zusätzliche Mitglieder heben beide Koeffizienten nur insofern an, als sie unabhängige Betreiber an verschiedenen Einrichtungen sind.

**Wie Diversität durchgesetzt wird.** Da es keine Auswahl pro Runde gibt, wird Diversität bei der **Zulassung** entschieden: Ein Mitglied wird nur registriert, wenn es den Anteil jedes Betreibers unter k und den Anteil jeder Einrichtung bei oder unter floor(N/3) hält, und k wird angehoben, um ceil(2N/3) zu folgen, während die Menge wächst. Die Konzentration der registrierten Menge wird kontinuierlich überwacht und als Fälschungsmarge (k minus der Anteil des größten Betreibers) und Liveness-Marge (floor(N/3) + 1 minus der Anteil der größten Einrichtung) veröffentlicht; eine nicht positive Marge ist ein Alarm. Das Einrichtungssignal ist heute ASN und das Ankunfts-Timing von Uptime-Proofs, bei HF23 geschärft auf Lokinet-Routing-Proximity, die physische Kollokation selbst über verschiedene ASNs hinweg erkennt. Diese Verteilungsfakten sind selbst über die typisierte Fakten-Schnittstelle des Oracles attestierbar, sodass die Konzentrationsmetrik ein vom Komitee signierter Wert ist statt des Outputs eines einzelnen vertrauenswürdigen Skripts.

Der Sidecar ist bewusst leicht: Er hält nur seinen eigenen Signierschlüssel, liest die Identität seines Nodes lokal und verarbeitet niemals die Spend Keys des Betreibers. Sein Betrieb ist der Mechanismus, durch den ein Service-Node-Betreiber die in den Abschnitten 3 und 4 beschriebenen zusätzlichen, nutzungsfinanzierten Einnahmen erzielt.

### Die breitere Vision: EXIOM Privacy Oracle

Das EXIOM Privacy Oracle erlaubt es Anwendungen, authentifizierte private Daten-Feeds zu konsumieren, ohne die zugrunde liegenden Quelldaten offenzulegen. Es verwendet Zero-Knowledge-Proof-Techniken, um die Datenherkunft von Standard-HTTPS-Endpunkten nachzuweisen, wobei keine serverseitige Kooperation und keine vertrauenswürdige Hardware erforderlich ist. Es ist ein Liefergegenstand der Phase 3, der auf die Stabilisierung der API-Plattform in Phase 2 und eine Kryptografie-Beratung folgt, bevor der vollständige Aufbau beginnt.

Das Oracle ist kein Allzweck-Daten-Feed. Es ist ein Privacy-First-Oracle für Anwendungsfälle, bei denen die Daten selbst vertraulich bleiben müssen: Preisschwellen, ohne exakte Preise offenzulegen, Kontostände, ohne Zugangsdaten offenzulegen, Compliance-Attestierungen, ohne den zugrunde liegenden Datensatz offenzulegen. Die EXIOM-RFQ-Plattform ist der erste interne Konsument und verwendet es, um nachzuweisen, dass eine XEQM/BTC-Ausführung zu einem Referenzpreis oder besser erfolgte, ohne der Plattform oder der anderen Partei den exakten Preis offenzulegen.

Sobald Lokinet als Netzwerktransport aktiv ist, wird die Oracle-Session-Kommunikation zwischen dem Prover und dem Verifier-Quorum durch das Service-Node-Netzwerk onion-geroutet. Weder der Ursprung des Provers noch die Netzwerkadressen der Quorum-Nodes sind für einen einzelnen Relay-Node sichtbar, wodurch die zentralisierte Koordinator-Vertrauensannahme eliminiert wird.

### Architektur

**Prover-Schicht.** Die Anwendung oder der Nutzer, der Zugang zur privaten Datenquelle hat, nimmt an einem kryptografischen Protokoll teil, das sich auf die TLS-Antwort festlegt, ohne sie offenzulegen. Zugangsdaten und Rohdaten verlassen niemals die Kontrolle des Provers.

**Verifier-Schicht.** Ein rotierendes Quorum von Service Nodes verifiziert, dass die festgelegten Daten die angeforderte Bedingung erfüllen. Verifier-Nodes erfahren nur das Ergebnis (wahr oder falsch, über oder unter einem Schwellenwert) und sehen niemals die zugrunde liegenden Daten oder Zugangsdaten.

**Konsumenten-Schicht.** Konsumenten erhalten nur den minimalen Output: ein boolesches Ergebnis, einen Schwellenwertvergleich, eine signierte Attestierung oder einen kleinen abgeleiteten Wert. Rohdaten der Quelle werden niemals veröffentlicht.

### Phasenweiser Aufbauplan

**Phase 1, Interner Proof of Concept.** Das Gründungsteam validiert das vollständige kryptografische Protokoll von Ende zu Ende gegen eine kleine Menge von Whitelist-Quellen, ohne externe Konsumenten oder Service-Node-Teilnahme.

**Phase 2, Föderiertes Oracle-Testnet.** Freiwillige Service-Node-Betreiber mit starker Uptime-Historie treten dem Verifier-Pool im Testnet bei. Adversariales Testen der Attestierungsintegrität vor jedem Mainnet-Deployment.

**Phase 3, Mainnet-Oracle mit internen Konsumenten.** Die Oracle-Verifier-Aufgabe öffnet sich für qualifizierte Mainnet-Nodes. Outputs speisen interne EXIOM-Verträge und die RFQ-Plattform. Oracle-Gebühren beginnen zu teilnehmenden Verifier-Nodes zu fließen.

**Phase 4, Externer Konsumentenzugang.** Oracle-Outputs stehen Entwicklern der Stufen Production und Enterprise sowie externen Konsumenten zur Verfügung. Abhängig vom Abschluss der Phase 3.

### Verifier-Hardware-Anforderungen

Indikative Anforderungen: 8 CPU-Kerne, 16 GB RAM, 200 GB SSD, 500 Mbps mit niedriger Latenz. Die Standard-Basis-Hardware eines API-Nodes ist für die Oracle-Verifier-Aufgabe nicht ausreichend.

### Verifier-Belohnungen

| Einnahmequelle | Beschreibung |
|---|---|
| Blockbelohnungen | Standard-Service-Node-Blockbelohnung, unverändert |
| Plattform-Einnahmenanteil | Proportionaler Anteil an den Einnahmen aus dem Entwicklerverbrauch für Betreiber, die den Oracle-Sidecar betreiben |
| Oracle-Session-Gebühren | Gebühr pro Session von Oracle-Konsumenten, verteilt an das Verifier-Quorum |
| Oracle-Aufgaben-Bonus | Ergänzende Governance-Emission während Phasen geringen Volumens, reduziert, sobald Session-Gebühren sich selbst tragen |

---

## 11. EXIOM RFQ-Handelsplattform

Die EXIOM-RFQ-Plattform ist ein Peer-to-Peer-Over-the-Counter-Handelssystem mit kryptografischen Settlement-Attestierungen, aufgebaut auf der EXIOM API. Das erste Handelspaar ist XEQM/BTC, beides native Layer-1-Assets ohne Tokenisierung, ohne Wrapping und ohne Bridge-Risiko.

Sobald Lokinet aktiv ist, wird die RFQ-Plattform als Lokinet-Hidden-Service erreichbar sein. Weder die IP-Adresse des Anforderers noch die des LP wird für die Plattform sichtbar sein. Die Oracle-Preisschicht erlaubt es einer Gegenpartei, nachzuweisen, dass eine Ausführung zu einem Referenzpreis aus einer Whitelist-Quelle oder besser erfolgte, ohne den exakten Ausführungspreis der Plattform oder der anderen Partei offenzulegen.

Die RFQ-Anwendungsspezifikation und das Datenmodell sind vollständig. Die aktive Entwicklung verläuft in Phase 2 auf der API-Schicht. Die vollständige Produktion der Handelsplattform ist ein Liefergegenstand der Phase 3, abhängig davon, dass die EXIOM API die Produktion erreicht und das Oracle-MVP seinen internen Proof of Concept abschließt.

---

---

## Verfügbare Sprachen

Community-Übersetzungen dieses Whitepapers werden zur Vereinfachung im Translations-Ordner gepflegt. **Die englische Version ist jederzeit das einzige maßgebliche Dokument.** Übersetzungen können hinter der aktuellen englischen Revision zurückbleiben und ihre Aktualität ist nicht garantiert; im Falle eines Konflikts, einer Mehrdeutigkeit oder einer Abweichung jeglicher Art ist die englische Version maßgebend.

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

*Dies ist ein Entwurfsdokument. Die hier beschriebenen Parameter, Emissionspläne und Roadmap-Phasen sind das beabsichtigte Design. Aktualisierungen werden veröffentlicht, während sich das Netzwerk und die Plattform weiterentwickeln.*

*Dieses Dokument stellt keine Finanz- oder Rechtsberatung dar. XEQM ist ein Utility-Coin für die EXIOM-Plattform, kein Anlageprodukt. Token-Klassifizierung, Wertpapierstatus und geltende Vorschriften variieren je nach Jurisdiktion. Teilnehmer sollten ihren lokalen rechtlichen und regulatorischen Rahmen konsultieren, bevor sie XEQM erwerben oder damit operieren. XEQM Labs ermutigt nicht zum Kauf von XEQM auf Basis spekulativer Preissteigerungen.*
