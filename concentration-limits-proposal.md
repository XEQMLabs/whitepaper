# Node Concentration Limits - Network Survivability Enforcement
## Technical Companion to the EXIOM Tokenomics Whitepaper
### 07/26/2026

This document is a companion to the EXIOM Tokenomics Whitepaper and assumes it has been read. The whitepaper covers what the concentration controls are and why they exist. This document covers the mechanical detail of how each control works, the testnet validation data behind HF22, the precise economic math behind the zero-reward modifier, the operator identity question on a privacy chain, and the residual risks the protocol does not fully solve.

---

## The Current Concentration Data

| Country | Active nodes |
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

France at approximately 71% of the network is almost entirely one Contabo facility in Grand Est. The survivability threshold established in the whitepaper is 30% of active nodes per cluster, approximately 208 nodes at current count. Grand Est at 426 nodes is more than double that threshold.

---

## What This Means for Node Operators

This section answers the question directly: how does HF23 affect how you run your nodes?

**HF23 does not require one node per IP, one node per VPS, or one node per wallet.** The cap is 30% of the active network per proximity cluster, currently approximately 208 nodes. An operator running 10, 50, or even 100 nodes on shared infrastructure is completely unaffected by HF23 as long as their cluster stays below that threshold. You can run multiple nodes on one machine, one VPS account, and one wallet. Nothing in HF23 changes that.

**The zero-reward modifier applies only to nodes above the 208-node cluster threshold.** The oldest registered nodes in a cluster earn full rewards up to that threshold. Only nodes ranked above it in an over-concentrated cluster earn zero, and only until they are migrated to a less concentrated cluster.

**The quorum deduplication caps consensus influence per round, not node count or income.** An operator running 50 nodes on one VPS earns block rewards on all 50 and manages their infrastructure exactly as they do today. They receive one quorum seat per cluster per round instead of potentially many, which is the intended outcome.

**The right approach for a new operator** is to check the node explorer, see where existing clusters are concentrated, and deploy into a lightly populated region. Ten nodes on one server in Brazil or Argentina works perfectly fine under HF23 because those regions are nowhere near the 30% threshold. Full rewards, full quorum participation, no issues.

**The dynamic works in your favor if you deploy into sparse regions.** If a region eventually fills up, the node explorer shows it and operators have a financial incentive to move before the cap affects them. Operators who got there first keep full rewards on their oldest nodes up to the threshold. New registrations into an over-concentrated cluster earn nothing immediately, so the economics naturally push new deployments toward lighter regions.

**The specific problem HF23 solves** is one facility in France currently hosting approximately 426 nodes, 61% of the network. If that facility goes offline the network stalls. The goal is getting that cluster below 208 nodes. Every other operator running a responsible multi-node setup in a non-concentrated region is exactly what the network needs more of.

---

## Why the Hard Forks Are Separated

HF22 ships after successful testing. Wallet-key quorum deduplication and unbonding period unification have no dependency on Lokinet. Both have been validated on testnet and holding them while the Lokinet assessment is pending is unjustified delay. A sophisticated actor who reads the whitepaper before HF22 ships could attempt wallet splitting to pre-empt the quorum control, but doing so is detectable through uptime proof timing correlation and IP/ASN analysis and creates a documented record for governance action.

HF23 ships after the Lokinet engineering assessment completes. If the assessment returns a configuration-change-only result, HF23 can follow HF22 quickly. If it returns a significant engineering effort, Grand Est stays exposed to the full survivability risk beyond quorum dedup until HF23 is ready. Separating the releases also gives clean failure domains: if something goes wrong post-HF23 activation there are fewer variables to isolate.

---

## HF22 Mechanics

### Wallet-Key Quorum Deduplication

The quorum selection algorithm runs a deduplication pass over each candidate set before finalizing. When the draw selects a candidate node, the algorithm checks its operator wallet address against all nodes already selected for the round. If a match is found, the candidate is replaced by drawing again from the remaining eligible pool, excluding all addresses already represented.

The replacement draw does not cycle back through already-rejected candidates. It draws from the remaining unselected pool in the same probability-weighted order used for the initial draw. This preserves the statistical properties of the quorum selection without introducing a deterministic bias toward any particular set of remaining nodes.

