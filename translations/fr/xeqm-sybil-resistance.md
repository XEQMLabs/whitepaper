# Risque Sybil et le modèle d'atténuation d'EXIOM
## Complément technique au livre blanc sur la tokenomique EXIOM
### 07/26/2026

> **Note (mise à jour octobre 2026).** La concentration est appliquée par *cluster de proximité* (infrastructure physique ou de routage partagée), **et non par pays**. Les chiffres de nœuds ici sont un instantané de juillet 2026 ; voir le livre blanc pour les totaux actuels. Lokinet est livré dans une version non contraignante avant HF23, et HF23 active l'application.

Ce document est un complément au livre blanc sur la tokenomique EXIOM et à la proposition sur les limites de concentration des nœuds, et suppose que les deux ont été lus. Le livre blanc couvre ce que sont les contrôles. La proposition sur les limites de concentration couvre les mécaniques du fonctionnement de chaque contrôle. Ce document couvre le modèle de menace : à quoi ressemble réellement une attaque Sybil sur une chaîne de confidentialité, ce qui rend l'architecture d'EXIOM spécifiquement résistante ou vulnérable, et comment la méthodologie de surveillance continue identifie la concentration en pratique.

---

## La menace Sybil sur une chaîne de confidentialité

Une attaque Sybil sur un réseau de nœuds de service signifie qu'un seul acteur exploite de nombreux nœuds sous des identités apparentes distinctes pour gagner une influence disproportionnée. Sur une blockchain transparente, l'analyse du graphe de portefeuilles peut souvent révéler que plusieurs adresses d'opérateur de nœud sont financées à partir d'une source commune, exposant le Sybil. Sur une chaîne de confidentialité, cet outil est indisponible par conception. La garantie de confidentialité qui protège les transactions des utilisateurs supprime aussi la méthode de détection Sybil la plus courante.

La surface Sybil d'EXIOM diffère donc d'une chaîne transparente d'une manière spécifique : un opérateur qui utilise correctement les fonctionnalités de confidentialité peut présenter plusieurs adresses de portefeuille qui apparaissent sans lien au niveau du protocole, quel que soit le capital qu'il contrôle. Ce n'est pas un défaut de la conception de confidentialité. C'est une propriété inhérente à toute chaîne de confidentialité qui doit être traitée par des mécanismes autres que l'analyse du graphe de transactions.

Les deux surfaces d'attaque Sybil sur EXIOM sont distinctes et nécessitent des contrôles séparés :

**Attaque d'influence sur le consensus.** Un opérateur accumule suffisamment de nœuds, à travers n'importe quelle structure de portefeuille, pour détenir un nombre disproportionné de sièges de quorum simultanément. Cela lui permet d'influencer les résultats des sessions oracle, les tours Pulse et les quorums d'obligations au-delà de ce que sa proportion de stake individuelle suggérerait comme équitable. Le dommage porte sur l'intégrité du consensus, pas nécessairement sur la disponibilité du réseau.

**Attaque de domaine de défaillance.** Un opérateur concentre des nœuds dans une seule installation physique. Cela peut être ou non intentionnel en tant qu'attaque ; cela peut résulter d'une optimisation des coûts. Le dommage porte sur la survivabilité du réseau : une panne d'installation met les nœuds de l'opérateur hors ligne simultanément, bloquant potentiellement la production de blocs si la concentration est assez importante.

---

## Ce qui rend EXIOM structurellement résistant

**Coût en capital par identité.** Contrairement aux attaques Sybil pures où les identités sont gratuites, chaque nœud de service EXIOM requiert 200,000 XEQM en stake, l'opérateur stakant personnellement au moins 100,000 XEQM. Un opérateur exploitant 100 nœuds a 10,000,000 XEQM de capital en stake et verrouillé. Créer des identités apparentes additionnelles par fractionnement de portefeuille ne réduit pas ce coût -- chaque nœud requiert toujours 100,000 XEQM de stake d'opérateur. L'attaque Sybil est coûteuse à chaque échelle.

