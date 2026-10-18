# XEQM Labs - Plateforme EXIOM
## Livre blanc sur la tokenomique
### Version préliminaire v12 | 09/27/2026

---

## Ce qui est en service aujourd'hui vs. ce qui est prévu

| Composant | Statut |
|---|---|
| Mainnet EXIOM | En service, opérationnel depuis le 6 mai 2026 |
| Réseau de nœuds de service | En service — 943 nœuds de service actifs au 27 septembre 2026 |
| Lokinet (LLARP) | Livré dans une version non contraignante avant HF23 (transport en service, regroupement par proximité observable) ; HF23 active l'application. La mise en œuvre commence au T4 2026 |
| Stockage en nœud léger SQLite | En développement ; livré avec la version Lokinet antérieure à HF23, pour une mémoire et un disque de nœud réduits, avec des nœuds légers optionnels à fenêtre récente |
| Échange de pièces XEQ vers XEQM | Livré et clôturé, exécution en production de 35 jours, registre public auditable |
| Portefeuille GUI | En service, github.com/XEQMLabs/XEQMLabs-GUI |
| Explorateur de nœuds | En service, surveillance active des nœuds de service |
| EXIOM Oracle | En service sur le mainnet (Robinhood Chain, chainId 4663) ; comité d'opérateurs de 12 membres au 28 septembre 2026 |
| API développeur EXIOM | En service en bêta — clés en libre-service, attestations de conformité signées et un moteur de vérification, OpenAPI à /docs ; développement gratuit avec un usage prépayé par appel en cours de déploiement (27 septembre 2026) |
| EXIOM Privacy Oracle (TLSNotary / ZK) | Fondations en service (moteur de vérification, sessions oracle) ; oracle complet de données web privées en Phase 3 |
| Plateforme de trading RFQ EXIOM | En développement, Phase 2/3, XEQM/BTC comme première paire |
| HF22, déduplication de quorum par clé de portefeuille, unification du déverrouillage, récupération après blocage Pulse | Activé au bloc mainnet 219120. La révision de récupération après blocage Pulse (snode_revision 1, repli basé sur signature) a été activée au bloc 236920 le 18 octobre 2026 |
| HF23, plafond de cluster par proximité et modificateur de récompense (application) | En conception ; active les limites de concentration une fois que la version non contraignante Lokinet + nœud léger a été éprouvée ; visée au T4 2026 |
| Gouvernance formelle on-chain | Prévue, Phase 6 |

---

## 1. Ce qu'est XEQM Labs

XEQM Labs est une entreprise de technologie de confidentialité. Son produit phare, EXIOM, est un réseau Layer 1 en Proof-of-Stake préservant la confidentialité et une plateforme commerciale pour développeurs, exploité par un ensemble mondial de nœuds de service. XEQM est la pièce d'accès et d'usage de la plateforme. Les développeurs construisent gratuitement et paient l'usage en production en XEQM, consommé au fur et à mesure de leurs appels à l'API. Les opérateurs de nœuds de service gagnent des XEQM pour sécuriser le réseau, et les mêmes opérateurs peuvent gagner des revenus supplémentaires en exploitant un sidecar oracle qui dessert les produits oracle de la plateforme.

Le projet porte une histoire communautaire et opérationnelle remontant à plus de sept ans. Le mainnet EXIOM a été construit pour offrir à cette communauté un réseau doté d'une offre vérifiable, d'un calendrier d'émission prévisible, d'un consensus Proof-of-Stake pur sans composante Proof-of-Work, et de mécaniques de nœud de service qui respectent le temps et le capital des opérateurs.

XEQM est une pièce Layer 1 native, non tokenisée sur aucune autre chaîne, ni ERC-20 ni actif enveloppé, et sans pontage. Les détenteurs interagissent directement avec le mainnet EXIOM.

### La famille de produits EXIOM

**Réseau de nœuds de service EXIOM.** En service sur le mainnet. Un ensemble mondial de nœuds de service sécurise la chaîne, gagne des récompenses de bloc et forme la couche d'infrastructure sur laquelle s'exécutent tous les autres produits EXIOM. 943 nœuds de service actifs au 27 septembre 2026.

**EXIOM Coin Swap.** Un produit commercial permettant aux projets de migrer leur communauté de détenteurs d'une chaîne héritée vers une nouvelle chaîne avec une auditabilité cryptographique complète. Le pilote fut la migration des détenteurs de XEQ vers XEQM sur le mainnet EXIOM, exécutée pendant 35 jours, chaque soumission étant traitée via un registre cryptographiquement vérifié portant une empreinte publique SHA256. Le produit est disponible pour d'autres projets nécessitant une migration de chaîne vérifiable.

**EXIOM Oracle.** En service sur le mainnet. Le premier produit oracle de la plateforme : un comité d'opérateurs de nœuds de service XEQM — chacun exécutant un sidecar oracle léger — qui produit des attestations de conformité agrégées BLS et signées EIP-712 (par exemple, qu'une adresse est éligible pour une juridiction donnée) que les applications consomment via l'API développeur. Il est déployé sur Robinhood Chain (chainId 4663) et exploite un comité d'opérateurs de 12 membres au 28 septembre 2026. Exécuter le sidecar est la manière dont un opérateur de nœud de service gagne des revenus supplémentaires, basés sur l'usage, en plus des récompenses de bloc.

**API développeur EXIOM.** En service en bêta. Une API structurée exposant les capacités de conformité et de vérification de la plateforme — attestations de conformité signées et un moteur de vérification (mécanismes de signed-claims, TLSNotary et à divulgation nulle de connaissance) — avec un accès en libre-service (un DID plus une clé API), une spécification OpenAPI 3.1, des webhooks et des requêtes idempotentes. Les développeurs construisent gratuitement sur une allocation mensuelle généreuse et paient l'usage en production en XEQM, consommé par appel. Phase 2, active.