**Testnet validation results:**
- Nine stall/recovery cycles completed
- 100% recovery rate across all cycles
- Zero manual intervention required in any cycle
- Mainnet pre-HF22 baseline: 1,000 blocks, 100% Pulse, zero GOV_SIGNED blocks
- R0 timeout analysis: no R0 timeouts introduced in production conditions. Density analysis of current mainnet confirms every high-density IP cluster is a single operator, meaning wallet-key dedup already provides full protection against the current whale deployments. The two largest single-IP deployments (58 nodes and 51 nodes respectively) are each one operator and are capped at one quorum seat per round under HF22.

**What one quorum seat means in practice:** Quorum size and rotation frequency determine how often a node participates. At current network size, a single-seat cap means a concentrated operator's influence in oracle sessions, Pulse rounds, and obligations quorums is identical to that of an operator with one node. Their block reward income is unchanged.

**The wallet-splitting gap and its interim detection:** An operator who splits 426 nodes across 10 wallets gets up to 10 quorum seats per round instead of one. This is the known gap HF23 closes. In the interim, wallet splitting is detectable through two signals already available without daemon changes. First, uptime proof timing: nodes on the same physical host or hypervisor submit proofs within milliseconds of each other, regardless of wallet key. A cluster of proofs arriving in sub-10ms windows from nodes registered to different wallets is a strong signal of shared infrastructure. Second, IP and ASN correlation: nodes on different wallets sharing an IP, subnet, or ASN are logged and flagged for governance review. An operator who wallet-splits but keeps all nodes in the same Contabo facility is identifiable through both signals and subject to governance action under the blocklist policy.

### Unbonding Period Unification

The forced deregistration unbonding period changes from 10,080 blocks (approximately 7 days) to 20,160 blocks (approximately 14 days), matching the voluntary withdrawal period. This is a consensus constant change.

The original 7-day forced period was a deliberate choice during network stabilization to limit the penalty on operators experiencing infrastructure events outside their control. That rationale no longer applies. The network is stable, the decommission credit system provides the buffer for short outages, and a unified 14-day period removes an asymmetry that has no remaining justification.

XEQM coins are locked on-chain during the unbonding period via the registration transaction. There is no mechanism to release the lock early without a protocol change. For documented infrastructure failures, governance can compensate missed rewards from the governance wallet as a XEQM transfer, but the on-chain lock runs its full duration regardless.

---

## HF23 Mechanics

### Lokinet Proximity Clustering

Lokinet (Low Latency Anonymous Routing Protocol, LLARP) routes traffic through the service node network at layer 3, supporting TCP, UDP, and ICMP. Every service node participates as a relay. The routing graph that emerges reflects physical network topology: nodes at the same facility route through the same upstream switch and the same datacenter backbone, producing correlated path selections and sub-millisecond inter-node latency. Nodes at different facilities route through different paths with measurably higher latency.

The clustering algorithm ingests pairwise Lokinet routing latency and path overlap measurements across all active nodes and groups them into clusters using these measurements as the proximity signal. A cluster is not a fixed geographic region; it is a dynamic grouping of nodes whose routing behavior indicates shared physical infrastructure. Two nodes at different Contabo facilities in different countries may route through enough shared Contabo backbone infrastructure to appear in the same cluster if their path overlap is high enough. Two nodes at the same datacenter but on different physical machines with different upstream connections will appear in different clusters if their path overlap is low.

Supplementary signals used alongside Lokinet proximity:

**Uptime proof timing correlation.** The network already receives uptime proofs from all active nodes on a regular schedule. The timestamp distribution of proof arrivals from each node is recorded by the receiving nodes. Nodes on the same physical host or VM hypervisor submit proofs within a characteristic tight window, typically under 10 milliseconds. Clustering this arrival timing distribution provides a physical co-location signal that requires no daemon changes and works before Lokinet is active.

**ASN analysis.** Each node's IP address maps to an Autonomous System Number via public BGP data. Nodes sharing an ASN share provider-level routing infrastructure and provider-level legal exposure. A provider that receives a jurisdiction-level order affecting all their infrastructure takes down all their ASN nodes simultaneously, regardless of how many Lokinet clusters they appear in. ASN concentration is tracked as a supplementary signal and contributes to governance review of operators near the cluster threshold.

### Cluster Registration Cap

At registration time, the protocol runs a proximity evaluation against all existing clusters. The registering node's Lokinet routing characteristics are measured against the centroid of each existing cluster. If the closest cluster already contains 30% or more of active nodes, the registration is rejected with a specific error code indicating cluster capacity and the node count of the nearest cluster.

