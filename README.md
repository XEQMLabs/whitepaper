# XEQM Labs
## Tokenomics Whitepaper
### Draft v9 | 07/15/2026

---

## 1. What XEQM Labs Is

XEQM Labs is a privacy-preserving Proof-of-Stake network and a developer platform for building applications on top of it. The network is operated by a global set of service nodes that earn XEQM for securing the chain. The developer platform exposes the network's privacy capabilities through a clean API and is the primary mechanism through which XEQM finds practical, ongoing utility.

The project carries forward a community and an operational history that go back more than seven years. The XEQM Labs mainnet is the technical foundation we built to give that community a network with a verifiable supply, a predictable emission schedule, a Proof-of-Stake consensus model with no Proof-of-Work component, and service node mechanics that respect operator time and capital.

XEQM is the access and usage token for the platform. Developers stake XEQM to unlock API tiers. Applications consume XEQM as they make calls. Service node operators earn XEQM for securing the network. API node operators earn XEQM for serving developer traffic. These four roles, with a fifth oracle role described in Section 10, form the economic backbone of the network.

This whitepaper documents the tokenomics, the service node structure, the security model, and the platform roadmap. The figures in this document reflect the completed migration to the XEQM Labs mainnet and the verified swap-issued supply.

---

## 2. Supply Provenance

The migration is complete. 276,917,604 XEQM were issued on the XEQM Labs mainnet in exchange for legacy holdings, and that figure is the verified starting supply of the network at mainnet launch on May 6, 2026.

Every legacy deposit was recorded in a public ledger with a SHA256 fingerprint. The new chain was minted once at the conclusion of the swap, to match that exact verified total. Spend keys for every wallet involved in the swap process have been published, and anyone can open those wallets and verify the complete transaction history from deposit to payout.

### Ongoing Emissions

Beyond the starting supply, new XEQM enters circulation through two protocol-level emission streams, both running on fixed and predictable schedules:

- **Service node block rewards.** The protocol mints 8.25 XEQM per 60-second block as a reward to the selected service node, generating approximately 11,880 XEQM per day in block emissions.
- **Governance emissions.** The protocol mints approximately 17,857 XEQM per day to the governance wallet for development, ecosystem programs, security audits, and long-term reserves.

These emissions are written into the protocol and follow a known schedule that anyone can compute from public parameters. Total supply grows over time as a result, and XEQM is therefore an uncapped-supply chain on the same model as Monero's tail emission. The "fixed-supply discipline" the project commits to refers to the absence of discretionary issuance, not a hard cap on protocol-driven emissions.

### No Discretionary Mints, No Burns

XEQM Labs commits to two supply-management rules that limit how total supply can change beyond the scheduled emissions described above.

No discretionary mints. The protocol does not allow ad-hoc issuance, manual supply adjustments, or off-schedule mints. Every new XEQM that enters circulation does so through the two emission streams described above, on schedules that are written into the protocol and that anyone can verify by computing them from public parameters.

No burns. The cryptographic architecture this network is built on does not support provable burns in the way that term is typically used. Any address a coin is sent to is only as unspendable as the key is demonstrably destroyed, and we will not represent any wallet as a burn address. Coins that were not swapped during the migration window remain on the inactive legacy chain and are not part of XEQM supply.

The supply curve a developer, exchange, or operator evaluates today, the verified starting supply plus the published emission schedules, is the supply curve they can rely on going forward.

---

## 3. Tokenomics Model

### Block Emissions

The network produces a new block every 60 seconds and awards 8.25 XEQM to the selected service node. This generates 11,880 XEQM per day across the network.

Starting with HF21, service node block rewards are distributed on a weekly batching schedule rather than per-block. Rewards accumulate over each 10,080-block window (approximately 7 days) and are paid out to operators at the end of each window. The total emission rate is unchanged; only the payment cadence shifts from per-block to weekly.

### Governance Emission

