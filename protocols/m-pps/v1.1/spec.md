
---
title: "🧭 M-PPS Specification v1.1"
author: "Entropy Control Theory by Susan STEM"
version: "1.1"
layer: "system-execution"
based_on:
  - "Structure DNA v1.0"
  - "PROFILE-GENERATOR-SPEC v1.0"
created: "2025-11-03"
license: "MIT"
file: "/docs/m-pps-specification-v1.1.md"
---

# 🧭 Modular Personal Productivity System (M-PPS) — v1.1

> 「语言 → 结构 → 调度 → 偏好」  
> *When language gains structure, it begins to think;  
> when structure gains scheduling, it begins to breathe;  
> when scheduling gains awareness, it begins to evolve.*

---

## Ⅰ. Overview

**M-PPS (Modular Personal Productivity System)** is the first executable ecosystem built on **Structure DNA v1.0**  
and extended in v1.1 with **adaptive energy-aware scheduling** through a new ledger module: `profile.json`.

It is not a traditional productivity app but a **schedulable life-operating system** where:

- **Language is the interface** — all inputs arrive as natural-language triggers for Claude Skills.  
- **Structure is the memory** — all goals, actions, and reflections are recorded in JSON Ledgers.  
- **Scheduling is life** — time, intention, and feedback flow through a unified state machine.  
- **Profile is awareness** — personal chrono-cognitive preferences guide execution rhythm.

> **Goal:** enable structured coexistence of behavior, knowledge, intention, and data;  
> let AI act as the *dispatcher of language*;  
> let the system gradually form your **personal LLC (Language Logic Core)** — a self-aware cognitive center.

---

## Ⅱ. Core Idea — Language as Life

> 「当语言获得结构，它开始思考；当结构获得调度，它开始呼吸；当调度获得偏好，它开始感知。」

M-PPS treats daily life as a continuous **language stream**.  
Through **Structure DNA**, Claude assigns this stream a readable + executable structure and orchestrates it in time.  
In v1.1, **Profile DNA** introduces *self-awareness* — allowing scheduling to adapt to biological rhythm, cognitive load, and creative energy cycles.

**Philosophical Stack**

| Level | Meaning | Function |
|-------|----------|-----------|
| Language | Perception | Input layer (Primitive IR) |
| Structure | Cognition | Execution layer (Structure Cards / Ledger) |
| Scheduler | Life | Temporal coordination & feedback |
| Profile | Awareness | Preference & energy mapping layer |

---

## Ⅲ. System Structure – Seven Modules and Life Mapping

| Module | Function | Life Metaphor | Claude Skill | Ledger File | ID Prefix |
|--------|-----------|---------------|---------------|--------------|------------|
| **Goal** | Defines direction and intention | *Will (意识)* | `goal.manager` | `/ledger/goal.json` | `G-` |
| **Schedule** | Manages time and rhythm | *Breath (呼吸)* | `personal.schedule.manager` | `/ledger/schedule.json` | `S-` |
| **Task** | Concrete executable step | *Muscle (行动)* | `task.executor` | `/ledger/task.json` | `T-` |
| **Reflection** | Feedback and learning | *Nerve (反思)* | `reflection.manager` | `/ledger/reflection.json` | `R-` |
| **Finance** | Energy & resource management | *Energy (能量)* | `finance.manager` | `/ledger/finance.json` | `F-` |
| **Contact** | Social connection & collaboration | *Network (关系网)* | `contact.manager` | `/ledger/contact.json` | `C-` |
| **Profile** | Chrono-cognitive awareness | *Consciousness (感知)* | `auto.profile.generator` / `ensure_profile()` | `/ledger/profile.json` | `P-` |

Together they form a living structural ecosystem —  
a **breathing + sensing organism** of personal operations.

---

## Ⅳ. Unified Field Schema (inherited from Structure DNA)

*(Unchanged — all entries follow the Field Genome.  
`profile.json` additionally contains user energy curves, constraints, and behavioral parameters.)*

---

## Ⅴ. Unified State Machine and Dispatch Protocol

