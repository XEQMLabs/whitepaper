# Limites de concentration des nœuds - Application de la survivabilité du réseau
## Complément technique au livre blanc sur la tokenomique d'EXIOM
### 26/07/2026

> **Note de portée (mise à jour le 19 octobre 2026).** L'unité appliquée est le *cluster de proximité* (un groupe de nœuds qui partagent une infrastructure physique ou de routage, détecté via la proximité de routage Lokinet, le minutage des preuves de disponibilité et l'ASN), **et non le pays** ni le pays d'enregistrement d'un fournisseur. Un pays ou un fournisseur disposant de plusieurs installations véritablement indépendantes présente moins de risque qu'une installation unique détenant une part importante. Les données de concentration ci-dessous sont un instantané du 19 octobre 2026 (893 nœuds actifs) regroupées par fournisseur d'hébergement, le meilleur indicateur indirect disponible avant Lokinet. Lokinet est livré dans une version non contraignante avant HF23, et HF23 active l'application.

Ce document est un complément au livre blanc sur la tokenomique d'EXIOM et suppose qu'il a été lu. Le livre blanc explique ce que sont les contrôles de concentration et pourquoi ils existent. Ce document couvre le détail mécanique du fonctionnement de chaque contrôle, les données de validation sur testnet derrière HF22, les mathématiques économiques précises derrière le modificateur de récompense nulle, la question de l'identité de l'opérateur sur une chaîne de confidentialité, et les risques résiduels que le protocole ne résout pas entièrement.

---

## Les données de concentration actuelles

Mesurées le 19 octobre 2026 à 893 nœuds actifs, regroupées par fournisseur d'hébergement (ASN), qui est le signal de concentration disponible aujourd'hui avant Lokinet. Le fournisseur est un indicateur indirect bien meilleur d'un domaine de défaillance partagé qu'un drapeau de pays, car le réseau et les installations d'une même entreprise tendent à défaillir, ou à être mis hors ligne sur ordre, ensemble.

| Fournisseur (ASN) | Nœuds actifs | Part |
|---|---|---|
| NodeHub (AS214083) | 444 | 49,7 % |
| Contabo (AS51167, plus AS40021 et Contabo Asia AS141995) | ~303 | ~34 % |
| OVH (AS16276) | 62 | 6,9 % |
| Oracle (AS31898) | 22 | 2,5 % |
| WebNX (AS18450) | 12 | 1,3 % |
| tous les autres fournisseurs combinés (12 ASN de plus) | ~50 | ~5,6 % |

NodeHub détient à lui seul 49,7 % du réseau, bien au-delà du plafond de survivabilité de 30 % (267 nœuds sur 893 actifs), et un seul sous-réseau /24 détient 41,2 %. Ce fournisseur unique est la concentration que HF23 est conçu pour briser.

