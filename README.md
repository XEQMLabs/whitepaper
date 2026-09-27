# XEQM Labs - EXIOM Platform
## Tokenomics Whitepaper
### Draft v12 | 09/27/2026

---

## What Is Live Today vs. What Is Planned

| Component | Status |
|---|---|
| EXIOM mainnet | Live, operational since May 6, 2026 |
| Service node network | Live — 943 active service nodes as of September 27, 2026 |
| Lokinet (LLARP) | Committed as HF23's network transport; implementation begins Q4 2026 |
| XEQ to XEQM coin swap | Delivered and closed, 35-day production run, public auditable ledger |
| GUI wallet | Live, github.com/XEQMLabs/XEQMLabs-GUI |
| Node explorer | Live, active service node monitoring |
| EXIOM Oracle | Live on mainnet (Robinhood Chain, chainId 4663); 11-member operator committee as of September 27, 2026 |
| EXIOM developer API | Live in beta — self-serve keys, signed compliance claims and a verification engine, OpenAPI at /docs; free-to-build with prepaid per-call usage rolling out (September 27, 2026) |
| EXIOM Privacy Oracle (TLSNotary / ZK) | Foundations live (verification engine, oracle sessions); full private-web-data oracle in Phase 3 |
| EXIOM RFQ trading platform | In development, Phase 2/3, XEQM/BTC first pair |
| HF22, wallet-key quorum dedup and unbonding unification | Built and validated; scheduled to activate at mainnet block 219120 (~early October 2026) |
| HF23, proximity cluster cap, reward modifier, Lokinet transport | In design; Lokinet transport committed; targeted Q4 2026 |
| Formal on-chain governance | Planned, Phase 6 |

---

## 1. What XEQM Labs Is

XEQM Labs is a privacy technology company. Its flagship product, EXIOM, is a privacy-preserving Proof-of-Stake Layer 1 network and commercial developer platform operated by a global set of service nodes. XEQM is the access and usage coin for the platform. Developers build for free and pay for production usage in XEQM, consumed as they call the API. Service node operators earn XEQM for securing the network, and the same operators can earn additional revenue by running an oracle sidecar that serves the platform's oracle products.

The project carries forward a community and operational history going back more than seven years. The EXIOM mainnet was built to give that community a network with a verifiable supply, a predictable emission schedule, pure Proof-of-Stake consensus with no Proof-of-Work component, and service node mechanics that respect operator time and capital.

XEQM is a native Layer 1 coin, not tokenized on any other chain, not an ERC-20 or wrapped asset, and not bridged. Holders interact directly with the EXIOM mainnet.

### The EXIOM Product Family

**EXIOM Service Node Network.** Live on mainnet. A global set of service nodes secures the chain, earns block rewards, and forms the infrastructure layer on which all other EXIOM products run. 943 active service nodes as of September 27, 2026.

**EXIOM Coin Swap.** A commercial product enabling projects to migrate their holder community from a legacy chain to a new chain with full cryptographic auditability. The pilot was the migration of XEQ holders to XEQM on the EXIOM mainnet, running for 35 days with every submission processed through a cryptographically verified ledger bearing a public SHA256 fingerprint. The product is available to other projects requiring a verifiable chain migration.

**EXIOM Oracle.** Live on mainnet. The platform's first oracle product: a committee of XEQM service-node operators — each running a lightweight oracle sidecar — that produces BLS-aggregate, EIP-712 signed compliance attestations (for example, that an address is eligible for a given jurisdiction) which applications consume through the developer API. It is deployed on Robinhood Chain (chainId 4663) and runs an 11-member operator committee as of September 27, 2026. Running the sidecar is how a service-node operator earns additional, usage-based revenue on top of block rewards.

**EXIOM Developer API.** Live in beta. A structured API exposing the platform's compliance and verification capabilities — signed compliance claims and a verification engine (signed-claims, TLSNotary, and zero-knowledge mechanisms) — with self-serve access (a DID plus API key), an OpenAPI 3.1 specification, webhooks, and idempotent requests. Developers build for free on a generous monthly allowance and pay for production usage in XEQM, consumed per call. Phase 2, active.

