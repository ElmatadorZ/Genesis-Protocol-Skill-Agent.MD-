---
name: genesis-runtime-spec
version: "1.0"
author: "Bunyawat Dechanon (ElmatadorZ)"
parent: "genesis-protocol"
license: "Open Cognitive License v1.0"
---

# GENESIS RUNTIME SPEC v1.0
## Claude ↔ Python Bridge Architecture

Genesis Protocol runs on two layers that must never merge:

```
╔══════════════════════════════╗
║   COGNITIVE BRAIN (Claude)   ║  ← GENESIS_CORE.md runs here
║   Thinking / Reasoning       ║  ← All Skills run here
╚══════════════╦═══════════════╝
               ║  structured JSON bridge
╔══════════════╩═══════════════╗
║   EXECUTION BODY (Python)    ║  ← skynet_genesis_masterpiece.py
║   Action / Memory / Runtime  ║  ← MT5, Ollama, SQLite, Telegram
╚══════════════════════════════╝
```

**Hard rule: Claude Skills = brain. Python = body. Never merged.**

---

## PYTHON RUNTIME COMPONENTS

### Core Runtime
```
skynet_genesis_masterpiece.py
  ├── GenesisMind class        — main orchestrator
  ├── AuditTrail               — tamper-evident hash chain
  ├── MemoryStore              — decay + reinforce + semantic search
  └── AgentDebateEngine        — parallel agent execution
```

### Domain Apps
```
moneyatlas_signal_app.py       — Signal + MT5 bridge
  ├── MT5Bridge                — MetaTrader5 connection
  ├── OllamaClient             — local LLM inference
  ├── SignalEngine             — SMC structure detection
  └── TelegramAlert            — notification system

skynet_commander.py            — orchestration runtime
  ├── UniversalLLMBackend      — Claude/GPT/Gemini/Ollama
  ├── AgenticToolLoop          — tool execution loop
  └── SessionManager           — context management
```

---

## GENOME SPEC

```python
# Strategy Genome Schema
{
  "version": "1.0",
  "created": "ISO-8601",
  "owner": "ElmatadorZ",

  "strategy_genome": {
    "rules": [
      {
        "id": "rule_001",
        "content": "pattern that works",
        "weight": 0.85,        # 0-1, reinforced by success
        "decay_rate": 0.02,    # per session without use
        "source": "session_id",
        "created": "ISO-8601"
      }
    ]
  },

  "failure_map": {
    # NEVER DELETE entries
    "failures": [
      {
        "id": "SIG-001",
        "signature": "Claude Code WSL2 startup failure",
        "symptom": "Failed to start workspace",
        "cause": "Hyper-V + WSL2 memory conflict",
        "fix": ["verify Hyper-V", "wsl --shutdown", "retry"],
        "first_seen": "ISO-8601",
        "recurrence": 2
      }
    ]
  },

  "affective_genome": {
    # High-charge decisions (intensity >= 7)
    "entries": [
      {
        "id": "AGE-202605-001",
        "state": "FEAR",
        "intensity": 8,
        "domain": "trading",
        "core_feeling": "กลัวว่าจะ lose ทุนหมด",
        "hidden_driver": "ไม่ได้กลัวเงิน — กลัวการพิสูจน์ตัวเองผิด",
        "decision": "cut loss 50%",
        "would_sober_decide_same": "YES",
        "outcome": null,   # fill retroactively
        "regret": null,
        "pattern_tag": "fear-driven"
      }
    ]
  }
}
```

---

## BRIDGE PROTOCOL (Claude → Python)

```python
# Input schema from Claude Skill to Python runtime
{
  "protocol": "genesis_v1",
  "session_id": "uuid",
  "timestamp": "ISO-8601",

  "cognitive_output": {
    "mode": "MARKET|STRATEGY|BUILD|PERSONAL",
    "emotional_state": {
      "detected": "FEAR",
      "intensity": 7,
      "signals": ["กลัว", "เครียด", "ถ้าพลาด"]
    },
    "council_result": {
      "strategist": "...",
      "skeptic": "...",
      "risk_officer": {"verdict": "GO", "veto": false},
      "synthesis": "..."
    },
    "action": {
      "type": "TRADE|ANALYZE|WRITE|DIAGNOSE|DELEGATE",
      "target": "specific target",
      "surgical_scope": {
        "touch": ["what to modify"],
        "boundary": ["what NOT to touch"]
      }
    },
    "confidence": 0.72,
    "failure_conditions": ["condition 1", "condition 2"]
  }
}

# Output schema from Python runtime back to Claude
{
  "execution_result": {
    "status": "SUCCESS|FAIL|PARTIAL",
    "action_taken": "...",
    "side_effects": ["effect 1", "effect 2"],
    "verify_pass": true,
    "genome_update": {
      "type": "reinforce|failure|affective",
      "entry": {}
    }
  }
}
```

---

## ENVIRONMENT SETUP

```bash
# WSL2 (Ubuntu) — primary runtime environment
python3 --version    # >= 3.10
ollama --version     # local LLM server

# Required packages
pip install anthropic ollama MetaTrader5 python-telegram-bot \
            sqlite3 hashlib pyqt6 --break-system-packages

# Ollama model
ollama pull gemma3:12b   # primary local model

# Environment variables
ANTHROPIC_API_KEY=...    # Claude API
TELEGRAM_BOT_TOKEN=...   # alerts
MT5_PATH=C:\Program Files\MetaTrader 5\terminal64.exe
```

---

## KNOWN FAILURE SIGNATURES

```
SIG-001: Claude Code WSL2 Startup
  Symptom : "Failed to start workspace"
  Cause   : Hyper-V + WSL2 memory conflict
  Fix     : wsl --shutdown → restart → retry

SIG-002: Ollama Connection Refused
  Symptom : ConnectionRefused on localhost:11434
  Cause   : Service not running / wrong host binding
  Fix     : ollama serve & → curl localhost:11434/api/tags

SIG-003: MT5 Python Connection Failed
  Symptom : MetaTrader5.initialize() returns False
  Cause   : MT5 not running / not logged in / WSL2 path issue
  Fix     : Run MT5.exe on Windows → login → use Windows Python

SIG-004: SQLite Genome Corruption
  Symptom : JSON decode error on atlas_genome.json
  Cause   : Process killed mid-write
  Fix     : Restore from .bak → reconstruct from defaults
```

---

*Genesis Runtime Spec v1.0 — Open Cognitive License v1.0*
*Built by Bunyawat Dechanon (ElmatadorZ)*
*"Brain thinks. Body acts. Never confuse the two."*
