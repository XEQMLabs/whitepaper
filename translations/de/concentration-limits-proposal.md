# Node-Konzentrationsgrenzen - Durchsetzung der Netzwerk-Überlebensfähigkeit
## Technischer Begleiter zum EXIOM-Tokenomics-Whitepaper
### 07/26/2026

> **Scope-Hinweis (aktualisiert Oktober 2026).** Die durchgesetzte Einheit ist das *Proximity-Cluster* (eine Gruppe von Nodes, die sich physische oder Routing-Infrastruktur teilen, erkannt über Lokinet-Routing-Proximity, Uptime-Proof-Timing und ASN), **nicht das Land**. Ein Land mit mehreren unabhängigen Einrichtungen ist nicht betroffen. Die unten stehenden Länderzahlen sind ein grober geografischer Proxy dafür, wo die Konzentration derzeit liegt, nicht das, was das Protokoll deckelt. Die Node-Zahlen in diesem Begleiter sind eine Momentaufnahme vom Juli 2026 (~672 Nodes); siehe das Whitepaper für aktuelle Netzwerksummen (943 Nodes mit Stand vom 27. September 2026). Lokinet wird in einer nicht durchsetzenden Version vor HF23 ausgeliefert, und HF23 aktiviert die Durchsetzung.

Dieses Dokument ist ein Begleiter zum EXIOM-Tokenomics-Whitepaper und setzt dessen Lektüre voraus. Das Whitepaper behandelt, was die Konzentrationskontrollen sind und warum es sie gibt. Dieses Dokument behandelt das mechanische Detail, wie jede Kontrolle funktioniert, die Testnet-Validierungsdaten hinter HF22, die präzise ökonomische Mathematik hinter dem Zero-Reward-Modifier, die Frage der Betreiberidentität auf einer Privacy-Chain und die Restrisiken, die das Protokoll nicht vollständig löst.

---

## Die aktuellen Konzentrationsdaten

| Land | Aktive Nodes |
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

Frankreich hält 492 der 672 Nodes in dieser Momentaufnahme (etwa 73% des Netzwerks), und diese Konzentration ist fast vollständig eine einzelne Contabo-Einrichtung in Grand Est, die grob 426 Nodes hält (etwa 63% des Netzwerks). Die Ländersumme ist nicht das, was das Protokoll deckelt; das Grand-Est-**Cluster** ist es. Der Überlebensfähigkeits-Schwellenwert beträgt 30% der aktiven Nodes pro Proximity-Cluster (etwa 202 Nodes bei den 672 dieser Momentaufnahme und etwa 283 bei den 943 Nodes im aktuellen Whitepaper), kontinuierlich neu berechnet, während das Netzwerk wächst. Grand Est mit grob 426 Nodes liegt mehr als doppelt so hoch wie dieser Cap.

---

## Was das für Node-Betreiber bedeutet

Dieser Abschnitt beantwortet die Frage direkt: Wie wirkt sich HF23 darauf aus, wie Sie Ihre Nodes betreiben?

**HF23 deckelt nicht nach Land und erfordert nicht einen Node pro IP, einen Node pro VPS oder einen Node pro Wallet.** Der Cap liegt bei 30% des aktiven Netzwerks pro *Proximity-Cluster* (Nodes, die sich physische oder Routing-Infrastruktur teilen). Ein Betreiber, der 10, 50 oder sogar 100 Nodes auf geteilter Infrastruktur betreibt, ist von HF23 völlig unberührt, solange sein Cluster unter diesem Schwellenwert bleibt. Sie können mehrere Nodes auf einer Maschine, einem VPS-Konto und einer Wallet betreiben. Nichts in HF23 ändert das.

**Der Zero-Reward-Modifier gilt nur für Nodes oberhalb des Caps pro Cluster (30% der aktiven Nodes).** Die ältesten registrierten Nodes in einem Cluster verdienen volle Belohnungen bis zu diesem Schwellenwert. Nur Nodes, die in einem überkonzentrierten Cluster darüber eingeordnet sind, verdienen null, und zwar nur, bis sie in ein weniger konzentriertes Cluster migriert werden.