**EXIOM Privacy Oracle.** Designed, foundations in place. The broader evolution of the oracle: proving facts about private web data (via TLSNotary and zero-knowledge techniques) without exposing the underlying source. The verification engine and oracle-session endpoints that underpin it are already live; the full private-web-data oracle is a Phase 3 deliverable. Both the EXIOM RFQ platform and third-party applications can consume oracle outputs.

**EXIOM RFQ Trading Platform.** In development. A peer-to-peer over-the-counter trading platform with cryptographic settlement attestations, built on the EXIOM API. The first trading pair is XEQM/BTC, both native Layer 1 assets with no tokenization, no wrapping, and no bridge risk. The oracle provides private price attestations for the pricing layer. Phase 2/3.

XEQM Labs operates EXIOM as a commercial software platform. The goal is sustainable platform revenue that reduces dependence on governance emissions over time. XEQM Labs does not encourage purchasing XEQM on the basis of speculative price appreciation.

---

## 2. Supply Provenance

The migration is complete. 276,917,604 XEQM were issued on the EXIOM mainnet in exchange for legacy holdings. That figure is the verified starting supply at mainnet launch on May 6, 2026. Every legacy deposit was recorded in a public ledger with a SHA256 fingerprint. The new chain was minted once at the conclusion of the swap to match that exact verified total. Spend keys for every wallet involved in the swap have been published, and anyone can verify the complete transaction history from deposit to payout.

Beyond the starting supply, new XEQM enters circulation through two protocol-level emission streams: service node block rewards and governance emissions. Both run on fixed and predictable schedules written into the protocol that anyone can compute from public parameters. Rates and operational detail are in Section 3. Total supply grows over time. XEQM is an uncapped-supply chain on the same model as Monero's tail emission. The fixed-supply discipline the project commits to refers to the absence of discretionary issuance, not a hard cap on protocol-driven emissions.

**No discretionary mints.** The protocol does not allow ad-hoc issuance, manual supply adjustments, or off-schedule mints. Every new XEQM entering circulation does so through the two scheduled emission streams above.

**No burns.** The cryptographic architecture this network is built on does not support provable burns in the way that term is typically used. Any address a coin is sent to is only as unspendable as the key is demonstrably destroyed. We will not represent any wallet as a burn address. Coins not swapped during the migration window remain on the inactive legacy chain and are not part of XEQM supply.

---

## 3. Tokenomics Model

### Block Emissions

The network produces a new block every 60 seconds and awards 8.25 XEQM to the selected service node, generating 11,880 XEQM per day. At 943 active nodes (September 27, 2026), each node earns approximately 12.6 XEQM per day, or about 380 XEQM per month.

Starting with HF21, block rewards are distributed on a weekly batching schedule. Prior to HF21, rewards were issued every 20 blocks. Rewards now accumulate over each 10,080-block window (approximately 7 days) and are paid out at the end of each window. The total emission rate is unchanged; only the payment cadence has shifted.

### Governance Emission

The treasury receives approximately 17,857 XEQM per day, or roughly 124,999 XEQM per week. This is the operating budget for an active commercial software development team. Engineers, security reviewers, infrastructure operators, and ecosystem contributors are compensated from this emission while the platform is pre-revenue. As each EXIOM product reaches revenue-generating status, the governance emission is reviewed and reduced accordingly. The long-term objective is for platform revenue to replace governance emission as the primary funding mechanism.

### Emission Allocation

| Allocation | Share | Purpose |
|---|---|---|
| Service Node Rewards | 40% | Block rewards paid directly to service nodes |
| Core Protocol Development | 25% | Blockchain, EXIOM platform, and core network services |
| Marketing and Awareness | 15% | Network visibility and adoption |
| Ecosystem and Community | 10% | Grants, bounties, community rewards, integration support |
| Security and Audits | 5% | Audits, security reviews, reliability testing |
| Long-Term Reserve | 5% | Stability, emergency needs, long-term operations |

### EXIOM Platform Revenue and Distribution

Beyond block rewards, the platform earns revenue from developer usage. Access is prepaid: a developer funds their account by depositing XEQM (non-refundable), and that balance is drawn down as they consume the production API, priced per call. Development and evaluation on the free allowance are not charged.

Consumed XEQM is recognized as platform revenue and distributed between the operators who serve the oracle and platform operations:

| Recipient | Share | Purpose |
|---|---|---|
| Oracle sidecar operators | 70% | Service-node operators running the oracle sidecar, rewarded in proportion to the oracle duties they help serve |
| Platform operations and development | 30% | Funds ongoing operations and development, reducing reliance on governance emission over time |

Operators take the majority because they run the infrastructure that serves the oracle. The 70/30 ratio is the initial value and is adjustable through governance. Revenue is recognized and distributed on the same weekly cadence as block rewards — each 10,080-block window (approximately 7 days), aligned to the HF21 reward batching — so an operator receives block rewards and the usage-revenue share on one rhythm. This revenue share is the mechanism by which the operator sidecar reward described in Section 4 is funded from real usage rather than emission.

Baseline hardware to run a service node (and its oracle sidecar): 4 CPU cores, 8 GB RAM, 100 GB SSD, 100 Mbps connection. Heavier privacy-oracle workloads require higher specifications, covered in Section 10.

---

## 4. Service Node Structure

### Staking Parameters

| Parameter | Value |
|---|---|
| Full node requirement | 200,000 XEQM |
| Minimum operator stake | 100,000 XEQM (50% of full requirement) |
| Maximum operator fee | 10% |
| Unbonding period, voluntary withdrawal | 14 days, rewards continue |
| Unbonding period, forced deregistration | 14 days, no rewards (unified in HF22) |
| Maximum contributor slots | 11 (including the operator) |
| Minimum community contribution per slot | 10,000 XEQM |
| Community staker window per node | Up to 100,000 XEQM across up to 10 contributor slots |

### Node Economics

Many cloud VPS providers offer a free service tier that can support service node operation at zero monthly cost. A paid VPS at approximately $5.28 per month can run 10 service nodes, bringing per-node hosting cost to roughly $0.53 per month. Managed hosting through Pecunia is available at $1.76 per node per month.

Per-node block rewards scale inversely with the active node count: at 943 active service nodes (September 27, 2026), the network's 11,880 XEQM daily emission works out to roughly 12.6 XEQM per node per day, about 380 XEQM per month. Because both the reward and the stake are denominated in XEQM, the block-reward APY is approximately 2.3% independent of price; hosting is the only material recurring cost, at roughly $0.53 per node per month self-hosted or $1.76 through Pecunia. Running the oracle sidecar (Section 10) adds a second income stream that is revenue-based and scales with actual platform usage, funded from developer consumption rather than emission.

### Contributor Economics

Operators who cannot or choose not to run infrastructure can contribute stake to an existing node across up to 10 contributor slots. The operator may charge 0% to 10% of the block reward before the remainder splits proportionally among contributors. Contributors carry no hosting cost, so at every price point a contributor's net yield exceeds that of a self-hosted or Pecunia-hosted operator.

### Node Lifecycle

Nodes remain active indefinitely with maintained collateral and performance requirements. A node that falls out of compliance can be remediated without penalty. If not remediated, forced deregistration triggers a 14-day unbonding period with no rewards. Voluntary exit carries a 14-day unbonding period with rewards continuing throughout.

---

## 5. Network Survivability and Attack Vectors

### Survivability Requirement

The EXIOM network makes reliability commitments to developers. A network that can be taken offline by a single datacenter outage cannot make those commitments. The protocol enforces a maximum failure domain size: no single physical facility, datacenter, or routing cluster may host more than 30% of active nodes.

At 943 nodes (September 27, 2026), 30% is approximately 283 nodes. Losing any single facility can take at most 283 nodes offline simultaneously, leaving at least 660 nodes operational, sufficient to maintain block production and quorum formation without cascading decommissions. This is an engineering requirement, not a decentralization preference.

### Two Hard Forks

Survivability enforcement is delivered in two stages, separated to reduce risk and ship validated work immediately.

**HF22, built and scheduled:** Operator wallet-key quorum deduplication and unbonding period unification. No Lokinet dependency. Validated through nine stall/recovery cycles with 100% recovery rate and zero intervention, and scheduled to activate at mainnet block 219120 (approximately early October 2026); nodes are being upgraded ahead of activation.

