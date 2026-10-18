# Limites de concentration des nœuds - Application de la survivabilité du réseau
## Complément technique au livre blanc sur la tokenomique EXIOM
### 07/26/2026

> **Note de portée (mise à jour octobre 2026).** L'unité appliquée est le *cluster de proximité* (un groupe de nœuds qui partagent une infrastructure physique ou de routage, détecté via la proximité de routage Lokinet, le timing des preuves de disponibilité et l'ASN), **et non le pays**. Un pays comptant plusieurs installations indépendantes n'est pas affecté. Les chiffres par pays ci-dessous sont un indicateur géographique grossier de l'endroit où se situe actuellement la concentration, et non l'élément que le protocole plafonne. Les décomptes de nœuds dans ce complément sont un instantané de juillet 2026 (~672 nœuds) ; voir le livre blanc pour les totaux actuels du réseau (943 nœuds au 27 septembre 2026). Lokinet est livré dans une version non contraignante avant HF23, et HF23 active l'application.

Ce document est un complément au livre blanc sur la tokenomique EXIOM et suppose qu'il a été lu. Le livre blanc couvre ce que sont les contrôles de concentration et pourquoi ils existent. Ce document couvre le détail mécanique du fonctionnement de chaque contrôle, les données de validation sur testnet derrière HF22, les calculs économiques précis derrière le modificateur de récompense nulle, la question de l'identité de l'opérateur sur une chaîne de confidentialité, et les risques résiduels que le protocole ne résout pas entièrement.

---

## Les données de concentration actuelles

| Pays | Nœuds actifs |
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

La France détient 492 des 672 nœuds de cet instantané (environ 73% du réseau), et cette concentration est presque entièrement une seule installation Contabo en Grand Est détenant environ 426 nœuds (environ 63% du réseau). Le total par pays n'est pas ce que le protocole plafonne ; le **cluster** Grand Est l'est. Le seuil de survivabilité est de 30% des nœuds actifs par cluster de proximité (environ 202 nœuds aux 672 de cet instantané, et environ 283 aux 943 nœuds du livre blanc actuel), recalculé en continu à mesure que le réseau croît. Grand Est, à environ 426 nœuds, dépasse le double de ce plafond.

---

## Ce que cela signifie pour les opérateurs de nœuds

Cette section répond directement à la question : comment HF23 affecte-t-il la manière dont vous exploitez vos nœuds ?

**HF23 ne plafonne pas par pays, et n'exige pas un nœud par IP, un nœud par VPS, ou un nœud par portefeuille.** Le plafond est de 30% du réseau actif par *cluster de proximité* (nœuds qui partagent une infrastructure physique ou de routage). Un opérateur exploitant 10, 50, voire 100 nœuds sur une infrastructure partagée n'est absolument pas affecté par HF23 tant que son cluster reste sous ce seuil. Vous pouvez exécuter plusieurs nœuds sur une seule machine, un seul compte VPS et un seul portefeuille. Rien dans HF23 ne change cela.

**Le modificateur de récompense nulle ne s'applique qu'aux nœuds au-dessus du plafond par cluster (30% des nœuds actifs).** Les nœuds enregistrés les plus anciens dans un cluster gagnent la récompense complète jusqu'à ce seuil. Seuls les nœuds classés au-dessus de celui-ci dans un cluster surconcentré gagnent zéro, et seulement jusqu'à ce qu'ils soient migrés vers un cluster moins concentré.

**La déduplication de quorum plafonne l'influence sur le consensus par tour, pas le nombre de nœuds ni le revenu.** Un opérateur exploitant 50 nœuds sur un seul VPS gagne des récompenses de bloc sur les 50 et gère son infrastructure exactement comme aujourd'hui. Il reçoit un siège de quorum par cluster par tour au lieu d'un nombre potentiellement élevé, ce qui est le résultat recherché.