**Die Quorum-Deduplizierung deckelt den Konsenseinfluss pro Runde, nicht die Node-Anzahl oder das Einkommen.** Ein Betreiber, der 50 Nodes auf einem VPS betreibt, verdient Blockbelohnungen auf allen 50 und verwaltet seine Infrastruktur genau wie heute. Er erhält einen Quorum-Sitz pro Cluster pro Runde statt potenziell vieler, was das beabsichtigte Ergebnis ist.

**Der richtige Ansatz für einen neuen Betreiber** besteht darin, den Node-Explorer zu prüfen, zu sehen, wo bestehende Cluster konzentriert sind, und in ein spärlich besiedeltes Cluster zu deployen. Zehn Nodes auf einem Server mit eigenem, eigenständigem Routing funktionieren unter HF23 völlig einwandfrei, weil dieses Cluster nirgends in der Nähe des 30%-Schwellenwerts liegt. Volle Belohnungen, volle Quorum-Teilnahme, keine Probleme.

**Die Dynamik arbeitet zu Ihren Gunsten, wenn Sie in spärliche Regionen deployen.** Wenn eine Region sich schließlich füllt, zeigt der Node-Explorer dies, und Betreiber haben einen finanziellen Anreiz, umzuziehen, bevor der Cap sie betrifft. Betreiber, die zuerst dort waren, behalten volle Belohnungen auf ihren ältesten Nodes bis zum Schwellenwert. Neue Registrierungen in ein überkonzentriertes Cluster verdienen sofort nichts, sodass die Ökonomie neue Deployments auf natürliche Weise in Richtung leichterer Regionen drängt.

**Das spezifische Problem, das HF23 löst,** ist eine Einrichtung in Frankreich (das Grand-Est-Contabo-Cluster), die grob 426 Nodes hostet, etwa 63% des Netzwerks in dieser Momentaufnahme. Wenn diese Einrichtung offline geht, stoppt das Netzwerk. Das Ziel ist, dieses Cluster unter den 30%-Cap zu bringen. Jeder andere Betreiber, der ein verantwortungsvolles Multi-Node-Setup in einem nicht konzentrierten Cluster betreibt, ist genau das, wovon das Netzwerk mehr braucht.

---

## Warum die Hard Forks getrennt sind

HF22 wird nach erfolgreichem Testen ausgeliefert. Die Wallet-Key-Quorum-Deduplizierung und die Vereinheitlichung der Unbonding-Periode haben keine Abhängigkeit von Lokinet. Beide wurden im Testnet validiert, und sie zurückzuhalten, während die Lokinet-Bewertung noch aussteht, ist eine ungerechtfertigte Verzögerung. Ein ausgeklügelter Akteur, der das Whitepaper liest, bevor HF22 ausgeliefert wird, könnte Wallet-Splitting versuchen, um der Quorum-Kontrolle zuvorzukommen, aber dies ist durch Uptime-Proof-Timing-Korrelation und IP-/ASN-Analyse erkennbar und erzeugt einen dokumentierten Datensatz für Governance-Maßnahmen.

Lokinet wird zuerst in einer eigenen nicht durchsetzenden Version ausgeliefert (zusammen mit der SQLite-Light-Node-Speicheränderung), sodass der neue Transport nicht im Moment seiner Einführung konsenskritisch gemacht wird. Während dieser Version läuft das Proximity-Clustering live und beobachtbar ohne Belohnungskonsequenzen, was der Zeitpunkt ist, zu dem die reale Cluster-Anzahl gemessen und der HF23-Schwellenwert und -Fallback abgestimmt werden. HF23 folgt dann und aktiviert die Durchsetzung. Die Trennung der Versionen gibt außerdem saubere Failure-Domains: Wenn nach der HF23-Aktivierung etwas schiefgeht, gibt es weniger Variablen zu isolieren. Bis die HF23-Durchsetzung live ist, bleibt Grand Est dem vollen Überlebensfähigkeitsrisiko über die HF22-Quorum-Dedup hinaus ausgesetzt.

---

