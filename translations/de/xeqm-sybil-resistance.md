# Sybil-Risiko und EXIOMs Mitigationsmodell
## Technischer Begleiter zum EXIOM-Tokenomics-Whitepaper
### 07/26/2026

> **Hinweis (aktualisiert Oktober 2026).** Die Konzentration wird pro *Proximity-Cluster* (geteilte physische oder Routing-Infrastruktur) durchgesetzt, **nicht pro Land**. Die Node-Zahlen hier sind eine Momentaufnahme vom Juli 2026; siehe das Whitepaper für aktuelle Summen. Lokinet wird in einer nicht durchsetzenden Version vor HF23 ausgeliefert, und HF23 aktiviert die Durchsetzung.

Dieses Dokument ist ein Begleiter zum EXIOM-Tokenomics-Whitepaper und zum Vorschlag zu Node-Konzentrationsgrenzen und setzt die Lektüre beider voraus. Das Whitepaper behandelt, was die Kontrollen sind. Der Vorschlag zu Konzentrationsgrenzen behandelt die Mechanik, wie jede Kontrolle funktioniert. Dieses Dokument behandelt das Bedrohungsmodell: wie ein Sybil-Angriff auf einer Privacy-Chain tatsächlich aussieht, was EXIOMs Architektur spezifisch resistent oder verwundbar macht und wie die laufende Überwachungsmethodik Konzentration in der Praxis identifiziert.

---

## Die Sybil-Bedrohung auf einer Privacy-Chain

Ein Sybil-Angriff auf ein Service-Node-Netzwerk bedeutet, dass ein einzelner Akteur viele Nodes unter verschiedenen scheinbaren Identitäten betreibt, um unverhältnismäßigen Einfluss zu gewinnen. Auf einer transparenten Blockchain kann die Wallet-Graph-Analyse oft offenbaren, dass mehrere Node-Betreiber-Adressen aus einer gemeinsamen Quelle finanziert werden, und den Sybil aufdecken. Auf einer Privacy-Chain ist dieses Werkzeug durch Design nicht verfügbar. Die Privacy-Garantie, die Nutzertransaktionen schützt, beseitigt auch die häufigste Sybil-Erkennungsmethode.

EXIOMs Sybil-Oberfläche unterscheidet sich daher auf eine spezifische Weise von einer transparenten Chain: Ein Betreiber, der die Privacy-Funktionen korrekt verwendet, kann mehrere Wallet-Adressen präsentieren, die auf Protokollebene unverbunden erscheinen, unabhängig davon, wie viel Kapital er kontrolliert. Dies ist kein Fehler im Privacy-Design. Es ist eine inhärente Eigenschaft jeder Privacy-Chain, die durch andere Mechanismen als die Transaktionsgraph-Analyse adressiert werden muss.

Die zwei Sybil-Angriffsoberflächen auf EXIOM sind verschieden und erfordern separate Kontrollen:

**Konsenseinfluss-Angriff.** Ein Betreiber sammelt durch eine beliebige Wallet-Struktur genug Nodes an, um gleichzeitig eine unverhältnismäßige Anzahl von Quorum-Sitzen zu halten. Dies erlaubt ihm, Ergebnisse von Oracle-Sessions, Pulse-Runden und Obligations-Quorums über das hinaus zu beeinflussen, was sein individueller Stake-Anteil als fair nahelegen würde. Der Schaden betrifft die Konsensintegrität, nicht notwendigerweise die Netzwerk-Uptime.

**Failure-Domain-Angriff.** Ein Betreiber konzentriert Nodes in einer einzelnen physischen Einrichtung. Dies kann als Angriff beabsichtigt sein oder auch nicht; es kann aus Kostenoptimierung resultieren. Der Schaden betrifft die Netzwerk-Überlebensfähigkeit: Ein Ausfall einer Einrichtung nimmt die Nodes des Betreibers gleichzeitig offline und könnte die Blockproduktion stoppen, wenn die Konzentration groß genug ist.

---

## Was EXIOM strukturell resistent macht

**Kapitalkosten pro Identität.** Anders als bei reinen Sybil-Angriffen, bei denen Identitäten kostenlos sind, erfordert jeder EXIOM-Service-Node 200.000 XEQM gestakt, wobei der Betreiber persönlich mindestens 100.000 XEQM stakt. Ein Betreiber, der 100 Nodes betreibt, hat 10.000.000 XEQM an Kapital gestakt und gesperrt. Das Schaffen zusätzlicher scheinbarer Identitäten durch Wallet-Splitting reduziert diese Kosten nicht -- jeder Node erfordert weiterhin 100.000 XEQM Betreiber-Stake. Der Sybil-Angriff ist auf jeder Skala teuer.