**La bonne approche pour un nouvel opérateur** est de consulter l'explorateur de nœuds, de voir où les clusters existants sont concentrés, et de déployer dans un cluster faiblement peuplé. Dix nœuds sur un serveur avec son propre routage distinct fonctionnent parfaitement sous HF23 parce que ce cluster est loin du seuil de 30%. Récompenses complètes, pleine participation au quorum, aucun problème.

**La dynamique joue en votre faveur si vous déployez dans des régions clairsemées.** Si une région finit par se remplir, l'explorateur de nœuds le montre et les opérateurs ont une incitation financière à se déplacer avant que le plafond ne les affecte. Les opérateurs arrivés en premier conservent les récompenses complètes sur leurs nœuds les plus anciens jusqu'au seuil. Les nouveaux enregistrements dans un cluster surconcentré ne gagnent rien immédiatement, de sorte que l'économie pousse naturellement les nouveaux déploiements vers les régions plus légères.

**Le problème précis que HF23 résout** est une installation en France (le cluster Contabo du Grand Est) hébergeant environ 426 nœuds, environ 63% du réseau dans cet instantané. Si cette installation tombe hors ligne, le réseau se bloque. L'objectif est de ramener ce cluster sous le plafond de 30%. Tout autre opérateur exploitant une configuration multi-nœuds responsable dans un cluster non concentré est exactement ce dont le réseau a besoin de plus.

---

## Pourquoi les hard forks sont séparés

HF22 est livré après des tests réussis. La déduplication de quorum par clé de portefeuille et l'unification de la période de déverrouillage n'ont aucune dépendance à Lokinet. Les deux ont été validées sur testnet et les retenir pendant que l'évaluation de Lokinet est en attente constitue un retard injustifié. Un acteur sophistiqué qui lit le livre blanc avant la livraison de HF22 pourrait tenter un fractionnement de portefeuille pour anticiper le contrôle de quorum, mais le faire est détectable via la corrélation du timing des preuves de disponibilité et l'analyse IP/ASN et crée un enregistrement documenté pour une action de gouvernance.

Lokinet est livré d'abord dans sa propre version non contraignante (aux côtés du changement de stockage en nœud léger SQLite), de sorte que le nouveau transport n'est pas rendu critique pour le consensus au moment même de son introduction. Pendant cette version, le regroupement par proximité fonctionne en service et observable sans conséquence sur les récompenses, c'est alors que le nombre réel de clusters est mesuré et que le seuil et le repli de HF23 sont réglés. HF23 suit ensuite et active l'application. Séparer les versions donne aussi des domaines de défaillance nets : si quelque chose tourne mal après l'activation de HF23, il y a moins de variables à isoler. Tant que l'application de HF23 n'est pas en service, Grand Est reste exposé au plein risque de survivabilité au-delà de la déduplication de quorum de HF22.

---

## Mécaniques de HF22

### Déduplication de quorum par clé de portefeuille

L'algorithme de sélection de quorum exécute une passe de déduplication sur chaque ensemble de candidats avant finalisation. Lorsque le tirage sélectionne un nœud candidat, l'algorithme vérifie son adresse de portefeuille d'opérateur contre tous les nœuds déjà sélectionnés pour le tour. Si une correspondance est trouvée, le candidat est remplacé par un nouveau tirage dans le pool éligible restant, excluant toutes les adresses déjà représentées.

Le tirage de remplacement ne repasse pas par les candidats déjà rejetés. Il tire dans le pool non sélectionné restant selon le même ordre pondéré par probabilité utilisé pour le tirage initial. Cela préserve les propriétés statistiques de la sélection de quorum sans introduire de biais déterministe vers un ensemble particulier de nœuds restants.