## HF22-Mechanik

### Wallet-Key-Quorum-Deduplizierung

Der Quorum-Auswahlalgorithmus führt vor der Finalisierung einen Deduplizierungsdurchlauf über jede Kandidatenmenge aus. Wenn die Ziehung einen Kandidaten-Node auswählt, prüft der Algorithmus dessen Betreiber-Wallet-Adresse gegen alle bereits für die Runde ausgewählten Nodes. Wird eine Übereinstimmung gefunden, wird der Kandidat ersetzt, indem erneut aus dem verbleibenden berechtigten Pool gezogen wird, unter Ausschluss aller bereits vertretenen Adressen.

Die Ersatzziehung geht nicht zurück durch bereits abgelehnte Kandidaten. Sie zieht aus dem verbleibenden nicht ausgewählten Pool in derselben wahrscheinlichkeitsgewichteten Reihenfolge, die für die erste Ziehung verwendet wurde. Dies bewahrt die statistischen Eigenschaften der Quorum-Auswahl, ohne eine deterministische Verzerrung zugunsten einer bestimmten Menge verbleibender Nodes einzuführen.

**Testnet-Validierungsergebnisse:**
- 20 Stall-/Recovery-Zyklen abgeschlossen (20/20)
- 100%ige Recovery-Rate über alle Zyklen
- Null manuelle Eingriffe in irgendeinem Zyklus erforderlich (schlechteste Blocklücke 83 Sekunden)
- Mainnet-Baseline vor HF22: 1.000 Blöcke, 100% Pulse, null GOV_SIGNED-Blöcke
- R0-Timeout-Analyse: keine R0-Timeouts unter Produktionsbedingungen eingeführt. Die Dichteanalyse des aktuellen Mainnets bestätigt, dass jedes hochdichte IP-Cluster ein einzelner Betreiber ist, was bedeutet, dass die Wallet-Key-Dedup bereits vollen Schutz gegen die aktuellen Whale-Deployments bietet. Die zwei größten Single-IP-Deployments (58 Nodes bzw. 51 Nodes) sind jeweils ein Betreiber und sind unter HF22 auf einen Quorum-Sitz pro Runde gedeckelt.

**Was ein Quorum-Sitz in der Praxis bedeutet:** Quorum-Größe und Rotationshäufigkeit bestimmen, wie oft ein Node teilnimmt. Bei der aktuellen Netzwerkgröße bedeutet ein Single-Seat-Cap, dass der Einfluss eines konzentrierten Betreibers in Oracle-Sessions, Pulse-Runden und Obligations-Quorums identisch mit dem eines Betreibers mit einem Node ist. Ihr Blockbelohnungs-Einkommen ist unverändert.

**Die Wallet-Splitting-Lücke und ihre vorläufige Erkennung:** Ein Betreiber, der 426 Nodes über 10 Wallets aufteilt, erhält bis zu 10 Quorum-Sitze pro Runde statt einem. Dies ist die bekannte Lücke, die HF23 schließt. In der Zwischenzeit ist Wallet-Splitting durch zwei bereits ohne Daemon-Änderungen verfügbare Signale erkennbar. Erstens Uptime-Proof-Timing: Nodes auf demselben physischen Host oder Hypervisor reichen Proofs innerhalb von Millisekunden voneinander ein, unabhängig vom Wallet-Key. Ein Cluster von Proofs, die in Sub-10ms-Fenstern von Nodes eintreffen, die unter verschiedenen Wallets registriert sind, ist ein starkes Signal für geteilte Infrastruktur. Zweitens IP- und ASN-Korrelation: Nodes auf verschiedenen Wallets, die sich eine IP, ein Subnetz oder ein ASN teilen, werden protokolliert und für die Governance-Überprüfung markiert. Ein Betreiber, der Wallet-Splitting betreibt, aber alle Nodes in derselben Contabo-Einrichtung behält, ist durch beide Signale identifizierbar und unter der Blocklist-Richtlinie Gegenstand von Governance-Maßnahmen.

### Vereinheitlichung der Unbonding-Periode

