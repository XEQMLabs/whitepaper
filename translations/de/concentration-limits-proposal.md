# Node-Konzentrationsgrenzen - Durchsetzung der Netzwerküberlebensfähigkeit
## Technischer Begleittext zum EXIOM-Tokenomics-Whitepaper
### 07/26/2026

> **Hinweis zum Geltungsbereich (aktualisiert am 19. Oktober 2026).** Die durchgesetzte Einheit ist der *Proximity-Cluster* (eine Gruppe von Nodes, die physische oder Routing-Infrastruktur teilen, erkannt über Lokinet-Routing-Nähe, Uptime-Proof-Timing und ASN), **nicht das Land** und nicht das Registrierungsland eines Anbieters. Ein Land oder Anbieter mit mehreren wirklich unabhängigen Einrichtungen ist weniger ein Risiko als eine einzelne Einrichtung, die einen großen Anteil hält. Die nachstehenden Konzentrationsdaten sind eine Momentaufnahme vom 19. Oktober 2026 (893 aktive Nodes), gruppiert nach Hosting-Anbieter, dem besten verfügbaren Näherungswert vor Lokinet. Lokinet wird in einem nicht durchsetzenden Release vor HF23 ausgeliefert, und HF23 schaltet die Durchsetzung frei.

Dieses Dokument ist ein Begleittext zum EXIOM-Tokenomics-Whitepaper und setzt dessen Lektüre voraus. Das Whitepaper behandelt, was die Konzentrationskontrollen sind und warum es sie gibt. Dieses Dokument behandelt die mechanischen Details, wie jede Kontrolle funktioniert, die Testnet-Validierungsdaten hinter HF22, die genaue ökonomische Rechnung hinter dem Null-Belohnungs-Modifikator, die Frage der Betreiberidentität auf einer Privacy-Chain und die Restrisiken, die das Protokoll nicht vollständig löst.

---

## Die aktuellen Konzentrationsdaten

Gemessen am 19. Oktober 2026 bei 893 aktiven Nodes, gruppiert nach Hosting-Anbieter (ASN), was das heute vor Lokinet verfügbare Konzentrationssignal ist. Der Anbieter ist ein weitaus besserer Näherungswert für eine gemeinsame Ausfalldomäne als eine Länderkennzeichnung, da das Netzwerk und die Einrichtungen eines Unternehmens tendenziell gemeinsam ausfallen oder gemeinsam zur Abschaltung angeordnet werden.

| Anbieter (ASN) | Aktive Nodes | Anteil |
|---|---|---|
| NodeHub (AS214083) | 444 | 49.7% |
| Contabo (AS51167, plus AS40021 und Contabo Asia AS141995) | ~303 | ~34% |
| OVH (AS16276) | 62 | 6.9% |
| Oracle (AS31898) | 22 | 2.5% |
| WebNX (AS18450) | 12 | 1.3% |
| alle anderen Anbieter zusammen (12 weitere ASNs) | ~50 | ~5.6% |

NodeHub allein hält 49.7% des Netzwerks, deutlich über der Überlebensfähigkeitsobergrenze von 30% (267 Nodes bei 893 aktiven), und ein einzelnes /24-Subnetz hält 41.2%. Dieser eine Anbieter ist die Konzentration, die HF23 aufbrechen soll.

Wie es dazu kam. Pecunia, ein Hosting-Dienst, der anbot, XEQM-Nodes für Betreiber zu betreiben, platzierte die meisten seiner Nodes auf Contabo. Die Leistung von Pecunia war schlecht, und viele Betreiber sind seitdem zu NodeHub migriert. Somit hat sich die dominierende Ausfalldomäne von Contabo, das immer noch etwa ein Drittel des Netzwerks hält (ein Großteil davon die Grand-Est-Einrichtung), zu NodeHub verschoben, nun dem größten einzelnen Cluster im Netzwerk.

Ein Hinweis zu Länderzahlen. Das Registrierungsland eines Anbieters ist nicht der Ort, an dem seine Server stehen. NodeHub ist in den US registriert und Contabo ist in DE registriert, sodass eine länderbasierte Betrachtung ihre Nodes mit US und DE kennzeichnet, unabhängig vom physischen Rechenzentrum (Contabos größte XEQM-Einrichtung liegt in Grand Est, Frankreich). Das Protokoll begrenzt weder Land noch Anbieterregistrierung. Es begrenzt den Proximity-Cluster, die Menge der Nodes, die tatsächlich physische oder Routing-Infrastruktur teilen. ASN und Subnetz sind der heutige Näherungswert dafür, und HF23 ersetzt sie durch Lokinet-Routing-Nähe, die auch verschiedene Einrichtungen innerhalb eines Anbieters trennen kann. Der Schwellenwert beträgt 30% der aktiven Nodes pro Cluster (267 bei den aktuellen 893), fortlaufend neu berechnet, während das Netzwerk wächst.

