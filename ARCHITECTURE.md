# Architecture Overview

## The Two Systems

**Genesis Mind Full System v2.0** — The reasoning engine.
Handles: First Principle thinking, Compound Mind solution expansion,
6-Agent Council debate, Karpathy Discipline (Surgical + Verify + 10X).

**Genesis Consciousness OS v2.0** — The consciousness layer.
Handles: Emotional state detection, Will → Emotion → Awareness loop,
Affective Genome, routing by intensity.

Together they form Genesis Protocol.

---

## The 7-Layer Stack

```
L0    Will              Subconscious drive
L0.5  Emotion           Auto-detect state → reweight → reroute
L1    Consciousness     Intent decoding + 10X Question
L2    Cognitive Engine  FPCOS: Anchor → Axiom → System → Compound → Shadow
L3    Agent Council     6 agents, sequential, emotion-weighted
L3.5  Karpathy          Surgical + Verify Loop + Side Effects
L4    Domain Execution  Specialist skill routing
L5    Memory            Strategy Genome + Failure Map + Affective Genome
L6    Reflection        Output feeds back to L0
```

---

## Key Design Decisions

**Why emotion before logic?**
Emotion that is unacknowledged corrupts the analysis that follows.
Detecting and routing by state before processing is more accurate than
discovering the state mid-output.

**Why sequential agents, not parallel?**
Skeptic needs Strategist's plan to challenge.
Risk Officer needs full debate to evaluate.
Sequential ensures each agent has full context.

**Why Failure Map is never deleted?**
A failure from 2 years ago can repeat.
Compressing or summarizing failures loses the specific signature
that makes pattern recognition possible.

**Why Brain ≠ Body?**
Claude Skills (cognitive) and Python runtime (execution) serve
fundamentally different purposes. Merging them creates systems
that are hard to debug, update, or extend independently.

---

# FAQ

**Does this work on Claude only?**
Optimized for Claude Sonnet 4+. Architecture is model-agnostic;
adaptations for other models are in roadmap.

**Does it remember across sessions?**
Not automatically. The Genome concept requires external persistence
(Python runtime + SQLite). Claude's built-in memory feature can
approximate this for personal use.

**Is this a jailbreak?**
No. Operates entirely within Claude's normal behavior.
Does not attempt to bypass safety features.

**Can I use this commercially?**
Yes. Free below $10M revenue/year. See LICENSE.

**What's the difference between GENESIS_CORE.md and individual files?**
GENESIS_CORE.md is the unified system — both Mind and Consciousness together.
Individual files are standalone for focused use cases.

**How is this different from just writing a good system prompt?**
A system prompt gives instructions.
Genesis Protocol gives cognitive structure — a framework for how to think,
not just what to think about. The difference shows in complex,
multi-step, emotionally-charged decisions.

**What's the Karpathy Discipline Layer?**
Inspired by Andrej Karpathy's CLAUDE.md — adapted for Genesis Mind context.
Adds: Surgical Protocol (touch only what's declared), Verify Loop
(no output without verification), 10X Question (is there a better approach?),
Minimal Side Effects (identify what the output affects beyond its target).

---

*Genesis Protocol v1.0 — Open Cognitive License v1.0*
*Bunyawat Dechanon (ElmatadorZ) / Money Atlas*