Die Unbonding-Periode bei erzwungener Deregistrierung ändert sich von 10.080 Blöcken (ungefähr 7 Tage) auf 20.160 Blöcke (ungefähr 14 Tage) und entspricht damit der freiwilligen Abzugsperiode. Dies ist eine Änderung einer Konsenskonstante.

Die ursprüngliche 7-tägige erzwungene Periode war eine bewusste Entscheidung während der Netzwerkstabilisierung, um die Strafe für Betreiber zu begrenzen, die Infrastrukturereignisse außerhalb ihrer Kontrolle erleben. Diese Begründung gilt nicht mehr. Das Netzwerk ist stabil, das Decommission-Credit-System bietet den Puffer für kurze Ausfälle, und eine vereinheitlichte 14-tägige Periode beseitigt eine Asymmetrie, die keine verbleibende Rechtfertigung hat.

XEQM-Coins werden während der Unbonding-Periode über die Registrierungstransaktion on-chain gesperrt. Es gibt keinen Mechanismus, um die Sperre ohne eine Protokolländerung vorzeitig freizugeben. Für dokumentierte Infrastrukturausfälle kann die Governance verpasste Belohnungen aus der Governance-Wallet als XEQM-Transfer kompensieren, aber die On-Chain-Sperre läuft unabhängig davon ihre volle Dauer.

---

## HF23-Mechanik

### Lokinet-Proximity-Clustering

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) leitet Verkehr durch das Service-Node-Netzwerk auf Layer 3 und unterstützt TCP, UDP und ICMP. Jeder Service Node nimmt als Relay teil. Der entstehende Routing-Graph spiegelt die physische Netzwerktopologie wider: Nodes an derselben Einrichtung routen durch denselben Upstream-Switch und denselben Rechenzentrums-Backbone, wodurch korrelierte Pfadauswahlen und Sub-Millisekunden-Latenz zwischen Nodes entstehen. Nodes an verschiedenen Einrichtungen routen durch verschiedene Pfade mit messbar höherer Latenz.

Der Clustering-Algorithmus nimmt paarweise Lokinet-Routing-Latenz- und Pfadüberlappungsmessungen über alle aktiven Nodes auf und gruppiert sie in Cluster, wobei diese Messungen als Proximity-Signal verwendet werden. Ein Cluster ist keine feste geografische Region; es ist eine dynamische Gruppierung von Nodes, deren Routing-Verhalten geteilte physische Infrastruktur anzeigt. Zwei Nodes an verschiedenen Contabo-Einrichtungen in verschiedenen Ländern können durch genug geteilte Contabo-Backbone-Infrastruktur routen, um im selben Cluster zu erscheinen, wenn ihre Pfadüberlappung hoch genug ist. Zwei Nodes im selben Rechenzentrum, aber auf verschiedenen physischen Maschinen mit verschiedenen Upstream-Verbindungen, erscheinen in verschiedenen Clustern, wenn ihre Pfadüberlappung gering ist.

Ergänzende Signale, die neben der Lokinet-Proximity verwendet werden:

**Uptime-Proof-Timing-Korrelation.** Das Netzwerk erhält bereits Uptime-Proofs von allen aktiven Nodes nach einem regelmäßigen Zeitplan. Die Zeitstempelverteilung der Proof-Ankünfte von jedem Node wird von den empfangenden Nodes aufgezeichnet. Nodes auf demselben physischen Host oder VM-Hypervisor reichen Proofs innerhalb eines charakteristischen engen Fensters ein, typischerweise unter 10 Millisekunden. Das Clustern dieser Ankunfts-Timing-Verteilung liefert ein Signal für physische Kollokation, das keine Daemon-Änderungen erfordert und funktioniert, bevor Lokinet aktiv ist.

