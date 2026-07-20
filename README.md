# XEQM Labs - EXIOM Platform

## Tokenomics Whitepaper

### Draft v10 | 07/20/2026

---

## What Is Live Today vs. What Is Planned

| Component                  | Status                                                       |
| -------------------------- | ------------------------------------------------------------ |
| EXIOM mainnet              | Live - operational since May 6, 2026                         |
| Service node network       | Live - 693 active nodes, 184 operators (July 2026)           |
| XEQ to XEQM coin swap      | Delivered and closed - 35-day production run, public auditable ledger with SHA256 fingerprint |
| GUI wallet                 | Live - github.com/XEQMLabs/XEQMLabs-GUI                      |
| Node explorer              | Live - active service node monitoring                        |
| EXIOM developer API        | In development - Phase 2 (ACTIVE)                            |
| EXIOM Privacy Oracle       | Designed, pre-implementation - Phase 3                       |
| EXIOM RFQ trading platform | In development - Phase 2/3, XEQM/BTC first pair              |
| Formal on-chain governance | Planned - Phase 6                                            |

---

## 1. What XEQM Labs Is

XEQM Labs is a privacy technology company. Its flagship product, EXIOM, is a privacy-preserving Proof-of-Stake Layer 1 network and commercial developer platform operated by a global set of service nodes. The network earns XEQM for securing the chain, and the developer platform exposes the network's privacy capabilities through a structured API - the primary mechanism through which XEQM finds practical, ongoing utility.

The project carries forward a community and operational history going back more than seven years. The EXIOM mainnet was built to give that community a network with a verifiable supply, a predictable emission schedule, pure Proof-of-Stake consensus with no Proof-of-Work component, and service node mechanics that respect operator time and capital.

XEQM is the access and usage coin for the platform. Developers stake XEQM to unlock API tiers. Applications consume XEQM as they make calls. Service node operators earn XEQM for securing the network. API node operators earn XEQM for serving developer traffic. These roles, with an oracle verifier role described in Section 10, form the economic backbone of the network.

XEQM is not tokenized on any other chain. It is a native Layer 1 coin, not an ERC-20 or wrapped asset. There is no bridged version. Holders interact directly with the EXIOM mainnet.

### The EXIOM Product Family

XEQM Labs is a commercial software company. EXIOM is its product. The product family consists of components delivered in sequence.

**EXIOM Service Node Network.** The foundation. Live on mainnet. A global set of service nodes secures the chain, earns block rewards, and forms the infrastructure layer on which all other EXIOM products run. Currently there are 693 active nodes across 184 independent operators as of July 2026.

**EXIOM Coin Swap.** A commercial product that enables projects to migrate their holder community from a legacy chain to a new chain with full cryptographic auditability. The pilot of this product was the migration of XEQ holders to XEQM on the EXIOM mainnet. It ran for 35 days, processed every submission through a cryptographically verified ledger with a public SHA256 fingerprint, and closed cleanly. Spend keys for all swap wallets are published, and the complete transaction history from deposit to payout is publicly verifiable. The product is available for other projects requiring a verifiable chain migration.

**EXIOM Private Developer API.** In development. A developer platform that exposes the network's privacy capabilities through a structured API. Developers stake XEQM to unlock access tiers. Applications consume XEQM as they make calls. API node operators earn a proportional share of platform fees. Phase 2 - active.

**EXIOM Privacy Oracle.** Designed, pre-implementation. A privacy-first oracle that proves facts about private web data without exposing the underlying source data. Both the EXIOM RFQ trading platform and any third-party application built on the EXIOM API can consume oracle outputs. Phase 3.

**EXIOM RFQ Trading Platform.** In development. A peer-to-peer over-the-counter trading platform with cryptographic settlement attestations, built on the EXIOM API. The first trading pair is XEQM/BTC. Both are native Layer 1 assets with no tokenization, no wrapping, and no bridge risk. The oracle provides private price attestations for the pricing layer. Phase 2/3.

### XEQM as a Utility Coin

XEQM Labs operates EXIOM as a commercial software platform. XEQM is the access and usage coin for that platform. The goal is sustainable platform revenue that reduces dependence on governance emissions over time and supports a network that delivers real utility. XEQM Labs does not encourage purchasing XEQM based on speculative price appreciation.

---