The protocol allocates a separate governance emission to the treasury wallet. The treasury receives approximately 17,857 XEQM per day, or roughly 124,999 XEQM per week. This funds development, the XEQM Labs platform, ecosystem support, security work, and long-term reserves on a stable, predictable schedule.

### Distribution Model

All newly issued XEQM follows a straightforward allocation. These are target percentages that guide long-term planning. The protocol does not hardcode them, and governance can adjust them.

| Allocation | Share | Purpose |
|---|---|---|
| Service Node Rewards | 40% | Paid directly to service nodes as compensation for securing the network |
| Core Protocol Development | 25% | Supports development of the blockchain, the XEQM Labs platform, and core network services |
| Marketing and Awareness | 15% | Improves network visibility and supports adoption |
| Ecosystem and Community | 10% | Grants, bounties, community rewards, and integration support |
| Security and Audits | 5% | Covers audits, security reviews, and reliability testing |
| Long-Term Reserve | 5% | Held for stability, emergency needs, or long-term operations |

### XEQM Labs Platform Fee Distribution

Beyond block rewards, the XEQM Labs developer platform generates fees that benefit the broader ecosystem. The platform distributes all revenue as follows:

| Recipient | Share | Notes |
|---|---|---|
| API Node Operators | 35% | Distributed proportionally by requests served to operators running XEQM Labs API nodes |
| XEQM Labs Treasury | 35% | Funds ongoing platform development |
| Community Governance | 30% | Flows to the governance wallet for community-directed allocation |

API nodes are independent infrastructure. They do not need to run on the same machine as a service node, and running one does not require a service node operator background. Any technically capable operator can run an API node, register with the platform, and begin earning a share of platform fees proportional to the requests they serve. Current baseline hardware requirements are modest: 4 CPU cores, 8 GB of RAM, 100 GB of SSD storage, and a 100 Mbps network connection. Future XEQM Privacy applications and oracle workloads will require higher specifications, and operators are encouraged to plan for vertical scaling as oracle duty becomes available. A standard VPS costs an estimated $20 to $40 per month at current baseline requirements.

Service node operators who also run an API node earn both block rewards from consensus participation and a proportional share of platform fees from API traffic. These are two separate and additive income streams. Operators who do not run an API node continue to earn block rewards as normal. Operators who additionally take on oracle verifier duty earn a third additive reward stream from oracle fees, described in Section 10.

### Long-Term Inflation Strategy

The mainnet runs on predictable, stable emissions, but these levels are not intended to remain permanent. As the XEQM Labs platform generates sustainable revenue, the network will work toward reducing governance emissions and relying less on token issuance for operational funding. Inflation decreases as protocol revenue increases. Service node operators, token holders, and ecosystem contributors all benefit from that outcome.

---

## 4. Service Node Structure

### Staking Parameters

The following parameters apply to service nodes on the XEQM Labs network.

| Parameter | Value |
|---|---|
| Full node requirement | 200,000 XEQM |
| Minimum operator stake | 100,000 XEQM (50% of full requirement) |
| Maximum operator fee | 10% |
| Unbonding period (voluntary withdrawal) | 14 days, rewards continue during period |
| Unbonding period (forced deregistration) | 10,080 blocks (~7 days), no rewards during period |
| Maximum contributor slots | 11 (including the operator) |
| Minimum community contribution per slot | 10,000 XEQM |
| Community staker window per node | Up to 100,000 XEQM across up to 10 contributor slots |

### Why 200,000 XEQM Per Node

The 200,000 XEQM full node requirement is calibrated against the verified starting supply of 276,917,604 XEQM. It is sized to lock a meaningful share of supply in active network security while leaving enough free float for exchange liquidity, developer onboarding, and ongoing API consumption.

At 200,000 XEQM per full node, 700 nodes lock 140,000,000 XEQM, which is approximately 50.6% of the starting supply. Removing that share from active circulation dampens speculative volatility and creates sustained demand for the token. The remaining approximately 137,000,000 XEQM in free float gives exchange markets and the developer onboarding pipeline the depth they need. As emissions grow total supply over time, the locked share declines as a percentage of supply, which is the intended trajectory: the network becomes proportionally more liquid as it matures and as platform activity creates additional demand for free-float XEQM.