The rejection is deterministic: any node that routes similarly enough to an over-concentrated cluster to be assigned to it is rejected, regardless of the operator's wallet key, registration history, or stake amount. The operator cannot appeal the rejection through governance. The only path forward is to register on infrastructure that routes to a different cluster.

The threshold is evaluated against active node count at the time of registration. As the network grows, the 30% threshold in absolute terms grows with it. An operator at the cap today can register additional nodes in a previously capped cluster as the network grows and the absolute cap rises, without migrating any existing nodes.

### Zero-Reward Modifier

The zero-reward modifier is applied at block reward calculation time. The reward calculation for a selected node includes a cluster eligibility check. If the node's cluster contains more nodes than the cap threshold, and the node's registration rank within that cluster is above the threshold (ranked oldest to newest), the reward calculation returns zero.

The ranking is computed from the node's registration block height within its cluster assignment. The oldest registered node in the cluster gets rank 1, the most recently registered gets rank N. Nodes with rank greater than the cap threshold earn zero. Nodes with rank at or below the cap threshold earn the full standard reward. The ranking is recomputed each time the cluster assignment changes, which occurs when nodes migrate out of the cluster, when new nodes join, or when the cluster boundary shifts due to network topology changes.

**The economic math for Grand Est:** At 426 nodes with a 208-node cap, 218 nodes earn zero block rewards. At self-hosted pricing of $0.53 per node per month, those 218 nodes cost $115.54 per month with zero income. At Pecunia pricing of $1.76 per node per month, the cost is $383.68 per month. The operator has two rational responses: migrate the excess nodes to non-concentrated clusters, restoring their rewards immediately upon the new registration being accepted, or deregister the excess nodes and recover the staked XEQM through the unbonding process. Either response reduces concentration. There is no rational basis for maintaining the excess nodes at zero reward.

**Grace period mechanics:** At HF23 activation block, the protocol takes a snapshot of all active clusters and their node counts. Any cluster exceeding the 30% threshold is marked as over-concentrated. For 30 days following the activation block, the zero-reward modifier is suspended for all nodes, including those above the cap threshold. During the grace period, node owners can observe the node explorer's cluster assignments, plan migrations, and begin executing them. At the grace period expiry block, the modifier activates. Nodes that have migrated out of the over-concentrated cluster by that block earn full rewards from that block forward. Nodes still above the threshold earn zero from that block forward until they migrate.

### Proximity Cluster Quorum Deduplication

The HF23 quorum deduplication upgrade replaces the wallet address check with a cluster membership check. When the draw selects a candidate node, the algorithm checks its cluster assignment against all nodes already selected for the round. If two nodes share a cluster assignment, the second is replaced by a draw from the remaining pool, excluding all clusters already represented.

The practical effect on a wallet-splitting operator: 10 wallet addresses across 426 nodes all in the same Contabo facility appear in the same proximity cluster. The cluster check catches them all as a single unit. One node from that cluster holds a seat. The other 425 nodes from that cluster do not, regardless of how many distinct wallet addresses they are registered under.

### Minimum Cluster Count Requirement and Fallback Rule

The EXIOM network quorum size is 12 seats per round. Proximity cluster deduplication therefore requires at least 12 distinct proximity clusters in the active node set to guarantee quorum formation. If the network produces fewer than 12 distinct clusters, the algorithm cannot satisfy the one-seat-per-cluster constraint and quorum formation fails.

The current network distribution, once Lokinet proximity clustering is applied, is estimated to produce between 12 and 18 distinct clusters. This is uncomfortably close to the 12-seat minimum. Shared provider backbone infrastructure between nominally separate facilities can cause two distinct IP locations to merge into one proximity cluster in the Lokinet routing graph. Any such merger that reduces the cluster count below 12 breaks quorum formation entirely.

The algorithm therefore implements a mandatory fallback rule:

1. The algorithm attempts to fill all 12 seats with one node per distinct cluster, working through the available clusters in random order.
2. If all distinct clusters are exhausted before 12 seats are filled, the algorithm enters a fallback pass.
3. In the fallback pass, it allows a second node from each cluster, starting with the smallest clusters first. The least concentrated clusters receive a second seat before the most concentrated ones.
4. The algorithm continues fallback passes, incrementing the maximum seats per cluster by one each pass, until 12 seats are filled.
5. The most concentrated cluster, such as Grand Est under current conditions, receives additional seats only after all smaller clusters have been given their fallback allocation.