**Friction de déverrouillage.** Une période de déverrouillage de 14 jours sur le retrait volontaire comme sur le déréférencement forcé signifie que le capital engagé dans des nœuds Sybil ne peut pas être extrait rapidement. Un attaquant qui décide de sortir ne peut pas le faire plus vite que n'importe quel autre opérateur.

**Registre public des nœuds.** La clé d'enregistrement et l'adresse de portefeuille d'opérateur de chaque nœud de service sont publiques. Un nœud ne peut pas participer au consensus anonymement. Bien que l'identité humaine derrière une adresse de portefeuille soit privée, l'empreinte opérationnelle du nœud s'accumule au fil du temps à travers les schémas d'enregistrement, le timing des preuves de disponibilité et le comportement de routage.

---

## Comment la concentration est identifiée sans analyse du graphe de transactions

Parce que l'analyse au niveau des transactions est indisponible, la détection de concentration d'EXIOM repose sur quatre signaux observables à partir du comportement des nœuds plutôt que de l'historique de financement.

**Regroupement par clé d'enregistrement.** Les nœuds enregistrés sous la même clé de portefeuille d'opérateur sont définitivement le même opérateur. C'est déterministe à partir des données on-chain. Un grand opérateur qui ne fractionne pas ses portefeuilles est entièrement visible via ce seul signal. Les plus grands déploiements actuels sur le réseau, incluant des nœuds exécutant respectivement 58 et 51 nœuds depuis des adresses IP uniques, sont chacun des opérateurs uniques confirmés via l'analyse de clé d'enregistrement.

**Regroupement par adresse IP et sous-réseau.** Actuellement le signal principal de co-localisation physique. Plusieurs nœuds de la même adresse IP sont presque certainement sur le même serveur. Plusieurs nœuds du même sous-réseau suggèrent le même compte d'hébergement ou bloc de datacenter. Ce signal est disponible aujourd'hui sans aucune modification du daemon et restera comme signal complémentaire après l'activation de Lokinet.

**Corrélation du timing des preuves de disponibilité.** Le réseau reçoit des preuves de disponibilité de chaque nœud actif selon un calendrier régulier. La distribution des horodatages d'arrivée de ces preuves est enregistrée par les nœuds récepteurs. Les nœuds exécutés sur le même hôte physique ou hyperviseur de VM soumettent des preuves dans une fenêtre étroite caractéristique, typiquement sous 10 millisecondes, parce qu'ils partagent la même horloge système et la même interface réseau. Un cluster de nœuds de différentes clés de portefeuille dont les preuves arrivent systématiquement dans cette fenêtre est un signal fort d'infrastructure physique partagée, détectable sans aucune modification du daemon et sans que Lokinet soit actif.

Ce signal est spécifiquement utile pour identifier les opérateurs fractionnant leurs portefeuilles qui gardent leurs nœuds sur une infrastructure partagée. Les clés de portefeuille diffèrent ; le timing des preuves non.

**Proximité de routage Lokinet (livrée non contraignante avant HF23 ; appliquée à HF23).** Une fois Lokinet actif comme transport du réseau, le graphe de routage fournit une carte topologique physique continue du réseau de nœuds. Les nœuds de la même installation routent à travers la même infrastructure en amont, produisant des sélections de chemins corrélées et une latence inter-nœuds inférieure à la milliseconde quelles que soient leurs clés de portefeuille ou leurs adresses IP annoncées. C'est le signal le plus robuste parce qu'il reflète une réalité réseau physique qui ne peut pas être modifiée par configuration logicielle sans réellement déplacer l'infrastructure.

---

## L'attaque par fractionnement de portefeuille en détail

L'approche Sybil la plus sophistiquée disponible sur EXIOM est le fractionnement de portefeuille : enregistrer des nœuds sous plusieurs adresses de portefeuille financées via la couche de transaction de la chaîne de confidentialité de sorte que la source de financement commune ne soit pas visible. Cela contourne le signal de regroupement par clé d'enregistrement mais pas les autres.

