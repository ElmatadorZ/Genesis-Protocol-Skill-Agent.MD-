# Frequently Asked Questions

**Does this work on Claude only?**
Optimized for Claude Sonnet 4+. Architecture is model-agnostic — adaptations for GPT-4o and Gemini are in roadmap.

**Does it remember across sessions?**
Not automatically. The Genome requires external persistence (Python runtime + SQLite). Claude's built-in memory feature approximates this for personal use.

**Is this a jailbreak?**
No. Operates within Claude's normal behavior. Does not bypass safety features.

**Can I use this commercially?**
Yes. Free below $10M revenue/year. See LICENSE.

**What's the difference between GENESIS_CORE.md and individual files?**
GENESIS_CORE.md is the unified system. Individual files are standalone for focused use cases.

**How is this different from a good system prompt?**
A system prompt gives instructions. Genesis Protocol gives cognitive structure — how to think, not just what to think about.

**What's the Karpathy Discipline Layer?**
Inspired by Andrej Karpathy's CLAUDE.md. Adds: Surgical Protocol, Verify Loop, 10X Question, Minimal Side Effects. See `wiki/06-karpathy-discipline.md`.

**What's the Affective Genome?**
Memory of decisions made under high emotional charge (intensity ≥7). Builds pattern recognition: "FEAR + trading → tend to over-hedge".

**Can I build my own version?**
Yes. See `docs/HOW_TO_BUILD_YOUR_OWN.md`. The architecture is a framework, not a personality.