### Why 10,000 XEQM Minimum Contributor Stake

Each service node supports up to 11 contributor slots, including the operator. The operator occupies one slot and contributes 100,000 XEQM, leaving 10 slots that share up to 100,000 XEQM of community stake. A 10,000 XEQM minimum per contributor slot filters trivial or dust contributions that serve no network purpose, and it gives each contributor a genuine economic stake in the node's performance. It also keeps community staking accessible to holders who cannot run a full node themselves.

### Why 50% Minimum Operator Stake

The minimum operator stake is set at 50% of the full node requirement, or 100,000 XEQM. The attack vector section below explains this in detail. In short, a low minimum stake gives a bad actor an economic incentive to open nodes with minimal capital and extract disproportionate rewards. Setting the minimum at 50% removes that incentive while still allowing community members to contribute the remaining stake across the available contributor slots.

### Service Node Lifecycle

Service nodes on the XEQM Labs network operate on continuous terms rather than fixed periods.

- Nodes remain active indefinitely as long as the operator maintains staked collateral and meets performance requirements. There are no fixed terms and no renewals required.
- If a node falls out of compliance, the operator can correct the issue and resume earning without losing the remainder of a fixed period. If the operator does not remediate the issue, the service node is deregistered and enters a forced unbonding period of 10,080 blocks (approximately 7 days). No rewards are paid during a forced unbonding period.
- Operators can exit at any time through a voluntary withdrawal. The voluntary unbonding period is 14 days. Unlike forced deregistration, rewards continue to accrue during a voluntary unbonding period.
- Community contributors can supply between 10,000 XEQM and the remaining unfunded portion of the node requirement, across up to 10 available contributor slots.

---

## 5. Attack Vectors and Protections

### The Operator Fee Capture Attack

This attack exists in the codebase the XEQM Labs mainnet was forked from and required a code change to patch. We disclose it here because community stakers need to understand the risk and the mitigations in place.

The network distributes service node rewards in two steps. First, it calculates the operator's fee percentage from the total block reward before any distribution occurs. Second, it splits the remaining reward proportionally among all contributors based on their stake share.

Without the controls described below, an operator could open a node with minimal capital and set a fee of up to 100%. At 100% fee, the operator would receive the entire block reward regardless of how much anyone else staked. Contributors staking the remainder would earn nothing. The operator would capture 100% of rewards using a fraction of the required collateral.

Two overlapping controls in the XEQM Labs parameters address this attack.

First, the maximum operator fee is capped at 10%. At a 10% fee, an operator staking exactly the 100,000 XEQM minimum earns 10% of the block reward as a fee, plus 50% of the remaining 90%, for a total of 55% of the block reward. A community contributor staking the other 100,000 XEQM earns 45% of the block reward. That is a proportional and reasonable outcome.

Second, the 50% minimum operator stake requires the operator to commit substantial capital before opening a node. A bad actor no longer has a path to 100% reward capture with minimal capital. Together, the fee cap and the higher minimum stake make the attack economically irrational.

Community stakers should still exercise judgment when choosing a node. The node explorer displays the fee, the operator's stake percentage, and the current contributor count before any staker makes a commitment.

These two controls — the fee cap and the minimum operator stake — address reward capture specifically. They do not prevent network concentration. An operator with sufficient capital can register many nodes while meeting the minimum stake requirement on each one, either by fully self-funding each node at 200,000 XEQM or by attracting community contributors to supply the remaining 100,000 XEQM per node. In both cases the operator retains full control of every node they register, and that control is what determines network influence. Community stakers who contribute to a node should understand that their stake increases that operator's network presence regardless of the fee terms. Network concentration is a separate attack surface with its own dedicated controls, described in the next section.

### Anti-Sybil Measures