**HF23, in design, targeted Q4 2026:** Proximity cluster registration cap, zero-reward modifier for excess nodes, and upgrade of quorum deduplication from wallet-key to proximity cluster. All three depend on Lokinet as the primary network transport, which is a committed part of HF23. Implementation begins in Q4 2026.

### HF22 Controls

**Operator wallet-key quorum deduplication.** At most one node per operator wallet address may hold a validator seat in any given Pulse round, oracle session, or obligations quorum. If a random draw selects two nodes from the same operator address, the second is replaced by a node from a different operator. Block rewards are unaffected; they are assigned by wait-time ordering independently of quorum participation.

Known limitation: defeated by wallet splitting. An operator using multiple wallet addresses presents multiple operator keys to the protocol. HF23 closes this gap through proximity cluster deduplication.

**Unbonding period unification.** Forced deregistration unbonding extended from 7 days to 14 days, matching voluntary withdrawal. Both cases are now 14 days.

### HF23 Controls

Once Lokinet is active as the network transport, nodes that are physically co-located will show characteristic routing signatures: sub-millisecond mutual latency and high path overlap through the Lokinet routing graph. Nodes at genuinely different facilities will show higher latency and lower path overlap. This clustering signal is derived from observable network behavior, with no requirement for operators to disclose their provider or location.

**Cluster registration cap.** New node registrations evaluated against Lokinet routing proximity to existing clusters. If the target cluster already contains 30% or more of active nodes, the registration is rejected by the protocol.

**Zero-reward modifier.** Nodes above the cluster cap threshold earn zero block rewards until migrated to a non-concentrated cluster. Nodes are ranked within each cluster by registration age; the oldest nodes up to the cap threshold earn full rewards. Every node above that threshold earns zero. A reduced rate can be rationalized against VPS costs; zero cannot.

A 30-day grace period applies at HF23 activation. All nodes earn full rewards during the grace period. At expiry, the zero-reward modifier activates on excess nodes.

**Proximity cluster quorum deduplication.** Upgrades HF22 wallet-key dedup to proximity cluster dedup. At most one node per proximity cluster per round, regardless of wallet structure. Closes the wallet-splitting gap.

The quorum size is 12 seats per round. The dedup therefore requires at least 12 distinct proximity clusters to function without a fallback. Given current network topology, the cluster count at HF23 activation may be close to this minimum. The algorithm implements a mandatory fallback: if all distinct clusters are exhausted before 12 seats are filled, additional seats are allocated starting from the smallest (least concentrated) clusters first, before the most concentrated cluster receives a second seat. Fallback frequency is logged and published in the node explorer as a real-time concentration risk indicator. A network never triggering the fallback has achieved adequate physical diversity.

### Additional Controls

**Capital cost barrier.** The 100,000 XEQM minimum operator stake ensures every operator commits real capital to each node. Running N nodes requires at least N x 100,000 XEQM staked.

**Operator fee capture protection.** EXIOM is not subject to the operator fee capture attack present in some service node networks, where an operator registers a node with minimal capital and sets a 100% fee to capture the entire block reward regardless of contributor stake. The maximum fee is capped at 10% and the 50% minimum operator stake makes this economically irrational.

**Uptime proof timing analysis.** Nodes on the same physical host submit uptime proofs in tight correlated clusters, detectable from existing proof receipt data without daemon changes.

**ASN analysis.** Nodes behind the same Autonomous System Number share provider-level infrastructure and legal exposure. ASN concentration contributes to cluster assignment and governance review.

**Governance blocklist.** A governance-managed public key blocklist prevents blocklisted registration keys from registering new nodes.

**Nakamoto coefficient target.** The network targets an operator coefficient of at least 8. As of September 27, 2026, across 943 active service nodes and 204 operators, the operator Nakamoto coefficient — the minimum number of operators controlling a majority of active nodes — is 9, meeting the target (up from 7 across 184 operators in July 2026). Physical-facility concentration is a separate and more acute problem: a single datacenter region still hosts a majority of nodes, which is exactly the concentration HF23's proximity-cluster cap is designed to break.