**ASN-Analyse.** Die IP-Adresse jedes Nodes wird über öffentliche BGP-Daten einer Autonomous System Number zugeordnet. Nodes, die sich ein ASN teilen, teilen sich Routing-Infrastruktur auf Anbieterebene und rechtliche Exposition auf Anbieterebene. Ein Anbieter, der eine Anordnung auf Jurisdiktionsebene erhält, die seine gesamte Infrastruktur betrifft, nimmt alle seine ASN-Nodes gleichzeitig offline, unabhängig davon, in wie vielen Lokinet-Clustern sie erscheinen. ASN-Konzentration wird als ergänzendes Signal verfolgt und trägt zur Governance-Überprüfung von Betreibern nahe dem Cluster-Schwellenwert bei.

### Cluster-Registrierungs-Cap

Zum Registrierungszeitpunkt führt das Protokoll eine Proximity-Bewertung gegen alle bestehenden Cluster aus. Die Lokinet-Routing-Eigenschaften des registrierenden Nodes werden gegen den Zentroiden jedes bestehenden Clusters gemessen. Wenn das nächstgelegene Cluster bereits 30% oder mehr der aktiven Nodes enthält, wird die Registrierung mit einem spezifischen Fehlercode abgelehnt, der die Cluster-Kapazität und die Node-Anzahl des nächstgelegenen Clusters angibt.

Die Ablehnung ist deterministisch: Jeder Node, der ähnlich genug routet, um einem überkonzentrierten Cluster zugewiesen zu werden, wird abgelehnt, unabhängig vom Wallet-Key, der Registrierungshistorie oder dem Stake-Betrag des Betreibers. Der Betreiber kann die Ablehnung nicht über Governance anfechten. Der einzige Weg nach vorn ist, sich auf Infrastruktur zu registrieren, die zu einem anderen Cluster routet.

Der Schwellenwert wird gegen die aktive Node-Anzahl zum Zeitpunkt der Registrierung bewertet. Während das Netzwerk wächst, wächst der 30%-Schwellenwert in absoluten Zahlen mit. Ein Betreiber am Cap kann heute zusätzliche Nodes in einem zuvor gedeckelten Cluster registrieren, während das Netzwerk wächst und der absolute Cap steigt, ohne bestehende Nodes zu migrieren.

### Zero-Reward-Modifier

Der Zero-Reward-Modifier wird zum Zeitpunkt der Blockbelohnungsberechnung angewendet. Die Belohnungsberechnung für einen ausgewählten Node umfasst eine Cluster-Berechtigungsprüfung. Wenn das Cluster des Nodes mehr Nodes als der Cap-Schwellenwert enthält und der Registrierungsrang des Nodes innerhalb dieses Clusters über dem Schwellenwert liegt (geordnet von ältester zu neuester), gibt die Belohnungsberechnung null zurück.

Das Ranking wird aus der Registrierungs-Blockhöhe des Nodes innerhalb seiner Cluster-Zuweisung berechnet. Der älteste registrierte Node im Cluster erhält Rang 1, der zuletzt registrierte erhält Rang N. Nodes mit einem Rang größer als der Cap-Schwellenwert verdienen null. Nodes mit einem Rang bei oder unter dem Cap-Schwellenwert verdienen die volle Standardbelohnung. Das Ranking wird jedes Mal neu berechnet, wenn sich die Cluster-Zuweisung ändert, was geschieht, wenn Nodes aus dem Cluster migrieren, wenn neue Nodes beitreten oder wenn sich die Cluster-Grenze aufgrund von Änderungen der Netzwerktopologie verschiebt.

**Die ökonomische Mathematik für Grand Est:** Bei 426 Nodes mit einem 208-Node-Cap verdienen 218 Nodes null Blockbelohnungen. Bei selbst gehosteten Preisen von 0,53 $ pro Node pro Monat kosten diese 218 Nodes 115,54 $ pro Monat bei null Einkommen. Bei Pecunia-Preisen von 1,76 $ pro Node pro Monat betragen die Kosten 383,68 $ pro Monat. Der Betreiber hat zwei rationale Reaktionen: die überschüssigen Nodes in nicht konzentrierte Cluster migrieren, wodurch ihre Belohnungen sofort nach Annahme der neuen Registrierung wiederhergestellt werden, oder die überschüssigen Nodes deregistrieren und das gestakte XEQM über den Unbonding-Prozess zurückgewinnen. Beide Reaktionen reduzieren die Konzentration. Es gibt keine rationale Grundlage dafür, die überschüssigen Nodes bei null Belohnung zu halten.

