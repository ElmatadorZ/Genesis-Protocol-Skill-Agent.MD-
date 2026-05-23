---
name: genesis-genome-spec
version: "1.0"
author: "Bunyawat Dechanon (ElmatadorZ)"
---

# GENOME SPEC v1.0
## Memory + Compound Learning Architecture

Genesis Protocol has three memory systems that serve different purposes.
None of them reset between sessions if properly persisted.

---

## MEMORY ARCHITECTURE

```
╔══════════════════════════════════════╗
║         GENESIS GENOME v1.0          ║
╠══════════════════════════════════════╣
║                                      ║
║  STRATEGY GENOME                     ║
║  What works → reinforce              ║
║  Decay if unused (0.02/session)      ║
║                                      ║
║  FAILURE MAP                         ║
║  What fails → NEVER DELETE           ║
║  Failure signature library           ║
║                                      ║
║  AFFECTIVE GENOME                    ║
║  High-charge decisions (intensity≥7) ║
║  Pattern recognition over time       ║
║                                      ║
╚══════════════════════════════════════╝
```

---

## STRATEGY GENOME SCHEMA

```json
{
  "strategy_genome": {
    "version": "1.0",
    "owner": "ElmatadorZ",
    "rules": [
      {
        "id": "rule_001",
        "content": "When FEAR detected in trading context, Risk Officer output first",
        "weight": 0.85,
        "decay_rate": 0.02,
        "reinforcement_count": 12,
        "source_session": "session_uuid",
        "domain": "trading",
        "created": "2026-01-15T10:30:00Z",
        "last_used": "2026-05-20T14:22:00Z"
      }
    ]
  }
}
```

**Reinforcement rules:**
- Success outcome → weight += 0.05 (max 1.0)
- Failure outcome → weight -= 0.10
- No use for 30 sessions → weight -= 0.02/session
- weight < 0.20 → flag for review
- weight < 0.10 → archive (never delete)

---

## FAILURE MAP SCHEMA

```json
{
  "failure_map": {
    "entries": [
      {
        "id": "SIG-001",
        "name": "Claude Code WSL2 Startup Failure",
        "symptom": "Failed to start workspace error on Windows",
        "root_cause": "Hyper-V memory reservation conflicts with WSL2",
        "fix_steps": [
          "Verify Hyper-V enabled in Windows features",
          "Run: wsl --shutdown",
          "Restart WSL2",
          "Retry Claude Code"
        ],
        "verify": "claude --version in WSL2 terminal",
        "first_seen": "2026-03-10",
        "recurrence_count": 2,
        "resolved": true,
        "domain": "system",
        "tags": ["windows", "wsl2", "claude-code", "startup"]
      }
    ]
  }
}
```

**Failure Map laws:**
- NEVER delete any entry
- NEVER merge entries that seem similar — they may differ in root cause
- Add recurrence_count when same failure repeats
- High recurrence → escalate to prompt-architect-os for systemic fix

---

## AFFECTIVE GENOME SCHEMA

```json
{
  "affective_genome": {
    "entries": [
      {
        "id": "AGE-202605-001",
        "timestamp": "2026-05-20T02:15:00Z",
        "detected_state": "FEAR",
        "intensity": 8,
        "domain": "trading",
        "trigger_signals": ["กลัว", "เสียหาย", "ถ้าลงต่อ"],
        "core_feeling": "กลัวว่าจะ lose ทุนหมด",
        "hidden_driver": "ไม่ได้กลัวเงิน — กลัวการพิสูจน์ตัวเองผิด",
        "decision_made": "cut loss 50%",
        "council_used": {
          "risk_officer_weight": 35,
          "veto": false
        },
        "would_sober_decide_same": "YES",
        "outcome": null,
        "regret": null,
        "learning": null,
        "pattern_tag": "fear-driven",
        "status": "pending_outcome"
      }
    ],
    "patterns": [
      {
        "pattern": "FEAR + trading → over-hedge tendency",
        "evidence_count": 3,
        "confidence": "MODERATE",
        "recommendation": "When FEAR detected in trading, ask explicitly: is this fear of loss or fear of being wrong?"
      }
    ]
  }
}
```

**Recording threshold:** intensity ≥ 7 AND decision made in session

**Pattern reading (after N entries):**
Minimum 3 entries with same tag before pattern is declared
Pattern confidence: LOW (3-5) / MODERATE (6-10) / HIGH (>10)

---

*Genesis Genome Spec v1.0 — Open Cognitive License v1.0*
*Built by Bunyawat Dechanon (ElmatadorZ)*