Un opérateur exploitant 426 nœuds à travers 10 portefeuilles, tous hébergés dans la même installation Contabo, est exposé par :

- Le timing des preuves de disponibilité : les preuves des 426 nœuds arrivent dans la fenêtre caractéristique inférieure à 10 ms d'une infrastructure partagée
- L'analyse IP et sous-réseau : même avec plusieurs IP, l'assignation de bloc de datacenter et l'ASN sont partagés
- La proximité Lokinet (post-HF23) : les 426 nœuds routent tous à travers la même dorsale Contabo quelle que soit la clé de portefeuille

Un opérateur exploitant 426 nœuds à travers 10 portefeuilles, réellement répartis sur 10 fournisseurs différents dans 10 pays différents, n'est pas significativement exposé par aucun signal actuel. Les clés d'enregistrement diffèrent, le timing des preuves diffère parce que l'infrastructure diffère, les ASN diffèrent, et les chemins Lokinet diffèrent. Au niveau du protocole, cela ressemble à 10 opérateurs différents.

C'est le risque Sybil résiduel sur EXIOM après application de tous les contrôles. Il est borné dans ses conséquences : la déduplication de quorum de HF23 limite chaque cluster de proximité à un siège de quorum par tour quelle que soit la structure de portefeuille, de sorte que même un opérateur fractionnant ses portefeuilles de manière distribuée ne gagne pas une influence illimitée sur le consensus. Son revenu de récompense de bloc évolue avec son nombre de nœuds, ce qui est équitable parce qu'il a staké un capital proportionnel. Son influence sur le consensus par tour est plafonnée par la déduplication de cluster quel que soit le nombre de portefeuilles qu'il utilise.

---

## Méthodologie de surveillance continue

**Liste de blocage de gouvernance.** Une liste de blocage de clés publiques gérée par la gouvernance empêche les clés d'enregistrement bloquées d'enregistrer de nouveaux nœuds. Un opérateur qui passe à une nouvelle clé de portefeuille alors que l'originale est sur liste de blocage crée un enregistrement documenté d'évasion, et le timing des preuves et le comportement de routage de la nouvelle clé sont corrélés contre le profil historique de la clé bloquée.

**Analyse du graphe des emplacements de contributeurs.** Les emplacements de contributeurs de nœuds de service sont un signal d'identité secondaire. Un opérateur qui finance des emplacements de contributeurs à travers plusieurs de ses propres clés de portefeuille crée un graphe de relations observable même sur une chaîne de confidentialité, parce que les transactions d'enregistrement de contributeur portent des données observables sur les nœuds auxquels elles contribuent. Un opérateur qui contribue systématiquement à des nœuds enregistrés sous le portefeuille A depuis les portefeuilles B et C, tandis que ces mêmes portefeuilles B et C enregistrent leurs propres nœuds, crée un graphe de corrélation qui complète le signal direct de regroupement par clé d'enregistrement.

**Surveillance ASN.** L'IP de chaque nœud actif correspond à un Autonomous System Number via des données BGP publiques. Le réseau suit la concentration d'ASN à travers l'ensemble des nœuds actifs. Les nœuds partageant un ASN partagent une infrastructure au niveau du fournisseur et une exposition juridique. Une concentration d'ASN élevée est signalée pour revue de gouvernance même lorsque les enregistrements de nœuds individuels apparaissent sans lien. Le signal ASN n'identifie pas un opérateur humain, mais il identifie un domaine de défaillance.

Le statut de mise en œuvre actuel pour tous les contrôles décrits dans ce document est maintenu dans la [proposition sur les limites de concentration des nœuds](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md).

---

*Ce document ne constitue pas un conseil financier ou juridique. XEQM est une pièce utilitaire pour la plateforme EXIOM, et non un produit d'investissement. La classification des tokens, le statut au regard des valeurs mobilières et les réglementations applicables varient selon la juridiction. Les participants doivent consulter leur cadre juridique et réglementaire local avant d'acquérir ou d'opérer avec XEQM. XEQM Labs n'encourage pas l'achat de XEQM sur la base d'une appréciation spéculative du prix.*