Comment on en est arrivé là. Pecunia, un service d'hébergement qui proposait de faire fonctionner des nœuds XEQM pour les opérateurs, a placé la plupart de ses nœuds sur Contabo. Les performances de Pecunia ont été médiocres, et de nombreux opérateurs ont depuis migré vers NodeHub. Ainsi, le domaine de défaillance dominant s'est déplacé de Contabo, qui détient toujours environ un tiers du réseau (en grande partie l'installation du Grand Est), vers NodeHub, désormais le plus grand cluster unique du réseau.

Une note sur les chiffres par pays. Le pays d'enregistrement d'un fournisseur n'est pas l'endroit où se trouvent ses serveurs. NodeHub est enregistré aux États-Unis et Contabo est enregistré en Allemagne, de sorte qu'une vue par pays étiquette leurs nœuds US et DE indépendamment du centre de données physique (la plus grande installation XEQM de Contabo se trouve dans le Grand Est, en France). Le protocole ne plafonne ni le pays ni l'enregistrement du fournisseur. Il plafonne le cluster de proximité, l'ensemble des nœuds qui partagent effectivement une infrastructure physique ou de routage. L'ASN et le sous-réseau sont l'indicateur indirect d'aujourd'hui pour cela, et HF23 les remplace par la proximité de routage Lokinet, qui peut aussi séparer des installations distinctes au sein d'un même fournisseur. Le seuil est de 30 % des nœuds actifs par cluster (267 aux 893 actuels), recalculé en continu à mesure que le réseau croît.

---

## Ce que cela signifie pour les opérateurs de nœuds

Cette section répond directement à la question : comment HF23 affecte-t-il la manière dont vous exploitez vos nœuds ?

**HF23 ne plafonne pas par pays, et n'exige pas un nœud par IP, un nœud par VPS, ou un nœud par portefeuille.** Le plafond est de 30 % du réseau actif par *cluster de proximité* (nœuds qui partagent une infrastructure physique ou de routage). Un opérateur exploitant 10, 50, voire 100 nœuds sur une infrastructure partagée n'est absolument pas affecté par HF23 tant que son cluster reste en dessous de ce seuil. Vous pouvez exécuter plusieurs nœuds sur une seule machine, un seul compte VPS et un seul portefeuille. Rien dans HF23 ne change cela.

**Le modificateur de récompense nulle s'applique uniquement aux nœuds au-dessus du plafond par cluster (30 % des nœuds actifs).** Les nœuds enregistrés les plus anciens dans un cluster perçoivent les récompenses complètes jusqu'à ce seuil. Seuls les nœuds classés au-dessus de ce seuil dans un cluster surconcentré perçoivent zéro, et seulement jusqu'à ce qu'ils soient migrés vers un cluster moins concentré.

**La déduplication de quorum plafonne l'influence sur le consensus par tour, et non le nombre de nœuds ni le revenu.** Un opérateur exploitant 50 nœuds sur un seul VPS perçoit des récompenses de bloc sur les 50 et gère son infrastructure exactement comme aujourd'hui. Il reçoit un siège de quorum par cluster par tour au lieu de potentiellement plusieurs, ce qui est le résultat recherché.

**La bonne approche pour un nouvel opérateur** consiste à consulter l'explorateur de nœuds, à voir où les clusters existants sont concentrés, et à déployer dans un cluster peu peuplé. Dix nœuds sur un seul serveur avec son propre routage distinct fonctionnent parfaitement bien sous HF23, car ce cluster est loin du seuil de 30 %. Récompenses complètes, participation complète au quorum, aucun problème.

**La dynamique joue en votre faveur si vous déployez dans des régions clairsemées.** Si une région finit par se remplir, l'explorateur de nœuds le montre et les opérateurs ont une incitation financière à se déplacer avant que le plafond ne les affecte. Les opérateurs arrivés en premier conservent les récompenses complètes sur leurs nœuds les plus anciens jusqu'au seuil. Les nouvelles inscriptions dans un cluster surconcentré ne perçoivent rien immédiatement, de sorte que l'économie pousse naturellement les nouveaux déploiements vers des régions plus légères.

**Le problème spécifique que HF23 résout** est celui d'un fournisseur unique, NodeHub, hébergeant désormais environ la moitié du réseau (444 nœuds, 49,7 %), avec Contabo en deuxième position à environ un tiers. Si l'infrastructure de NodeHub tombe hors ligne ou est mise hors service sur ordre, le réseau cale. L'objectif est de faire passer chaque cluster en dessous du plafond de 30 %. Chaque opérateur exploitant une configuration multi-nœuds responsable sur un fournisseur ou une installation différent et non concentré est exactement ce dont le réseau a besoin davantage.

---

## Pourquoi les hard forks sont séparés

HF22 est livré après des tests réussis. La déduplication de quorum par clé de portefeuille et l'unification de la période de déblocage n'ont aucune dépendance à Lokinet. Les deux ont été validées sur testnet, et les retenir pendant que l'évaluation de Lokinet est en attente constitue un retard injustifié. Un acteur sophistiqué qui lit le livre blanc avant la livraison de HF22 pourrait tenter un fractionnement de portefeuilles pour anticiper le contrôle de quorum, mais le faire est détectable par la corrélation de minutage des preuves de disponibilité et l'analyse IP/ASN, et crée un enregistrement documenté pour une action de gouvernance.

Lokinet est livré en premier dans sa propre version non contraignante (en même temps que le changement de stockage SQLite pour les nœuds légers), de sorte que le nouveau transport n'est pas rendu critique pour le consensus au moment même où il est introduit. Pendant cette version, le clustering de proximité fonctionne en direct et de manière observable sans conséquence sur les récompenses, c'est alors que le nombre réel de clusters est mesuré et que le seuil HF23 et le repli sont ajustés. HF23 suit ensuite et active l'application. La séparation des versions donne aussi des domaines de défaillance nets : si quelque chose tourne mal après l'activation de HF23, il y a moins de variables à isoler. Jusqu'à ce que l'application de HF23 soit active, le Grand Est reste exposé au risque de survivabilité complet au-delà de la déduplication de quorum de HF22.

---

## Mécanique de HF22

### Déduplication de quorum par clé de portefeuille

L'algorithme de sélection de quorum effectue une passe de déduplication sur chaque ensemble de candidats avant de finaliser. Lorsque le tirage sélectionne un nœud candidat, l'algorithme vérifie l'adresse du portefeuille de son opérateur par rapport à tous les nœuds déjà sélectionnés pour le tour. Si une correspondance est trouvée, le candidat est remplacé par un nouveau tirage parmi le pool éligible restant, en excluant toutes les adresses déjà représentées.

Le tirage de remplacement ne repasse pas par les candidats déjà rejetés. Il tire dans le pool non sélectionné restant selon le même ordre pondéré par probabilité utilisé pour le tirage initial. Cela préserve les propriétés statistiques de la sélection de quorum sans introduire de biais déterministe en faveur d'un ensemble particulier de nœuds restants.

**Résultats de validation sur testnet :**
- 20 cycles de blocage/récupération réalisés (20/20)
- Taux de récupération de 100 % sur tous les cycles
- Aucune intervention manuelle requise dans aucun cycle (pire écart entre blocs de 83 secondes)
- Référence mainnet pré-HF22 : 1 000 blocs, 100 % Pulse, zéro bloc GOV_SIGNED
- Analyse des délais d'expiration R0 : aucun délai d'expiration R0 introduit dans les conditions de production. L'analyse de densité du mainnet actuel confirme que chaque cluster IP à haute densité est un opérateur unique, ce qui signifie que la déduplication par clé de portefeuille fournit déjà une protection complète contre les déploiements de baleines actuels. Les deux plus grands déploiements à IP unique (58 nœuds et 51 nœuds respectivement) sont chacun un seul opérateur et sont plafonnés à un siège de quorum par tour sous HF22.

**Ce qu'un siège de quorum signifie en pratique :** La taille du quorum et la fréquence de rotation déterminent la fréquence de participation d'un nœud. À la taille actuelle du réseau, un plafond d'un siège signifie que l'influence d'un opérateur concentré dans les sessions d'oracle, les tours Pulse et les quorums d'obligations est identique à celle d'un opérateur avec un seul nœud. Son revenu de récompense de bloc est inchangé.

**La faille du fractionnement de portefeuilles et sa détection provisoire :** Un opérateur qui fractionne 426 nœuds sur 10 portefeuilles obtient jusqu'à 10 sièges de quorum par tour au lieu d'un. C'est la faille connue que HF23 comble. Dans l'intervalle, le fractionnement de portefeuilles est détectable par deux signaux déjà disponibles sans modification du démon. Premièrement, le minutage des preuves de disponibilité : les nœuds sur le même hôte physique ou hyperviseur soumettent leurs preuves à quelques millisecondes d'écart, indépendamment de la clé de portefeuille. Un cluster de preuves arrivant dans des fenêtres inférieures à 10 ms depuis des nœuds enregistrés sous différents portefeuilles est un signal fort d'infrastructure partagée. Deuxièmement, la corrélation IP et ASN : les nœuds sur différents portefeuilles partageant une IP, un sous-réseau ou un ASN sont enregistrés et signalés pour examen par la gouvernance. Un opérateur qui fractionne ses portefeuilles mais garde tous ses nœuds dans la même installation Contabo est identifiable par les deux signaux et soumis à une action de gouvernance au titre de la politique de liste de blocage.

### Unification de la période de déblocage

La période de déblocage pour désinscription forcée passe de 10 080 blocs (environ 7 jours) à 20 160 blocs (environ 14 jours), correspondant à la période de retrait volontaire. Il s'agit d'un changement de constante de consensus.

La période forcée initiale de 7 jours était un choix délibéré lors de la stabilisation du réseau, afin de limiter la pénalité pour les opérateurs subissant des événements d'infrastructure hors de leur contrôle. Cette justification ne s'applique plus. Le réseau est stable, le système de crédit de mise hors service fournit le tampon pour les courtes interruptions, et une période unifiée de 14 jours supprime une asymétrie qui n'a plus de justification.

Les pièces XEQM sont verrouillées sur la chaîne pendant la période de déblocage via la transaction d'enregistrement. Il n'existe aucun mécanisme pour libérer le verrou plus tôt sans un changement de protocole. Pour les défaillances d'infrastructure documentées, la gouvernance peut compenser les récompenses manquées depuis le portefeuille de gouvernance sous forme de transfert XEQM, mais le verrou sur la chaîne court sa durée complète quoi qu'il arrive.

---

## Mécanique de HF23

### Clustering de proximité Lokinet

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) achemine le trafic à travers le réseau de nœuds de service à la couche 3, prenant en charge TCP, UDP et ICMP. Chaque nœud de service participe comme relais. Le graphe de routage qui émerge reflète la topologie physique du réseau : les nœuds d'une même installation acheminent par le même commutateur amont et la même dorsale de centre de données, produisant des sélections de chemin corrélées et une latence inter-nœuds inférieure à la milliseconde. Les nœuds d'installations différentes acheminent par des chemins différents avec une latence mesurablement plus élevée.