**Unbonding-Reibung.** Eine 14-tägige Unbonding-Periode sowohl bei freiwilligem Abzug als auch bei erzwungener Deregistrierung bedeutet, dass das für Sybil-Nodes eingesetzte Kapital nicht schnell extrahiert werden kann. Ein Angreifer, der sich zum Ausstieg entscheidet, kann dies nicht schneller tun als jeder andere Betreiber.

**Öffentliches Node-Register.** Der Registrierungsschlüssel und die Betreiber-Wallet-Adresse jedes Service Nodes sind öffentlich. Ein Node kann nicht anonym am Konsens teilnehmen. Während die menschliche Identität hinter einer Wallet-Adresse privat ist, akkumuliert sich der operative Fingerabdruck des Nodes im Laufe der Zeit durch Registrierungsmuster, Uptime-Proof-Timing und Routing-Verhalten.

---

## Wie Konzentration ohne Transaktionsgraph-Analyse identifiziert wird

Da eine Analyse auf Transaktionsebene nicht verfügbar ist, stützt sich EXIOMs Konzentrationserkennung auf vier Signale, die aus dem Node-Verhalten statt aus der Finanzierungshistorie beobachtbar sind.

**Registrierungsschlüssel-Clustering.** Nodes, die unter demselben Betreiber-Wallet-Key registriert sind, sind definitiv derselbe Betreiber. Dies ist aus On-Chain-Daten deterministisch. Ein großer Betreiber, der kein Wallet-Splitting betreibt, ist allein durch dieses Signal vollständig sichtbar. Die aktuell größten Deployments im Netzwerk, einschließlich Nodes, die 58 bzw. 51 Nodes von einzelnen IP-Adressen betreiben, sind jeweils einzelne Betreiber, bestätigt durch die Registrierungsschlüssel-Analyse.

**IP-Adressen- und Subnetz-Clustering.** Derzeit das primäre Signal für physische Kollokation. Mehrere Nodes von derselben IP-Adresse sind fast sicher auf demselben Server. Mehrere Nodes vom selben Subnetz legen dasselbe Hosting-Konto oder denselben Rechenzentrumsblock nahe. Dieses Signal ist heute ohne jegliche Daemon-Änderungen verfügbar und wird nach der Lokinet-Aktivierung als ergänzendes Signal bestehen bleiben.

**Uptime-Proof-Timing-Korrelation.** Das Netzwerk erhält Uptime-Proofs von jedem aktiven Node nach einem regelmäßigen Zeitplan. Die Ankunfts-Zeitstempelverteilung dieser Proofs wird von den empfangenden Nodes aufgezeichnet. Nodes, die auf demselben physischen Host oder VM-Hypervisor laufen, reichen Proofs innerhalb eines charakteristischen engen Fensters ein, typischerweise unter 10 Millisekunden, weil sie dieselbe Systemuhr und Netzwerkschnittstelle teilen. Ein Cluster von Nodes aus verschiedenen Wallet-Keys, deren Proofs konsequent innerhalb dieses Fensters eintreffen, ist ein starkes Signal für geteilte physische Infrastruktur, erkennbar ohne jegliche Daemon-Änderungen und ohne dass Lokinet aktiv ist.

Dieses Signal ist spezifisch nützlich, um Wallet-Splitting-Betreiber zu identifizieren, die ihre Nodes auf geteilter Infrastruktur halten. Die Wallet-Keys unterscheiden sich; das Proof-Timing nicht.

**Lokinet-Routing-Proximity (wird nicht durchsetzend vor HF23 ausgeliefert; durchgesetzt bei HF23).** Sobald Lokinet als Netzwerktransport aktiv ist, liefert der Routing-Graph eine kontinuierliche physische Topologiekarte des Node-Netzwerks. Nodes an derselben Einrichtung routen durch dieselbe Upstream-Infrastruktur, wodurch korrelierte Pfadauswahlen und Sub-Millisekunden-Latenz zwischen Nodes entstehen, unabhängig von ihren Wallet-Keys oder angekündigten IP-Adressen. Dies ist das robusteste Signal, weil es die physische Netzwerkrealität widerspiegelt, die durch Softwarekonfiguration nicht geändert werden kann, ohne tatsächlich Infrastruktur zu bewegen.

---

## Der Wallet-Splitting-Angriff im Detail

Der ausgeklügeltste auf EXIOM verfügbare Sybil-Ansatz ist Wallet-Splitting: das Registrieren von Nodes unter mehreren Wallet-Adressen, die über die Transaktionsschicht der Privacy-Chain finanziert werden, sodass die gemeinsame Finanzierungsquelle nicht sichtbar ist. Dies hebelt das Registrierungsschlüssel-Clustering-Signal aus, aber nicht die anderen.