Every round that triggers the fallback is logged with the cluster count that caused it. Governance monitors fallback frequency as a direct concentration risk indicator. A network with 12 or more distinct clusters never triggers the fallback. A network consistently triggering the fallback is signaling that HF23 concentration enforcement is not yet achieving adequate physical diversity and that the cluster cap or grace period enforcement requires governance attention.

The fallback log is published in the node explorer alongside cluster assignments so the operator community can observe concentration risk in real time.

---

## Operator Identity on a Privacy Chain

The protocol does not need to identify which human operator owns which nodes in order to enforce the cluster cap and zero-reward modifier. Both controls operate at the cluster level. What can and cannot be determined is useful context for governance monitoring but is not required for protocol enforcement.

**What is deterministic from on-chain data:** nodes registered under the same operator wallet key are definitively the same operator. This is public information in the registration transaction.

**What is inferable with high confidence from Lokinet and timing data:** the number of distinct physical hosts underlying a cluster of nodes, regardless of how many wallet keys they use. Five wallet keys each running 85 nodes, all on the same two physical servers, produce two distinct timing signatures and two Lokinet proximity centroids, not five.

**What cannot be determined on a privacy chain:** whether two different wallet keys with distinct infrastructure belong to the same human operator. The funding source of each wallet key is private by design. A sophisticated operator using five wallets funded from five different sources through the privacy chain's transaction layer presents five distinct identities at the protocol level.

For survivability enforcement, this does not matter. The cluster contains 426 nodes. The oldest 208 earn rewards. The newest 218 earn zero. The operator's identity is irrelevant to that calculation.

---

## Implementation Status

| Control | Status |
|---|---|
| Operator wallet-key quorum dedup | HF22, entering testnet, validated |
| Unbonding period unification, 7 to 14 days | HF22, entering testnet |
| Lokinet activation as network transport | Engineering assessment underway |
| Proximity clustering algorithm | Design phase, pending Lokinet assessment |
| Cluster registration cap, 30% threshold | HF23, design phase |
| Zero-reward modifier for excess nodes | HF23, design phase |
| Grace period mechanism | HF23, design phase |
| Proximity cluster quorum dedup with fallback rule | HF23, design phase |
| Minimum cluster count monitoring and fallback logging | HF23, design phase |
| Uptime proof timing correlation tooling | No daemon changes required, tooling in development |
| ASN clustering supplement | No daemon changes required, tooling in development |

---

## What These Controls Do Not Solve

**Provider-level legal concentration.** A provider receiving a jurisdiction-level legal order affecting all their global infrastructure takes down all their nodes simultaneously, even if those nodes appear in multiple Lokinet proximity clusters. ASN analysis surfaces this risk but the protocol cannot enforce provider diversity without requiring operator disclosure of their provider identity. The geographic spread naturally produced by the cluster cap substantially mitigates this risk in practice, since operators forced to distribute across clusters will in practice use multiple providers.

**Determination of human operator identity across privacy-chain wallet splits.** As described above, a sophisticated operator using multiple wallets funded through the privacy chain cannot be identified at the protocol level. The cluster cap and zero-reward modifier address the failure domain risk regardless of identity. The quorum dedup closes the consensus influence gap in HF23. The residual risk is that a sophisticated operator runs many nodes across many genuinely distinct clusters, accumulating block reward income proportional to their node count while contributing proportionally to network health. This is the acceptable outcome: concentrated consensus influence is bounded; distributed capital participation is rewarded.

Operators with questions about cluster assignment, migration planning, or the HF22/HF23 timeline are encouraged to post in the Node Operators Telegram channel or open an issue in this repository.

---

## Available Languages

Community translations of this document are maintained in the whitepaper repository. In the event of any conflict between a translation and the English version, the English version governs.

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

*This document does not constitute financial or legal advice. XEQM is a utility coin for the EXIOM platform, not an investment product. Token classification, securities status, and applicable regulations vary by jurisdiction. Participants should consult their local legal and regulatory framework before acquiring or operating with XEQM. XEQM Labs does not encourage purchasing XEQM on the basis of speculative price appreciation.*