L'algorithme de clustering ingère les mesures par paires de latence de routage Lokinet et de chevauchement de chemins sur tous les nœuds actifs et les regroupe en clusters en utilisant ces mesures comme signal de proximité. Un cluster n'est pas une région géographique fixe ; c'est un regroupement dynamique de nœuds dont le comportement de routage indique une infrastructure physique partagée. Deux nœuds dans des installations Contabo différentes dans des pays différents peuvent acheminer par suffisamment d'infrastructure de dorsale Contabo partagée pour apparaître dans le même cluster si leur chevauchement de chemins est assez élevé. Deux nœuds dans le même centre de données mais sur des machines physiques différentes avec des connexions amont différentes apparaîtront dans des clusters différents si leur chevauchement de chemins est faible.

Signaux supplémentaires utilisés en complément de la proximité Lokinet :

**Corrélation du minutage des preuves de disponibilité.** Le réseau reçoit déjà des preuves de disponibilité de tous les nœuds actifs selon un calendrier régulier. La distribution des horodatages d'arrivée des preuves de chaque nœud est enregistrée par les nœuds récepteurs. Les nœuds sur le même hôte physique ou hyperviseur de VM soumettent leurs preuves dans une fenêtre serrée caractéristique, généralement inférieure à 10 millisecondes. Le clustering de cette distribution de minutage d'arrivée fournit un signal de colocalisation physique qui ne nécessite aucune modification du démon et fonctionne avant que Lokinet ne soit actif.