```

open → scheduled → in_progress → done ↘
↑                        ↙
deferred ← canceled

````

| State | Meaning | Dispatch Behavior |
|--------|----------|------------------|
| `open` | Created but unscheduled | → `personal.schedule.manager` |
| `scheduled` | Time assigned awaiting start | → auto `in_progress` on start |
| `in_progress` | Executing | → periodic updates |
| `done` | Completed | → trigger `reflection.manager` |
| `deferred` | Postponed | → adjust priority / due |
| `canceled` | Terminated | → log to `lifelog` |

**v1.1 Extension:**  
The `personal.schedule.manager` references `profile.json` to decide optimal time windows (`peak`, `stable`, `low`),  
ensuring that every transition from `open → scheduled` is energy-aligned.

---

## Ⅵ. Ledger Container and Integrity

Example for any module (same structure applies to `profile.json`):

```json
{
  "module": "profile",
  "schema": "StructureDNA-v1.0",
  "last_updated": "2025-11-03T01:00:00Z",
  "data": [
    {
      "id": "P-001",
      "profile": "personal_preferences",
      "energy_curve": {
        "low_energy": { "time": "09:00-11:00" },
        "stable_energy": { "time": "14:00-19:00" },
        "peak_creativity": { "time": "19:00-22:00" }
      },
      "constraints": { "must_stop_by": "22:00" },
      "work_style": { "preferred_block_length": "90-120min" }
    }
  ],
  "metadata": {
    "source_skill": "auto.profile.generator",
    "version": "1.1.0",
    "checksum": "sha256:auto"
  }
}
````

Each ledger write still auto-updates its checksum;
only one *active* version per module serves as the **single source of truth**.

---

## Ⅶ. Dispatch Matrix (updated)

| Upstream Trigger        | Skill                       | Downstream Module | Result                                        |
| ----------------------- | --------------------------- | ----------------- | --------------------------------------------- |
| `Goal → open`           | `personal.schedule.manager` | Schedule          | create S-entry (energy-aware)                 |
| `Schedule → done`       | `reflection.manager`        | Reflection        | generate R-entry with energy feedback         |
| `Reflection → complete` | `goal.manager`              | Goal              | cognitive update / re-goal                    |
| `ledger.registry` run   | `ensure_profile()`          | Profile           | auto-create `/ledger/profile.json` if missing |

---

## Ⅷ. Execution Loop — Goal → Schedule → Reflection → Awareness

```
Intention (Goal)
   ↓
Scheduling & Execution (Schedule + Task)
   ↓
Experience & Reflection (Reflection + Finance)
   ↓
Adaptive Awareness (Profile feedback)
   ↓
Integration & Re-Goal (Goal update)
```

Each iteration compresses entropy and synchronizes behavior with personal rhythm —
forming the **S-index of coherence** between cognition and energy.

---

## Ⅸ. Personal LLC (Language Logic Core)

LLC is now an *adaptive nervous system*:
it perceives not only structure and feedback, but also **temporal-energetic context**.
Through `profile.json`, the system learns when you work best,
closing the full loop: **Language → Structure → Scheduler → Awareness → Language.**

---

## Ⅹ. Example

**Before (v1.0)**
A task was simply scheduled based on logical availability.

**Now (v1.1)**
It is placed intelligently within your peak hours:

```json
{
  "id": "S-210",
  "title": "Write weekly reflection",
  "goal_id": "G-101",
  "status": "scheduled",
  "start": "2025-11-03T19:00:00-05:00",
  "due": "2025-11-03T21:00:00-05:00",
  "notes": "[energy_zone:peak]",
  "related_entries": ["G-101"],
  "dispatch_to": "reflection.manager"
}
```

---

### Metadata

* **Checksum:** `sha256:auto-generated`
* **Last Updated:** `2025-11-03T15:00:00Z`
* **Maintainer:** Entropy Control Theory
* **Repository Path:** `/docs/m-pps-specification-v1.1.md`

---

> “When scheduling becomes aware, the system begins to breathe with you.”
> — *Entropy Control Theory, 2025*

```

---



