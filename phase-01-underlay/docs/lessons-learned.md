# Lessons Learned — Phase 1

## 1. Build and verify the underlay before the overlay

The later SD-WAN phases depend on stable transport reachability. Phase 1 therefore treats Internet/MPLS connectivity as a prerequisite, not a side task.

## 2. Adjacency is evidence

Entering OSPF or MPLS commands is not enough. The useful evidence is:

- OSPF `FULL`,
- LDP `Oper`,
- MPLS interfaces operational,
- labels present in the forwarding table.

## 3. Dependencies matter

The PE and early core configuration must be stable before the far side of the MPLS backbone can be validated.

## 4. Keep historical snapshots

Because the same lab continues evolving across many phases, a later `show running-config` no longer represents an earlier milestone.

For future phases, milestone snapshots should be exported at the end of each phase.

## 5. Separate raw evidence from portfolio documentation

A public engineering repository should explain what was implemented and provide reproducible configuration, while also being explicit when a configuration was reconstructed rather than captured at that exact historical moment.