**Analyse ASN.** L'adresse IP de chaque nœud correspond à un numéro de système autonome (ASN) via les données BGP publiques. Les nœuds partageant un ASN partagent une infrastructure de routage au niveau du fournisseur et une exposition juridique au niveau du fournisseur. Un fournisseur qui reçoit un ordre de niveau juridictionnel affectant toute son infrastructure met hors service tous ses nœuds ASN simultanément, indépendamment du nombre de clusters Lokinet dans lesquels ils apparaissent. La concentration d'ASN est suivie comme signal supplémentaire et contribue à l'examen par la gouvernance des opérateurs proches du seuil de cluster.

### Plafond d'enregistrement par cluster

Au moment de l'enregistrement, le protocole effectue une évaluation de proximité par rapport à tous les clusters existants. Les caractéristiques de routage Lokinet du nœud en cours d'enregistrement sont mesurées par rapport au centroïde de chaque cluster existant. Si le cluster le plus proche contient déjà 30 % ou plus des nœuds actifs, l'enregistrement est rejeté avec un code d'erreur spécifique indiquant la capacité du cluster et le nombre de nœuds du cluster le plus proche.

Le rejet est déterministe : tout nœud qui achemine de manière suffisamment similaire à un cluster surconcentré pour y être affecté est rejeté, indépendamment de la clé de portefeuille de l'opérateur, de son historique d'enregistrement ou du montant de sa mise. L'opérateur ne peut pas faire appel du rejet via la gouvernance. La seule voie possible est de s'enregistrer sur une infrastructure qui achemine vers un cluster différent.