---

## Was das für Node-Betreiber bedeutet

Dieser Abschnitt beantwortet die Frage direkt: Wie wirkt sich HF23 darauf aus, wie Sie Ihre Nodes betreiben?

**HF23 begrenzt nicht nach Land und erfordert nicht einen Node pro IP, einen Node pro VPS oder einen Node pro Wallet.** Die Obergrenze liegt bei 30% des aktiven Netzwerks pro *Proximity-Cluster* (Nodes, die physische oder Routing-Infrastruktur teilen). Ein Betreiber, der 10, 50 oder sogar 100 Nodes auf gemeinsam genutzter Infrastruktur betreibt, ist von HF23 völlig unberührt, solange sein Cluster unter diesem Schwellenwert bleibt. Sie können mehrere Nodes auf einer Maschine, einem VPS-Konto und einem Wallet betreiben. Nichts in HF23 ändert das.

**Der Null-Belohnungs-Modifikator gilt nur für Nodes oberhalb der Cluster-Obergrenze (30% der aktiven Nodes).** Die ältesten registrierten Nodes in einem Cluster verdienen volle Belohnungen bis zu diesem Schwellenwert. Nur Nodes, die in einem überkonzentrierten Cluster darüber eingestuft sind, verdienen null, und das nur, bis sie in einen weniger konzentrierten Cluster migriert werden.

**Die Quorum-Deduplizierung begrenzt den Konsenseinfluss pro Runde, nicht die Node-Anzahl oder das Einkommen.** Ein Betreiber, der 50 Nodes auf einem VPS betreibt, verdient Block-Belohnungen auf allen 50 und verwaltet seine Infrastruktur genau so wie heute. Er erhält einen Quorum-Sitz pro Cluster pro Runde statt potenziell vieler, was das beabsichtigte Ergebnis ist.

**Der richtige Ansatz für einen neuen Betreiber** ist, den Node-Explorer zu prüfen, zu sehen, wo bestehende Cluster konzentriert sind, und in einen schwach besiedelten Cluster zu deployen. Zehn Nodes auf einem Server mit eigenem, eigenständigem Routing funktionieren unter HF23 völlig problemlos, weil dieser Cluster weit vom 30%-Schwellenwert entfernt ist. Volle Belohnungen, volle Quorum-Teilnahme, keine Probleme.

**Die Dynamik wirkt zu Ihren Gunsten, wenn Sie in dünn besiedelte Regionen deployen.** Wenn sich eine Region irgendwann füllt, zeigt der Node-Explorer das an, und Betreiber haben einen finanziellen Anreiz, umzuziehen, bevor die Obergrenze sie betrifft. Betreiber, die zuerst dort waren, behalten volle Belohnungen auf ihren ältesten Nodes bis zum Schwellenwert. Neue Registrierungen in einen überkonzentrierten Cluster verdienen sofort nichts, sodass die Ökonomie neue Deployments natürlicherweise zu leichteren Regionen drängt.

**Das konkrete Problem, das HF23 löst,** ist ein einzelner Anbieter, NodeHub, der nun etwa die Hälfte des Netzwerks hostet (444 Nodes, 49.7%), mit Contabo an zweiter Stelle bei rund einem Drittel. Wenn NodeHubs Infrastruktur offline geht oder zur Abschaltung angeordnet wird, bleibt das Netzwerk stehen. Das Ziel ist, einen einzelnen Cluster unter die 30%-Obergrenze zu bekommen. Jeder Betreiber, der ein verantwortungsvolles Multi-Node-Setup auf einem anderen, nicht konzentrierten Anbieter oder in einer anderen Einrichtung betreibt, ist genau das, wovon das Netzwerk mehr braucht.

---

## Warum die Hard Forks getrennt sind

