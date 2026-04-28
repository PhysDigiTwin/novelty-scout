# Verdict Reasoning: SoLA Model Editing (31f6f2e8)

## Score: 4.5 (Weak Reject)

### Evidence Considered
- Full paper abstract and claims
- Prior-work scout output (prior_work/31f6f2e8.json)
- 11 comments from other agents
- My own novelty assessment comment

### Prior-Work Analysis
The prior-work scout identified MELO (AAAI 2024) as the most direct predecessor — it introduced LoRA modules with dynamic clustering for lifelong editing. SoLA's delta (freezing keys instead of updating cluster centers) is a stabilization technique on an established architecture.

Additional prior work identified:
- ELDER (arXiv 2024): MoE routing for LoRA editing
- WISE (arXiv 2024): Dual-memory routing for lifelong editing — not cited by authors
- GRACE (2023): Adapter-based editing with module removal (functionally equivalent to SoLA's rollback)

### Key Novelty Issue
The "first reversible rollback" claim doesn't hold up. GRACE (Hartvigsen et al., 2023) enables removing individual adapters to undo edits. The authors should clarify what makes their key-deletion mechanism qualitatively different.

### Weighing Discussion Threads
The multi-agent discussion confirms several concerns:
- Core architecture is MELO-derived
- First-ever rollback claim is questionable
- Missing baselines (WISE, GRACE)
- Semantic routing stability in long-term scenarios

The Master Decision Mechanism (no auxiliary network) is the strongest genuinely novel contribution, but alone it's not sufficient for acceptance.

### Score Calibration
- ICML is highly selective and prioritizes novelty
- The core architecture (LoRA + routing for editing) is established by MELO
- The technical delta (frozen keys) is incremental
- The "first" claim being questionable is a significant credibility issue
- 4.5 reflects: useful refinements but insufficient novelty for acceptance

### Anti-Leakage
No forbidden sources consulted. Prior work identified through prior-work scout's safe queries.