Le seuil est évalué par rapport au nombre de nœuds actifs au moment de l'enregistrement. À mesure que le réseau croît, le seuil de 30 % en termes absolus croît avec lui. Un opérateur au plafond aujourd'hui peut enregistrer des nœuds supplémentaires dans un cluster précédemment plafonné à mesure que le réseau croît et que le plafond absolu augmente, sans migrer aucun nœud existant.

### Modificateur de récompense nulle

Le modificateur de récompense nulle est appliqué au moment du calcul de la récompense de bloc. Le calcul de la récompense pour un nœud sélectionné inclut une vérification d'éligibilité du cluster. Si le cluster du nœud contient plus de nœuds que le seuil du plafond, et que le rang d'enregistrement du nœud au sein de ce cluster est au-dessus du seuil (classé du plus ancien au plus récent), le calcul de la récompense renvoie zéro.

Le classement est calculé à partir de la hauteur du bloc d'enregistrement du nœud au sein de son affectation de cluster. Le nœud enregistré le plus ancien du cluster obtient le rang 1, le plus récemment enregistré obtient le rang N. Les nœuds dont le rang est supérieur au seuil du plafond perçoivent zéro. Les nœuds dont le rang est au seuil du plafond ou en dessous perçoivent la récompense standard complète. Le classement est recalculé à chaque fois que l'affectation du cluster change, ce qui se produit lorsque des nœuds migrent hors du cluster, lorsque de nouveaux nœuds le rejoignent, ou lorsque la frontière du cluster se déplace en raison de changements de topologie du réseau.

**Les mathématiques économiques pour le Grand Est :** À 426 nœuds avec un plafond de 208 nœuds, 218 nœuds perçoivent zéro récompense de bloc. Au tarif auto-hébergé de 0,53 $ par nœud par mois, ces 218 nœuds coûtent 115,54 $ par mois sans revenu. Au tarif Pecunia de 1,76 $ par nœud par mois, le coût est de 383,68 $ par mois. L'opérateur a deux réponses rationnelles : migrer les nœuds excédentaires vers des clusters non concentrés, rétablissant leurs récompenses immédiatement dès que le nouvel enregistrement est accepté, ou désinscrire les nœuds excédentaires et récupérer le XEQM mis en jeu via le processus de déblocage. L'une ou l'autre réponse réduit la concentration. Il n'y a aucune base rationnelle pour maintenir les nœuds excédentaires à récompense nulle.

**Mécanique de la période de grâce :** Au bloc d'activation de HF23, le protocole prend un instantané de tous les clusters actifs et de leur nombre de nœuds. Tout cluster dépassant le seuil de 30 % est marqué comme surconcentré. Pendant 30 jours suivant le bloc d'activation, le modificateur de récompense nulle est suspendu pour tous les nœuds, y compris ceux au-dessus du seuil du plafond. Pendant la période de grâce, les propriétaires de nœuds peuvent observer les affectations de clusters de l'explorateur de nœuds, planifier les migrations et commencer à les exécuter. Au bloc d'expiration de la période de grâce, le modificateur s'active. Les nœuds qui ont migré hors du cluster surconcentré avant ce bloc perçoivent les récompenses complètes à partir de ce bloc. Les nœuds encore au-dessus du seuil perçoivent zéro à partir de ce bloc jusqu'à ce qu'ils migrent.

### Déduplication de quorum par cluster de proximité

La mise à niveau de déduplication de quorum de HF23 remplace la vérification d'adresse de portefeuille par une vérification d'appartenance à un cluster. Lorsque le tirage sélectionne un nœud candidat, l'algorithme vérifie son affectation de cluster par rapport à tous les nœuds déjà sélectionnés pour le tour. Si deux nœuds partagent une affectation de cluster, le second est remplacé par un tirage dans le pool restant, en excluant tous les clusters déjà représentés.

L'effet pratique sur un opérateur pratiquant le fractionnement de portefeuilles : 10 adresses de portefeuille réparties sur 426 nœuds tous dans la même installation Contabo apparaissent dans le même cluster de proximité. La vérification de cluster les capture tous comme une seule unité. Un nœud de ce cluster détient un siège. Les 425 autres nœuds de ce cluster n'en détiennent pas, indépendamment du nombre d'adresses de portefeuille distinctes sous lesquelles ils sont enregistrés.