**Résultats de validation sur testnet :**
- 20 cycles de blocage/récupération terminés (20/20)
- Taux de récupération de 100% sur tous les cycles
- Zéro intervention manuelle requise dans aucun cycle (écart de bloc maximum 83 secondes)
- Référence mainnet pré-HF22 : 1,000 blocs, 100% Pulse, zéro bloc GOV_SIGNED
- Analyse de timeout R0 : aucun timeout R0 introduit en conditions de production. L'analyse de densité du mainnet actuel confirme que chaque cluster IP à haute densité est un seul opérateur, ce qui signifie que la déduplication par clé de portefeuille fournit déjà une protection complète contre les déploiements de baleines actuels. Les deux plus grands déploiements à IP unique (58 nœuds et 51 nœuds respectivement) sont chacun un seul opérateur et sont plafonnés à un siège de quorum par tour sous HF22.

**Ce qu'un siège de quorum signifie en pratique :** La taille du quorum et la fréquence de rotation déterminent la fréquence à laquelle un nœud participe. À la taille actuelle du réseau, un plafond d'un seul siège signifie que l'influence d'un opérateur concentré dans les sessions oracle, les tours Pulse et les quorums d'obligations est identique à celle d'un opérateur avec un seul nœud. Son revenu de récompense de bloc est inchangé.

**La lacune du fractionnement de portefeuille et sa détection intérimaire :** Un opérateur qui fractionne 426 nœuds sur 10 portefeuilles obtient jusqu'à 10 sièges de quorum par tour au lieu d'un. C'est la lacune connue que HF23 comble. Dans l'intervalle, le fractionnement de portefeuille est détectable via deux signaux déjà disponibles sans modification du daemon. Premièrement, le timing des preuves de disponibilité : les nœuds sur le même hôte physique ou hyperviseur soumettent des preuves à quelques millisecondes les uns des autres, quelle que soit la clé de portefeuille. Un cluster de preuves arrivant dans des fenêtres inférieures à 10 ms depuis des nœuds enregistrés sur différents portefeuilles est un signal fort d'infrastructure partagée. Deuxièmement, la corrélation IP et ASN : les nœuds sur différents portefeuilles partageant une IP, un sous-réseau ou un ASN sont journalisés et signalés pour revue de gouvernance. Un opérateur qui fractionne ses portefeuilles mais garde tous ses nœuds dans la même installation Contabo est identifiable via les deux signaux et sujet à une action de gouvernance sous la politique de liste de blocage.

### Unification de la période de déverrouillage

La période de déverrouillage du déréférencement forcé passe de 10,080 blocs (environ 7 jours) à 20,160 blocs (environ 14 jours), correspondant à la période de retrait volontaire. C'est un changement de constante de consensus.

La période forcée originale de 7 jours était un choix délibéré pendant la stabilisation du réseau pour limiter la pénalité sur les opérateurs subissant des événements d'infrastructure hors de leur contrôle. Cette justification ne s'applique plus. Le réseau est stable, le système de crédit de décommission fournit le tampon pour les pannes courtes, et une période unifiée de 14 jours supprime une asymétrie qui n'a plus de justification.

Les pièces XEQM sont verrouillées on-chain pendant la période de déverrouillage via la transaction d'enregistrement. Il n'existe aucun mécanisme pour libérer le verrou plus tôt sans un changement de protocole. Pour des défaillances d'infrastructure documentées, la gouvernance peut compenser les récompenses manquées depuis le portefeuille de gouvernance sous forme de transfert XEQM, mais le verrou on-chain court toute sa durée quoi qu'il arrive.

---

## Mécaniques de HF23

### Regroupement par proximité Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) achemine le trafic à travers le réseau de nœuds de service au niveau de la couche 3, prenant en charge TCP, UDP et ICMP. Chaque nœud de service participe comme relais. Le graphe de routage qui émerge reflète la topologie réseau physique : les nœuds de la même installation routent à travers le même commutateur en amont et la même dorsale de datacenter, produisant des sélections de chemins corrélées et une latence inter-nœuds inférieure à la milliseconde. Les nœuds d'installations différentes routent à travers des chemins différents avec une latence mesurablement plus élevée.