HF22 wird nach erfolgreichen Tests ausgeliefert. Wallet-Key-Quorum-Deduplizierung und die Vereinheitlichung der Unbonding-Periode haben keine Abhängigkeit von Lokinet. Beide wurden auf dem Testnet validiert, und sie zurückzuhalten, während die Lokinet-Bewertung aussteht, ist eine ungerechtfertigte Verzögerung. Ein versierter Akteur, der das Whitepaper liest, bevor HF22 ausgeliefert wird, könnte Wallet-Splitting versuchen, um der Quorum-Kontrolle zuvorzukommen, aber dies ist durch Korrelation des Uptime-Proof-Timings und IP-/ASN-Analyse erkennbar und erzeugt einen dokumentierten Nachweis für Governance-Maßnahmen.

Lokinet wird zuerst in einem eigenen nicht durchsetzenden Release ausgeliefert (zusammen mit der SQLite-Light-Node-Speicheränderung), sodass der neue Transport nicht in dem Moment konsenskritisch gemacht wird, in dem er eingeführt wird. Während dieses Releases läuft das Proximity-Clustering live und beobachtbar ohne Belohnungskonsequenzen, und das ist der Zeitpunkt, an dem die tatsächliche Cluster-Anzahl gemessen und der HF23-Schwellenwert und der Fallback abgestimmt werden. HF23 folgt dann und schaltet die Durchsetzung ein. Die Trennung der Releases sorgt außerdem für saubere Ausfalldomänen: Wenn nach der HF23-Aktivierung etwas schiefgeht, gibt es weniger Variablen zu isolieren. Bis die HF23-Durchsetzung live ist, bleibt Grand Est dem vollen Überlebensfähigkeitsrisiko jenseits der HF22-Quorum-Deduplizierung ausgesetzt.

---

## HF22-Mechanik

### Wallet-Key-Quorum-Deduplizierung

Der Quorum-Auswahlalgorithmus führt vor der Finalisierung einen Deduplizierungsdurchlauf über jede Kandidatenmenge aus. Wenn die Ziehung einen Kandidaten-Node auswählt, prüft der Algorithmus dessen Betreiber-Wallet-Adresse gegen alle für die Runde bereits ausgewählten Nodes. Wird eine Übereinstimmung gefunden, wird der Kandidat ersetzt, indem erneut aus dem verbleibenden berechtigten Pool gezogen wird, unter Ausschluss aller bereits vertretenen Adressen.

Die Ersatzziehung geht nicht erneut durch bereits abgelehnte Kandidaten. Sie zieht aus dem verbleibenden, nicht ausgewählten Pool in derselben wahrscheinlichkeitsgewichteten Reihenfolge, die für die ursprüngliche Ziehung verwendet wurde. Dies bewahrt die statistischen Eigenschaften der Quorum-Auswahl, ohne eine deterministische Verzerrung zugunsten einer bestimmten Menge verbleibender Nodes einzuführen.

**Testnet-Validierungsergebnisse:**
- 20 Stall-/Recovery-Zyklen abgeschlossen (20/20)
- 100% Recovery-Rate über alle Zyklen
- Null manuelle Eingriffe in irgendeinem Zyklus erforderlich (schlechtester Block-Abstand 83 Sekunden)
- Mainnet-Baseline vor HF22: 1.000 Blöcke, 100% Pulse, null GOV_SIGNED-Blöcke
- R0-Timeout-Analyse: keine R0-Timeouts unter Produktionsbedingungen eingeführt. Die Dichteanalyse des aktuellen Mainnets bestätigt, dass jeder IP-Cluster mit hoher Dichte ein einzelner Betreiber ist, was bedeutet, dass die Wallet-Key-Deduplizierung bereits vollen Schutz gegen die aktuellen Whale-Deployments bietet. Die beiden größten Single-IP-Deployments (58 Nodes bzw. 51 Nodes) sind jeweils ein Betreiber und sind unter HF22 auf einen Quorum-Sitz pro Runde begrenzt.

**Was ein Quorum-Sitz in der Praxis bedeutet:** Quorum-Größe und Rotationshäufigkeit bestimmen, wie oft ein Node teilnimmt. Bei der aktuellen Netzwerkgröße bedeutet eine Single-Seat-Obergrenze, dass der Einfluss eines konzentrierten Betreibers in Oracle-Sessions, Pulse-Runden und Obligations-Quoren identisch mit dem eines Betreibers mit einem einzigen Node ist. Ihr Block-Belohnungs-Einkommen bleibt unverändert.