Ein Betreiber, der 426 Nodes über 10 Wallets betreibt, alle in derselben Contabo-Einrichtung gehostet, wird exponiert durch:

- Uptime-Proof-Timing: Proofs von allen 426 Nodes treffen im charakteristischen Sub-10ms-Fenster geteilter Infrastruktur ein
- IP- und Subnetz-Analyse: selbst bei mehreren IPs sind die Rechenzentrumsblock-Zuweisung und das ASN geteilt
- Lokinet-Proximity (nach HF23): alle 426 Nodes routen durch denselben Contabo-Backbone, unabhängig vom Wallet-Key

Ein Betreiber, der 426 Nodes über 10 Wallets betreibt, wirklich verteilt über 10 verschiedene Anbieter in 10 verschiedenen Ländern, wird durch kein aktuelles Signal nennenswert exponiert. Die Registrierungsschlüssel unterscheiden sich, das Proof-Timing unterscheidet sich, weil die Infrastruktur sich unterscheidet, die ASNs unterscheiden sich, und die Lokinet-Pfade unterscheiden sich. Auf Protokollebene sieht dies wie 10 verschiedene Betreiber aus.

Dies ist das Rest-Sybil-Risiko auf EXIOM, nachdem alle Kontrollen angewendet wurden. Es ist in seinen Konsequenzen begrenzt: Die HF23-Quorum-Deduplizierung beschränkt jedes Proximity-Cluster auf einen Quorum-Sitz pro Runde, unabhängig von der Wallet-Struktur, sodass selbst ein verteilter Wallet-Splitting-Betreiber keinen unbegrenzten Konsenseinfluss gewinnt. Ihr Blockbelohnungs-Einkommen skaliert mit ihrer Node-Anzahl, was fair ist, weil sie proportionales Kapital gestakt haben. Ihr Konsenseinfluss pro Runde ist durch die Cluster-Dedup gedeckelt, unabhängig davon, wie viele Wallets sie verwenden.

---

## Laufende Überwachungsmethodik

**Governance-Blocklist.** Eine von der Governance verwaltete öffentliche Schlüssel-Blocklist verhindert, dass auf der Blocklist stehende Registrierungsschlüssel neue Nodes registrieren. Ein Betreiber, der zu einem neuen Wallet-Key wechselt, während der ursprüngliche auf der Blocklist steht, erzeugt einen dokumentierten Datensatz der Umgehung, und das Proof-Timing und Routing-Verhalten des neuen Schlüssels werden gegen das historische Profil des auf der Blocklist stehenden Schlüssels korreliert.

**Beitragenden-Slot-Graph-Analyse.** Service-Node-Beitragenden-Slots sind ein sekundäres Identitätssignal. Ein Betreiber, der Beitragenden-Slots über mehrere seiner eigenen Wallet-Keys finanziert, erzeugt auch auf einer Privacy-Chain einen beobachtbaren Beziehungsgraphen, weil die Beitragenden-Registrierungstransaktionen beobachtbare Daten darüber tragen, zu welchen Nodes sie beitragen. Ein Betreiber, der konsequent von den Wallets B und C zu Nodes beiträgt, die unter Wallet A registriert sind, während dieselben Wallets B und C ihre eigenen Nodes registrieren, erzeugt einen Korrelationsgraphen, der das direkte Registrierungsschlüssel-Clustering-Signal ergänzt.

**ASN-Überwachung.** Die IP jedes aktiven Nodes wird über öffentliche BGP-Daten einer Autonomous System Number zugeordnet. Das Netzwerk verfolgt die ASN-Konzentration über die aktive Node-Menge. Nodes, die sich ein ASN teilen, teilen sich Infrastruktur auf Anbieterebene und rechtliche Exposition. Hohe ASN-Konzentration wird für die Governance-Überprüfung markiert, selbst wenn einzelne Node-Registrierungen unverbunden erscheinen. Das ASN-Signal identifiziert keinen menschlichen Betreiber, aber es identifiziert eine Failure-Domain.

Der aktuelle Implementierungsstatus für alle in diesem Dokument beschriebenen Kontrollen wird im [Vorschlag zu Node-Konzentrationsgrenzen](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md) gepflegt.

---

*Dieses Dokument stellt keine Finanz- oder Rechtsberatung dar. XEQM ist ein Utility-Coin für die EXIOM-Plattform, kein Anlageprodukt. Token-Klassifizierung, Wertpapierstatus und geltende Vorschriften variieren je nach Jurisdiktion. Teilnehmer sollten ihren lokalen rechtlichen und regulatorischen Rahmen konsultieren, bevor sie XEQM erwerben oder damit operieren. XEQM Labs ermutigt nicht zum Kauf von XEQM auf Basis spekulativer Preissteigerungen.*