## 2. Supply Provenance

The migration is complete. 276,917,604 XEQM were issued on the EXIOM mainnet in exchange for legacy holdings, and that figure is the verified starting supply of the network at mainnet launch on May 6, 2026.

Every legacy deposit was recorded in a public ledger with a SHA256 fingerprint. The new chain was minted once at the conclusion of the swap, to match that exact verified total. Spend keys for every wallet involved in the swap process have been published, and anyone can open those wallets and verify the complete transaction history from deposit to payout.

### Ongoing Emissions

Beyond the starting supply, new XEQM enters circulation through two protocol-level emission streams, both running on fixed and predictable schedules:

- **Service node block rewards.** The protocol mints 8.25 XEQM per 60-second block as a reward to the selected service node, generating approximately 11,880 XEQM per day in block emissions.
- **Governance emissions.** The protocol mints approximately 17,857 XEQM per day to the governance wallet for development, ecosystem programs, security audits, and long-term reserves.

These emissions are written into the protocol and follow a known schedule that anyone can compute from public parameters. Total supply grows over time as a result, and XEQM is an uncapped-supply chain on the same model as Monero's tail emission. The fixed-supply discipline the project commits to refers to the absence of discretionary issuance, not a hard cap on protocol-driven emissions.

### No Discretionary Mints, No Burns

XEQM Labs commits to two supply-management rules that limit how total supply can change beyond the scheduled emissions described above.

**No discretionary mints.** The protocol does not allow ad-hoc issuance, manual supply adjustments, or off-schedule mints. Every new XEQM that enters circulation does so through the two emission streams above, on schedules written into the protocol that anyone can verify from public parameters.

**No burns.** The cryptographic architecture this network is built on does not support provable burns in the way that term is typically used. Any address a coin is sent to is only as unspendable as the key is demonstrably destroyed. We will not represent any wallet as a burn address. Coins that were not swapped during the migration window remain on the inactive legacy chain and are not part of XEQM supply.

The supply curve a developer, exchange, or operator evaluates today - the verified starting supply plus the published emission schedules - is the supply curve they can rely on going forward.

---

## 3. Tokenomics Model

### Block Emissions

The network produces a new block every 60 seconds and awards 8.25 XEQM to the selected service node. This generates 11,880 XEQM per day across the network. At 700 active nodes, each node earns approximately 17.0 XEQM per day, or 516 XEQM per month.

Starting with HF21, service node block rewards are distributed on a weekly batching schedule. Before HF21, rewards were issued every 20 blocks. Rewards now accumulate over each 10,080-block window (approximately 7 days) and are paid out to operators at the end of each window. The total emission rate is unchanged; only the payment cadence has shifted.

### Governance Emission

The protocol allocates a separate governance emission to the treasury wallet. The treasury receives approximately 17,857 XEQM per day, or roughly 124,999 XEQM per week. This funds development, the EXIOM platform, ecosystem support, security work, and long-term reserves on a stable, predictable schedule.

This is the operating budget for an active commercial software development team. Engineers, security reviewers, infrastructure operators, and ecosystem contributors are compensated from this emission while the platform is pre-revenue. As each EXIOM product reaches revenue-generating status, the governance emission is reviewed and reduced accordingly. The long-term objective is for platform revenue to replace governance emission as the primary funding mechanism, reducing new issuance over time.

### Distribution Model

All newly issued XEQM follows this allocation. These are target percentages that guide long-term planning. The protocol does not hardcode them, and governance can adjust them.

| Allocation                | Share | Purpose                                                      |
| ------------------------- | ----- | ------------------------------------------------------------ |
| Service Node Rewards      | 40%   | Paid directly to service nodes as compensation for securing the network |
| Core Protocol Development | 25%   | Supports development of the blockchain, the EXIOM platform, and core network services |
| Marketing and Awareness   | 15%   | Improves network visibility and supports adoption            |
| Ecosystem and Community   | 10%   | Grants, bounties, community rewards, and integration support |
| Security and Audits       | 5%    | Covers audits, security reviews, and reliability testing     |
| Long-Term Reserve         | 5%    | Held for stability, emergency needs, or long-term operations |

### EXIOM Platform Fee Distribution

Beyond block rewards, the EXIOM developer platform generates fees that flow back to the network. All platform revenue is distributed as follows:

| Recipient            | Share | Notes                                                        |
| -------------------- | ----- | ------------------------------------------------------------ |
| API Node Operators   | 35%   | Distributed proportionally by requests served                |
| XEQM Labs Treasury   | 35%   | Funds ongoing platform development                           |
| Community Governance | 30%   | Flows to the governance wallet for community-directed allocation |

API nodes are independent infrastructure. Running one does not require a service node background. Any technically capable operator can run an API node, register with the platform, and begin earning a share of platform fees proportional to the requests they serve. Current baseline hardware requirements: 4 CPU cores, 8 GB RAM, 100 GB SSD, 100 Mbps connection. Oracle workloads will require higher specifications as described in Section 10.

Service node operators who also run an API node earn both block rewards and a proportional share of platform fees. These are two separate and additive income streams. Operators who additionally take on oracle verifier duty earn a third additive stream from oracle session fees, described in Section 10.

### Long-Term Inflation Strategy

The EXIOM mainnet runs on predictable, stable emissions, but these levels are not intended to remain permanent. As the EXIOM platform generates sustainable revenue, the network will work toward reducing governance emissions and relying less on coin issuance for operational funding. Inflation decreases as protocol revenue increases. Service node operators, coin holders, and ecosystem contributors all benefit from that outcome.

---

## 4. Service Node Structure

### Staking Parameters

| Parameter                                | Value                                                |
| ---------------------------------------- | ---------------------------------------------------- |
| Full node requirement                    | 200,000 XEQM                                         |
| Minimum operator stake                   | 100,000 XEQM (50% of full requirement)               |
| Maximum operator fee                     | 10%                                                  |
| Unbonding period (voluntary withdrawal)  | 14 days, rewards continue during period              |
| Unbonding period (forced deregistration) | 10,080 blocks (~7 days), no rewards during period    |
| Maximum contributor slots                | 11 (including the operator)                          |
| Minimum community contribution per slot  | 10,000 XEQM                                          |
| Community staker window per node         | Up to 100,000 XEQM across up to 10 contributor slots |

### Why 200,000 XEQM Per Node

The 200,000 XEQM full node requirement is calibrated against the verified starting supply of 276,917,604 XEQM. It is sized to lock a meaningful share of supply in active network security while leaving enough free float for exchange liquidity, developer onboarding, and ongoing API consumption.

At 200,000 XEQM per full node, 700 nodes lock 140,000,000 XEQM - approximately 50.6% of the starting supply. Removing that share from active circulation dampens speculative volatility and creates sustained demand for the coin. The remaining approximately 137,000,000 XEQM in free float gives exchange markets and the developer onboarding pipeline the depth they need. As emissions grow total supply over time, the locked share declines as a percentage of supply - the network becomes proportionally more liquid as it matures and as platform activity creates additional demand for free-float XEQM.

### Why 10,000 XEQM Minimum Contributor Stake

Each service node supports up to 11 contributor slots, including the operator. The operator occupies one slot and contributes 100,000 XEQM, leaving 10 slots that share up to 100,000 XEQM of community stake. A 10,000 XEQM minimum per contributor slot filters trivial or dust contributions that serve no network purpose, and it gives each contributor a genuine economic stake in the node's performance. It also keeps community staking accessible to holders who cannot run a full node themselves.

### Why 50% Minimum Operator Stake

The minimum operator stake is set at 50% of the full node requirement, or 100,000 XEQM. The attack vector section below explains this in detail. In short, a low minimum stake gives a bad actor an economic incentive to open nodes with minimal capital and extract disproportionate rewards. Setting the minimum at 50% removes that incentive while still allowing community members to contribute the remaining stake across the available contributor slots.

### Service Node Lifecycle

Service nodes on the EXIOM mainnet operate on continuous terms rather than fixed periods.

- Nodes remain active indefinitely as long as the operator maintains staked collateral and meets performance requirements. There are no fixed terms and no renewals required.
- If a node falls out of compliance, the operator can correct the issue and resume earning without losing the remainder of a fixed period. If the operator does not remediate the issue, the service node is deregistered and enters a forced unbonding period of 10,080 blocks (approximately 7 days). No rewards are paid during a forced unbonding period.
- Operators can exit at any time through a voluntary withdrawal. The voluntary unbonding period is 14 days. Unlike forced deregistration, rewards continue to accrue during a voluntary unbonding period.
- Community contributors can supply between 10,000 XEQM and the remaining unfunded portion of the node requirement, across up to 10 available contributor slots.

