# Node Concentration Limits — Options and Proposal

As the network has grown to 762 active nodes across 185 operators, two operators now exceed our current voluntary governance cap of ~50 nodes. This has been a topic of discussion in the Telegram Node Operators channel. This is a good time to have a conversation with the full operator community about how we want to handle concentration limits as we advance, because the right answer involves a protocol change and I want operator input before I build it.

The network's Nakamoto coefficient — the number of independent operators who would need to cooperate to control 51% of active nodes — is currently 7, an improvement from 4 when I originally wrote the white paper. Our target is 8. A single operator controlling 14% of nodes is a meaningful concentration of consensus influence, independent of whether their intentions are good. The protocol should not require trusting any single operator.

A node cap cannot be perfectly enforced in code on a pseudonymous chain. An operator using multiple wallets, different IP addresses, and multiple hosting providers is essentially undetectable at the protocol level. Any comments stating otherwise are not being honest with you. To address this, I see three options:

---

## 1) Keep the voluntary cap as-is

The current governance cap of ~50 nodes per operator is enforced through public monitoring, community pressure, and a governance blocklist. When I identify a violation, assuming I know who the operator is, I contact them, and operators who do not comply face public identification and blocklisting of their registration keys.

**Advantage:** No hard fork or code changes are required.

**Disadvantage:** A bad actor who deliberately obscures their identity across multiple wallets faces no protocol-level resistance. The cap is only as strong as my ability to identify operators, which is a heuristic process. It is also only as strong as my willingness to enforce it.

---

## 2) Per-wallet registration cap enforced in the protocol

The registration code is changed to reject any new node registration from an operator address that already controls N or more active nodes. The network itself enforces the limit; no governance action or manual monitoring is needed to stop a single-wallet operator from exceeding it.

This eliminates the need to monitor and intervene in the common case: an honest large operator using a single wallet is automatically stopped at the cap. It also means that even if a bad actor splits across multiple wallets, each wallet is still bounded, which reduces the maximum influence any single wallet can accumulate before it becomes detectable.

It does not stop a motivated actor willing to use multiple wallets. A second wallet with a fresh operator address faces the same cap from zero, with no connection to the first in the protocol's view. The cap is therefore a ceiling on single-wallet accumulation, not a ceiling on total operator accumulation.

Hitting the cap exactly is not evidence of wallet splitting; honest operators respecting the limit will also hit it. The useful detection signal is two separate operator addresses sharing the same IP address or subnet. Nodes must publicly announce their IP to participate in the network, so shared infrastructure across wallets is an operational fact rather than a coincidence. IP correlation combined with the per-wallet cap gives investigators a concrete, specific basis for follow-up rather than a guess.

**Advantage:** Automatically enforces the cap against single-wallet operators without governance involvement. Bounds per-wallet accumulation even for actors who split, limiting the damage any one wallet can do before it surfaces in monitoring.

**Disadvantage:** Does not protect against a determined actor willing to manage multiple wallets and use distinct infrastructure for each. Offers a false sense of security if treated as a complete solution. The cap number also requires careful calibration; set it too low and professional operators running legitimate large infrastructure hit it before any bad actor does; set it too high and it rarely triggers.

---

## 3) Quorum deduplication

The quorum selection logic is modified so that in any given Pulse round, oracle session, or obligations quorum, at most one node per operator address may hold a validator seat. If a random draw selects two nodes from the same operator, one is replaced with a node from a different operator.

**Advantage:** This limits the influence an operator can exercise in any single consensus round, regardless of how many nodes they run or how many wallets they use across their own addresses. An operator with 100 nodes and 100 separate wallets still only gets one validator seat per quorum. It cannot be bypassed without significant coordination overhead, and even then the effect is bounded by quorum size.

It does not affect rewards. Block rewards are assigned by a separate mechanism — the protocol selects the next reward recipient based on which active node has waited the longest since its last reward, cycling through all active nodes in turn. That selection is completely independent of quorum participation. An operator with 100 nodes still earns block rewards proportional to those 100 nodes at the same rate as before. Quorum deduplication only caps simultaneous consensus influence, not income.

**Disadvantage:** This is a protocol change requiring a hard fork. It takes time to build, test on testnet, and coordinate activation with the operator community.

---

## My proposal

I propose we implement and enforce all three layers:

1. Keep the voluntary governance cap and blocklist enforcement, which remains the fastest tool when I identify a node operator over the governance cap.
2. Add a per-wallet registration cap as a protocol floor. It is not a hard barrier, but it bounds single-wallet accumulation automatically and removes the need for manual intervention in the common case.
3. Build quorum deduplication at 1 seat per operator, test it on testnet, and activate it via hard fork.

The hard fork is the right long-term answer for the network. I need to build it carefully, run it on testnet against adversarial conditions, finalize parameters, and communicate a timeline to the operator community before activation.

I want your feedback on this proposal. Please respond in the operator channel.
