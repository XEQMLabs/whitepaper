# XEQM Labs - Plateforme EXIOM
## Livre Blanc de Tokenomie
### Brouillon v11 | 26/07/2026

> *Cette traduction a été produite à l'aide d'outils de traduction par intelligence artificielle. Elle est fournie uniquement à titre informatif. En cas de conflit ou d'ambiguïté entre cette traduction et l'original en anglais, la version anglaise prévaut. La version anglaise est disponible sur [github.com/XEQMLabs/whitepaper](https://github.com/XEQMLabs/whitepaper).*

---

## Ce Qui Est Actif Aujourd'hui vs. Ce Qui Est Planifié

| Composant | Statut |
|---|---|
| EXIOM mainnet | Actif, opérationnel depuis le 6 mai 2026 |
| Réseau de nœuds de service | Actif, 693 nœuds actifs, 184 opérateurs (juillet 2026) |
| Lokinet (LLARP) | Présent dans le code source, statut d'activation en cours d'évaluation |
| Échange de monnaies XEQ vers XEQM | Livré et clôturé, exécution de production de 35 jours, registre auditable public |
| Portefeuille GUI | Actif, github.com/XEQMLabs/XEQMLabs-GUI |
| Explorateur de nœuds | Actif, surveillance active des nœuds de service |
| API développeur EXIOM | En développement, Phase 2 (ACTIF) |
| Oracle de confidentialité EXIOM | Conçu, pré-implémentation, Phase 3 |
| Plateforme de trading RFQ EXIOM | En développement, Phase 2/3, première paire XEQM/BTC |
| HF22, déduplication de quorum et unification du déblocage | En cours d'entrée en testnet, validé, sans dépendance Lokinet |
| HF23, limite de cluster de proximité, modificateur de récompense, transport Lokinet | Phase de conception, en attente d'évaluation technique Lokinet |
| Gouvernance formelle sur chaîne | Planifié, Phase 6 |

---

## 1. Qu'est-ce que XEQM Labs

XEQM Labs est une entreprise de technologie de confidentialité. Son produit phare, EXIOM, est un réseau Layer 1 de Preuve d'Enjeu préservant la confidentialité et une plateforme commerciale pour développeurs exploitée par un ensemble mondial de nœuds de service. XEQM est la monnaie d'accès et d'utilisation de la plateforme.

Le projet perpétue une communauté et un historique opérationnel de plus de sept ans. La mainnet EXIOM a été construite pour donner à cette communauté un réseau avec une offre vérifiable, un calendrier d'émission prévisible, un consensus pur de Preuve d'Enjeu sans composant de Preuve de Travail.

XEQM est une monnaie native Layer 1, non tokenisée sur aucune autre chaîne, pas un ERC-20 ni un actif enveloppé, et sans pont. Les détenteurs interagissent directement avec la mainnet EXIOM.

### La Famille de Produits EXIOM

**Réseau de Nœuds de Service EXIOM.** Actif sur mainnet. 693 nœuds actifs sur 184 opérateurs indépendants en juillet 2026.

**Échange de Monnaies EXIOM.** Un produit commercial permettant aux projets de migrer leur communauté de détenteurs d'une chaîne héritée vers une nouvelle chaîne avec une auditabilité cryptographique complète. Le pilote fut la migration des détenteurs de XEQ vers XEQM, s'exécutant pendant 35 jours avec chaque soumission traitée via un registre vérifié cryptographiquement portant une empreinte SHA256 publique.

**API Développeur Privé EXIOM.** En développement. Une plateforme développeur exposant les capacités de confidentialité du réseau via une API structurée. Phase 2, actif.

**Oracle de Confidentialité EXIOM.** Conçu, pré-implémentation. Un oracle axé sur la confidentialité prouvant des faits sur des données web privées sans exposer la source sous-jacente. Phase 3.

**Plateforme de Trading RFQ EXIOM.** En développement. Une plateforme de trading de gré à gré peer-to-peer avec des attestations de règlement cryptographiques. La première paire de trading est XEQM/BTC. Phase 2/3.

XEQM Labs n'encourage pas l'achat de XEQM sur la base d'une appréciation de prix spéculative.

---

## 2. Provenance de l'Offre

La migration est terminée. 276.917.604 XEQM ont été émis sur la mainnet EXIOM en échange des avoirs hérités. Ce chiffre est l'offre de départ vérifiée au lancement de la mainnet le 6 mai 2026. Chaque dépôt hérité a été enregistré dans un registre public avec une empreinte SHA256. Les clés de dépense de chaque portefeuille impliqué dans l'échange ont été publiées.

**Pas d'émissions discrétionnaires.** Le protocole n'autorise pas les émissions ad hoc ni les frappes hors calendrier.

**Pas de brûlage.** L'architecture cryptographique de ce réseau ne prend pas en charge les brûlages démontrables. Nous ne représenterons aucun portefeuille comme adresse de brûlage.

---

## 3. Modèle de Tokenomie

Le réseau produit un nouveau bloc toutes les 60 secondes et attribue 8,25 XEQM au nœud de service sélectionné, générant 11.880 XEQM par jour. Avec 700 nœuds actifs, chaque nœud gagne environ 17,0 XEQM par jour, ou 516 XEQM par mois.

Le trésor reçoit environ 17.857 XEQM par jour. C'est le budget opérationnel pour l'équipe de développement active pendant la période pré-revenus.

### Allocation des Émissions

| Allocation | Part | Objectif |
|---|---|---|
| Récompenses des Nœuds de Service | 40% | Récompenses de bloc payées directement aux nœuds |
| Développement du Protocole Central | 25% | Blockchain, plateforme EXIOM et services réseau |
| Marketing et Sensibilisation | 15% | Visibilité du réseau et adoption |
| Écosystème et Communauté | 10% | Subventions, primes, récompenses communautaires |
| Sécurité et Audits | 5% | Audits et revues de sécurité |
| Réserve à Long Terme | 5% | Stabilité et besoins d'urgence |

### Distribution des Frais de la Plateforme EXIOM

| Destinataire | Part |
|---|---|
| Opérateurs de Nœuds API | 35% |
| Trésor XEQM Labs | 35% |
| Gouvernance Communautaire | 30% |

---

## 4. Structure des Nœuds de Service

| Paramètre | Valeur |
|---|---|
| Exigence de nœud complet | 200.000 XEQM |
| Mise minimale de l'opérateur | 100.000 XEQM (50%) |
| Frais maximum de l'opérateur | 10% |
| Période de déblocage, retrait volontaire | 14 jours, les récompenses continuent |
| Période de déblocage, désenregistrement forcé | 14 jours, sans récompenses (HF22) |
| Slots maximum de contributeurs | 11 (opérateur inclus) |
| Contribution minimale par slot | 10.000 XEQM |

### Économie des Nœuds

Un VPS payant à environ 5,28 USD par mois peut faire fonctionner 10 nœuds de service, portant le coût par nœud à environ 0,53 USD par mois. L'hébergement géré via Pecunia est disponible à 1,76 USD par nœud par mois.

| Prix | Brut/mois | Net: auto-hébergé ($0,53) | Net: Pecunia ($1,76) | APY sur mise 200k |
|---|---|---|---|---|
| $0,01547 (aujourd'hui) | $0,008 | -$0,52 | -$1,75 | 3,1% |
| $0,05 | $0,026 | -$0,50 | -$1,73 | 3,1% |
| $0,10 | $0,052 | -$0,48 | -$1,71 | 3,1% |
| $0,25 | $0,129 | -$0,40 | -$1,63 | 3,1% |
| $0,50 | $0,258 | -$0,27 | -$1,50 | 3,1% |
| $1,00 | $0,516 | -$0,01 | -$1,24 | 3,1% |
| $2,00 | $1,032 | +$0,50 | -$0,73 | 3,1% |
| $5,00 | $2,580 | +$2,05 | +$0,82 | 3,1% |

---

## 6. XEQM comme Monnaie Utilitaire

| Niveau | Mise Requise | Appels Inclus |
|---|---|---|
| Gratuit | Aucun | 10.000 appels testnet par mois |
| Constructeur | 1.000 XEQM | 100.000 appels mainnet par mois |
| Production | 10.000 XEQM | 1.000.000 appels par mois, webhooks, support prioritaire |
| Entreprise | 50.000 XEQM | Appels illimités, limites de taux personnalisées, SLA |

---

## 8. Résumé des Paramètres

| Paramètre | Valeur |
|---|---|
| Mécanisme de consensus | 100% Preuve d'Enjeu |
| Temps de bloc | 60 secondes |
| Récompense de bloc | 8,25 XEQM par bloc |
| Émissions de bloc quotidiennes | 11.880 XEQM |
| Émission de gouvernance | ~17.857 XEQM par jour |
| Exigence de nœud complet | 200.000 XEQM |
| Taille du quorum | 12 sièges par tour |
| Coefficient de Nakamoto (juillet 2026) | 7 (objectif: 8) |
| Dépôts centraux | github.com/XEQMLabs |

---

## Langues Disponibles

| Langue | Livre Blanc |
|---|---|
| English | [README.md](../../README.md) |
| Español | [../es/README.md](../es/README.md) |
| Deutsch | [../de/README.md](../de/README.md) |
| 中文 | [../zh/README.md](../zh/README.md) |
| Português | [../pt/README.md](../pt/README.md) |
| Türkçe | [../tr/README.md](../tr/README.md) |
| Polski | [../pl/README.md](../pl/README.md) |
| Bahasa Indonesia | [../id/README.md](../id/README.md) |

---

*Ce document est un brouillon. Les paramètres, calendriers d'émission et phases de la feuille de route décrits ici sont la conception prévue.*

*Ce document ne constitue pas un conseil financier ou juridique. XEQM est une monnaie utilitaire pour la plateforme EXIOM, pas un produit d'investissement. La classification des jetons, le statut des valeurs mobilières et les réglementations applicables varient selon la juridiction. Les participants doivent consulter leur cadre juridique et réglementaire local avant d'acquérir ou d'opérer avec XEQM. XEQM Labs n'encourage pas l'achat de XEQM sur la base d'une appréciation de prix spéculative.*