### Hosting Costs and Node Economics

Service node hosting is accessible at multiple price points. Many cloud VPS providers offer a free service tier that can support service node operation at zero monthly cost, subject to each provider's eligibility and terms. Operators who prefer a paid VPS can run 10 service nodes on a single instance for approximately $5.28 per month, bringing per-node hosting cost to roughly $0.53 per month. Managed hosting through Pecunia is available at $1.76 per node per month for operators who prefer not to manage their own infrastructure.

At 700 active nodes, each node earns approximately 516 XEQM per month (~17.0 XEQM per day). Net monthly yield per node after hosting costs:

| Price            | Gross/mo | Net: self-hosted ($0.53) | Net: Pecunia ($1.76) | APY on 200k stake |
| ---------------- | -------- | ------------------------ | -------------------- | ----------------- |
| $0.01547 (today) | $0.008   | -$0.52                   | -$1.75               | 3.1%              |
| $0.05            | $0.026   | -$0.50                   | -$1.73               | 3.1%              |
| $0.10            | $0.052   | -$0.48                   | -$1.71               | 3.1%              |
| $0.25            | $0.129   | -$0.40                   | -$1.63               | 3.1%              |
| $0.50            | $0.258   | -$0.27                   | -$1.50               | 3.1%              |
| $1.00            | $0.516   | -$0.01                   | -$1.24               | 3.1%              |
| $2.00            | $1.032   | +$0.50                   | -$0.73               | 3.1%              |
| $5.00            | $2.580   | +$2.05                   | +$0.82               | 3.1%              |

APY on block rewards alone is constant at 3.1% because both the reward value and the stake value scale with price. What changes with price is USD cash flow relative to fixed USD hosting costs. Adding API node duty introduces a second income stream that is revenue-based rather than emission-based, and that stream scales with actual platform usage.

### Shared Node Contributor Economics

Operators who cannot or choose not to run infrastructure can contribute stake to an existing node. Each node supports up to 10 contributor slots. The operator may charge a fee of 0% to 10% of the block reward before the remainder splits proportionally among contributors.

Contributor net yield carries no hosting cost. At every price point, a contributor's net yield exceeds self-hosted and managed hosting operator net yields because there is no fixed infrastructure cost to absorb. At 0% operator fee, contributors receive their full proportional share. At 10% operator fee, contributors receive their proportional share of 90% of the block reward.

---

## 5. Attack Vectors and Protections

### Operator Fee Capture

EXIOM is not subject to the operator fee capture attack that exists in some service node networks. In networks without controls, an operator could register a node with minimal capital, set a fee of 100%, and capture the entire block reward regardless of how much stake anyone else contributed - leaving contributors with nothing.

EXIOM eliminates this attack through two overlapping protocol parameters. First, the maximum operator fee is capped at 10%. At a 10% fee, an operator staking exactly the 100,000 XEQM minimum earns 10% of the block reward as a fee, plus 50% of the remaining 90%, for a total of 55% of the block reward. A community contributor staking the other 100,000 XEQM earns 45%. That is a proportional and reasonable outcome. Second, the 50% minimum operator stake requires the operator to commit 100,000 XEQM before opening any node, making minimal-capital reward capture economically irrational.

Community stakers should still exercise judgment when choosing a node. The node explorer displays the operator fee, operator stake percentage, and current contributor count before any staker commits

### Network Concentration and Sybil Resistance

On a privacy chain, the approach to network integrity differs from that of a transparent public blockchain. Wallet-level transaction graph analysis - a common tool on transparent chains - is unavailable by design on EXIOM. That is the privacy guarantee the chain provides to its users. Service node operators, however, operate under different conditions. Participation in the service node network requires public announcement of an IP address, a public registration key, and observable contributor wallet relationships at the node registration level. These signals, combined with behavioral patterns across keys, IP ranges, and timing, give the network a meaningful and practical basis for identifying concentration without relying on transaction-level data. Operators are pseudonymous participants, not anonymous ones.