L'algorithme de regroupement ingère les mesures par paires de latence de routage Lokinet et de recouvrement de chemins à travers tous les nœuds actifs et les groupe en clusters en utilisant ces mesures comme signal de proximité. Un cluster n'est pas une région géographique fixe ; c'est un regroupement dynamique de nœuds dont le comportement de routage indique une infrastructure physique partagée. Deux nœuds dans des installations Contabo différentes dans des pays différents peuvent router à travers suffisamment d'infrastructure de dorsale Contabo partagée pour apparaître dans le même cluster si leur recouvrement de chemins est assez élevé. Deux nœuds dans le même datacenter mais sur des machines physiques différentes avec des connexions en amont différentes apparaîtront dans des clusters différents si leur recouvrement de chemins est faible.

Signaux complémentaires utilisés aux côtés de la proximité Lokinet :

**Corrélation du timing des preuves de disponibilité.** Le réseau reçoit déjà des preuves de disponibilité de tous les nœuds actifs selon un calendrier régulier. La distribution des horodatages d'arrivée des preuves de chaque nœud est enregistrée par les nœuds récepteurs. Les nœuds sur le même hôte physique ou hyperviseur de VM soumettent des preuves dans une fenêtre étroite caractéristique, typiquement sous 10 millisecondes. Regrouper cette distribution de timing d'arrivée fournit un signal de co-localisation physique qui ne nécessite aucune modification du daemon et fonctionne avant que Lokinet ne soit actif.

**Analyse ASN.** L'adresse IP de chaque nœud correspond à un Autonomous System Number via des données BGP publiques. Les nœuds partageant un ASN partagent une infrastructure de routage au niveau du fournisseur et une exposition juridique au niveau du fournisseur. Un fournisseur qui reçoit un ordre au niveau juridictionnel affectant toute son infrastructure met hors service tous ses nœuds ASN simultanément, quel que soit le nombre de clusters Lokinet dans lesquels ils apparaissent. La concentration d'ASN est suivie comme un signal complémentaire et contribue à la revue de gouvernance des opérateurs proches du seuil de cluster.

### Plafond d'enregistrement de cluster

Au moment de l'enregistrement, le protocole exécute une évaluation de proximité contre tous les clusters existants. Les caractéristiques de routage Lokinet du nœud enregistré sont mesurées contre le centroïde de chaque cluster existant. Si le cluster le plus proche contient déjà 30% ou plus des nœuds actifs, l'enregistrement est rejeté avec un code d'erreur spécifique indiquant la capacité du cluster et le nombre de nœuds du cluster le plus proche.

Le rejet est déterministe : tout nœud qui route suffisamment similairement à un cluster surconcentré pour y être assigné est rejeté, quelle que soit la clé de portefeuille de l'opérateur, son historique d'enregistrement ou son montant de stake. L'opérateur ne peut pas faire appel du rejet via la gouvernance. La seule voie à suivre est de s'enregistrer sur une infrastructure qui route vers un cluster différent.

Le seuil est évalué contre le nombre de nœuds actifs au moment de l'enregistrement. À mesure que le réseau croît, le seuil de 30% en termes absolus croît avec lui. Un opérateur au plafond aujourd'hui peut enregistrer des nœuds additionnels dans un cluster précédemment plafonné à mesure que le réseau croît et que le plafond absolu s'élève, sans migrer aucun nœud existant.

### Modificateur de récompense nulle

Le modificateur de récompense nulle est appliqué au moment du calcul de la récompense de bloc. Le calcul de récompense pour un nœud sélectionné inclut une vérification d'éligibilité de cluster. Si le cluster du nœud contient plus de nœuds que le seuil de plafond, et que le rang d'enregistrement du nœud au sein de ce cluster est au-dessus du seuil (classé du plus ancien au plus récent), le calcul de récompense retourne zéro.