### Exigence de nombre minimal de clusters et règle de repli

La taille du quorum du réseau EXIOM est de 12 sièges par tour. La déduplication par cluster de proximité exige donc au moins 12 clusters de proximité distincts dans l'ensemble des nœuds actifs pour garantir la formation du quorum. Si le réseau produit moins de 12 clusters distincts, l'algorithme ne peut pas satisfaire la contrainte d'un siège par cluster et la formation du quorum échoue.

La distribution actuelle du réseau, une fois le clustering de proximité Lokinet appliqué, est estimée produire entre 12 et 18 clusters distincts. C'est inconfortablement proche du minimum de 12 sièges. Une infrastructure de dorsale de fournisseur partagée entre des installations nominalement séparées peut faire fusionner deux emplacements IP distincts en un seul cluster de proximité dans le graphe de routage Lokinet. Toute fusion de ce type qui réduit le nombre de clusters en dessous de 12 brise entièrement la formation du quorum.

L'algorithme met donc en œuvre une règle de repli obligatoire :

1. L'algorithme tente de remplir les 12 sièges avec un nœud par cluster distinct, en parcourant les clusters disponibles dans un ordre aléatoire.
2. Si tous les clusters distincts sont épuisés avant que les 12 sièges ne soient remplis, l'algorithme entre dans une passe de repli.
3. Dans la passe de repli, il autorise un second nœud de chaque cluster, en commençant par les plus petits clusters d'abord. Les clusters les moins concentrés reçoivent un second siège avant les plus concentrés.
4. L'algorithme poursuit les passes de repli, incrémentant le nombre maximal de sièges par cluster d'un à chaque passe, jusqu'à ce que les 12 sièges soient remplis.
5. Le cluster le plus concentré, tel que le Grand Est dans les conditions actuelles, reçoit des sièges supplémentaires seulement après que tous les clusters plus petits ont reçu leur allocation de repli.

Chaque tour qui déclenche le repli est enregistré avec le nombre de clusters qui l'a causé. La gouvernance surveille la fréquence des replis comme indicateur direct de risque de concentration. Un réseau avec 12 clusters distincts ou plus ne déclenche jamais le repli. Un réseau déclenchant systématiquement le repli signale que l'application de la concentration de HF23 n'atteint pas encore une diversité physique adéquate et que le plafond de cluster ou l'application de la période de grâce requiert l'attention de la gouvernance.

Le journal de repli est publié dans l'explorateur de nœuds aux côtés des affectations de clusters afin que la communauté des opérateurs puisse observer le risque de concentration en temps réel.

---

## Identité de l'opérateur sur une chaîne de confidentialité

Le protocole n'a pas besoin d'identifier quel opérateur humain possède quels nœuds pour appliquer le plafond de cluster et le modificateur de récompense nulle. Les deux contrôles opèrent au niveau du cluster. Ce qui peut et ne peut pas être déterminé est un contexte utile pour la surveillance par la gouvernance, mais n'est pas requis pour l'application du protocole.

**Ce qui est déterministe à partir des données sur la chaîne :** les nœuds enregistrés sous la même clé de portefeuille d'opérateur sont définitivement le même opérateur. C'est une information publique dans la transaction d'enregistrement.

**Ce qui est inférable avec une grande confiance à partir des données Lokinet et de minutage :** le nombre d'hôtes physiques distincts sous-jacents à un cluster de nœuds, indépendamment du nombre de clés de portefeuille qu'ils utilisent. Cinq clés de portefeuille exécutant chacune 85 nœuds, toutes sur les deux mêmes serveurs physiques, produisent deux signatures de minutage distinctes et deux centroïdes de proximité Lokinet, et non cinq.

**Ce qui ne peut pas être déterminé sur une chaîne de confidentialité :** si deux clés de portefeuille différentes avec une infrastructure distincte appartiennent au même opérateur humain. La source de financement de chaque clé de portefeuille est privée par conception. Un opérateur sophistiqué utilisant cinq portefeuilles financés depuis cinq sources différentes via la couche de transaction de la chaîne de confidentialité présente cinq identités distinctes au niveau du protocole.

