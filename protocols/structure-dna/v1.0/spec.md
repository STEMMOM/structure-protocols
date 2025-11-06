


---
title: "🧬 Structure DNA Specification v1.0"
schema_id: "StructureDNA-v1.0"
author: "Entropy Control Theory by Susan STEM"
version: "1.0"
created: "2025-10-31"
license: "MIT"
file: "/docs/structure-dna.md"
---




## Ⅰ. Core Principle

> “字段统一 → 语义稳定 → 自动调度 → 结构生命体的生成。”

**Structure DNA** defines the *minimal consensus format* that allows language to become schedulable and structure to become evolvable.  
It serves as the **base protocol** connecting all Claude Skills and Ledger modules under the Entropy Control framework.

**Purpose:**  
To unify the underlying schema of tasks, goals, reflections, and ledgers — enabling human and AI to share the same *readable + executable* world model.

---

## Ⅱ. Field Genome

Every entry (the smallest recognizable structural unit) follows a unified field schema.

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | string | ✅ | Globally unique ID; prefixed by module (G-, S-, R-, L-, F-, etc.) |
| `title` / `action` | string | ✅ | Main semantic unit — task, goal, or event description |
| `goal_id` | string | ⛔ | Reference to parent goal (`G-xxx`) |
| `start` | ISO datetime | ⛔ | Start time |
| `due` | ISO datetime | ⛔ | Due or end time |
| `duration` | string | ⛔ | Duration string (`2h`, `30min`, etc.) |
| `status` | enum | ✅ | Lifecycle state (see section Ⅲ) |
| `tags` | array[string] | ⛔ | Semantic labels or triggers |
| `notes` | string | ⛔ | Optional notes or context |
| `related_entries` | array[string] | ⛔ | Cross-module references (Goal, Reflection, etc.) |
| `dispatch_to` | string | ⛔ | Downstream Skill or module name |
| `created_at` | ISO datetime | ✅ | Creation timestamp |
| `updated_at` | ISO datetime | ✅ | Last modified timestamp |

---

## Ⅲ. Unified Status Machine

```

open → scheduled → in_progress → done ↘
↑                        ↙
deferred ← canceled

```

| Status | Meaning | Dispatch Behavior |
| --- | --- | --- |
| `open` | Created but not yet scheduled | → dispatch to `schedule` module |
| `scheduled` | Time assigned, waiting to start | → transition to `in_progress` when `start` reached |
| `in_progress` | Currently being executed | → periodic state updates |
| `done` | Completed | → trigger `reflection` or `summary` |
| `deferred` | Postponed or rescheduled | → generate new `due`, adjust priority |
| `canceled` | Canceled or dropped | → log into `lifelog` as a termination record |

This state machine ensures all modules (goal, schedule, reflection, ledger) remain temporally and semantically consistent.

---

## Ⅳ. Temporal Semantics

Only three temporal keys are recognized:

```

start / due / duration

````

- All timestamps **must** use ISO-8601 format.  
- Claude can directly compute remaining time, overdue status, and duration.  
- Deprecated synonyms: `deadline`, `end`, `finish`, `until`.

**Example:**

```json
{
  "start": "2025-11-01T09:00:00-04:00",
  "due": "2025-11-01T11:00:00-04:00",
  "duration": "2h"
}
````

---

## Ⅴ. Relational Linking

Cross-module relationships use the `related_entries` array:

```json
"related_entries": ["G-101", "S-112", "R-230"]
```

### ID Prefix Convention

| Prefix | Module              | Example |
| ------ | ------------------- | ------- |
| G-     | Goal / Goalloop     | `G-101` |
| S-     | Schedule / Task     | `S-112` |
| R-     | Reflection / Review | `R-230` |
| L-     | LifeLog / Journal   | `L-055` |
| F-     | Finance / Resource  | `F-014` |
| K-     | Knowledge / Note    | `K-031` |

All IDs follow `module + sequence` format for **global uniqueness** and **traceability**.
These IDs allow Claude and external schedulers to link data across different subsystems.

---

## Ⅵ. Dispatch Protocol

Dispatch defines how entries trigger actions across modules or Skills.

| Trigger           | Dispatch Behavior                                                |
| ----------------- | ---------------------------------------------------------------- |
| `dispatch_to`     | Directly specify target Skill (`schedule`, `reflection`, etc.)   |
| `status` change   | State transitions trigger downstream calls (`done` → reflection) |
| `related_entries` | Establish bidirectional relational feedback loops                |
| `tags`            | Custom trigger rules (e.g., `urgent` → priority scheduling)      |