Le classement est calculé à partir de la hauteur de bloc d'enregistrement du nœud au sein de son assignation de cluster. Le nœud enregistré le plus ancien du cluster obtient le rang 1, le plus récemment enregistré obtient le rang N. Les nœuds avec un rang supérieur au seuil de plafond gagnent zéro. Les nœuds avec un rang égal ou inférieur au seuil de plafond gagnent la récompense standard complète. Le classement est recalculé chaque fois que l'assignation de cluster change, ce qui se produit lorsque des nœuds migrent hors du cluster, lorsque de nouveaux nœuds rejoignent, ou lorsque la frontière du cluster se déplace en raison de changements de topologie réseau.

**Le calcul économique pour Grand Est :** À 426 nœuds avec un plafond de 208 nœuds, 218 nœuds gagnent zéro récompense de bloc. Au tarif auto-hébergé de 0,53 $ par nœud et par mois, ces 218 nœuds coûtent 115,54 $ par mois sans aucun revenu. Au tarif Pecunia de 1,76 $ par nœud et par mois, le coût est de 383,68 $ par mois. L'opérateur a deux réponses rationnelles : migrer les nœuds excédentaires vers des clusters non concentrés, restaurant leurs récompenses immédiatement dès l'acceptation du nouvel enregistrement, ou déréférencer les nœuds excédentaires et récupérer les XEQM en stake via le processus de déverrouillage. L'une ou l'autre réponse réduit la concentration. Il n'y a aucune base rationnelle pour maintenir les nœuds excédentaires à récompense nulle.

**Mécaniques de la période de grâce :** Au bloc d'activation de HF23, le protocole prend un instantané de tous les clusters actifs et de leurs décomptes de nœuds. Tout cluster dépassant le seuil de 30% est marqué comme surconcentré. Pendant les 30 jours suivant le bloc d'activation, le modificateur de récompense nulle est suspendu pour tous les nœuds, y compris ceux au-dessus du seuil de plafond. Pendant la période de grâce, les propriétaires de nœuds peuvent observer les assignations de cluster de l'explorateur de nœuds, planifier les migrations et commencer à les exécuter. Au bloc d'expiration de la période de grâce, le modificateur s'active. Les nœuds qui ont migré hors du cluster surconcentré avant ce bloc gagnent la récompense complète à partir de ce bloc. Les nœuds encore au-dessus du seuil gagnent zéro à partir de ce bloc jusqu'à leur migration.

### Déduplication de quorum par cluster de proximité

La mise à niveau de la déduplication de quorum de HF23 remplace la vérification d'adresse de portefeuille par une vérification d'appartenance à un cluster. Lorsque le tirage sélectionne un nœud candidat, l'algorithme vérifie son assignation de cluster contre tous les nœuds déjà sélectionnés pour le tour. Si deux nœuds partagent une assignation de cluster, le second est remplacé par un tirage dans le pool restant, excluant tous les clusters déjà représentés.

L'effet pratique sur un opérateur fractionnant ses portefeuilles : 10 adresses de portefeuille réparties sur 426 nœuds, tous dans la même installation Contabo, apparaissent dans le même cluster de proximité. La vérification de cluster les attrape tous comme une seule unité. Un nœud de ce cluster détient un siège. Les 425 autres nœuds de ce cluster ne le détiennent pas, quel que soit le nombre d'adresses de portefeuille distinctes sous lesquelles ils sont enregistrés.

### Exigence de nombre minimum de clusters et règle de repli

La taille du quorum du réseau EXIOM est de 12 sièges par tour. La déduplication par cluster de proximité nécessite donc au moins 12 clusters de proximité distincts dans l'ensemble des nœuds actifs pour garantir la formation du quorum. Si le réseau produit moins de 12 clusters distincts, l'algorithme ne peut pas satisfaire la contrainte d'un siège par cluster et la formation du quorum échoue.

