# LaneTrace conflict engine

Explain declared Soroban footprint dependencies. For each pair, an edge exists when one transaction's read-write set overlaps the other's read-only or read-write set. Shared reads are independent. Every edge retains its exact key identity and access-mode reason.

The engine finds connected components, then greedily assigns whole components to 1–16 illustrative clusters, balancing declared instruction resources. Conflicting pairs never land in separate clusters within the one illustrated stage. Independent components may share a cluster when the chosen lane count is small. A connected component is not a minimum sequential stage count: other stage decompositions may permit different schedules.

This is an educational single-stage model, not a protocol transaction-set builder or validator profiler. It does not implement hash ordering, source-account sequence constraints, fee processing, admission limits, instruction-budget validation or actual network cluster configuration. Resource sums are not latency measurements or throughput estimates.

`analyze(trace,{lanes,selectedIds})` validates version/network, unique transaction IDs, complete bounded access sets, disjoint access roles, integer instruction resources and ledger context. Old observations are visibly STALE_RECAPTURE. Input hashes identify exact JSON serialization. Testnet trace labels claim simulations only. Uploaded evidence is not independently authenticated.

Run `node --test test.mjs` with the sibling fixtures repository. Eighteen tests cover reads, writers, transitive components, cluster independence, resource arithmetic, stale and malformed input.

## Protocol reference

[CAP-0063](https://github.com/stellar/stellar-protocol/blob/master/core/cap-0063.md) defines the footprint conflict rule and staged cluster semantics. LaneTrace implements the declared-key conflict rule and an illustrative clustering model only.