**EXIOM Privacy Oracle.** Conçu, fondations en place. L'évolution plus large de l'oracle : prouver des faits sur des données web privées (via TLSNotary et des techniques à divulgation nulle de connaissance) sans exposer la source sous-jacente. Le moteur de vérification et les points de terminaison de session oracle qui le sous-tendent sont déjà en service ; l'oracle complet de données web privées est un livrable de Phase 3. La plateforme RFQ EXIOM comme les applications tierces peuvent consommer les sorties de l'oracle.

**Plateforme de trading RFQ EXIOM.** En développement. Une plateforme de trading de gré à gré pair-à-pair avec des attestations de règlement cryptographiques, construite sur l'API EXIOM. La première paire de trading est XEQM/BTC, deux actifs Layer 1 natifs sans tokenisation, sans enveloppement et sans risque de pont. L'oracle fournit des attestations de prix privées pour la couche de tarification. Phase 2/3.

XEQM Labs exploite EXIOM comme une plateforme logicielle commerciale. L'objectif est un revenu de plateforme durable qui réduit au fil du temps la dépendance aux émissions de gouvernance. XEQM Labs n'encourage pas l'achat de XEQM sur la base d'une appréciation spéculative du prix.

---

## 2. Provenance de l'offre

La migration est achevée. 276,917,604 XEQM ont été émis sur le mainnet EXIOM en échange d'avoirs hérités. Ce chiffre est l'offre de départ vérifiée au lancement du mainnet le 6 mai 2026. Chaque dépôt hérité a été enregistré dans un registre public avec une empreinte SHA256. La nouvelle chaîne a été frappée une seule fois à la conclusion de l'échange pour correspondre à ce total vérifié exact. Les clés de dépense de chaque portefeuille impliqué dans l'échange ont été publiées, et quiconque peut vérifier l'historique complet des transactions, du dépôt au paiement.

Au-delà de l'offre de départ, de nouveaux XEQM entrent en circulation par le biais de deux flux d'émission au niveau du protocole : les récompenses de bloc des nœuds de service et les émissions de gouvernance. Les deux fonctionnent selon des calendriers fixes et prévisibles inscrits dans le protocole, que quiconque peut calculer à partir de paramètres publics. Les taux et les détails opérationnels figurent en Section 3. L'offre totale croît au fil du temps. XEQM est une chaîne à offre non plafonnée, sur le même modèle que l'émission résiduelle de Monero. La discipline d'offre fixe à laquelle le projet s'engage renvoie à l'absence d'émission discrétionnaire, et non à un plafond strict sur les émissions pilotées par le protocole.

**Aucune frappe discrétionnaire.** Le protocole n'autorise pas d'émission ad hoc, d'ajustements manuels de l'offre ou de frappes hors calendrier. Chaque nouveau XEQM entrant en circulation le fait par le biais des deux flux d'émission programmés ci-dessus.

**Aucun burn.** L'architecture cryptographique sur laquelle ce réseau est construit ne prend pas en charge les burns prouvables au sens où ce terme est habituellement employé. Toute adresse vers laquelle une pièce est envoyée n'est aussi indépensable que la clé n'est démontrablement détruite. Nous ne présenterons aucun portefeuille comme une adresse de burn. Les pièces non échangées pendant la fenêtre de migration restent sur la chaîne héritée inactive et ne font pas partie de l'offre de XEQM.

---

## 3. Modèle de tokenomique

### Émissions de bloc

Le réseau produit un nouveau bloc toutes les 60 secondes et attribue 8.25 XEQM au nœud de service sélectionné, générant 11,880 XEQM par jour. À 943 nœuds actifs (27 septembre 2026), chaque nœud gagne environ 12.6 XEQM par jour, soit environ 380 XEQM par mois.

À partir de HF21, les récompenses de bloc sont distribuées selon un calendrier de regroupement hebdomadaire. Avant HF21, les récompenses étaient émises tous les 20 blocs. Les récompenses s'accumulent désormais sur chaque fenêtre de 10,080 blocs (environ 7 jours) et sont versées à la fin de chaque fenêtre. Le taux d'émission total est inchangé ; seule la cadence de paiement a changé.

### Émission de gouvernance

La trésorerie reçoit environ 17,857 XEQM par jour, soit environ 124,999 XEQM par semaine. C'est le budget de fonctionnement d'une équipe active de développement de logiciels commerciaux. Les ingénieurs, les réviseurs de sécurité, les opérateurs d'infrastructure et les contributeurs de l'écosystème sont rémunérés à partir de cette émission tant que la plateforme est pré-revenus. À mesure que chaque produit EXIOM atteint un statut générateur de revenus, l'émission de gouvernance est revue et réduite en conséquence. L'objectif à long terme est que le revenu de plateforme remplace l'émission de gouvernance comme principal mécanisme de financement.

### Allocation de l'émission

| Allocation | Part | Objet |
|---|---|---|
| Récompenses des nœuds de service | 40% | Récompenses de bloc versées directement aux nœuds de service |
| Développement du protocole central | 25% | Blockchain, plateforme EXIOM et services réseau centraux |
| Marketing et notoriété | 15% | Visibilité et adoption du réseau |
| Écosystème et communauté | 10% | Subventions, primes, récompenses communautaires, support d'intégration |
| Sécurité et audits | 5% | Audits, revues de sécurité, tests de fiabilité |
| Réserve à long terme | 5% | Stabilité, besoins d'urgence, opérations à long terme |

### Revenu et distribution de la plateforme EXIOM

Au-delà des récompenses de bloc, la plateforme tire des revenus de l'usage par les développeurs. L'accès est prépayé : un développeur approvisionne son compte en déposant des XEQM (non remboursables), et ce solde est débité à mesure qu'il consomme l'API de production, tarifée par appel. Le développement et l'évaluation sur l'allocation gratuite ne sont pas facturés.