La distribution actuelle du réseau, une fois le regroupement par proximité Lokinet appliqué, est estimée produire entre 12 et 18 clusters distincts. C'est inconfortablement proche du minimum de 12 sièges. Une infrastructure de dorsale de fournisseur partagée entre des installations nominalement distinctes peut faire fusionner deux localisations IP distinctes en un seul cluster de proximité dans le graphe de routage Lokinet. Toute fusion de ce type qui réduit le nombre de clusters sous 12 brise entièrement la formation du quorum.

L'algorithme met donc en œuvre une règle de repli obligatoire :

1. L'algorithme tente de pourvoir les 12 sièges avec un nœud par cluster distinct, parcourant les clusters disponibles dans un ordre aléatoire.
2. Si tous les clusters distincts sont épuisés avant que les 12 sièges ne soient pourvus, l'algorithme entre dans une passe de repli.
3. Dans la passe de repli, il autorise un deuxième nœud de chaque cluster, en commençant par les plus petits clusters. Les clusters les moins concentrés reçoivent un deuxième siège avant les plus concentrés.
4. L'algorithme poursuit les passes de repli, incrémentant le nombre maximum de sièges par cluster d'une unité à chaque passe, jusqu'à ce que les 12 sièges soient pourvus.
5. Le cluster le plus concentré, tel que Grand Est dans les conditions actuelles, ne reçoit des sièges supplémentaires qu'après que tous les clusters plus petits ont reçu leur allocation de repli.

Chaque tour qui déclenche le repli est journalisé avec le nombre de clusters qui l'a causé. La gouvernance surveille la fréquence des replis comme indicateur direct de risque de concentration. Un réseau avec 12 clusters distincts ou plus ne déclenche jamais le repli. Un réseau déclenchant constamment le repli signale que l'application de la concentration de HF23 n'atteint pas encore une diversité physique adéquate et que le plafond de cluster ou l'application de la période de grâce requiert l'attention de la gouvernance.

Le journal de repli est publié dans l'explorateur de nœuds aux côtés des assignations de cluster afin que la communauté d'opérateurs puisse observer le risque de concentration en temps réel.

---

## Identité de l'opérateur sur une chaîne de confidentialité

Le protocole n'a pas besoin d'identifier quel opérateur humain possède quels nœuds pour appliquer le plafond de cluster et le modificateur de récompense nulle. Les deux contrôles opèrent au niveau du cluster. Ce qui peut et ne peut pas être déterminé est un contexte utile pour la surveillance de gouvernance mais n'est pas requis pour l'application du protocole.

**Ce qui est déterministe à partir des données on-chain :** les nœuds enregistrés sous la même clé de portefeuille d'opérateur sont définitivement le même opérateur. C'est une information publique dans la transaction d'enregistrement.

**Ce qui est inférable avec une grande confiance à partir des données Lokinet et de timing :** le nombre d'hôtes physiques distincts sous-tendant un cluster de nœuds, quel que soit le nombre de clés de portefeuille qu'ils utilisent. Cinq clés de portefeuille exécutant chacune 85 nœuds, tous sur les deux mêmes serveurs physiques, produisent deux signatures de timing distinctes et deux centroïdes de proximité Lokinet, non cinq.

**Ce qui ne peut pas être déterminé sur une chaîne de confidentialité :** si deux clés de portefeuille différentes avec une infrastructure distincte appartiennent au même opérateur humain. La source de financement de chaque clé de portefeuille est privée par conception. Un opérateur sophistiqué utilisant cinq portefeuilles financés à partir de cinq sources différentes via la couche de transaction de la chaîne de confidentialité présente cinq identités distinctes au niveau du protocole.

Pour l'application de la survivabilité, cela n'a pas d'importance. Le cluster contient 426 nœuds. Les 208 plus anciens gagnent des récompenses. Les 218 plus récents gagnent zéro. L'identité de l'opérateur est sans pertinence pour ce calcul.

---