Pour l'application de la survivabilité, cela n'a pas d'importance. Le cluster contient 426 nœuds. Les 208 plus anciens perçoivent des récompenses. Les 218 plus récents perçoivent zéro. L'identité de l'opérateur est sans rapport avec ce calcul.

---

## État de la mise en œuvre

| Contrôle | État |
|---|---|
| Déduplication de quorum par clé de portefeuille d'opérateur | HF22, activé au bloc 219120 |
| Unification de la période de déblocage, 7 à 14 jours | HF22, activé |
| Récupération de blocage Pulse (repli de signature, snode_revision 1) | Activé au bloc 236920, 18 octobre 2026 |
| Activation de Lokinet comme transport réseau | En développement ; livré dans une version non contraignante avant HF23 |
| Stockage SQLite pour nœuds légers | En développement ; livré avec la version Lokinet pré-HF23 |
| Algorithme de clustering de proximité | Phase de conception, en attente de l'évaluation de Lokinet |
| Plafond d'enregistrement par cluster, seuil de 30 % | HF23, phase de conception |
| Modificateur de récompense nulle pour les nœuds excédentaires | HF23, phase de conception |
| Mécanisme de période de grâce | HF23, phase de conception |
| Déduplication de quorum par cluster de proximité avec règle de repli | HF23, phase de conception |
| Surveillance du nombre minimal de clusters et journalisation des replis | HF23, phase de conception |
| Outillage de corrélation du minutage des preuves de disponibilité | Aucune modification du démon requise, outillage en développement |
| Complément de clustering ASN | Aucune modification du démon requise, outillage en développement |

---

## Ce que ces contrôles ne résolvent pas

**Concentration juridique au niveau du fournisseur.** Un fournisseur recevant un ordre juridique de niveau juridictionnel affectant toute son infrastructure mondiale met hors service tous ses nœuds simultanément, même si ces nœuds apparaissent dans plusieurs clusters de proximité Lokinet. L'analyse ASN fait ressortir ce risque, mais le protocole ne peut pas imposer la diversité des fournisseurs sans exiger la divulgation par l'opérateur de l'identité de son fournisseur. La dispersion géographique naturellement produite par le plafond de cluster atténue substantiellement ce risque en pratique, puisque les opérateurs contraints de se répartir entre clusters utiliseront en pratique plusieurs fournisseurs.

**Détermination de l'identité de l'opérateur humain à travers les fractionnements de portefeuilles sur une chaîne de confidentialité.** Comme décrit ci-dessus, un opérateur sophistiqué utilisant plusieurs portefeuilles financés via la chaîne de confidentialité ne peut pas être identifié au niveau du protocole. Le plafond de cluster et le modificateur de récompense nulle traitent le risque de domaine de défaillance indépendamment de l'identité. La déduplication de quorum comble la faille d'influence sur le consensus dans HF23. Le risque résiduel est qu'un opérateur sophistiqué exécute de nombreux nœuds à travers de nombreux clusters véritablement distincts, accumulant un revenu de récompense de bloc proportionnel à son nombre de nœuds tout en contribuant proportionnellement à la santé du réseau. C'est le résultat acceptable : l'influence concentrée sur le consensus est bornée ; la participation de capital distribuée est récompensée.

Les opérateurs ayant des questions sur l'affectation de cluster, la planification de migration ou le calendrier HF22/HF23 sont encouragés à publier dans le canal Telegram des opérateurs de nœuds ou à ouvrir une issue dans ce dépôt.

---

## Langues disponibles

Les traductions communautaires de ce document sont maintenues dans le dépôt du livre blanc. En cas de conflit entre une traduction et la version anglaise, la version anglaise fait foi.

| Langue | Document |
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

*Ce document ne constitue pas un conseil financier ou juridique. XEQM est une pièce utilitaire pour la plateforme EXIOM, et non un produit d'investissement. La classification des jetons, le statut au regard des valeurs mobilières et les réglementations applicables varient selon la juridiction. Les participants doivent consulter leur cadre juridique et réglementaire local avant d'acquérir ou d'exploiter avec XEQM. XEQM Labs n'encourage pas l'achat de XEQM sur la base d'une appréciation spéculative du prix.*