Les XEQM consommés sont comptabilisés comme revenu de plateforme et distribués entre les opérateurs qui desservent l'oracle et les opérations de la plateforme :

| Bénéficiaire | Part | Objet |
|---|---|---|
| Opérateurs de sidecar oracle | 70% | Opérateurs de nœuds de service exécutant le sidecar oracle, récompensés proportionnellement aux tâches oracle qu'ils contribuent à assurer |
| Opérations et développement de la plateforme | 30% | Finance les opérations et le développement continus, réduisant au fil du temps la dépendance à l'émission de gouvernance |

Les opérateurs prennent la majorité parce qu'ils exploitent l'infrastructure qui dessert l'oracle. Le ratio 70/30 est la valeur initiale et est ajustable par la gouvernance. Le revenu est comptabilisé et distribué selon la même cadence hebdomadaire que les récompenses de bloc — chaque fenêtre de 10,080 blocs (environ 7 jours), alignée sur le regroupement de récompenses de HF21 — de sorte qu'un opérateur reçoit les récompenses de bloc et la part de revenu d'usage sur un seul rythme. Cette part de revenu est le mécanisme par lequel la récompense de sidecar d'opérateur décrite en Section 4 est financée par un usage réel plutôt que par l'émission.

Matériel de base pour exécuter un nœud de service (et son sidecar oracle) : 4 cœurs CPU, 8 Go de RAM, 100 Go de SSD, connexion 100 Mbps. Les charges de travail plus lourdes de l'oracle de confidentialité nécessitent des spécifications supérieures, traitées en Section 10.

---

## 4. Structure des nœuds de service

### Paramètres de staking

| Paramètre | Valeur |
|---|---|
| Exigence pour un nœud complet | 200,000 XEQM |
| Stake minimum de l'opérateur | 100,000 XEQM (50% de l'exigence complète) |
| Frais maximum de l'opérateur | 10% |
| Période de déverrouillage, retrait volontaire | 14 jours, les récompenses continuent |
| Période de déverrouillage, déréférencement forcé | 14 jours, pas de récompenses (unifié dans HF22) |
| Nombre maximum d'emplacements de contributeurs | 11 (y compris l'opérateur) |
| Contribution communautaire minimum par emplacement | 10,000 XEQM |
| Fenêtre de staking communautaire par nœud | Jusqu'à 100,000 XEQM répartis sur jusqu'à 10 emplacements de contributeurs |

### Économie des nœuds

De nombreux fournisseurs de VPS cloud offrent un niveau de service gratuit qui peut supporter l'exploitation d'un nœud de service sans coût mensuel. Un VPS payant à environ 5,28 $ par mois peut exécuter 10 nœuds de service, ramenant le coût d'hébergement par nœud à environ 0,53 $ par mois. L'hébergement géré via Pecunia est disponible à 1,76 $ par nœud et par mois.

Les récompenses de bloc par nœud évoluent inversement au nombre de nœuds actifs : à 943 nœuds de service actifs (27 septembre 2026), l'émission quotidienne du réseau de 11,880 XEQM revient à environ 12.6 XEQM par nœud et par jour, soit environ 380 XEQM par mois. Parce que la récompense et le stake sont tous deux libellés en XEQM, l'APY de récompense de bloc est d'environ 2.3% indépendamment du prix ; l'hébergement est le seul coût récurrent important, à environ 0,53 $ par nœud et par mois en auto-hébergement ou 1,76 $ via Pecunia. Exécuter le sidecar oracle (Section 10) ajoute un second flux de revenus basé sur le revenu et qui évolue avec l'usage réel de la plateforme, financé par la consommation des développeurs plutôt que par l'émission.

### Économie des contributeurs

Les opérateurs qui ne peuvent pas ou choisissent de ne pas exploiter d'infrastructure peuvent contribuer du stake à un nœud existant sur jusqu'à 10 emplacements de contributeurs. L'opérateur peut facturer de 0% à 10% de la récompense de bloc avant que le reste ne soit réparti proportionnellement entre les contributeurs. Les contributeurs ne supportent aucun coût d'hébergement, de sorte qu'à chaque niveau de prix, le rendement net d'un contributeur dépasse celui d'un opérateur auto-hébergé ou hébergé par Pecunia.

### Cycle de vie des nœuds

Les nœuds restent actifs indéfiniment avec le maintien du collatéral et des exigences de performance. Un nœud qui ne respecte plus la conformité peut être remédié sans pénalité. S'il n'est pas remédié, le déréférencement forcé déclenche une période de déverrouillage de 14 jours sans récompenses. La sortie volontaire comporte une période de déverrouillage de 14 jours avec maintien des récompenses tout du long.

---

## 5. Survivabilité du réseau et vecteurs d'attaque

### Exigence de survivabilité

Le réseau EXIOM prend des engagements de fiabilité envers les développeurs. Un réseau qui peut être mis hors ligne par une seule panne de datacenter ne peut pas prendre ces engagements. Le protocole impose une taille maximale de domaine de défaillance : aucune installation physique, datacenter ou cluster de routage unique ne peut héberger plus de 30% des nœuds actifs.

À 943 nœuds (27 septembre 2026), 30% représente environ 283 nœuds. La perte d'une seule installation peut mettre au maximum 283 nœuds hors ligne simultanément, laissant au moins 660 nœuds opérationnels, suffisant pour maintenir la production de blocs et la formation de quorum sans déréférencements en cascade. C'est une exigence d'ingénierie, pas une préférence de décentralisation.

### Deux hard forks

L'application de la survivabilité est livrée en deux étapes, séparées pour réduire le risque et livrer immédiatement un travail validé.