**Example:**

```json
{
  "id": "S-301",
  "title": "Write weekly reflection",
  "status": "done",
  "dispatch_to": "reflection.manager",
  "related_entries": ["R-055"],
  "tags": ["weekly", "auto-reflect"]
}
```

→ When `status` = `done`, dispatches to `reflection.manager` and opens `R-055` for update.

---

## Ⅶ. Ledger Container Schema

Every module ledger file follows a standardized container structure:

```json
{
  "module": "schedule",
  "schema": "StructureDNA-v1.0",
  "last_updated": "2025-10-30T14:00:00Z",
  "data": [ /* Entries */ ],
  "metadata": {
    "source_skill": "schedule.manager",
    "version": "1.0.0",
    "checksum": "sha256:abc123..."
  }
}
```

**Explanation:**

* `module` → identifies which subsystem the file belongs to.
* `schema` → ensures compatibility with current StructureDNA version.
* `metadata` → stores skill source, version, and integrity hash.

---

## Ⅷ. Naming & Path Convention

* **File naming:** all lowercase, `<module>.json`
  e.g. `schedule.json`, `reflection.json`
* **Path example:** `/ledger/schedule.json`
* **Manifest registry:** `/ledger/manifest.json` lists all active ledgers.
* **Versioning:** uses [Semantic Versioning](https://semver.org/) — `major.minor.patch`

**Example structure:**

```
/ledger/
 ├─ goal.json
 ├─ schedule.json
 ├─ reflection.json
 ├─ lifelog.json
 ├─ finance.json
 ├─ manifest.json
```

---

## Ⅸ. Security & Integrity

To maintain systemic consistency:

1. Every write operation **auto-updates** `updated_at`.
2. Each commit generates a **checksum** (SHA-256).
3. Archived snapshots stored under `/archive/`, **immutable**.
4. Only one **active version** per module is recognized as *the single source of truth*.
5. Backups can be restored through manifest reconstruction.

---

## Ⅹ. Evolution Path

When **fields**, **status**, **time**, and **relation** protocols stabilize,
Claude can autonomously orchestrate cross-module cycles such as:

```
Goal → Schedule → Reflection
Shopping → Finance → Inventory
Journal ↔ LifeLog
```

Resulting in:

* **Self-stability:** internal state coherence
* **Explainability:** structure = semantics
* **Evolvability:** feedback-driven self-adaptation

Together, these enable the formation of a **Living Structure** —
a dynamic system where language, structure, and scheduling form a living cognitive loop.

---

## XI. Conceptual Summary

| Layer                   | Role                    | Example                 |
| ----------------------- | ----------------------- | ----------------------- |
| **Language Protocol**   | Perception of meaning   | Primitive IR            |
| **Structure Framework** | Cognition and execution | Structure Cards         |
| **Scheduler Runtime**   | Life and feedback       | Claude Skills / Ledgers |

---

## XII. Sample Entry (Full JSON)

```json
{
  "id": "S-202",
  "title": "Plan Structure DNA documentation",
  "goal_id": "G-101",
  "start": "2025-10-30T10:00:00-04:00",
  "due": "2025-10-30T12:00:00-04:00",
  "duration": "2h",
  "status": "done",
  "tags": ["writing", "documentation", "StructureDNA"],
  "notes": "Draft completed and versioned under /docs/",
  "related_entries": ["R-303", "G-101"],
  "dispatch_to": "reflection.manager",
  "created_at": "2025-10-29T09:00:00-04:00",
  "updated_at": "2025-10-30T13:45:00-04:00"
}
```

---

## XIII. Structural Philosophy

> **Structure DNA v1.0 = The Genetic Code of Structured Systems**

* Each **Ledger** → an *organic tissue*.
* Each **Skill** → a *functional cell*.
* The **Scheduler** → a *nervous system*.

Together, they form a **language-based living organism** —
a system that can perceive, act, reflect, and evolve through feedback.

---

### Metadata

* **Checksum:** `sha256:auto-generated`
* **Last Updated:** `2025-10-31T12:00:00Z`
* **Maintainer:** Entropy Control Theory
* **Repository Path:** `/docs/structure-dna.md`

---

> **“Language becomes life when structured and scheduled.”**
>
> — *Entropy Control Theory, 2025*

```

---

```

