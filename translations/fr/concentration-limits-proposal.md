# Limites de Concentration des Nœuds - Application de la Résilience du Réseau
## Document Technique Complémentaire au Livre Blanc de Tokenomie EXIOM
### 26/07/2026

> *Cette traduction a été produite à l'aide d'outils de traduction AI. En cas de conflit, la version anglaise prévaut: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

---

## Ce Que Cela Signifie pour les Opérateurs de Nœuds

HF23 **n'exige pas** un nœud par IP, un nœud par VPS ou un nœud par portefeuille. La limite est de 30% du réseau actif par cluster de proximité, soit environ 208 nœuds actuellement. Un opérateur gérant 10, 50 ou 100 nœuds sur une infrastructure partagée n'est pas affecté par HF23 tant que son cluster reste en dessous de ce seuil.

Le modificateur de récompense zéro s'applique uniquement aux nœuds au-dessus du seuil de 208 nœuds dans un cluster surconcentré, classés par ancienneté d'enregistrement.

Le problème spécifique que HF23 résout: une installation en France héberge actuellement environ 426 nœuds, soit 61% du réseau. Si cette installation tombe en panne, le réseau s'arrête.

---

## Données de Concentration Actuelles

| Pays | Nœuds actifs |
|---|---|
| France | 492 |
| Allemagne | 70 |
| États-Unis | 55 |
| Canada | 18 |
| Pologne | 13 |
| Royaume-Uni | 10 |
| Turquie | 5 |
| Australie | 4 |
| Singapour | 2 |
| Lituanie | 2 |
| Serbie | 1 |

---

## Contrôles HF22 (En Cours d'Entrée en Testnet, Validé)

**Déduplication de quorum par clé de portefeuille opérateur.** Au plus un nœud par adresse de portefeuille opérateur par tour. Validé sur neuf cycles avec un taux de récupération de 100%.

**Unification de la période de déblocage.** La période de déblocage de désenregistrement forcé passe de 7 à 14 jours.

---

## Contrôles HF23 (Phase de Conception)

**Limite d'enregistrement de cluster.** Nouveaux enregistrements rejetés quand un cluster dépasse 30% des nœuds actifs.

**Modificateur de récompense zéro.** Les nœuds au-dessus du seuil gagnent zéro récompense jusqu'à migration.

**Règle de repli du quorum.** Taille de quorum: 12 sièges. Si moins de 12 clusters distincts existent, l'algorithme accorde des sièges supplémentaires en commençant par les plus petits clusters.

---

*Pour la spécification technique complète, consultez la version anglaise: [concentration-limits-proposal.md](../../concentration-limits-proposal.md)*

*Ce document ne constitue pas un conseil financier ou juridique. En cas de conflit, la version anglaise prévaut.*