**HF22, activé :** Déduplication de quorum par clé de portefeuille d'opérateur et unification de la période de déverrouillage, plus une révision de récupération après blocage Pulse (snode_revision 1) qui remplace le repli de récupération Proof-of-Work antérieur par un repli basé sur signature. Aucune dépendance à Lokinet. Validé sur 20 cycles de blocage/récupération avec un taux de récupération de 100%, zéro intervention, et un écart de bloc maximum de 83 secondes. HF22 a été activé au bloc mainnet 219120 ; la révision de récupération après blocage a été activée au bloc 236920 le 18 octobre 2026.

**HF23, en conception, visé au T4 2026 :** Plafond d'enregistrement de cluster par proximité, modificateur de récompense nulle pour les nœuds excédentaires, et mise à niveau de la déduplication de quorum de la clé de portefeuille vers le cluster de proximité. Les trois reposent sur le graphe de routage Lokinet comme signal de proximité. Pour éviter de rendre un nouveau transport critique pour le consensus au moment même de son introduction, Lokinet est livré d'abord dans une version non contraignante distincte (aux côtés du changement de stockage en nœud léger SQLite), où le regroupement par proximité est en service et observable mais n'a aucune conséquence sur les récompenses. HF23 active ensuite l'application, après que cette version a été éprouvée, que le nombre réel de clusters a été mesuré et que le seuil et le repli ont été réglés.

### Contrôles HF22

**Déduplication de quorum par clé de portefeuille d'opérateur.** Au plus un nœud par adresse de portefeuille d'opérateur peut détenir un siège de validateur dans un tour Pulse, une session oracle ou un quorum d'obligations donné. Si un tirage aléatoire sélectionne deux nœuds de la même adresse d'opérateur, le second est remplacé par un nœud d'un opérateur différent. Les récompenses de bloc ne sont pas affectées ; elles sont attribuées par ordre de temps d'attente, indépendamment de la participation au quorum.

Limitation connue : contournée par le fractionnement de portefeuille. Un opérateur utilisant plusieurs adresses de portefeuille présente plusieurs clés d'opérateur au protocole. HF23 comble cette lacune par la déduplication de cluster par proximité.

**Unification de la période de déverrouillage.** La période de déverrouillage du déréférencement forcé est étendue de 7 jours à 14 jours, correspondant au retrait volontaire. Les deux cas sont désormais de 14 jours.

### Contrôles HF23

Une fois Lokinet actif comme transport du réseau, les nœuds physiquement co-localisés présenteront des signatures de routage caractéristiques : latence mutuelle inférieure à la milliseconde et fort recouvrement de chemins à travers le graphe de routage Lokinet. Les nœuds situés dans des installations réellement différentes présenteront une latence plus élevée et un recouvrement de chemins plus faible. Ce signal de regroupement est dérivé d'un comportement réseau observable, sans aucune obligation pour les opérateurs de divulguer leur fournisseur ou leur localisation.

**Plafond d'enregistrement de cluster.** Les nouveaux enregistrements de nœuds sont évalués par rapport à la proximité de routage Lokinet des clusters existants. Si le cluster cible contient déjà 30% ou plus des nœuds actifs, l'enregistrement est rejeté par le protocole.

**Modificateur de récompense nulle.** Les nœuds au-dessus du seuil de plafond de cluster gagnent zéro récompense de bloc jusqu'à leur migration vers un cluster non concentré. Les nœuds sont classés au sein de chaque cluster selon l'ancienneté d'enregistrement ; les nœuds les plus anciens jusqu'au seuil de plafond gagnent la récompense complète. Chaque nœud au-dessus de ce seuil gagne zéro. Un taux réduit peut se justifier par rapport aux coûts de VPS ; zéro ne le peut pas.

Une période de grâce de 30 jours s'applique à l'activation de HF23. Tous les nœuds gagnent la récompense complète pendant la période de grâce. À l'expiration, le modificateur de récompense nulle s'active sur les nœuds excédentaires.

**Déduplication de quorum par cluster de proximité.** Met à niveau la déduplication par clé de portefeuille de HF22 vers la déduplication par cluster de proximité. Au plus un nœud par cluster de proximité par tour, quelle que soit la structure de portefeuille. Comble la lacune du fractionnement de portefeuille.

La taille du quorum est de 12 sièges par tour. La déduplication nécessite donc au moins 12 clusters de proximité distincts pour fonctionner sans repli. Compte tenu de la topologie réseau actuelle, le nombre de clusters à l'activation de HF23 pourrait être proche de ce minimum. L'algorithme met en œuvre un repli obligatoire : si tous les clusters distincts sont épuisés avant que les 12 sièges ne soient pourvus, des sièges supplémentaires sont alloués en commençant par les plus petits clusters (les moins concentrés), avant que le cluster le plus concentré ne reçoive un deuxième siège. La fréquence des replis est journalisée et publiée dans l'explorateur de nœuds comme indicateur en temps réel du risque de concentration. Un réseau ne déclenchant jamais le repli a atteint une diversité physique adéquate.

### Contrôles additionnels

**Barrière de coût en capital.** Le stake minimum de 100,000 XEQM de l'opérateur garantit que chaque opérateur engage un capital réel sur chaque nœud. Exécuter N nœuds requiert au moins N x 100,000 XEQM en stake.

**Protection contre la capture des frais par l'opérateur.** EXIOM n'est pas sujet à l'attaque de capture des frais par l'opérateur présente dans certains réseaux de nœuds de service, où un opérateur enregistre un nœud avec un capital minimal et fixe des frais de 100% pour capturer l'intégralité de la récompense de bloc, quel que soit le stake des contributeurs. Les frais maximum sont plafonnés à 10% et le stake minimum de 50% de l'opérateur rend cela économiquement irrationnel.