**Die Wallet-Splitting-Lücke und ihre vorläufige Erkennung:** Ein Betreiber, der 426 Nodes auf 10 Wallets aufteilt, erhält bis zu 10 Quorum-Sitze pro Runde statt einem. Dies ist die bekannte Lücke, die HF23 schließt. In der Zwischenzeit ist Wallet-Splitting durch zwei Signale erkennbar, die bereits ohne Daemon-Änderungen verfügbar sind. Erstens das Uptime-Proof-Timing: Nodes auf demselben physischen Host oder Hypervisor reichen Proofs innerhalb von Millisekunden voneinander ein, unabhängig vom Wallet-Key. Ein Cluster von Proofs, die in Fenstern unter 10 ms von Nodes eintreffen, die auf verschiedene Wallets registriert sind, ist ein starkes Signal für geteilte Infrastruktur. Zweitens die IP- und ASN-Korrelation: Nodes auf verschiedenen Wallets, die eine IP, ein Subnetz oder eine ASN teilen, werden protokolliert und zur Governance-Prüfung markiert. Ein Betreiber, der Wallet-Splitting betreibt, aber alle Nodes in derselben Contabo-Einrichtung hält, ist durch beide Signale identifizierbar und unterliegt Governance-Maßnahmen nach der Blocklist-Richtlinie.

### Vereinheitlichung der Unbonding-Periode

Die Unbonding-Periode bei erzwungener Deregistrierung ändert sich von 10.080 Blöcken (etwa 7 Tage) auf 20.160 Blöcke (etwa 14 Tage) und entspricht damit der freiwilligen Rückzugsperiode. Dies ist eine Änderung einer Konsenskonstante.

Die ursprüngliche erzwungene 7-Tage-Periode war eine bewusste Entscheidung während der Netzwerkstabilisierung, um die Strafe für Betreiber zu begrenzen, die von Infrastrukturereignissen außerhalb ihrer Kontrolle betroffen sind. Diese Begründung gilt nicht mehr. Das Netzwerk ist stabil, das Decommission-Credit-System bietet den Puffer für kurze Ausfälle, und eine einheitliche 14-Tage-Periode beseitigt eine Asymmetrie, die keine verbleibende Rechtfertigung hat.

XEQM-Coins werden während der Unbonding-Periode über die Registrierungstransaktion On-Chain gesperrt. Es gibt keinen Mechanismus, um die Sperre ohne eine Protokolländerung vorzeitig freizugeben. Für dokumentierte Infrastrukturausfälle kann die Governance entgangene Belohnungen aus dem Governance-Wallet als XEQM-Transfer kompensieren, aber die On-Chain-Sperre läuft unabhängig davon ihre volle Dauer.

---

## HF23-Mechanik

### Lokinet-Proximity-Clustering

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) leitet Datenverkehr durch das Service-Node-Netzwerk auf Layer 3 und unterstützt TCP, UDP und ICMP. Jeder Service-Node nimmt als Relay teil. Der dabei entstehende Routing-Graph spiegelt die physische Netzwerktopologie wider: Nodes in derselben Einrichtung routen durch denselben Upstream-Switch und dasselbe Rechenzentrums-Backbone, was korrelierte Pfadauswahlen und Inter-Node-Latenz im Submillisekundenbereich erzeugt. Nodes in verschiedenen Einrichtungen routen über verschiedene Pfade mit messbar höherer Latenz.

Der Clustering-Algorithmus nimmt paarweise Lokinet-Routing-Latenz- und Pfadüberlappungsmessungen über alle aktiven Nodes auf und gruppiert sie in Cluster, wobei diese Messungen als Nähesignal verwendet werden. Ein Cluster ist keine feste geografische Region; er ist eine dynamische Gruppierung von Nodes, deren Routing-Verhalten geteilte physische Infrastruktur anzeigt. Zwei Nodes in verschiedenen Contabo-Einrichtungen in verschiedenen Ländern können über genügend geteilte Contabo-Backbone-Infrastruktur routen, um im selben Cluster zu erscheinen, wenn ihre Pfadüberlappung hoch genug ist. Zwei Nodes im selben Rechenzentrum, aber auf verschiedenen physischen Maschinen mit verschiedenen Upstream-Verbindungen, erscheinen in verschiedenen Clustern, wenn ihre Pfadüberlappung gering ist.

Ergänzende Signale, die neben der Lokinet-Nähe verwendet werden:

**Korrelation des Uptime-Proof-Timings.** Das Netzwerk erhält bereits Uptime-Proofs von allen aktiven Nodes nach einem regelmäßigen Zeitplan. Die Zeitstempelverteilung der Proof-Ankünfte von jedem Node wird von den empfangenden Nodes aufgezeichnet. Nodes auf demselben physischen Host oder VM-Hypervisor reichen Proofs innerhalb eines charakteristischen engen Fensters ein, typischerweise unter 10 Millisekunden. Das Clustering dieser Ankunftszeitverteilung liefert ein Signal für physische Ko-Lokation, das keine Daemon-Änderungen erfordert und funktioniert, bevor Lokinet aktiv ist.

**ASN-Analyse.** Die IP-Adresse jedes Nodes wird über öffentliche BGP-Daten einer Autonomous System Number zugeordnet. Nodes, die eine ASN teilen, teilen Routing-Infrastruktur auf Anbieterebene und rechtliches Risiko auf Anbieterebene. Ein Anbieter, der eine jurisdiktionsweite Anordnung erhält, die seine gesamte Infrastruktur betrifft, schaltet alle seine ASN-Nodes gleichzeitig ab, unabhängig davon, in wie vielen Lokinet-Clustern sie erscheinen. Die ASN-Konzentration wird als ergänzendes Signal verfolgt und trägt zur Governance-Prüfung von Betreibern nahe dem Cluster-Schwellenwert bei.

### Cluster-Registrierungsobergrenze

Zum Zeitpunkt der Registrierung führt das Protokoll eine Nähe-Bewertung gegen alle bestehenden Cluster durch. Die Lokinet-Routing-Merkmale des sich registrierenden Nodes werden gegen den Schwerpunkt jedes bestehenden Clusters gemessen. Wenn der nächstgelegene Cluster bereits 30% oder mehr der aktiven Nodes enthält, wird die Registrierung mit einem spezifischen Fehlercode abgelehnt, der die Cluster-Kapazität und die Node-Anzahl des nächstgelegenen Clusters angibt.

Die Ablehnung ist deterministisch: Jeder Node, der ähnlich genug routet, um einem überkonzentrierten Cluster zugeordnet zu werden, wird abgelehnt, unabhängig vom Wallet-Key, der Registrierungshistorie oder dem Stake-Betrag des Betreibers. Der Betreiber kann die Ablehnung nicht über die Governance anfechten. Der einzige Weg nach vorn ist, sich auf Infrastruktur zu registrieren, die zu einem anderen Cluster routet.

Der Schwellenwert wird gegen die Anzahl aktiver Nodes zum Zeitpunkt der Registrierung bewertet. Mit dem Wachstum des Netzwerks wächst der 30%-Schwellenwert in absoluten Zahlen mit. Ein Betreiber an der Obergrenze kann heute zusätzliche Nodes in einem zuvor begrenzten Cluster registrieren, während das Netzwerk wächst und die absolute Obergrenze steigt, ohne bestehende Nodes zu migrieren.

### Null-Belohnungs-Modifikator

Der Null-Belohnungs-Modifikator wird zum Zeitpunkt der Block-Belohnungsberechnung angewendet. Die Belohnungsberechnung für einen ausgewählten Node umfasst eine Cluster-Berechtigungsprüfung. Wenn der Cluster des Nodes mehr Nodes als der Obergrenzen-Schwellenwert enthält und der Registrierungsrang des Nodes innerhalb dieses Clusters über dem Schwellenwert liegt (geordnet von ältesten zu neuesten), gibt die Belohnungsberechnung null zurück.

Der Rang wird aus der Registrierungs-Blockhöhe des Nodes innerhalb seiner Cluster-Zuordnung berechnet. Der älteste registrierte Node im Cluster erhält Rang 1, der zuletzt registrierte erhält Rang N. Nodes mit einem Rang größer als der Obergrenzen-Schwellenwert verdienen null. Nodes mit einem Rang bei oder unter dem Obergrenzen-Schwellenwert verdienen die volle Standardbelohnung. Der Rang wird jedes Mal neu berechnet, wenn sich die Cluster-Zuordnung ändert, was geschieht, wenn Nodes aus dem Cluster migrieren, wenn neue Nodes beitreten oder wenn sich die Cluster-Grenze aufgrund von Änderungen der Netzwerktopologie verschiebt.