The full concentration limits proposal is at [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md). The sybil resistance methodology is at [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

### Lokinet as the Future Network Transport

The EXIOM network's addressing infrastructure will migrate from publicly announced IP addresses to Lokinet addressing as part of HF23 (targeted Q4 2026). Lokinet (Low Latency Anonymous Routing Protocol, LLARP) is a layer 3 onion routing protocol routing any IP-based traffic through multiple service nodes via multi-hop onion routing, with no single node in the path knowing both the origin and destination.

Once Lokinet is active:

- Service nodes will be addressed by their Lokinet cryptographic identifier rather than a publicly announced IP address
- The EXIOM developer API will be accessible as a hidden service at a `.loki` address, concealing the developer's origin IP from the API node
- The RFQ trading platform will be accessible as a hidden service, concealing requester and LP IP addresses from the platform
- Oracle session communication between prover and verifier quorum will be routed over Lokinet, eliminating the centralized coordinator trust assumption

Lokinet is a committed part of HF23, targeted for Q4 2026. The LLARP codebase is present in the EXIOM repository; implementation of Lokinet as the primary network transport begins in Q4 2026.

---

## 6. XEQM as a Utility Coin

XEQM demand comes from three sources. Node staking locks the largest share of supply, approximately 68% at the current 943 active nodes (September 27, 2026). Developer consumption creates a continuous velocity layer: applications pay for production API usage in XEQM, so platform adoption converts directly into recurring demand for the coin. Oracle access adds a third layer for higher-volume consumers.

Access follows a prepaid, usage-based model rather than a stake-to-unlock gate — developers do not have to acquire and lock a fixed stake to build:

| Tier | Access model |
|---|---|
| Free | Build and evaluate at no cost: a generous monthly call allowance, no deposit required |
| Production | Prepaid usage: deposit XEQM and pay per call; webhooks and higher limits |
| Enterprise | Custom limits, SLA, and support; volume terms |

Production usage is metered per API call and drawn from the developer's prepaid XEQM balance. Deposits are non-refundable and are recognized as platform revenue as they are consumed (see Section 3). An earlier design gated tiers behind a fixed XEQM stake; that has been replaced by this prepaid model, which is simpler for developers and standard for commercial APIs.

---

## 7. Governance and Treasury

The governance wallet address and view key are published. Anyone can verify the balance at any time. Governance currently runs through the founding team with community input through open Telegram channels and GitHub discussions.

Treasury allocations, drawn from the governance emission described in Section 3:

- Core development (25%): engineering for the EXIOM API, oracle, and RFQ platform
- Marketing and awareness (15%): exchange listings, content, community growth
- Ecosystem and community (10%): grants, bounties, integration support
- Security and audits (5%): code audits, security reviews, penetration testing
- Long-term reserve (5%): operational stability and emergency reserves

Phase 3 introduces a formal proposal and comment process. Phase 6 introduces weighted voting where service node and API node operators hold formal rights proportional to stake and tenure.

---

## 8. Parameter Summary

| Parameter | Value |
|---|---|
| Consensus mechanism | 100% Proof-of-Stake |
| Block time | 60 seconds |
| Block reward | 8.25 XEQM per block |
| Daily block emissions | 11,880 XEQM |
| Governance emission | ~17,857 XEQM per day |
| Full node requirement | 200,000 XEQM |
| Minimum operator stake | 100,000 XEQM (50%) |
| Maximum operator fee | 10% |
| Maximum contributor slots | 11 (including operator) |
| Minimum community contribution | 10,000 XEQM per slot |
| Community staker window per node | Up to 100,000 XEQM across 10 slots |
| Unbonding period, voluntary withdrawal | 14 days, rewards continue |
| Unbonding period, forced deregistration | 14 days, no rewards (HF22) |
| Total supply | 276,917,604 XEQM at launch, growing through scheduled emissions |
| Supply locked at 943 nodes (Sep 27, 2026) | ~188,600,000 XEQM (~68% of starting supply) |
| Freely circulating at 943 nodes | ~88,300,000 XEQM at starting supply, growing with emissions |
| Solo operator APY at 943 nodes | ~2.3% (block rewards only, paid weekly via HF21) |
| Self-hosted cost per node | ~$0.53/month ($5.28/mo VPS, 10 nodes) |
| Managed hosting cost (Pecunia) | $1.76/node/month |
| Active service nodes (September 27, 2026) | 943 |
| Operator Nakamoto coefficient (Sep 27, 2026) | 9 — majority control; target >= 8; 943 nodes, 204 operators |
| Oracle external activation | Nakamoto >= 6 reached; gated on Phase 3 completion |
| Quorum size | 12 seats per round |
| Quorum dedup, HF22 | One operator wallet address per quorum seat per round |
| Quorum dedup, HF23 | One proximity cluster per quorum seat per round (requires Lokinet) |
| Quorum dedup fallback, HF23 | If fewer than 12 distinct clusters exist, smallest clusters receive additional seats first before most concentrated clusters; fallback frequency logged and published |
| Network survivability cap, HF23 | 30% of active nodes per proximity cluster (~283 nodes at current count) |
| Zero-reward modifier, HF23 | Zero block rewards for nodes above cluster cap, ranked by registration age |
| Core repos | github.com/XEQMLabs |

---

## 9. Roadmap

**Phase 1, Network stabilization. COMPLETE.** The service node network grew to 943 active service nodes as of September 27, 2026 (from 693 across 184 operators in July 2026, Nakamoto coefficient 7). XEQ to XEQM coin swap ran and closed successfully.

**Phase 2, EXIOM developer API and EXIOM Oracle. ACTIVE.** The EXIOM Oracle is live on mainnet with an operator committee, and the developer API is live in beta (self-serve credentials, compliance and verification endpoints, OpenAPI). Remaining Phase 2 work: prepaid consumption billing, the operator revenue share, and first production integrations. EXIOM RFQ trading platform development proceeds in parallel, XEQM/BTC as the first trading pair.

**Phase 3, EXIOM Privacy Oracle and RFQ platform.** The oracle rolls out in phases: internal proof of concept, federated testnet, then mainnet with internal consumers. The RFQ trading platform reaches production in this phase, using the oracle for private price attestation on the XEQM/BTC pair. Both are built on the EXIOM API.

**Phase 4, External oracle consumer access.** Oracle outputs available to Production and Enterprise tier developers and external consumers. Nakamoto coefficient threshold of 6 already reached; activation gated on Phase 3 completion.

**HF22, built and scheduled (mainnet block 219120, ~early October 2026).** Two validated consensus changes with no Lokinet dependency: operator wallet-key quorum deduplication (one operator address per quorum seat per round) and unbonding period unification (forced deregistration extended from 7 to 14 days). Nodes are being upgraded across the network ahead of activation.

**HF23, in design, targeted Q4 2026.** Once Lokinet is active as the network transport: Lokinet activation as primary transport replacing publicly announced IP addresses; proximity cluster registration cap (registrations rejected when a cluster exceeds 30% of active nodes); zero-reward modifier for nodes above the cap threshold ranked by registration age; upgrade of quorum deduplication from wallet-key to proximity cluster, with a mandatory fallback rule ensuring quorum formation is always possible even when fewer than 12 distinct clusters exist (smallest clusters receive additional seats first before most concentrated clusters, with fallback frequency logged and published as a concentration risk indicator). A 30-day grace period applies at activation before the zero-reward modifier takes effect.

**Phase 6, Formal governance.** Structured proposal process, weighted voting for operators, long-term transition away from founding-team governance.

---

## 10. EXIOM Oracle

### The first live oracle: EXIOM Oracle

The platform's first oracle product is live on mainnet. The EXIOM Oracle is a committee of XEQM service-node operators — each running a lightweight oracle sidecar alongside their node — that collectively produce BLS-aggregate, EIP-712 signed attestations about compliance facts, most directly whether a given address is eligible for a given jurisdiction. Applications consume these attestations through the developer API and can submit the signed result on-chain. The committee is deployed on Robinhood Chain (chainId 4663) and runs an 11-member operator committee as of September 27, 2026, with a two-thirds signing threshold.

The sidecar is deliberately light: it holds only its own signing key, reads its node's identity locally, and never handles the operator's spend keys. Running it is the mechanism by which a service-node operator earns the additional, usage-funded revenue described in Sections 3 and 4.

### The broader vision: EXIOM Privacy Oracle

The EXIOM Privacy Oracle allows applications to consume authenticated private data feeds without exposing the underlying source data. It uses zero-knowledge proof techniques to prove data provenance from standard HTTPS endpoints, requiring no server-side cooperation and no trusted hardware. It is a Phase 3 deliverable, following Phase 2 API platform stabilization and a cryptography consultation before the full build begins.

The oracle is not a general-purpose data feed. It is a privacy-first oracle for use cases where the data itself must remain confidential: price thresholds without revealing exact prices, account balances without exposing credentials, compliance attestations without disclosing the underlying record. The EXIOM RFQ platform is the first internal consumer, using it to prove that a XEQM/BTC fill occurred at or better than a reference price without revealing the exact price to the platform or the other party.

Once Lokinet is active as the network transport, oracle session communication between the prover and verifier quorum will be onion-routed through the service node network. Neither the prover's origin nor the quorum nodes' network addresses will be visible to any single relay node, eliminating the centralized coordinator trust assumption.

### Architecture

**Prover layer.** The application or user holding access to the private data source participates in a cryptographic protocol that commits to the TLS response without revealing it. Credentials and raw data never leave the prover's control.

**Verifier layer.** A rotating quorum of service nodes verifies that committed data satisfies the requested condition. Verifier nodes learn only the result (true or false, above or below a threshold) and never see the underlying data or credentials.

**Consumer layer.** Consumers receive only the minimal output: a boolean result, a threshold comparison, a signed attestation, or a small derived value. Raw source data is never published.

### Phased Build Plan

**Phase 1, Internal proof of concept.** Founding team validates the full cryptographic protocol end to end against a small set of whitelisted sources, no external consumers or service node participation.

**Phase 2, Federated oracle testnet.** Volunteer service node operators with strong uptime history join the verifier pool on testnet. Adversarial testing of attestation integrity before any mainnet deployment.

**Phase 3, Mainnet oracle with internal consumers.** Oracle verifier duty opens to qualified mainnet nodes. Outputs feed internal EXIOM contracts and the RFQ platform. Oracle fees begin flowing to participating verifier nodes.

**Phase 4, External consumer access.** Oracle outputs available to Production and Enterprise tier developers and external consumers. Gated on Phase 3 completion.

### Verifier Hardware Requirements

Indicative requirements: 8 CPU cores, 16 GB RAM, 200 GB SSD, 500 Mbps with low latency. Standard API node baseline hardware is not sufficient for oracle verifier duty.

### Verifier Rewards

| Revenue Source | Description |
|---|---|
| Block rewards | Standard service node block reward, unchanged |
| Platform revenue share | Proportional share of developer-consumption revenue for operators running the oracle sidecar |
| Oracle session fees | Per-session fee from oracle consumers, distributed to the verifier quorum |
| Oracle duty bonus | Supplemental governance emission during low-volume periods, reduced as session fees self-sustain |

---

## 11. EXIOM RFQ Trading Platform

The EXIOM RFQ platform is a peer-to-peer over-the-counter trading system with cryptographic settlement attestations, built on the EXIOM API. The first trading pair is XEQM/BTC, both native Layer 1 assets with no tokenization, no wrapping, and no bridge risk.

Once Lokinet is active, the RFQ platform will be accessible as a Lokinet hidden service. Neither the requester's nor the LP's IP address will be visible to the platform. The oracle pricing layer allows a counterparty to prove that a fill occurred at or better than a reference price from a whitelisted source, without revealing the exact fill price to the platform or the other party.

RFQ application specification and data model are complete. Active development proceeds in Phase 2 on the API layer. Full trading platform production is a Phase 3 deliverable, dependent on the EXIOM API reaching production and the oracle MVP completing its internal proof of concept.

---

---

## Available Languages

Community translations of this whitepaper are maintained in the translations folder. In the event of any conflict between a translation and the English version, the English version governs.

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

*This is a draft document. Parameters, emission schedules, and roadmap phases described here are the intended design. Updates will be published as the network and platform evolve.*

*This document does not constitute financial or legal advice. XEQM is a utility coin for the EXIOM platform, not an investment product. Token classification, securities status, and applicable regulations vary by jurisdiction. Participants should consult their local legal and regulatory framework before acquiring or operating with XEQM. XEQM Labs does not encourage purchasing XEQM on the basis of speculative price appreciation.*