**Analyse du timing des preuves de disponibilité.** Les nœuds sur le même hôte physique soumettent des preuves de disponibilité en clusters étroitement corrélés, détectables à partir des données de réception de preuves existantes sans modification du daemon.

**Analyse ASN.** Les nœuds derrière le même Autonomous System Number partagent une infrastructure au niveau du fournisseur et une exposition juridique. La concentration d'ASN contribue à l'assignation de cluster et à la revue de gouvernance.

**Liste de blocage de gouvernance.** Une liste de blocage de clés publiques gérée par la gouvernance empêche les clés d'enregistrement bloquées d'enregistrer de nouveaux nœuds.

**Cible de coefficient de Nakamoto.** Le réseau vise un coefficient d'opérateurs d'au moins 8. Au 27 septembre 2026, à travers 943 nœuds de service actifs et 204 opérateurs, le coefficient de Nakamoto d'opérateurs — le nombre minimum d'opérateurs contrôlant une majorité de nœuds actifs — est de 9, atteignant la cible (en hausse par rapport à 7 à travers 184 opérateurs en juillet 2026). La concentration d'installation physique est un problème distinct et plus aigu : une seule région de datacenter héberge encore une majorité de nœuds, ce qui est exactement la concentration que le plafond de cluster par proximité de HF23 est conçu pour briser.