**Mechanik der Schonfrist:** Beim HF23-Aktivierungsblock nimmt das Protokoll eine Momentaufnahme aller aktiven Cluster und ihrer Node-Anzahlen. Jedes Cluster, das den 30%-Schwellenwert überschreitet, wird als überkonzentriert markiert. Für 30 Tage nach dem Aktivierungsblock ist der Zero-Reward-Modifier für alle Nodes ausgesetzt, einschließlich derjenigen über dem Cap-Schwellenwert. Während der Schonfrist können Node-Besitzer die Cluster-Zuweisungen des Node-Explorers beobachten, Migrationen planen und beginnen, sie durchzuführen. Beim Ablaufblock der Schonfrist aktiviert sich der Modifier. Nodes, die bis zu diesem Block aus dem überkonzentrierten Cluster migriert sind, verdienen ab diesem Block volle Belohnungen. Nodes, die noch über dem Schwellenwert liegen, verdienen ab diesem Block null, bis sie migrieren.

### Proximity-Cluster-Quorum-Deduplizierung

Das HF23-Quorum-Deduplizierungs-Upgrade ersetzt die Wallet-Adressprüfung durch eine Cluster-Mitgliedschaftsprüfung. Wenn die Ziehung einen Kandidaten-Node auswählt, prüft der Algorithmus dessen Cluster-Zuweisung gegen alle bereits für die Runde ausgewählten Nodes. Wenn zwei Nodes eine Cluster-Zuweisung teilen, wird der zweite durch eine Ziehung aus dem verbleibenden Pool ersetzt, unter Ausschluss aller bereits vertretenen Cluster.

Die praktische Auswirkung auf einen Wallet-Splitting-Betreiber: 10 Wallet-Adressen über 426 Nodes, alle in derselben Contabo-Einrichtung, erscheinen im selben Proximity-Cluster. Die Cluster-Prüfung erfasst sie alle als eine einzige Einheit. Ein Node aus diesem Cluster hält einen Sitz. Die anderen 425 Nodes aus diesem Cluster nicht, unabhängig davon, unter wie vielen verschiedenen Wallet-Adressen sie registriert sind.

### Anforderung an die Mindest-Cluster-Anzahl und Fallback-Regel

Die Quorum-Größe des EXIOM-Netzwerks beträgt 12 Sitze pro Runde. Die Proximity-Cluster-Deduplizierung erfordert daher mindestens 12 verschiedene Proximity-Cluster in der aktiven Node-Menge, um die Quorum-Bildung zu garantieren. Wenn das Netzwerk weniger als 12 verschiedene Cluster produziert, kann der Algorithmus die Ein-Sitz-pro-Cluster-Beschränkung nicht erfüllen und die Quorum-Bildung schlägt fehl.

Die aktuelle Netzwerkverteilung, sobald das Lokinet-Proximity-Clustering angewendet wird, produziert schätzungsweise zwischen 12 und 18 verschiedene Cluster. Dies liegt unangenehm nahe am 12-Sitz-Minimum. Geteilte Anbieter-Backbone-Infrastruktur zwischen nominell separaten Einrichtungen kann dazu führen, dass zwei verschiedene IP-Standorte im Lokinet-Routing-Graphen zu einem Proximity-Cluster verschmelzen. Jede solche Verschmelzung, die die Cluster-Anzahl unter 12 senkt, bricht die Quorum-Bildung vollständig.

Der Algorithmus implementiert daher eine verpflichtende Fallback-Regel:

1. Der Algorithmus versucht, alle 12 Sitze mit einem Node pro verschiedenem Cluster zu füllen und arbeitet die verfügbaren Cluster in zufälliger Reihenfolge ab.
2. Wenn alle verschiedenen Cluster erschöpft sind, bevor 12 Sitze gefüllt sind, tritt der Algorithmus in einen Fallback-Durchlauf ein.
3. Im Fallback-Durchlauf erlaubt er einen zweiten Node aus jedem Cluster, beginnend mit den kleinsten Clustern zuerst. Die am wenigsten konzentrierten Cluster erhalten einen zweiten Sitz vor den am stärksten konzentrierten.
4. Der Algorithmus setzt die Fallback-Durchläufe fort und erhöht die maximalen Sitze pro Cluster bei jedem Durchlauf um eins, bis 12 Sitze gefüllt sind.
5. Das am stärksten konzentrierte Cluster, wie Grand Est unter den aktuellen Bedingungen, erhält zusätzliche Sitze erst, nachdem alle kleineren Cluster ihre Fallback-Zuteilung erhalten haben.

Jede Runde, die den Fallback auslöst, wird mit der Cluster-Anzahl protokolliert, die ihn verursacht hat. Die Governance überwacht die Fallback-Häufigkeit als direkten Indikator für Konzentrationsrisiken. Ein Netzwerk mit 12 oder mehr verschiedenen Clustern löst den Fallback nie aus. Ein Netzwerk, das den Fallback konsequent auslöst, signalisiert, dass die HF23-Konzentrationsdurchsetzung noch keine ausreichende physische Diversität erreicht und dass der Cluster-Cap oder die Durchsetzung der Schonfrist Aufmerksamkeit der Governance erfordert.

Das Fallback-Log wird im Node-Explorer zusammen mit den Cluster-Zuweisungen veröffentlicht, sodass die Betreiber-Community Konzentrationsrisiken in Echtzeit beobachten kann.

---

## Betreiberidentität auf einer Privacy-Chain

Das Protokoll muss nicht identifizieren, welcher menschliche Betreiber welche Nodes besitzt, um den Cluster-Cap und den Zero-Reward-Modifier durchzusetzen. Beide Kontrollen arbeiten auf Cluster-Ebene. Was bestimmt werden kann und was nicht, ist nützlicher Kontext für die Governance-Überwachung, aber für die Protokolldurchsetzung nicht erforderlich.

**Was aus On-Chain-Daten deterministisch ist:** Nodes, die unter demselben Betreiber-Wallet-Key registriert sind, sind definitiv derselbe Betreiber. Dies ist öffentliche Information in der Registrierungstransaktion.

**Was aus Lokinet- und Timing-Daten mit hoher Sicherheit ableitbar ist:** die Anzahl der verschiedenen physischen Hosts, die einem Cluster von Nodes zugrunde liegen, unabhängig davon, wie viele Wallet-Keys sie verwenden. Fünf Wallet-Keys, die jeweils 85 Nodes betreiben, alle auf denselben zwei physischen Servern, produzieren zwei verschiedene Timing-Signaturen und zwei Lokinet-Proximity-Zentroiden, nicht fünf.

**Was auf einer Privacy-Chain nicht bestimmt werden kann:** ob zwei verschiedene Wallet-Keys mit eigenständiger Infrastruktur demselben menschlichen Betreiber gehören. Die Finanzierungsquelle jedes Wallet-Keys ist durch Design privat. Ein ausgeklügelter Betreiber, der fünf Wallets verwendet, die aus fünf verschiedenen Quellen über die Transaktionsschicht der Privacy-Chain finanziert werden, präsentiert auf Protokollebene fünf verschiedene Identitäten.

Für die Durchsetzung der Überlebensfähigkeit spielt dies keine Rolle. Das Cluster enthält 426 Nodes. Die ältesten 208 verdienen Belohnungen. Die neuesten 218 verdienen null. Die Identität des Betreibers ist für diese Berechnung irrelevant.

---

## Implementierungsstatus