## Statut de mise en œuvre

| Contrôle | Statut |
|---|---|
| Déduplication de quorum par clé de portefeuille d'opérateur | HF22, activé au bloc 219120 |
| Unification de la période de déverrouillage, 7 à 14 jours | HF22, activé |
| Récupération après blocage Pulse (repli par signature, snode_revision 1) | Activé au bloc 236920, 18 octobre 2026 |
| Activation de Lokinet comme transport du réseau | En développement ; livré dans une version non contraignante avant HF23 |
| Stockage en nœud léger SQLite | En développement ; livré avec la version Lokinet antérieure à HF23 |
| Algorithme de regroupement par proximité | Phase de conception, en attente de l'évaluation Lokinet |
| Plafond d'enregistrement de cluster, seuil de 30% | HF23, phase de conception |
| Modificateur de récompense nulle pour les nœuds excédentaires | HF23, phase de conception |
| Mécanisme de période de grâce | HF23, phase de conception |
| Déduplication de quorum par cluster de proximité avec règle de repli | HF23, phase de conception |
| Surveillance du nombre minimum de clusters et journalisation des replis | HF23, phase de conception |
| Outillage de corrélation du timing des preuves de disponibilité | Aucune modification du daemon requise, outillage en développement |
| Complément de regroupement ASN | Aucune modification du daemon requise, outillage en développement |

---

## Ce que ces contrôles ne résolvent pas

**Concentration juridique au niveau du fournisseur.** Un fournisseur recevant un ordre juridique au niveau juridictionnel affectant toute son infrastructure mondiale met hors service tous ses nœuds simultanément, même si ces nœuds apparaissent dans plusieurs clusters de proximité Lokinet. L'analyse ASN fait émerger ce risque mais le protocole ne peut pas imposer la diversité des fournisseurs sans exiger la divulgation par l'opérateur de l'identité de son fournisseur. La dispersion géographique naturellement produite par le plafond de cluster atténue substantiellement ce risque en pratique, puisque les opérateurs forcés de se répartir entre clusters utiliseront en pratique plusieurs fournisseurs.

**Détermination de l'identité de l'opérateur humain à travers les fractionnements de portefeuille sur chaîne de confidentialité.** Comme décrit ci-dessus, un opérateur sophistiqué utilisant plusieurs portefeuilles financés via la chaîne de confidentialité ne peut pas être identifié au niveau du protocole. Le plafond de cluster et le modificateur de récompense nulle traitent le risque de domaine de défaillance quelle que soit l'identité. La déduplication de quorum comble la lacune d'influence sur le consensus dans HF23. Le risque résiduel est qu'un opérateur sophistiqué exploite de nombreux nœuds à travers de nombreux clusters réellement distincts, accumulant un revenu de récompense de bloc proportionnel à son nombre de nœuds tout en contribuant proportionnellement à la santé du réseau. C'est le résultat acceptable : l'influence concentrée sur le consensus est bornée ; la participation en capital distribuée est récompensée.

Les opérateurs ayant des questions sur l'assignation de cluster, la planification de migration ou le calendrier HF22/HF23 sont encouragés à publier dans le canal Telegram des Node Operators ou à ouvrir une issue dans ce dépôt.

---

## Langues disponibles

Des traductions communautaires de ce document sont maintenues dans le dépôt du livre blanc. En cas de conflit entre une traduction et la version anglaise, la version anglaise prévaut.

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

*Ce document ne constitue pas un conseil financier ou juridique. XEQM est une pièce utilitaire pour la plateforme EXIOM, et non un produit d'investissement. La classification des tokens, le statut au regard des valeurs mobilières et les réglementations applicables varient selon la juridiction. Les participants doivent consulter leur cadre juridique et réglementaire local avant d'acquérir ou d'opérer avec XEQM. XEQM Labs n'encourage pas l'achat de XEQM sur la base d'une appréciation spéculative du prix.*