La proposition complète sur les limites de concentration se trouve à [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). La méthodologie de résistance au Sybil se trouve à [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Lokinet comme futur transport du réseau

L'infrastructure d'adressage du réseau EXIOM migrera des adresses IP annoncées publiquement vers l'adressage Lokinet. Lokinet est livré d'abord dans une version non contraignante avant HF23 (visée au T4 2026) ; HF23 ajoute ensuite l'application de la concentration qui utilise le graphe de routage Lokinet. Lokinet (Low Latency Anonymous Routing Protocol, LLARP) est un protocole de routage en oignon de couche 3 acheminant tout trafic basé sur IP à travers plusieurs nœuds de service via un routage en oignon multi-sauts, aucun nœud unique du chemin ne connaissant à la fois l'origine et la destination.

Une fois Lokinet actif :

- Les nœuds de service seront adressés par leur identifiant cryptographique Lokinet plutôt que par une adresse IP annoncée publiquement
- L'API développeur EXIOM sera accessible comme service caché à une adresse `.loki`, dissimulant l'IP d'origine du développeur au nœud API
- La plateforme de trading RFQ sera accessible comme service caché, dissimulant les adresses IP du demandeur et du LP à la plateforme
- La communication de session oracle entre le prouveur et le quorum de vérificateurs sera acheminée via Lokinet, éliminant l'hypothèse de confiance en un coordinateur centralisé

Lokinet est livré dans une version non contraignante avant HF23, visée au T4 2026, HF23 suivant une fois qu'elle a été éprouvée. Le code source LLARP est présent dans le dépôt EXIOM ; la mise en œuvre de Lokinet comme transport principal du réseau commence au T4 2026.

---

## 6. XEQM comme pièce utilitaire

La demande de XEQM provient de trois sources. Le staking de nœuds verrouille la plus grande part de l'offre, environ 68% aux 943 nœuds actifs actuels (27 septembre 2026). La consommation des développeurs crée une couche de vélocité continue : les applications paient l'usage de l'API de production en XEQM, de sorte que l'adoption de la plateforme se convertit directement en demande récurrente pour la pièce. L'accès à l'oracle ajoute une troisième couche pour les consommateurs à plus fort volume.

L'accès suit un modèle prépayé, basé sur l'usage, plutôt qu'une barrière de type stake-to-unlock — les développeurs n'ont pas à acquérir et verrouiller un stake fixe pour construire :

| Niveau | Modèle d'accès |
|---|---|
| Gratuit | Construire et évaluer sans frais : une allocation mensuelle généreuse d'appels, aucun dépôt requis |
| Production | Usage prépayé : déposer des XEQM et payer par appel ; webhooks et limites supérieures |
| Entreprise | Limites personnalisées, SLA et support ; conditions de volume |

L'usage en production est mesuré par appel API et débité du solde XEQM prépayé du développeur. Les dépôts sont non remboursables et sont comptabilisés comme revenu de plateforme à mesure qu'ils sont consommés (voir Section 3). Une conception antérieure conditionnait les niveaux derrière un stake XEQM fixe ; cela a été remplacé par ce modèle prépayé, qui est plus simple pour les développeurs et standard pour les API commerciales.

---

## 7. Gouvernance et trésorerie

L'adresse du portefeuille de gouvernance et la clé de visualisation sont publiées. Quiconque peut vérifier le solde à tout moment. La gouvernance est actuellement assurée par l'équipe fondatrice avec les apports de la communauté via des canaux Telegram ouverts et des discussions GitHub.

Allocations de trésorerie, tirées de l'émission de gouvernance décrite en Section 3 :

- Développement central (25%) : ingénierie pour l'API EXIOM, l'oracle et la plateforme RFQ
- Marketing et notoriété (15%) : listages sur les exchanges, contenu, croissance de la communauté
- Écosystème et communauté (10%) : subventions, primes, support d'intégration
- Sécurité et audits (5%) : audits de code, revues de sécurité, tests de pénétration
- Réserve à long terme (5%) : stabilité opérationnelle et réserves d'urgence

La Phase 3 introduit un processus formel de proposition et de commentaires. La Phase 6 introduit un vote pondéré où les opérateurs de nœuds de service et de nœuds API détiennent des droits formels proportionnels au stake et à l'ancienneté.

---

## 8. Résumé des paramètres

| Paramètre | Valeur |
|---|---|
| Mécanisme de consensus | 100% Proof-of-Stake |
| Temps de bloc | 60 secondes |
| Récompense de bloc | 8.25 XEQM par bloc |
| Émissions de bloc quotidiennes | 11,880 XEQM |
| Émission de gouvernance | ~17,857 XEQM par jour |
| Exigence pour un nœud complet | 200,000 XEQM |
| Stake minimum de l'opérateur | 100,000 XEQM (50%) |
| Frais maximum de l'opérateur | 10% |
| Nombre maximum d'emplacements de contributeurs | 11 (y compris l'opérateur) |
| Contribution communautaire minimum | 10,000 XEQM par emplacement |
| Fenêtre de staking communautaire par nœud | Jusqu'à 100,000 XEQM répartis sur 10 emplacements |
| Période de déverrouillage, retrait volontaire | 14 jours, les récompenses continuent |
| Période de déverrouillage, déréférencement forcé | 14 jours, pas de récompenses (HF22) |
| Offre totale | 276,917,604 XEQM au lancement, croissant par les émissions programmées |
| Offre verrouillée à 943 nœuds (27 sept. 2026) | ~188,600,000 XEQM (~68% de l'offre de départ) |
| Librement en circulation à 943 nœuds | ~88,300,000 XEQM à l'offre de départ, croissant avec les émissions |
| APY d'opérateur solo à 943 nœuds | ~2.3% (récompenses de bloc uniquement, versées hebdomadairement via HF21) |
| Coût auto-hébergé par nœud | ~0,53 $/mois (VPS à 5,28 $/mois, 10 nœuds) |
| Coût d'hébergement géré (Pecunia) | 1,76 $/nœud/mois |
| Nœuds de service actifs (27 septembre 2026) | 943 |
| Coefficient de Nakamoto d'opérateurs (27 sept. 2026) | 9 — contrôle majoritaire ; cible >= 8 ; 943 nœuds, 204 opérateurs |
| Activation externe de l'oracle | Nakamoto >= 6 atteint ; conditionné à l'achèvement de la Phase 3 |
| Taille du quorum | 12 sièges par tour |
| Déduplication de quorum, HF22 | Une adresse de portefeuille d'opérateur par siège de quorum par tour |
| Déduplication de quorum, HF23 | Un cluster de proximité par siège de quorum par tour (nécessite Lokinet) |
| Repli de déduplication de quorum, HF23 | S'il existe moins de 12 clusters distincts, les plus petits clusters reçoivent d'abord des sièges supplémentaires avant les clusters les plus concentrés ; fréquence des replis journalisée et publiée |
| Plafond de survivabilité du réseau, HF23 | 30% des nœuds actifs par cluster de proximité (~283 nœuds au nombre actuel) |
| Modificateur de récompense nulle, HF23 | Zéro récompense de bloc pour les nœuds au-dessus du plafond de cluster, classés par ancienneté d'enregistrement |
| Dépôts centraux | github.com/XEQMLabs |

---

## 9. Feuille de route

**Phase 1, Stabilisation du réseau. TERMINÉE.** Le réseau de nœuds de service a atteint 943 nœuds de service actifs au 27 septembre 2026 (contre 693 à travers 184 opérateurs en juillet 2026, coefficient de Nakamoto 7). L'échange de pièces XEQ vers XEQM s'est exécuté et clôturé avec succès.

**Phase 2, API développeur EXIOM et EXIOM Oracle. ACTIVE.** L'EXIOM Oracle est en service sur le mainnet avec un comité d'opérateurs, et l'API développeur est en service en bêta (identifiants en libre-service, points de terminaison de conformité et de vérification, OpenAPI). Travaux restants de Phase 2 : facturation de consommation prépayée, part de revenu des opérateurs et premières intégrations en production. Le développement de la plateforme de trading RFQ EXIOM se poursuit en parallèle, XEQM/BTC comme première paire de trading.

**Phase 3, EXIOM Privacy Oracle et plateforme RFQ.** L'oracle est déployé par phases : preuve de concept interne, testnet fédéré, puis mainnet avec consommateurs internes. La plateforme de trading RFQ atteint la production dans cette phase, utilisant l'oracle pour l'attestation de prix privée sur la paire XEQM/BTC. Les deux sont construits sur l'API EXIOM.

**Phase 4, Accès des consommateurs externes à l'oracle.** Sorties de l'oracle disponibles pour les développeurs de niveau Production et Entreprise et les consommateurs externes. Seuil de coefficient de Nakamoto de 6 déjà atteint ; activation conditionnée à l'achèvement de la Phase 3.

**HF22, activé (bloc mainnet 219120).** Deux changements de consensus sans dépendance à Lokinet, déduplication de quorum par clé de portefeuille d'opérateur (une adresse d'opérateur par siège de quorum par tour) et unification de la période de déverrouillage (déréférencement forcé étendu de 7 à 14 jours), plus une révision de récupération après blocage Pulse (snode_revision 1) qui a été activée au bloc 236920 le 18 octobre 2026, remplaçant la récupération Proof-of-Work par un repli basé sur signature. Validé sur 20 cycles de blocage/récupération (100% de récupération, écart de bloc maximum 83 secondes).