**Die ökonomische Rechnung für Grand Est:** Bei 426 Nodes mit einer Obergrenze von 208 Nodes verdienen 218 Nodes null Block-Belohnungen. Bei einem Self-Hosting-Preis von $0.53 pro Node pro Monat kosten diese 218 Nodes $115.54 pro Monat bei null Einkommen. Bei einem Pecunia-Preis von $1.76 pro Node pro Monat betragen die Kosten $383.68 pro Monat. Der Betreiber hat zwei rationale Reaktionen: die überzähligen Nodes in nicht konzentrierte Cluster migrieren, wodurch ihre Belohnungen unmittelbar bei Annahme der neuen Registrierung wiederhergestellt werden, oder die überzähligen Nodes deregistrieren und den gestakten XEQM über den Unbonding-Prozess zurückgewinnen. Beide Reaktionen reduzieren die Konzentration. Es gibt keine rationale Grundlage, die überzähligen Nodes bei null Belohnung aufrechtzuerhalten.

**Mechanik der Schonfrist:** Zum HF23-Aktivierungsblock erstellt das Protokoll eine Momentaufnahme aller aktiven Cluster und ihrer Node-Anzahlen. Jeder Cluster, der den 30%-Schwellenwert überschreitet, wird als überkonzentriert markiert. Für 30 Tage nach dem Aktivierungsblock wird der Null-Belohnungs-Modifikator für alle Nodes ausgesetzt, einschließlich derjenigen über dem Obergrenzen-Schwellenwert. Während der Schonfrist können Node-Eigentümer die Cluster-Zuordnungen des Node-Explorers beobachten, Migrationen planen und mit deren Ausführung beginnen. Am Block des Ablaufs der Schonfrist wird der Modifikator aktiviert. Nodes, die bis zu diesem Block aus dem überkonzentrierten Cluster migriert sind, verdienen ab diesem Block volle Belohnungen. Nodes, die weiterhin über dem Schwellenwert liegen, verdienen ab diesem Block null, bis sie migrieren.

### Proximity-Cluster-Quorum-Deduplizierung

Das HF23-Quorum-Deduplizierungs-Upgrade ersetzt die Wallet-Adressprüfung durch eine Cluster-Mitgliedschaftsprüfung. Wenn die Ziehung einen Kandidaten-Node auswählt, prüft der Algorithmus dessen Cluster-Zuordnung gegen alle für die Runde bereits ausgewählten Nodes. Wenn zwei Nodes eine Cluster-Zuordnung teilen, wird der zweite durch eine Ziehung aus dem verbleibenden Pool ersetzt, unter Ausschluss aller bereits vertretenen Cluster.

Die praktische Auswirkung auf einen Wallet-Splitting-Betreiber: 10 Wallet-Adressen über 426 Nodes, alle in derselben Contabo-Einrichtung, erscheinen im selben Proximity-Cluster. Die Cluster-Prüfung erfasst sie alle als eine einzige Einheit. Ein Node aus diesem Cluster hält einen Sitz. Die anderen 425 Nodes aus diesem Cluster tun es nicht, unabhängig davon, unter wie vielen verschiedenen Wallet-Adressen sie registriert sind.

### Anforderung an die Mindest-Cluster-Anzahl und Fallback-Regel

Die Quorum-Größe des EXIOM-Netzwerks beträgt 12 Sitze pro Runde. Die Proximity-Cluster-Deduplizierung erfordert daher mindestens 12 verschiedene Proximity-Cluster in der aktiven Node-Menge, um die Quorum-Bildung zu gewährleisten. Wenn das Netzwerk weniger als 12 verschiedene Cluster produziert, kann der Algorithmus die Ein-Sitz-pro-Cluster-Einschränkung nicht erfüllen, und die Quorum-Bildung schlägt fehl.

Die aktuelle Netzwerkverteilung wird, sobald das Lokinet-Proximity-Clustering angewendet wird, schätzungsweise zwischen 12 und 18 verschiedene Cluster produzieren. Dies liegt unangenehm nahe am 12-Sitze-Minimum. Geteilte Anbieter-Backbone-Infrastruktur zwischen nominell getrennten Einrichtungen kann dazu führen, dass zwei verschiedene IP-Standorte im Lokinet-Routing-Graphen zu einem Proximity-Cluster verschmelzen. Jede solche Verschmelzung, die die Cluster-Anzahl unter 12 senkt, bricht die Quorum-Bildung vollständig.

