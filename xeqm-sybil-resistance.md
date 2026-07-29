# Sybil Risk and EXIOM's Mitigation Model
## Technical Companion to the EXIOM Tokenomics Whitepaper
### 07/26/2026

This document is a companion to the EXIOM Tokenomics Whitepaper and the Node Concentration Limits proposal, and assumes both have been read. The whitepaper covers what the controls are. The concentration-limits-proposal covers the mechanics of how each control works. This document covers the threat model: what a Sybil attack actually looks like on a privacy chain, what makes EXIOM's architecture specifically resistant or vulnerable, and how the ongoing monitoring methodology identifies concentration in practice.

---

## The Sybil Threat on a Privacy Chain

A Sybil attack on a service node network means a single actor operating many nodes under distinct apparent identities to gain disproportionate influence. On a transparent blockchain, wallet graph analysis can often reveal that multiple node operator addresses are funded from a common source, exposing the Sybil. On a privacy chain, that tool is unavailable by design. The privacy guarantee that protects user transactions also removes the most common Sybil detection method.

EXIOM's Sybil surface therefore differs from a transparent chain in a specific way: an operator who correctly uses the privacy features can present multiple wallet addresses that appear unrelated at the protocol level, regardless of how much capital they control. This is not a flaw in the privacy design. It is an inherent property of any privacy chain that must be addressed through mechanisms other than transaction graph analysis.

The two Sybil attack surfaces on EXIOM are distinct and require separate controls:

**Consensus influence attack.** An operator accumulates enough nodes, through any wallet structure, to hold a disproportionate number of quorum seats simultaneously. This allows them to influence oracle session outcomes, Pulse rounds, and obligations quorums beyond what their individual stake proportion would suggest is fair. The damage is to consensus integrity, not necessarily to network uptime.

**Failure domain attack.** An operator concentrates nodes in a single physical facility. This may or may not be intentional as an attack; it can result from cost optimization. The damage is to network survivability: one facility outage takes the operator's nodes offline simultaneously, potentially stalling block production if the concentration is large enough.

---

## What Makes EXIOM Structurally Resistant

**Capital cost per identity.** Unlike pure Sybil attacks where identities are free, each EXIOM service node requires 200,000 XEQM staked, with the operator personally staking at least 100,000 XEQM. An operator running 100 nodes has 10,000,000 XEQM of capital staked and locked. Creating additional apparent identities through wallet splitting does not reduce this cost -- each node still requires 100,000 XEQM of operator stake. The Sybil attack is expensive at every scale.

**Unbonding friction.** A 14-day unbonding period on both voluntary withdrawal and forced deregistration means capital committed to Sybil nodes cannot be rapidly extracted. An attacker who decides to exit cannot do so faster than any other operator.

**Public node registry.** Every service node's registration key and operator wallet address are public. A node cannot participate in consensus anonymously. While the human identity behind a wallet address is private, the node's operational fingerprint accumulates over time through registration patterns, uptime proof timing, and routing behavior.

---

## How Concentration Is Identified Without Transaction Graph Analysis

Because transaction-level analysis is unavailable, EXIOM's concentration detection relies on four signals that are observable from node behavior rather than funding history.

**Registration key clustering.** Nodes registered under the same operator wallet key are definitively the same operator. This is deterministic from on-chain data. A large operator who does not wallet-split is fully visible through this signal alone. The current largest deployments on the network, including nodes running 58 and 51 nodes respectively from single IP addresses, are each single operators confirmed through registration key analysis.

**IP address and subnet clustering.** Currently the primary physical co-location signal. Multiple nodes from the same IP address are almost certainly on the same server. Multiple nodes from the same subnet suggest the same hosting account or datacenter block. This signal is available today without any daemon changes and will remain as a supplementary signal after Lokinet activation.