**Version Lokinet et nœud léger, avant HF23.** Une version non contraignante qui met Lokinet en service comme transport du réseau (regroupement par proximité en service et observable dans l'explorateur de nœuds, sans conséquence sur les récompenses) et introduit le stockage en nœud léger SQLite (mémoire et disque par nœud réduits, avec des nœuds légers optionnels à fenêtre récente). Cette version est éprouvée afin que le nombre réel de clusters de proximité puisse être mesuré et que le seuil et le repli de HF23 soient réglés avant que toute application ne prenne effet.

**HF23, en conception, visé au T4 2026.** Active l'application une fois que la version non contraignante Lokinet et nœud léger ci-dessus a été éprouvée : plafond d'enregistrement de cluster par proximité (enregistrements rejetés lorsqu'un cluster dépasse 30% des nœuds actifs) ; modificateur de récompense nulle pour les nœuds au-dessus du seuil de plafond classés par ancienneté d'enregistrement ; mise à niveau de la déduplication de quorum de la clé de portefeuille vers le cluster de proximité, avec une règle de repli obligatoire garantissant que la formation du quorum est toujours possible même lorsqu'il existe moins de 12 clusters distincts (les plus petits clusters reçoivent d'abord des sièges supplémentaires avant les clusters les plus concentrés, avec la fréquence des replis journalisée et publiée comme indicateur de risque de concentration). Une période de grâce de 30 jours s'applique à l'activation avant que le modificateur de récompense nulle ne prenne effet.

**Phase 6, Gouvernance formelle.** Processus de proposition structuré, vote pondéré pour les opérateurs, transition à long terme hors de la gouvernance par l'équipe fondatrice.

---

## 10. EXIOM Oracle

### Le premier oracle en service : EXIOM Oracle

Le premier produit oracle de la plateforme est en service sur le mainnet. L'EXIOM Oracle est un comité d'opérateurs de nœuds de service XEQM — chacun exécutant un sidecar oracle léger aux côtés de son nœud — qui produisent collectivement des attestations agrégées BLS et signées EIP-712 sur des faits de conformité, le plus directement si une adresse donnée est éligible pour une juridiction donnée. Les applications consomment ces attestations via l'API développeur et peuvent soumettre le résultat signé on-chain. Le comité est déployé sur Robinhood Chain (chainId 4663) et exploite un comité d'opérateurs de 12 membres au 28 septembre 2026, avec un seuil de signature de deux tiers (8 sur 12).

**Modèle de sécurité : ensemble enregistré versus seuil.** L'EXIOM Oracle n'échantillonne pas un comité par tour. Parce qu'une agrégation BLS coûte le même à vérifier pour la gate, que huit membres ou huit cents aient signé, chaque membre enregistré signe chaque tour ; échantillonner un sous-ensemble n'apporterait rien et réintroduirait le risque qu'un tirage malheureux détienne par hasard suffisamment de membres complices pour forger. La sécurité se réduit donc à deux propriétés de l'ensemble de membres enregistrés de taille N, au seuil de deux tiers k = ceil(2N/3) que la gate impose :

- **La forgerie** requiert qu'un adversaire contrôle au moins k membres enregistrés — une collusion, et donc une question de concentration d'**opérateurs**.
- **Le blocage** (une défaillance de vivacité) requiert qu'au moins N - k + 1 = floor(N/3) + 1 membres enregistrés deviennent inactifs en même temps — une panne corrélée, et donc une question de concentration d'**infrastructure**.

Ce sont les deux coefficients de Nakamoto, et ce sont des propriétés de l'ensemble enregistré, non de la flotte plus large de nœuds de service : la distribution de la flotte borne le consensus, tandis que la résistance de l'oracle à la forgerie et à la perte de vivacité dépend uniquement de qui détient les sièges enregistrés.

**Réalisation actuelle.** Au 28 septembre 2026, les membres enregistrés sont tous exploités par l'opérateur du projet, de sorte que le coefficient d'opérateurs de l'oracle est de 1 : aujourd'hui, sa résistance à la forgerie repose sur la confiance en un seul opérateur, non sur une cryptographie distribuée. C'est l'état de départ honnête. Le modèle de sécurité est k-parmi-N à travers des opérateurs indépendants ; la réalisation se durcit à mesure que des indépendants s'inscrivent, ce qui est l'objet de l'intégration d'opérateurs de nœuds de service additionnels comme membres sidecar. Le nombre de nœuds seul n'aide pas — des membres additionnels n'élèvent les deux coefficients que dans la mesure où ils sont des opérateurs indépendants sur des installations distinctes.

**Comment la diversité est appliquée.** Parce qu'il n'y a pas de sélection par tour, la diversité est décidée à l'**admission** : un membre n'est enregistré que s'il maintient la part de chaque opérateur sous k et la part de chaque installation à ou sous floor(N/3), et k est relevé pour suivre ceil(2N/3) à mesure que l'ensemble croît. La concentration de l'ensemble enregistré est surveillée en continu et publiée comme une marge de forgerie (k moins la part du plus grand opérateur) et une marge de vivacité (floor(N/3) + 1 moins la part de la plus grande installation) ; une marge non positive est une alarme. Le signal d'installation est aujourd'hui l'ASN et le timing d'arrivée des preuves de disponibilité, affiné à HF23 vers la proximité de routage Lokinet, qui détecte la co-localisation physique même à travers des ASN distincts. Ces faits de distribution sont eux-mêmes attestables via l'interface de faits typés de l'oracle, de sorte que la métrique de concentration est une valeur signée par le comité plutôt que la sortie d'un unique script de confiance.

Le sidecar est délibérément léger : il ne détient que sa propre clé de signature, lit l'identité de son nœud localement, et ne manipule jamais les clés de dépense de l'opérateur. L'exécuter est le mécanisme par lequel un opérateur de nœud de service gagne le revenu additionnel, financé par l'usage, décrit dans les Sections 3 et 4.

### La vision plus large : EXIOM Privacy Oracle

L'EXIOM Privacy Oracle permet aux applications de consommer des flux de données privées authentifiés sans exposer les données source sous-jacentes. Il utilise des techniques de preuve à divulgation nulle de connaissance pour prouver la provenance des données à partir de points de terminaison HTTPS standard, ne nécessitant aucune coopération côté serveur ni matériel de confiance. C'est un livrable de Phase 3, faisant suite à la stabilisation de la plateforme API de Phase 2 et à une consultation de cryptographie avant le début de la construction complète.

L'oracle n'est pas un flux de données à usage général. C'est un oracle axé sur la confidentialité pour les cas d'usage où les données elles-mêmes doivent rester confidentielles : seuils de prix sans révéler les prix exacts, soldes de comptes sans exposer les identifiants, attestations de conformité sans divulguer l'enregistrement sous-jacent. La plateforme RFQ EXIOM est le premier consommateur interne, l'utilisant pour prouver qu'un remplissage XEQM/BTC s'est produit à un prix de référence ou meilleur sans révéler le prix exact à la plateforme ou à l'autre partie.

Une fois Lokinet actif comme transport du réseau, la communication de session oracle entre le prouveur et le quorum de vérificateurs sera routée en oignon à travers le réseau de nœuds de service. Ni l'origine du prouveur ni les adresses réseau des nœuds du quorum ne seront visibles pour aucun nœud relais unique, éliminant l'hypothèse de confiance en un coordinateur centralisé.

### Architecture

**Couche prouveur.** L'application ou l'utilisateur détenant l'accès à la source de données privée participe à un protocole cryptographique qui s'engage sur la réponse TLS sans la révéler. Les identifiants et les données brutes ne quittent jamais le contrôle du prouveur.

**Couche vérificateur.** Un quorum tournant de nœuds de service vérifie que les données engagées satisfont la condition demandée. Les nœuds vérificateurs n'apprennent que le résultat (vrai ou faux, au-dessus ou en dessous d'un seuil) et ne voient jamais les données ou identifiants sous-jacents.