| Kontrolle | Status |
|---|---|
| Betreiber-Wallet-Key-Quorum-Dedup | HF22, aktiviert bei Block 219120 |
| Vereinheitlichung der Unbonding-Periode, 7 auf 14 Tage | HF22, aktiviert |
| Pulse-Stall-Recovery (Signatur-Fallback, snode_revision 1) | Aktiviert bei Block 236920, 18. Oktober 2026 |
| Lokinet-Aktivierung als Netzwerktransport | In Entwicklung; wird in einer nicht durchsetzenden Version vor HF23 ausgeliefert |
| SQLite-Light-Node-Speicher | In Entwicklung; wird mit der Lokinet-Version vor HF23 ausgeliefert |
| Proximity-Clustering-Algorithmus | Entwurfsphase, ausstehende Lokinet-Bewertung |
| Cluster-Registrierungs-Cap, 30%-Schwellenwert | HF23, Entwurfsphase |
| Zero-Reward-Modifier für überschüssige Nodes | HF23, Entwurfsphase |
| Schonfrist-Mechanismus | HF23, Entwurfsphase |
| Proximity-Cluster-Quorum-Dedup mit Fallback-Regel | HF23, Entwurfsphase |
| Überwachung der Mindest-Cluster-Anzahl und Fallback-Logging | HF23, Entwurfsphase |
| Tooling für Uptime-Proof-Timing-Korrelation | Keine Daemon-Änderungen erforderlich, Tooling in Entwicklung |
| ASN-Clustering-Ergänzung | Keine Daemon-Änderungen erforderlich, Tooling in Entwicklung |

---

## Was diese Kontrollen nicht lösen

**Rechtliche Konzentration auf Anbieterebene.** Ein Anbieter, der eine rechtliche Anordnung auf Jurisdiktionsebene erhält, die seine gesamte globale Infrastruktur betrifft, nimmt alle seine Nodes gleichzeitig offline, selbst wenn diese Nodes in mehreren Lokinet-Proximity-Clustern erscheinen. Die ASN-Analyse bringt dieses Risiko ans Licht, aber das Protokoll kann keine Anbieterdiversität durchsetzen, ohne von Betreibern die Offenlegung ihrer Anbieteridentität zu verlangen. Die durch den Cluster-Cap natürlich erzeugte geografische Verteilung mildert dieses Risiko in der Praxis erheblich, da Betreiber, die gezwungen sind, über Cluster zu verteilen, in der Praxis mehrere Anbieter verwenden werden.

**Bestimmung der menschlichen Betreiberidentität über Privacy-Chain-Wallet-Splits hinweg.** Wie oben beschrieben, kann ein ausgeklügelter Betreiber, der mehrere über die Privacy-Chain finanzierte Wallets verwendet, auf Protokollebene nicht identifiziert werden. Der Cluster-Cap und der Zero-Reward-Modifier adressieren das Failure-Domain-Risiko unabhängig von der Identität. Die Quorum-Dedup schließt in HF23 die Konsenseinfluss-Lücke. Das Restrisiko ist, dass ein ausgeklügelter Betreiber viele Nodes über viele wirklich verschiedene Cluster betreibt und Blockbelohnungs-Einkommen proportional zu seiner Node-Anzahl ansammelt, während er proportional zur Netzwerkgesundheit beiträgt. Dies ist das akzeptable Ergebnis: Konzentrierter Konsenseinfluss ist begrenzt; verteilte Kapitalbeteiligung wird belohnt.

Betreiber mit Fragen zur Cluster-Zuweisung, Migrationsplanung oder dem HF22/HF23-Zeitplan sind eingeladen, im Node-Operators-Telegram-Kanal zu posten oder ein Issue in diesem Repository zu öffnen.

---

## Verfügbare Sprachen

Community-Übersetzungen dieses Dokuments werden im Whitepaper-Repository gepflegt. Im Falle eines Konflikts zwischen einer Übersetzung und der englischen Version ist die englische Version maßgebend.

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

*Dieses Dokument stellt keine Finanz- oder Rechtsberatung dar. XEQM ist ein Utility-Coin für die EXIOM-Plattform, kein Anlageprodukt. Token-Klassifizierung, Wertpapierstatus und geltende Vorschriften variieren je nach Jurisdiktion. Teilnehmer sollten ihren lokalen rechtlichen und regulatorischen Rahmen konsultieren, bevor sie XEQM erwerben oder damit operieren. XEQM Labs ermutigt nicht zum Kauf von XEQM auf Basis spekulativer Preissteigerungen.*
