---
name: genesis-bridge-spec
version: "1.0"
author: "Bunyawat Dechanon (ElmatadorZ)"
---

# BRIDGE SPEC v1.0
## Claude ↔ Python Communication Protocol

The bridge is the contract between the cognitive brain (Claude) and the execution body (Python).

**Hard rule: Claude thinks. Python acts. The bridge is the only connection.**

---

## ARCHITECTURE

```
Claude (GENESIS_CORE.md)
  │
  │ JSON output (structured)
  ▼
Bridge Layer (bridge.py)
  │
  ├── GenesisMind runtime
  ├── Genome read/write
  ├── Domain app routing
  └── Result back to Claude
  │
  ▼
Execution Layer
  ├── MT5 (trading)
  ├── Ollama (local LLM)
  ├── Telegram (alerts)
  └── SQLite (persistence)
```

---

## INPUT: Claude → Python

```python
# Every Claude output that requires Python execution
# must follow this schema exactly

GENESIS_OUTPUT = {
    "protocol": "genesis_v1",
    "session_id": "uuid-string",
    "timestamp": "ISO-8601",
    "mode": "MARKET|STRATEGY|BUILD|PERSONAL|AUDIT",

    "emotional_context": {
        "detected_state": "FEAR|EXCITEMENT|FATIGUE|...",
        "intensity": 7,          # 1-10
        "signals_detected": ["word1", "word2"],
        "council_weights_applied": {
            "strategist": 10,
            "skeptic": 25,
            "analyst": 20,
            "risk_officer": 35,
            "builder": 5,
            "cosmic_mind": 5
        }
    },

    "council_result": {
        "strategist_plan": "primary plan text",
        "skeptic_verdict": "STRONG|MODERATE|WEAK",
        "analyst_confidence_adjustment": 0.65,
        "risk_officer": {
            "veto": False,
            "worst_case": "description",
            "conditions": ["condition 1"]
        },
        "cosmic_mind_verdict": "COMPOUND|NEUTRAL|DECAY",
        "synthesis": "final integrated recommendation"
    },

    "action_required": {
        "type": "TRADE|ANALYZE|WRITE|DIAGNOSE|NONE",
        "target": "specific target",
        "surgical_scope": {
            "touch": ["item1"],
            "boundary": ["item2"],
            "side_effects": ["effect1"]
        },
        "priority": "HIGH|MED|LOW",
        "reversible": True
    },

    "confidence": 0.72,
    "failure_conditions": ["condition 1", "condition 2"],

    "genome_update": {
        "record_affective": False,  # True if intensity >= 7
        "affective_entry": None,    # fill if record_affective True
        "strategy_update": None,    # pattern to reinforce/decay
        "failure_signature": None   # new failure to log
    }
}
```

---

## OUTPUT: Python → Claude

```python
EXECUTION_RESULT = {
    "protocol": "genesis_v1",
    "session_id": "same-uuid",
    "timestamp": "ISO-8601",
    "status": "SUCCESS|FAIL|PARTIAL|VETO_BLOCKED",

    "action_taken": "description of what was done",
    "action_skipped": "description of what was NOT done (surgical)",

    "results": {
        # domain-specific results
        # trading: signal data, position info
        # analysis: structured findings
        # writing: generated content
    },

    "verify_result": {
        "passed": True,
        "checklist": {
            "intent_match": True,
            "surgical_scope_maintained": True,
            "shadow_gate_run": True,
            "confidence_explicit": True,
            "failure_conditions_named": True,
            "side_effects_identified": True
        },
        "issues": []  # list issues if not passed
    },

    "side_effects_observed": ["actual effect 1"],

    "genome_updated": {
        "affective_recorded": False,
        "strategy_reinforced": None,
        "failure_logged": None
    },

    "next_action": "what Python suggests Claude should do next",
    "error": None  # error details if status FAIL
}
```

---

## BRIDGE IMPLEMENTATION (Python)

```python
# bridge.py — minimal reference implementation

import json
import anthropic
from datetime import datetime
from genome import GenomeManager

class GenesisBridge:
    def __init__(self):
        self.client = anthropic.Anthropic()
        self.genome = GenomeManager()

    def process_claude_output(self, output: dict) -> dict:
        """Route Claude's cognitive output to execution"""

        # Validate schema
        if output.get("protocol") != "genesis_v1":
            return self._error("invalid protocol")

        # Check veto
        if output["council_result"]["risk_officer"]["veto"]:
            return self._veto_blocked(output)

        # Route by mode
        mode = output.get("mode")
        action = output.get("action_required", {})

        if action.get("type") == "TRADE":
            result = self._execute_trade(action)
        elif action.get("type") == "ANALYZE":
            result = self._execute_analysis(action)
        elif action.get("type") == "NONE":
            result = {"status": "SUCCESS", "action_taken": "analysis only"}
        else:
            result = self._error(f"unknown action type: {action.get('type')}")

        # Update genome
        if output.get("genome_update", {}).get("record_affective"):
            self.genome.record_affective(
                output["genome_update"]["affective_entry"]
            )

        # Run verify
        verify = self._verify(output, result)

        return {
            "protocol": "genesis_v1",
            "session_id": output["session_id"],
            "timestamp": datetime.utcnow().isoformat(),
            "status": result["status"],
            "action_taken": result.get("action_taken"),
            "verify_result": verify,
            "side_effects_observed": result.get("side_effects", []),
            "genome_updated": self.genome.last_update,
            "error": result.get("error")
        }

    def _verify(self, output: dict, result: dict) -> dict:
        """Verify loop — check all 6 conditions"""
        checklist = {
            "intent_match": True,  # validate manually or via LLM
            "surgical_scope_maintained": self._check_surgical(output, result),
            "shadow_gate_run": True,  # Claude guarantees this
            "confidence_explicit": output.get("confidence") is not None,
            "failure_conditions_named": bool(output.get("failure_conditions")),
            "side_effects_identified": bool(
                output["action_required"].get("surgical_scope", {})
                .get("side_effects")
            )
        }
        passed = all(checklist.values())
        return {"passed": passed, "checklist": checklist, "issues": [
            k for k, v in checklist.items() if not v
        ]}
```

---

## ERROR HANDLING

```python
# Status codes
SUCCESS         = all executed, verify passed
FAIL            = execution failed, see error field
PARTIAL         = some steps executed, some failed
VETO_BLOCKED    = Risk Officer veto prevented execution
VERIFY_FAILED   = executed but verify loop did not pass

# On FAIL: retry with adjusted parameters
# On VETO_BLOCKED: report to Claude, do not retry
# On VERIFY_FAILED: diagnose via Shadow Gate, adjust, retry
```

---

*Genesis Bridge Spec v1.0 — Open Cognitive License v1.0*
*Built by Bunyawat Dechanon (ElmatadorZ)*
*"The bridge is not smart. The brain is smart. The bridge just carries the message."*