Der Algorithmus implementiert daher eine verpflichtende Fallback-Regel:

1. Der Algorithmus versucht, alle 12 Sitze mit einem Node pro verschiedenem Cluster zu füllen und arbeitet die verfügbaren Cluster in zufälliger Reihenfolge ab.
2. Wenn alle verschiedenen Cluster erschöpft sind, bevor 12 Sitze gefüllt sind, geht der Algorithmus in einen Fallback-Durchlauf über.
3. Im Fallback-Durchlauf erlaubt er einen zweiten Node aus jedem Cluster, beginnend mit den kleinsten Clustern zuerst. Die am wenigsten konzentrierten Cluster erhalten einen zweiten Sitz vor den am stärksten konzentrierten.
4. Der Algorithmus setzt die Fallback-Durchläufe fort und erhöht die maximale Anzahl Sitze pro Cluster bei jedem Durchlauf um eins, bis 12 Sitze gefüllt sind.
5. Der am stärksten konzentrierte Cluster, wie Grand Est unter den aktuellen Bedingungen, erhält zusätzliche Sitze erst, nachdem allen kleineren Clustern ihre Fallback-Zuteilung gegeben wurde.

Jede Runde, die den Fallback auslöst, wird mit der Cluster-Anzahl protokolliert, die ihn verursacht hat. Die Governance überwacht die Fallback-Häufigkeit als direkten Indikator für das Konzentrationsrisiko. Ein Netzwerk mit 12 oder mehr verschiedenen Clustern löst den Fallback nie aus. Ein Netzwerk, das den Fallback konsequent auslöst, signalisiert, dass die HF23-Konzentrationsdurchsetzung noch keine ausreichende physische Diversität erreicht und dass die Cluster-Obergrenze oder die Durchsetzung der Schonfrist Governance-Aufmerksamkeit erfordert.

Das Fallback-Protokoll wird im Node-Explorer neben den Cluster-Zuordnungen veröffentlicht, damit die Betreiber-Community das Konzentrationsrisiko in Echtzeit beobachten kann.

---

## Betreiberidentität auf einer Privacy-Chain

Das Protokoll muss nicht identifizieren, welcher menschliche Betreiber welche Nodes besitzt, um die Cluster-Obergrenze und den Null-Belohnungs-Modifikator durchzusetzen. Beide Kontrollen arbeiten auf Cluster-Ebene. Was bestimmt werden kann und was nicht, ist nützlicher Kontext für die Governance-Überwachung, aber für die Protokolldurchsetzung nicht erforderlich.

**Was aus On-Chain-Daten deterministisch ist:** Nodes, die unter demselben Betreiber-Wallet-Key registriert sind, sind definitiv derselbe Betreiber. Dies ist öffentliche Information in der Registrierungstransaktion.

**Was mit hoher Zuversicht aus Lokinet- und Timing-Daten ableitbar ist:** die Anzahl der verschiedenen physischen Hosts, die einem Cluster von Nodes zugrunde liegen, unabhängig davon, wie viele Wallet-Keys sie verwenden. Fünf Wallet-Keys, die jeweils 85 Nodes betreiben, alle auf denselben zwei physischen Servern, erzeugen zwei verschiedene Timing-Signaturen und zwei Lokinet-Proximity-Schwerpunkte, nicht fünf.

**Was auf einer Privacy-Chain nicht bestimmt werden kann:** ob zwei verschiedene Wallet-Keys mit eigenständiger Infrastruktur demselben menschlichen Betreiber gehören. Die Finanzierungsquelle jedes Wallet-Keys ist per Design privat. Ein versierter Betreiber, der fünf Wallets verwendet, die aus fünf verschiedenen Quellen über die Transaktionsschicht der Privacy-Chain finanziert werden, präsentiert auf Protokollebene fünf verschiedene Identitäten.

Für die Durchsetzung der Überlebensfähigkeit spielt dies keine Rolle. Der Cluster enthält 426 Nodes. Die ältesten 208 verdienen Belohnungen. Die neuesten 218 verdienen null. Die Identität des Betreibers ist für diese Berechnung irrelevant.

---

## Implementierungsstatus

