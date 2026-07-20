# Node Concentration Limits - Proposal and Implementation Status

As the network has grown to 693 active nodes across 184 operators, concentration of service nodes among a small number of operators has been an ongoing topic of discussion in the Telegram Node Operators channel. This document describes the problem, the options considered, the approach we have chosen, and the current implementation status of each layer.

The network's Nakamoto coefficient - the number of independent operators who would need to cooperate to control 51% of active nodes - is currently 7, up from 4 at initial mainnet launch. Our target is 8. A single operator controlling 10% or more of active nodes is a meaningful concentration of consensus influence, independent of whether their intentions are good. The protocol should not require trusting any single operator.

A node cap cannot be perfectly enforced in code on a pseudonymous network. An operator using multiple wallets, different IP addresses, and multiple hosting providers is difficult to detect at the protocol level. Any claim otherwise is not being honest with you. This is why the approach described here is layered: no single control is sufficient on its own, but together they raise the cost and complexity of evasion to the point where it becomes impractical for most actors and detectable for determined ones.

---

## The Problem

On a privacy chain, the tools available for identifying operator concentration differ from those on a transparent public blockchain. Transaction-level graph analysis is unavailable by design - that is the privacy guarantee the chain provides to users. Service node operators, however, operate under different conditions. Participation in the service node network requires public announcement of an IP address, a public registration key, and observable contributor wallet relationships at the node registration level.

These signals - IP address, subnet, registration key patterns, contributor wallet relationships, and behavioral timing across registrations - give the network a practical basis for identifying concentration without relying on transaction-level data. Operators are pseudonymous participants, not anonymous ones. An operator running many nodes from shared infrastructure has a visible footprint.

The full monitoring methodology and blocklist schema are published at [XEQMLabs/xeqm-sybil-resistance](https://github.com/XEQMLabs/xeqm-sybil-resistance).

---

## Options Considered

### Option 1 - Voluntary governance cap only

The current governance cap of approximately 50 nodes per operator is enforced through public monitoring, community pressure, and a governance blocklist. When a violation is identified, the operator is contacted and given the opportunity to voluntarily reduce. Operators who do not comply face public identification and blocklisting of their registration keys.

**Advantage:** No hard fork or code changes required.

**Disadvantage:** A bad actor who deliberately obscures their identity across multiple wallets and providers faces no protocol-level resistance. Enforcement depends on the team's ability to identify operators, which is a heuristic process.

### Option 2 - Per-wallet registration cap enforced in the protocol

The registration code is changed to reject any new node registration from an operator address that already controls N or more active nodes. The network itself enforces the limit for single-wallet operators without governance action.

**Advantage:** Automatically enforces a ceiling on single-wallet accumulation. Removes the need for manual intervention in the common case.

**Disadvantage:** Does not stop a motivated actor willing to manage multiple wallets with distinct infrastructure. Offers a false sense of security if treated as a complete solution. The cap number requires careful calibration.

After further analysis, this option has been superseded by quorum deduplication as the primary protocol control. Quorum deduplication addresses the same single-wallet concentration problem with broader coverage and cannot be bypassed by wallet splitting. The per-wallet cap is therefore not being implemented as a separate layer.

### Option 3 - Quorum deduplication

The quorum selection logic is modified so that in any given Pulse round, oracle session, or obligations quorum, at most one node per operator address may hold a validator seat. If a random draw selects two nodes from the same operator, one is replaced with a node from a different operator.

This directly limits the consensus influence any single operator can exercise per round, regardless of how many nodes they run or how many wallets they use. An operator with 100 nodes across 100 separate wallets still holds only one validator seat per quorum. It cannot be bypassed without significant coordination overhead, and even then the effect is bounded by quorum size.

This change does not affect block rewards. Reward selection cycles through all active nodes by wait time, independently of quorum participation. An operator with more nodes still earns block rewards proportional to those nodes. Quorum deduplication caps simultaneous consensus influence, not income.

**Disadvantage:** This is a protocol change requiring a hard fork. It requires careful implementation, adversarial testnet validation, and coordinated activation with the operator community.

---

## The Chosen Approach

We implement two active layers and retire the per-wallet cap option as redundant.

### Layer 1 - Per-IP node cap (near-term, protocol-enforced)

A per-IP node limit is being introduced at the protocol level as an immediate interim guardrail. Running a large number of nodes from a single IP address creates a single point of failure that can take a material fraction of the network offline simultaneously - not just a concentration of consensus influence, but a single infrastructure event that can drop many nodes at once.

The per-IP cap removes the most acute risk in the current network while the quorum deduplication hard fork is built and tested. This is an interim measure, not the primary long-term control.

### Layer 2 - Quorum deduplication (primary protocol control, entering testnet)

Quorum deduplication is the primary and definitive protocol-level control. The quorum selection logic is modified to allow at most one node per operator address to hold a validator seat in any given Pulse round, oracle session, or obligations quorum.

This is entering testnet shortly. The testnet phase will validate the selection logic under normal and adversarial conditions, confirm that reward assignment is fully independent of quorum participation, and finalize activation parameters before the hard fork is proposed to the mainnet operator community.

### Layer 3 - Governance monitoring and blocklist (ongoing)

IP address monitoring, registration key pattern analysis, contributor slot graph analysis, and the governance blocklist remain active in parallel with the protocol controls. The governance cap of approximately 50 nodes per identifiable operator is enforced through this layer.

A governance-managed public key blocklist prevents blocklisted keys from registering new nodes. Operating under a new key while the original is blocklisted creates a documented record of evasion and triggers escalating monitoring of the new key's associated infrastructure.

This layer remains the fastest tool when concentration is identified before the protocol controls catch it, and it provides the human judgment layer that protocol code cannot replicate for cases involving deliberate obfuscation across providers.

---

## Current Status

| Control | Status |
|---|---|
| Voluntary governance cap (~50 nodes per operator) | Active - enforced through monitoring and blocklist |
| Per-IP node cap | Implementation in progress - protocol-enforced, near-term |
| Per-wallet registration cap | Not proceeding - superseded by quorum deduplication |
| Quorum deduplication hard fork | Entering testnet - mainnet activation follows testnet validation |

---

## What This Does Not Solve

No combination of controls prevents a well-resourced, patient actor from accumulating nodes across many wallets and fully independent infrastructure at different providers with non-overlapping IP ranges. The protocol cannot distinguish that operator from 100 independent operators at the protocol level alone.

What the combined approach does is raise the cost and operational complexity of large-scale evasion, eliminate the most common and careless forms of concentration, and ensure that even a sophisticated actor cannot convert that accumulation into disproportionate consensus influence in any single round. That is a realistic and honest goal for a pseudonymous network.

Operators with feedback on the quorum deduplication proposal or the per-IP cap parameters are encouraged to respond in the Node Operators Telegram channel or open an issue in this repository.