**Couche consommateur.** Les consommateurs ne reçoivent que la sortie minimale : un résultat booléen, une comparaison de seuil, une attestation signée, ou une petite valeur dérivée. Les données source brutes ne sont jamais publiées.

### Plan de construction par phases

**Phase 1, Preuve de concept interne.** L'équipe fondatrice valide le protocole cryptographique complet de bout en bout contre un petit ensemble de sources sur liste blanche, sans consommateurs externes ni participation de nœuds de service.

**Phase 2, Testnet d'oracle fédéré.** Des opérateurs de nœuds de service volontaires avec un solide historique de disponibilité rejoignent le pool de vérificateurs sur testnet. Tests adverses de l'intégrité des attestations avant tout déploiement sur mainnet.

**Phase 3, Oracle mainnet avec consommateurs internes.** La tâche de vérificateur d'oracle s'ouvre aux nœuds mainnet qualifiés. Les sorties alimentent les contrats EXIOM internes et la plateforme RFQ. Les frais d'oracle commencent à affluer vers les nœuds vérificateurs participants.

**Phase 4, Accès des consommateurs externes.** Sorties de l'oracle disponibles pour les développeurs de niveau Production et Entreprise et les consommateurs externes. Conditionné à l'achèvement de la Phase 3.

### Exigences matérielles des vérificateurs

Exigences indicatives : 8 cœurs CPU, 16 Go de RAM, 200 Go de SSD, 500 Mbps avec faible latence. Le matériel de base standard des nœuds API n'est pas suffisant pour la tâche de vérificateur d'oracle.

### Récompenses des vérificateurs

| Source de revenu | Description |
|---|---|
| Récompenses de bloc | Récompense de bloc standard de nœud de service, inchangée |
| Part de revenu de plateforme | Part proportionnelle du revenu de consommation des développeurs pour les opérateurs exécutant le sidecar oracle |
| Frais de session oracle | Frais par session des consommateurs de l'oracle, distribués au quorum de vérificateurs |
| Bonus de tâche oracle | Émission de gouvernance supplémentaire pendant les périodes de faible volume, réduite à mesure que les frais de session s'autofinancent |

---

## 11. Plateforme de trading RFQ EXIOM

La plateforme RFQ EXIOM est un système de trading de gré à gré pair-à-pair avec des attestations de règlement cryptographiques, construit sur l'API EXIOM. La première paire de trading est XEQM/BTC, deux actifs Layer 1 natifs sans tokenisation, sans enveloppement et sans risque de pont.

Une fois Lokinet actif, la plateforme RFQ sera accessible comme service caché Lokinet. Ni l'adresse IP du demandeur ni celle du LP ne seront visibles pour la plateforme. La couche de tarification de l'oracle permet à une contrepartie de prouver qu'un remplissage s'est produit à un prix de référence ou meilleur provenant d'une source sur liste blanche, sans révéler le prix exact du remplissage à la plateforme ou à l'autre partie.

La spécification de l'application RFQ et le modèle de données sont achevés. Le développement actif se poursuit en Phase 2 sur la couche API. La production complète de la plateforme de trading est un livrable de Phase 3, dépendant de l'atteinte de la production par l'API EXIOM et de l'achèvement par le MVP de l'oracle de sa preuve de concept interne.

---

---

## Langues disponibles

Des traductions communautaires de ce livre blanc sont maintenues dans le dossier translations pour plus de commodité. **La version anglaise est le document faisant autorité à tout moment.** Les traductions peuvent accuser un retard par rapport à la révision anglaise actuelle et ne sont pas garanties à jour ; en cas de conflit, d'ambiguïté ou de différence de quelque nature que ce soit, la version anglaise prévaut.

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

*Ceci est un document préliminaire. Les paramètres, calendriers d'émission et phases de feuille de route décrits ici sont la conception prévue. Des mises à jour seront publiées à mesure que le réseau et la plateforme évoluent.*

*Ce document ne constitue pas un conseil financier ou juridique. XEQM est une pièce utilitaire pour la plateforme EXIOM, et non un produit d'investissement. La classification des tokens, le statut au regard des valeurs mobilières et les réglementations applicables varient selon la juridiction. Les participants doivent consulter leur cadre juridique et réglementaire local avant d'acquérir ou d'opérer avec XEQM. XEQM Labs n'encourage pas l'achat de XEQM sur la base d'une appréciation spéculative du prix.*