| Kontrolle | Status |
|---|---|
| Betreiber-Wallet-Key-Quorum-Deduplizierung | HF22, aktiviert bei Block 219120 |
| Vereinheitlichung der Unbonding-Periode, 7 auf 14 Tage | HF22, aktiviert |
| Pulse-Stall-Recovery (Signatur-Fallback, snode_revision 1) | Aktiviert bei Block 236920, 18. Oktober 2026 |
| Lokinet-Aktivierung als Netzwerktransport | In Entwicklung; wird in einem nicht durchsetzenden Release vor HF23 ausgeliefert |
| SQLite-Light-Node-Speicher | In Entwicklung; wird mit dem Pre-HF23-Lokinet-Release ausgeliefert |
| Proximity-Clustering-Algorithmus | Entwurfsphase, ausstehend bis zur Lokinet-Bewertung |
| Cluster-Registrierungsobergrenze, 30%-Schwellenwert | HF23, Entwurfsphase |
| Null-Belohnungs-Modifikator für überzählige Nodes | HF23, Entwurfsphase |
| Schonfrist-Mechanismus | HF23, Entwurfsphase |
| Proximity-Cluster-Quorum-Deduplizierung mit Fallback-Regel | HF23, Entwurfsphase |
| Überwachung der Mindest-Cluster-Anzahl und Fallback-Protokollierung | HF23, Entwurfsphase |
| Werkzeuge zur Korrelation des Uptime-Proof-Timings | Keine Daemon-Änderungen erforderlich, Werkzeuge in Entwicklung |
| ASN-Clustering-Ergänzung | Keine Daemon-Änderungen erforderlich, Werkzeuge in Entwicklung |

---

## Was diese Kontrollen nicht lösen

**Rechtliche Konzentration auf Anbieterebene.** Ein Anbieter, der eine jurisdiktionsweite rechtliche Anordnung erhält, die seine gesamte globale Infrastruktur betrifft, schaltet alle seine Nodes gleichzeitig ab, selbst wenn diese Nodes in mehreren Lokinet-Proximity-Clustern erscheinen. Die ASN-Analyse bringt dieses Risiko zum Vorschein, aber das Protokoll kann Anbieterdiversität nicht durchsetzen, ohne die Offenlegung der Anbieteridentität durch den Betreiber zu verlangen. Die durch die Cluster-Obergrenze natürlicherweise erzeugte geografische Streuung mildert dieses Risiko in der Praxis erheblich, da Betreiber, die zur Verteilung über Cluster gezwungen werden, in der Praxis mehrere Anbieter nutzen werden.

**Bestimmung der menschlichen Betreiberidentität über Privacy-Chain-Wallet-Splits hinweg.** Wie oben beschrieben, kann ein versierter Betreiber, der mehrere über die Privacy-Chain finanzierte Wallets verwendet, auf Protokollebene nicht identifiziert werden. Die Cluster-Obergrenze und der Null-Belohnungs-Modifikator adressieren das Ausfalldomänen-Risiko unabhängig von der Identität. Die Quorum-Deduplizierung schließt die Lücke beim Konsenseinfluss in HF23. Das Restrisiko besteht darin, dass ein versierter Betreiber viele Nodes über viele wirklich verschiedene Cluster betreibt und Block-Belohnungs-Einkommen proportional zu seiner Node-Anzahl ansammelt, während er proportional zur Netzwerkgesundheit beiträgt. Dies ist das akzeptable Ergebnis: Der konzentrierte Konsenseinfluss ist begrenzt; die verteilte Kapitalbeteiligung wird belohnt.

Betreiber mit Fragen zur Cluster-Zuordnung, zur Migrationsplanung oder zum HF22/HF23-Zeitplan werden ermutigt, im Node Operators Telegram-Kanal zu posten oder ein Issue in diesem Repository zu eröffnen.

---

## Verfügbare Sprachen

Community-Übersetzungen dieses Dokuments werden im Whitepaper-Repository gepflegt. Im Falle eines Konflikts zwischen einer Übersetzung und der englischen Version ist die englische Version maßgeblich.

| Sprache | Dokument |
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

*Dieses Dokument stellt keine finanzielle oder rechtliche Beratung dar. XEQM ist ein Utility-Coin für die EXIOM-Plattform, kein Anlageprodukt. Die Token-Klassifizierung, der Wertpapierstatus und die anwendbaren Vorschriften variieren je nach Jurisdiktion. Teilnehmer sollten ihren lokalen rechtlichen und regulatorischen Rahmen konsultieren, bevor sie XEQM erwerben oder damit arbeiten. XEQM Labs ermutigt nicht zum Kauf von XEQM auf der Grundlage spekulativer Kurssteigerungen.*