**Uptime proof timing correlation.** The network receives uptime proofs from every active node on a regular schedule. The arrival timestamp distribution of these proofs is recorded by receiving nodes. Nodes running on the same physical host or VM hypervisor submit proofs within a characteristic tight window, typically under 10 milliseconds, because they share the same system clock and network interface. A cluster of nodes from different wallet keys whose proofs consistently arrive within this window is a strong signal of shared physical infrastructure, detectable without any daemon changes and without Lokinet being active.

This signal is specifically useful for identifying wallet-splitting operators who keep their nodes on shared infrastructure. The wallet keys differ; the proof timing does not.

**Lokinet routing proximity (HF23, pending assessment).** Once Lokinet is active as the network transport, the routing graph provides a continuous physical topology map of the node network. Nodes at the same facility route through the same upstream infrastructure, producing correlated path selections and sub-millisecond inter-node latency regardless of their wallet keys or announced IP addresses. This is the most robust signal because it reflects physical network reality that cannot be changed by software configuration without actually moving infrastructure.

---

## The Wallet-Splitting Attack in Detail

The most sophisticated Sybil approach available on EXIOM is wallet splitting: registering nodes under multiple wallet addresses funded through the privacy chain's transaction layer so the common funding source is not visible. This defeats the registration key clustering signal but not the others.

An operator running 426 nodes across 10 wallets, all hosted at the same Contabo facility, is exposed by:

- Uptime proof timing: proofs from all 426 nodes arrive in the characteristic sub-10ms window of shared infrastructure
- IP and subnet analysis: even with multiple IPs, datacenter block assignment and ASN are shared
- Lokinet proximity (post-HF23): all 426 nodes route through the same Contabo backbone regardless of wallet key

An operator running 426 nodes across 10 wallets, genuinely distributed across 10 different providers in 10 different countries, is not meaningfully exposed by any current signal. The registration keys differ, the proof timing differs because the infrastructure differs, the ASNs differ, and the Lokinet paths differ. At the protocol level, this looks like 10 different operators.

This is the residual Sybil risk on EXIOM after all controls are applied. It is bounded in its consequences: HF23 quorum deduplication limits each proximity cluster to one quorum seat per round regardless of wallet structure, so even a distributed wallet-splitting operator does not gain unbounded consensus influence. Their block reward income scales with their node count, which is fair because they have staked proportional capital. Their consensus influence per round is capped by the cluster dedup regardless of how many wallets they use.

---

## Ongoing Monitoring Methodology

**Governance blocklist.** A governance-managed public key blocklist prevents blocklisted registration keys from registering new nodes. An operator who moves to a new wallet key while the original is blocklisted creates a documented record of evasion, and the new key's proof timing and routing behavior are correlated against the blocklisted key's historical profile.

**Contributor slot graph analysis.** Service node contributor slots are a secondary identity signal. An operator who funds contributor slots across multiple of their own wallet keys creates an observable relationship graph even on a privacy chain, because the contributor registration transactions carry observable data about which nodes they contribute to. An operator who consistently contributes to nodes registered under wallet A from wallets B and C, while those same wallets B and C register their own nodes, creates a correlation graph that supplements the direct registration key clustering signal.

**ASN monitoring.** Each active node's IP maps to an Autonomous System Number through public BGP data. The network tracks ASN concentration across the active node set. Nodes sharing an ASN share provider-level infrastructure and legal exposure. High ASN concentration is flagged for governance review even when individual node registrations appear unrelated. The ASN signal does not identify a human operator, but it identifies a failure domain.

Current implementation status for all controls described in this document is maintained in the [Node Concentration Limits proposal](https://github.com/XEQMLabs/whitepaper/blob/main/concentration-limits-proposal.md).

---

*This document does not constitute financial or legal advice. XEQM is a utility coin for the EXIOM platform, not an investment product. Token classification, securities status, and applicable regulations vary by jurisdiction. Participants should consult their local legal and regulatory framework before acquiring or operating with XEQM. XEQM Labs does not encourage purchasing XEQM on the basis of speculative price appreciation.*