In this context, a Sybil attack means a single actor operating a large number of nodes to gain disproportionate influence over the network. The concern is real. The swap ledger shows that the top 10 wallets in the migration hold a substantial concentration of XEQM, and several wallets appear to have been deliberately split into near-identical balances.

Wallet splitting does not necessarily indicate malicious intent. Large holders commonly distribute holdings across multiple addresses for security and operational reasons. We note and monitor the pattern regardless.

The following protections are in place or are enforced through governance policy.

The full technical specification for these anti-sybil measures, including the public key blocklist schema and the contributor slot graph analysis methodology, is published at [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

**Capital cost barrier.** The 100,000 XEQM minimum operator stake ensures that every operator commits real capital to each node they register. An operator running N nodes at the minimum stake must hold at least N × 100,000 XEQM in staked collateral. This raises the cost of accumulation but does not cap it — a well-capitalized operator can still self-fund many nodes above the minimum, and an operator who attracts community contributors to fill the remaining stake per node can accumulate nodes at half the self-funding cost while retaining full operational control of each one. The minimum stake is therefore the primary control against the reward capture attack, not against concentration. The governance node concentration cap below is the binding constraint on how many nodes any one operator may control.

**Governance node concentration cap.** A governance-enforced policy caps identifiable operators at approximately 50 nodes, roughly 7% of a 700-node network. The node explorer publicly lists every active service node along with its registration public key and announced IP address. The team and community monitor that list for patterns indicating a single operator controls more than the cap. When we identify a pattern, we contact the operator and give them the opportunity to voluntarily reduce their node count. Operators who do not comply face public identification and governance action, which at minimum means we add their registration keys to a protocol blocklist that prevents future node registration.

**Public key blocklisting.** A governance-managed blocklist of registration public keys is maintained, and the network refuses those keys for future node registration. When a bad actor is deregistered for misbehavior, their public key is permanently added to that list. Generating a new key pair costs nothing, but operating under a new key while the original sits on the blocklist is visible to monitoring tools and creates a documented record of evasion that strengthens the case for further governance action.

**IP address monitoring.** Service nodes must publicly announce their IP address to participate in the network. This is a functional requirement, not optional. Multiple nodes running from the same IP address or subnet almost certainly belong to the same operator. Multiple nodes running from the same hosting provider and datacenter block strongly suggest a single operator even across different IP addresses. We flag nodes that appear from related IP ranges shortly after a deregistration event for review. A sophisticated operator who uses different VPS providers across regions adds cost and complexity to their operation without eliminating their visibility, because the pattern of behavior across keys, addresses, and timing still produces a traceable record.

**Contributor slot graph analysis.** Each service node supports up to 11 contributor slots, and each contributor registers a wallet address against the node. An operator who runs multiple nodes and uses the same secondary contributor addresses across those nodes, or who funds contributor slots from wallets with observable relationships to the operator wallet, creates a graph that monitoring tools can analyze. On a privacy-preserving chain this analysis is less straightforward than on a transparent chain, but the contributor registrations carry observable data that supplements IP and key monitoring.

**Nakamoto coefficient target.** The network targets a Nakamoto coefficient of at least 8, meaning at least 8 independent operators should need to cooperate to control 51% of active nodes. As of July 2026, with 761 active nodes across 184 independent operators, the network Nakamoto coefficient is 7. Continued enforcement of the governance node cap and ongoing growth of the operator set are the primary mechanisms for maintaining and improving that number over time.

The Nakamoto coefficient of 7 is approaching the long-term target of 8. We state that here because honest disclosure of a known weakness is more valuable than silence. The gap closes as more operators join the network and as the governance concentration cap is enforced. Oracle quorum selection, described in Section 10, will not be opened to external contract consumers until the Nakamoto coefficient reaches at least 6. That threshold has been reached. External oracle access in Phase 4 is now gated on completing the Phase 3 mainnet oracle rollout rather than on the Nakamoto coefficient floor.

---

## 6. XEQM as a Utility Token

XEQM is the access and usage token for a developer platform, and that distinction matters when thinking about supply dynamics.

The XEQM Labs developer platform requires XEQM at every level of interaction. Developers stake XEQM to unlock API access tiers. When they leave, they get that stake back; it is a commitment mechanism, not a fee. Applications consume XEQM when they make API calls above their tier limit. Operators earn XEQM for the infrastructure they contribute.

| Tier | Stake Required | Included Calls |
|---|---|---|
| Free | None | 10,000 testnet calls per month |
| Builder | 1,000 XEQM | 100,000 mainnet calls per month |
| Production | 10,000 XEQM | 1,000,000 calls per month, webhooks, priority support |
| Enterprise | 50,000 XEQM | Unlimited calls, custom rate limits, SLA |

Oracle data feed access aligns with the existing tier structure. Production and Enterprise tier developers gain access to oracle outputs as part of their included capabilities. Oracle-heavy workloads that exceed standard rate limits consume XEQM at the same per-call model as other API traffic. This creates a fourth demand layer on top of the three sinks already described: node staking, developer tier staking, and API call consumption. Oracle consumers must hold and spend XEQM to access authenticated private data feeds.

Three distinct demand sinks operate simultaneously. Service node staking locks the largest share of supply. Developer tier staking creates ongoing buy pressure from new market participants who must acquire XEQM before they can access the platform. API call consumption creates a continuous velocity layer as applications process requests above their tier allowance.

The supply parameters in this document were designed with all of these sinks in mind. A freely circulating float of approximately 137 million XEQM at the starting supply, after 700 nodes are fully staked, gives exchange markets, developer onboarding, and ongoing API consumption enough liquidity to function. Free-float liquidity grows over time as emissions add to total supply. Tighter node requirements would shrink the float to a level that would make developer onboarding difficult and API cost budgeting unreliable, which would directly undermine the platform's value proposition.

---

## 7. Governance and Treasury

The XEQM Labs treasury model consolidates all governance funding into a single predictable emission schedule.

Governance currently runs through the founding team. The team makes decisions with input from the community through open Telegram channels and GitHub discussions. This is an honest description of how things work today. No on-chain voting mechanism exists yet, and there is no way to cryptographically verify that a participant in a community discussion actually holds XEQM. Any governance process must account for that reality rather than assume good-faith participation from every voice in every channel.

Later roadmap phases move toward a more structured governance model. Phase 3 introduces a formal proposal and comment process. Phase 4 introduces weighted voting where service node and API node operators hold formal rights proportional to their stake and tenure. Operators who have skin in the game through staked collateral are the most meaningful constituency for governance decisions, and the weighted model reflects that.

The 40/25/15/10/5/5 allocation described in Section 3 guides planning as a target. The founding team will propose changes publicly, discuss them openly, and decide them in consultation with the operator community until a more formal governance mechanism is in place.

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
| Unbonding period (voluntary withdrawal) | 14 days, rewards continue during period |
| Unbonding period (forced deregistration) | 10,080 blocks (~7 days), no rewards during period |
| Total supply | Verified starting supply: 276,917,604 XEQM. Grows over time through scheduled emissions. |
| Supply locked at 700 nodes | 140,000,000 XEQM (approximately 50.6% of starting supply, declining as a share over time) |
| Freely circulating at 700 nodes | Approximately 137,000,000 XEQM at starting supply, growing with emissions |
| Solo operator APY at 700 nodes | ~3.1% (block rewards only, paid weekly via HF21 batching) |
| Nakamoto coefficient (July 2026) | 7 (target: 8; 761 nodes, 184 operators) |
| Oracle quorum external activation | Nakamoto coefficient ≥ 6 |

---

## 9. Roadmap

The XEQM Labs mainnet is live. The roadmap that follows describes the work ahead.

**Phase 1: Network stabilization.** COMPLETE. Block production is stable, the operator fleet has grown to 761 active nodes across 184 independent operators, and the network Nakamoto coefficient has reached 7. Ongoing monitoring of block production, service node uptime, and network health continues. Hardware upgrades across the operator fleet are underway to meet increasing network demands and maintain high service-level requirements as the platform scales toward Phase 2 and oracle workloads.

**Phase 2: XEQM Labs API platform production launch.** ACTIVE. Public release of the developer API, tier registration, API node onboarding, and the first production integrations. API node fee distribution becomes active.

**Phase 3: Privacy Oracle phased rollout.** Internal proof of concept, federated testnet, and mainnet oracle with internal consumers, as described in Section 10.

**Phase 4: External oracle consumer access.** Oracle outputs become available to external smart contract consumers and Production and Enterprise tier XEQM Labs developers. This phase activates only after the Nakamoto coefficient reaches at least 6.

**Phase 5: Formal governance.** Structured proposal process, weighted voting for operators, and the long-term transition away from founding-team governance.

---

## 10. XEQM Privacy Oracle

### Overview

The XEQM Privacy Oracle is a planned capability of the XEQM Labs platform that allows smart contracts and external applications to consume authenticated private data feeds without exposing the underlying source data. It is built on a decentralized oracle protocol for TLS that proves data provenance from standard HTTPS endpoints using zero-knowledge proofs, requiring no server-side cooperation and no trusted hardware.

The oracle is not part of the initial mainnet feature set. It is a later-phase platform capability, developed after the XEQM Labs mainnet is stable and the XEQM Labs API platform has reached production. This section describes the architecture, the phased build plan, and how oracle participation integrates with the existing service node and API node reward model.

### Why This Fits XEQM

XEQM's core value proposition is privacy. The oracle extends that value proposition beyond the chain itself into the broader data economy. Applications built on XEQM Labs can use the oracle to prove facts about private web data, such as price thresholds, account balances, credential attributes, and compliance conditions, without revealing the underlying data to the oracle network, the application, or the blockchain.

This is not a general-purpose oracle that competes with existing data feed providers. It is a privacy-first oracle designed specifically for use cases where the data itself must remain confidential. That is a narrow and defensible niche that aligns with what XEQM already does.

### Architecture

The oracle operates as a three-layer system sitting on top of the existing service node infrastructure.

**Prover layer.** The application or user who holds access to the private data source acts as the prover. The prover fetches data from a standard TLS endpoint, such as a price API, an account portal, or a compliance feed, and participates in a cryptographic protocol that commits to the response without revealing it.

**Verifier layer.** A rotating quorum of service nodes acts as verifiers. The verifier nodes assist the prover in generating an unforgeable commitment to the TLS session data using a three-party handshake protocol, then verify that the committed data satisfies the requested condition. Verifier nodes learn only the result of the condition, true or false, above or below a threshold, and never see the underlying data or the prover's credentials.

**Consumer layer.** Smart contracts or XEQM Labs API consumers receive only the minimal output: a boolean result, a threshold comparison, a signed attestation, or a small derived value. Raw source data is never published to any consumer.

Verifier nodes are trusted for integrity, not for privacy. Even if all verifier nodes in a quorum were compromised simultaneously, the protocol design preserves the privacy of the prover's data. Multiple verifiers can be required to reach quorum agreement before any output is signed, which limits the impact of a single dishonest node on integrity.

### Phased Build Plan

**Phase 1, Internal proof of concept (post-mainnet stabilization).** A single prover and a single verifier node operated by the founding team validate the full cryptographic protocol end to end against a small set of whitelisted data sources. No external consumers. No service node participation. The goal is confirming the protocol works against real TLS endpoints under production network conditions before involving the broader operator community.

**Phase 2, Federated oracle testnet.** A small set of volunteer service node operators, selected from nodes with strong uptime history and meeting an enhanced hardware specification, join the verifier pool on testnet. Oracle duty rotates through this set using an adaptation of the existing quorum selection logic. Slashing conditions for provably false attestations are tested under adversarial conditions before any mainnet deployment. This phase does not open oracle outputs to external contract consumers.

**Phase 3, Mainnet oracle with internal consumers.** Oracle verifier duty opens to a larger set of qualified service nodes on mainnet. Outputs feed internal XEQM Labs contracts only. Quorum size, rotation parameters, and slashing conditions are finalized based on testnet observations. Oracle fees begin flowing to participating verifier nodes as an additive reward stream.

**Phase 4, External consumer access.** Oracle outputs become available to Production and Enterprise tier XEQM Labs developers and to external smart contract consumers. This phase does not activate until the network Nakamoto coefficient reaches at least 6. External activation before that threshold would expose oracle outputs to an unacceptable concentration risk.

### Oracle Verifier Hardware Requirements

Oracle verifier duty is computationally intensive. The three-party handshake and two-party computation protocols that underpin the oracle involve multiple rounds of interactive cryptography that are meaningfully more demanding than standard service node operation.

Nodes electing to participate in oracle verifier duty must meet an enhanced hardware specification at the time that specification is finalized. Current indicative requirements are a minimum of 8 CPU cores, 16 GB of RAM, 200 GB of SSD storage, and a 500 Mbps network connection with low latency. These figures reflect benchmarking against comparable protocol implementations and will be confirmed before Phase 2 begins. Standard API node baseline hardware is not sufficient for oracle verifier duty.

Operators who meet the enhanced specification and opt into oracle duty are identified in the node explorer. Quorum selection for oracle sessions draws exclusively from this opt-in pool.

### Oracle Verifier Rewards

Oracle verifier nodes earn compensation beyond standard block rewards. The reward structure for oracle participation is as follows.

| Revenue Source | Description |
|---|---|
| Block rewards | Standard service node block reward, unchanged |
| API node fees | Proportional share of XEQM Labs platform fees for operators also running an API node |
| Oracle session fees | Per-session fee paid by oracle consumers, distributed to the verifier quorum that processed the session |
| Oracle duty bonus | A supplemental emission allocated from the governance wallet to oracle-eligible nodes during periods of low consumer volume, ensuring verifier nodes remain economically viable before oracle demand reaches self-sustaining levels |

The oracle duty bonus is a bootstrapping mechanism. As oracle consumer volume grows and session fees become the primary revenue source for verifier nodes, the governance emission component is reduced proportionally. The long-term model is session fee sustainability without ongoing governance subsidy.

### Data Source Governance

Not all data sources are appropriate for oracle consumption. The oracle maintains a tiered source registry managed by governance.

**Tier 1, Whitelisted production sources.** Sources reviewed and approved for mainnet oracle use. These are the only sources available to external consumers in Phase 4.

**Tier 2, Cross-validation sources.** Sources used internally to validate Tier 1 outputs but not exposed directly to consumers. A Tier 1 price feed that deviates materially from all available Tier 2 sources triggers a hold on that session's output pending manual review.

**Tier 3, Excluded sources.** Sources that raise legal, compliance, or reliability concerns. Oracle nodes will not process sessions targeting excluded sources. Governance maintains and publishes the excluded list.

Both oracle operators and users bear legal responsibility for the data sources they access. The oracle protocol does not grant permission to access data that terms of service prohibit. Governance vetting of Tier 1 sources includes a review of the applicable terms of service and any known legal exposure. Operators are informed of this review before a source is whitelisted.

### MVP Scope

The minimum viable oracle product targets a single use case: private price threshold attestation. A prover fetches a price from a whitelisted Tier 1 source and proves to a verifier quorum that the price is above or below a specified value, without revealing the exact price or the prover's API credentials. The verifier quorum signs the boolean result. The signed attestation is delivered to the requesting contract or application.

This scope is deliberately narrow. It validates the full protocol stack, three-party handshake, two-party computation query execution, zero-knowledge proof generation, quorum signing, and output delivery, without requiring the broader context integrity and multi-source aggregation capabilities that later phases will add. Expanding the MVP to additional use cases follows after the core protocol is stable in production.

---

*This is a draft document. Parameters, emission schedules, and roadmap phases described here are the intended design. Updates to this whitepaper will be published as the network and platform evolve.*