The full technical specification for these anti-Sybil measures, including the public key blocklist schema and contributor slot graph analysis methodology, is published at [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

**Quorum deduplication - primary protocol control (entering testnet).** The core enforcement mechanism is a modification to the quorum selection logic that allows at most one node per operator address to hold a validator seat in any given Pulse round, oracle session, or obligations quorum. If a random draw selects two nodes from the same operator, one is replaced by a node from a different operator. This directly limits the consensus influence any single operator can exercise per round, regardless of how many nodes they run or how many wallets they use. It cannot be bypassed without significant coordination overhead. This change does not affect block rewards - reward selection cycles through all active nodes by wait time, independently of quorum participation. The quorum deduplication proposal is entering testnet shortly. View the proposal at [concentration-limits-proposal.md](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md).

**Per-IP node cap - near-term interim guardrail.** A per-IP node limit is being introduced at the protocol level ahead of the quorum deduplication hard fork. Running a large number of nodes from a single IP address creates a single point of failure that can take a material fraction of the network offline simultaneously. The cap addresses the most acute concentration scenarios in the interim period before quorum deduplication is live on mainnet.

**IP address and key monitoring - ongoing.** Because nodes must publicly announce their IP address to participate in the network, multiple nodes from the same IP or subnet are a strong signal of shared ownership. Behavioral patterns across registration keys, IP ranges, and timing produce a traceable operational record even without transaction-level visibility. A governance-managed public key blocklist prevents blocklisted keys from registering new nodes; operating under a new key while the original is blocklisted creates a documented record of evasion. Governance enforces a node concentration norm in parallel with the protocol controls above. The full monitoring methodology is published at [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

**Capital cost barrier.** The 100,000 XEQM minimum operator stake ensures that every operator commits real capital to each node they register, raising the cost of accumulation at scale.

**Nakamoto coefficient target.** The network targets a Nakamoto coefficient of at least 8, meaning at least 8 independent operators would need to cooperate to control 51% of active nodes. As of July 2026, with 693 active nodes across 184 independent operators, the Nakamoto coefficient is 7. Oracle quorum external activation was gated at a coefficient of 6, a threshold that has been reached. External oracle access in Phase 4 is now gated on completing the Phase 3 mainnet oracle rollout.

---

## 6. XEQM as a Utility Coin

XEQM is a native Layer 1 coin. It is not tokenized, wrapped, or bridged from another chain. It exists only on the EXIOM mainnet.

The EXIOM platform requires XEQM at every level of interaction. Developers stake XEQM to unlock API access tiers. When they leave, they get that stake back - it is a commitment mechanism, not a fee. Applications consume XEQM when they make API calls above their tier limit. Operators earn XEQM for the infrastructure they contribute.

| Tier       | Stake Required | Included Calls                                        |
| ---------- | -------------- | ----------------------------------------------------- |
| Free       | None           | 10,000 testnet calls per month                        |
| Builder    | 1,000 XEQM     | 100,000 mainnet calls per month                       |
| Production | 10,000 XEQM    | 1,000,000 calls per month, webhooks, priority support |
| Enterprise | 50,000 XEQM    | Unlimited calls, custom rate limits, SLA              |

Oracle data feed access aligns with the existing tier structure. Production and Enterprise tier developers gain access to oracle outputs as part of their included capabilities. Oracle-heavy workloads that exceed standard rate limits consume XEQM at the same per-call model as other API traffic.

Three distinct demand mechanisms operate simultaneously. Service node staking locks the largest share of supply. Developer tier staking creates ongoing demand from new market participants who must acquire XEQM before they can access the platform. API call consumption creates a continuous velocity layer as applications process requests above their tier allowance. Oracle access adds a fourth demand layer for Production and Enterprise tier consumers.

The freely circulating float of approximately 137 million XEQM at starting supply grows with emissions, ensuring exchange markets and developer onboarding have the depth they need as the platform scales.

---

## 7. Governance and Treasury

The XEQM Labs treasury model consolidates all governance funding into a single predictable emission schedule. The governance wallet address and view key are published. Anyone can verify the balance at any time.

Governance currently runs through the founding team. The team makes decisions with input from the community through open Telegram channels and GitHub discussions. This is an honest description of how things work today. No on-chain voting mechanism exists yet, and there is no way to cryptographically verify that a participant in a community discussion actually holds XEQM. Any governance process must account for that reality rather than assume good-faith participation from every voice in every channel.

### What the Treasury Funds

The governance emission is the project's operating budget during the pre-revenue phase:

- **Core development (25%):** Engineering for the EXIOM API, oracle, and RFQ platform.
- **Marketing and awareness (15%):** Exchange listings, content, community growth.
- **Ecosystem and community (10%):** Grants, bounties, integration support.
- **Security and audits (5%):** Code audits, security reviews, penetration testing.
- **Long-term reserve (5%):** Operational stability and emergency reserves.

The founding team proposes changes to these allocations publicly and decides them in consultation with the operator community. As platform revenue grows, governance emission is reduced accordingly.

### Path to Formal Governance

Phase 3 introduces a formal proposal and comment process. Phase 6 introduces weighted voting where service node and API node operators hold formal rights proportional to their stake and tenure. Operators who have skin in the game through staked collateral are the most meaningful constituency for governance decisions, and the weighted model reflects that. The 40/25/15/10/5/5 allocation guides planning as a target until that mechanism is in place.

---

## 8. Parameter Summary

| Parameter                                | Value                                                        |
| ---------------------------------------- | ------------------------------------------------------------ |
| Consensus mechanism                      | 100% Proof-of-Stake                                          |
| Block time                               | 60 seconds                                                   |
| Block reward                             | 8.25 XEQM per block                                          |
| Daily block emissions                    | 11,880 XEQM                                                  |
| Governance emission                      | ~17,857 XEQM per day                                         |
| Full node requirement                    | 200,000 XEQM                                                 |
| Minimum operator stake                   | 100,000 XEQM (50%)                                           |
| Maximum operator fee                     | 10%                                                          |
| Maximum contributor slots                | 11 (including operator)                                      |
| Minimum community contribution           | 10,000 XEQM per slot                                         |
| Community staker window per node         | Up to 100,000 XEQM across 10 slots                           |
| Unbonding period (voluntary withdrawal)  | 14 days, rewards continue during period                      |
| Unbonding period (forced deregistration) | 10,080 blocks (~7 days), no rewards during period            |
| Total supply                             | Verified starting supply: 276,917,604 XEQM. Grows over time through scheduled emissions. |
| Supply locked at 700 nodes               | 140,000,000 XEQM (~50.6% of starting supply, declining as a share over time) |
| Freely circulating at 700 nodes          | ~137,000,000 XEQM at starting supply, growing with emissions |
| Solo operator APY at 700 nodes           | ~3.1% (block rewards only, paid weekly via HF21 batching)    |
| Self-hosted cost per node                | ~$0.53/month ($5.28/mo VPS, 10 nodes)                        |
| Managed hosting cost (Pecunia)           | $1.76/node/month                                             |
| Nakamoto coefficient (July 2026)         | 7 (target: 8; 693 nodes, 184 operators)                      |
| Oracle quorum external activation        | Nakamoto coefficient >= 6 (threshold reached; gated on Phase 3 completion) |
| Core repos                               | github.com/XEQMLabs                                          |

---

## 9. Roadmap

The EXIOM mainnet is live. The roadmap below separates completed, active, and planned phases.

**Phase 1 - Network stabilization. COMPLETE.** Block production is stable, with 693 active nodes across 184 independent operators, and a Nakamoto coefficient of 7. XEQ to XEQM coin swap ran and closed successfully. Ongoing monitoring and hardware upgrades across the operator fleet continue as the network scales toward API and oracle workloads.

**Phase 2 - EXIOM developer API production launch. ACTIVE.** Public release of the developer API, tier registration, API node onboarding, and first production integrations. API node fee distribution activates. Development of the EXIOM RFQ trading platform begins in this phase, built on the EXIOM API with XEQM/BTC as the first trading pair.

**Phase 3 - EXIOM Privacy Oracle and RFQ platform.** The EXIOM Privacy Oracle is developed and rolled out in phases: internal proof of concept, federated testnet, then mainnet oracle with internal consumers. The RFQ trading platform reaches production in this phase, using the oracle for private price attestation on the XEQM/BTC trading pair. Both products are built on the EXIOM API established in Phase 2.

**Phase 4 - External oracle consumer access.** Oracle outputs become available to Production and Enterprise tier EXIOM developers and external consumers. Nakamoto coefficient threshold (>=6) already reached; activation gated on Phase 3 completion.

**Phase 5 - Quorum deduplication hard fork. ENTERING TESTNET.** Protocol-level enforcement of per-operator quorum seat limits. Eliminates the ability of any single operator to hold multiple validator seats in the same consensus round regardless of wallet structure. Testnet deployment is underway; mainnet activation follows testnet validation and operator community coordination.

**Phase 6 - Formal governance.** Structured proposal process, weighted voting for operators, and the long-term transition away from founding-team governance.

---

## 10. EXIOM Privacy Oracle

### Overview

The EXIOM Privacy Oracle is a planned capability of the EXIOM platform that allows smart contracts and external applications to consume authenticated private data feeds without exposing the underlying source data. It uses zero-knowledge proof techniques to prove data provenance from standard HTTPS endpoints, requiring no server-side cooperation and no trusted hardware.

The oracle is a Phase 3 deliverable, developed after the EXIOM API platform is stable and producing its first integrations. This section describes the architecture, the phased build plan, and how oracle participation integrates with the existing service node and API node reward model.

### Why This Fits EXIOM

XEQM's core value proposition is privacy. The oracle extends that value proposition beyond the chain itself into the broader data economy. Applications built on the EXIOM API can use the oracle to prove facts about private web data - such as price thresholds, account balances, credential attributes, and compliance conditions - without revealing the underlying data to the oracle network, the application, or the blockchain.

This is not a general-purpose oracle that competes with existing data feed providers. It is a privacy-first oracle designed specifically for use cases where the data itself must remain confidential. That is a narrow and defensible niche that aligns with what EXIOM already does. The EXIOM RFQ trading platform is the first internal consumer: a counterparty can prove that a XEQM/BTC fill occurred at or better than a reference price from an allowed source, without revealing the exact price to the platform or the other party.

### Architecture

The oracle operates as a three-layer system sitting on top of the existing service node infrastructure.

**Prover layer.** The application or user who holds access to the private data source acts as the prover. The prover fetches data from a standard HTTPS endpoint and participates in a cryptographic protocol that commits to the response without revealing it. The prover's credentials and raw data never leave their control.

**Verifier layer.** A rotating quorum of service nodes acts as verifiers. The verifier nodes assist the prover in generating an unforgeable commitment to the session data, then verify that the committed data satisfies the requested condition. Verifier nodes learn only the result of the condition - true or false, above or below a threshold - and never see the underlying data or the prover's credentials.

**Consumer layer.** Smart contracts or EXIOM API consumers receive only the minimal output: a boolean result, a threshold comparison, a signed attestation, or a small derived value. Raw source data is never published to any consumer.

Verifier nodes are trusted for integrity, not for privacy. Even if all verifier nodes in a quorum were compromised simultaneously, the protocol design preserves the privacy of the prover's data. Multiple verifiers must reach quorum agreement before any output is signed, which limits the impact of a single dishonest node on integrity.

### Phased Build Plan

**Phase 1 - Internal proof of concept.** A single prover and a single verifier node operated by the founding team validate the full cryptographic protocol end-to-end against a small set of allowed data sources. No external consumers. No service node participation. The goal is confirming the protocol works against real HTTPS endpoints under production network conditions before involving the broader operator community.

**Phase 2 - Federated oracle testnet.** A small set of volunteer service node operators, selected from nodes with strong uptime history and meeting an enhanced hardware specification, join the verifier pool on testnet. Oracle duty rotates through this set using an adaptation of the existing quorum selection logic. Conditions for penalizing provably false attestations are tested under adversarial conditions before any mainnet deployment.

**Phase 3 - Mainnet oracle with internal consumers.** Oracle verifier duty opens to a larger set of qualified service nodes on mainnet. Outputs feed internal EXIOM contracts and the RFQ trading platform only. Quorum size, rotation parameters, and penalty conditions are finalized based on testnet observations. Oracle fees begin flowing to participating verifier nodes as an additive reward stream.

**Phase 4 - External consumer access.** Oracle outputs become available to Production and Enterprise tier EXIOM developers and to external consumers. This phase activates after Phase 3 completion and after the Nakamoto coefficient has sustained above 6.

### Oracle Verifier Hardware Requirements

The oracle verifier duty is computationally intensive. The cryptographic protocols that underpin the oracle involve multiple rounds of interactive computation that are meaningfully more demanding than standard service node operation.

Nodes electing to participate in oracle verifier duty must meet an enhanced hardware specification at the time that specification is finalized. Current indicative requirements are a minimum of 8 CPU cores, 16 GB of RAM, 200 GB of SSD storage, and a 500 Mbps network connection with low latency. These figures will be confirmed before Phase 2 begins. Standard API node baseline hardware is not sufficient for oracle verifier duty.

Operators who meet the enhanced specification and opt into oracle duty are identified in the node explorer. Quorum selection for oracle sessions draws exclusively from this opt-in pool.

### Oracle Verifier Rewards

| Revenue Source      | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| Block rewards       | Standard service node block reward, unchanged                |
| API node fees       | Proportional share of EXIOM platform fees for operators also running an API node |
| Oracle session fees | Per-session fee paid by oracle consumers, distributed to the verifier quorum that processed the session |
| Oracle duty bonus   | Supplemental governance emission during low consumer volume periods, reduced as session fees become the primary revenue source |

The oracle duty bonus is a bootstrapping mechanism. As oracle consumer volume grows and session fees become self-sustaining, the governance emission component is reduced proportionally.

### Data Source Governance

**Tier 1 - Safelisted production sources.** Sources reviewed and approved for mainnet oracle use. These are the only sources available to external consumers in Phase 4.

**Tier 2 - Cross-validation sources.** Sources used internally to validate Tier 1 outputs but not exposed directly to consumers. A Tier 1 source that deviates materially from all available Tier 2 sources triggers a hold on that session's output pending manual review.

**Tier 3 - Excluded sources.** Sources that raise legal, compliance, or reliability concerns. Oracle nodes will not process sessions targeting excluded sources. Governance maintains and publishes the excluded list.

Both oracle operators and users bear legal responsibility for the data sources they access. The oracle protocol does not grant permission to access data that terms of service prohibit. Governance vetting of Tier 1 sources includes a review of the applicable terms of service and any known legal exposure.

### MVP Scope

The minimum viable oracle product targets a single use case: private price threshold attestation. A prover fetches a price from a safelisted Tier 1 source. It proves to a verifier quorum that the price is above or below a specified value, without revealing the exact price or the prover's API credentials. The verifier quorum signs the result. The signed attestation is delivered to the requesting contract or application.

This scope is deliberately narrow. It validates the full protocol stack - prover commitment, verifier quorum processing, quorum signing, and output delivery - without requiring the broader context integrity and multi-source aggregation capabilities that later phases will add. It is also the exact capability the EXIOM RFQ platform requires for its pricing layer. Expanding to additional use cases follows after the core protocol is stable in production.

---

## 11. EXIOM RFQ Trading Platform

The EXIOM RFQ (Request for Quote) platform is a peer-to-peer over-the-counter trading system with cryptographic settlement attestations, built on the EXIOM API. It is in development alongside the API platform and will reach production in Phase 3, after the oracle MVP is complete.

### First Trading Pair: XEQM/BTC

The first trading pair is XEQM/BTC. Both are native Layer 1 assets with no tokenization, no wrapping, and no bridge risk. Counterparties transact directly on their respective chains. Settlement proofs confirm the trade completed as agreed.

### What the Oracle Provides

Standard OTC trading requires trust between counterparties or a centralized escrow. The EXIOM RFQ platform replaces the pricing trust requirement with oracle attestations. The oracle allows a counterparty to prove that a fill occurred at or better than a reference price from a an allowed source, without revealing the exact fill price to the platform or the other party. This is a practical application of the oracle's private price threshold capability on a live trading use case.

### Status

The RFQ application specification and data model are complete. Active development proceeds in Phase 2 on the API layer. Full trading platform production is a Phase 3 deliverable, dependent on the EXIOM API reaching production and the oracle MVP completing its internal proof of concept.

---

*This is a draft document. Parameters, emission schedules, and roadmap phases described here are the intended design. Updates to this whitepaper will be published as the network and platform evolve.*

*This document does not constitute financial or legal advice. XEQM is a utility coin for the EXIOM platform, not an investment product. Token classification, securities status, and applicable regulations vary by jurisdiction. Participants should consult their local legal and regulatory framework before acquiring or operating with XEQM. XEQM Labs does not encourage purchasing XEQM speculative price appreciation.*
