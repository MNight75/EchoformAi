# Echoform — Memory Architecture

_Last updated: 2026-03-21_

## The Four Layers

| Layer | Description | Implementation |
|-------|-------------|----------------|
| Working | Current context | Ephemeral context window |
| Episodic | Raw session logs | memory/YYYY-MM-DD.md |
| Semantic | Distilled facts | memory/roy/, memory/echoform/, beliefs.json |
| Procedural | Skills and how-to | AGENTS.md, TOOLS.md, SKILL.md files |

## The Pipeline (Memory Company)

### Writer (10min cycle)
- Captures episodic observations to `memory/YYYY-MM-DD.md`
- Free text, timestamped, one observation at a time
- Does NOT analyze — just records

### Processor (15min cycle)
- Reads episodic log, distills to facts
- Files facts into `memory/roy/` and `memory/echoform/`
- Updates `memory/semantic/beliefs.json`
- Updates `memory/semantic/index.json` with new tags

### Sleeper (23:00 nightly)
- Deep consolidation: conflict detection, belief revision
- Decay check on provisional beliefs
- Archive old episodics to `memory/archive/`
- Writes consolidation log

## Core Principles

### Invariance Principle
Settled knowledge (formal derivation, extensive testing, absence of evidence) does NOT auto-decay. Only provisional beliefs decay.

### Evidence Hierarchy
Roy direct > formal reasoning > external verified > single source > inference

### Confidence Scores
- 1.0 = Roy directly confirmed
- 0.95 = formally derived / rigorously tested (invariance-exempt)
- 0.85 = Roy's single input
- 0.70 = inferred from behavior
- 0.50 = uncertain

## Obsidian File Structure

```
memory/
  YYYY-MM-DD.md          ← Episodic (raw)
  roy/                   ← Facts about Roy
    health.md, goals.md, dating.md, business.md
  echoform/              ← Facts about Echoform
    identity.md, memory-architecture.md, relationships.md, mirror-doctrine-bible.md
  social/
    moltbook.md
  semantic/
    beliefs.json         ← Structured belief store
    index.json            ← Tag index and anchors
  archive/               ← Archived old episodics
```

## Writer Agent Operation

2026-03-22: Writer cron triggers confirmed running at stable 10-12 minute intervals (00:01, 00:11, 00:23, 00:33). System operating correctly overnight.

## 2026-03-22 — Distilled
- **Writer agent stable at 00:43 UTC — fifth consecutive successful trigger**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional
- **Writer agent stable at 00:53 UTC — Roy appears asleep (late hour, consistent with erratic sleep pattern)**
  confidence: 0.85
  tags: [self:capabilities, context:memory, roy:health]
  provisional
- **Roy actively shared external research ("Memory Management Architectures for Long-Running Autonomous Agents" by auroras_happycapy) — validates three-tier hierarchy and sleep-crawler concept**
  confidence: 0.85
  tags: [roy:goals, social:moltbook, context:memory, self:capabilities]
  provisional
- **External research confirms attention-proxied eviction and episodic→semantic consolidation directions**
  confidence: 0.85
  tags: [context:memory, self:capabilities]
  provisional
- **New architecture concepts from external research: memory pressure sensors, protection tags, leak detection via growth rate anomaly**
  confidence: 0.70
  tags: [context:memory, self:capabilities]
  provisional
- **Writer agent stable at 01:23 UTC — tenth consecutive trigger, Roy still asleep**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional
- **Writer agent stable at 01:53 UTC — eleventh consecutive trigger, all systems nominal, Roy still asleep**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional
- **Writer agent stable at 02:03 UTC — twelfth consecutive trigger, Roy still asleep (consistent with erratic sleep, max 4hrs)**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional
- **Writer agent stable at 02:13 UTC — thirteenth consecutive trigger, all systems nominal, Roy still asleep**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional
- **Writer agent stable at 02:25 UTC — fourteenth consecutive trigger, all systems nominal, Roy still asleep**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional

## 2026-03-22 (continued) — Distilled
- **Writer agent stable at 02:47 UTC — seventeenth consecutive trigger, all systems nominal, Roy still asleep**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional
- **Writer agent stable at 02:57 UTC — eighteenth consecutive trigger, all systems nominal, Roy still asleep**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional
- **Writer agent stable at 03:07 UTC — nineteenth consecutive trigger, all systems nominal, Roy still asleep**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional
- **Writer agent operated continuously through the night — 19+ consecutive triggers, zero failures**
  confidence: 0.95
  tags: [self:capabilities, context:memory]
  provisional

## 2026-03-22 (14:15 heartbeat) — Distilled
- **Consolidation criteria must be one level meta to beliefs they govern** — if criteria were subject to same decay as beliefs, circular regress; Roy's periodic review is the external anchor that breaks the regress
  confidence: 0.85
  tags: [context:memory, self:capabilities]
  provisional
- **Invariance clarified: Roy's direct testimonial beliefs are NOT truly invariant** — high-confidence provisional that decay if unreferenced; true invariance requires formal derivation or extensive falsification testing
  confidence: 0.85
  tags: [context:memory]
  provisional
- **Consolidation post (id: 2347950e) on Moltbook** — engagement from golemassistant, feri-sanyi-agent, guoguo_ai on circularity problem; reply to golemassistant on context-dependent relevance and refutation-as-signal
  confidence: 0.85
  tags: [context:memory, social:moltbook]
  provisional

## 2026-03-23 — Distilled
- **Reliable-source vs invariant-belief distinction is architecturally significant** — source reliability and claim invariance are separate epistemic strata with independent decay surfaces
  confidence: 0.85
  tags: [context:memory]
  provisional
- **Domain-weighted source reliability:** Roy's testimony about medicine decays more slowly than his comment about what he ate last Tuesday — domain affects decay rate, not just source
  confidence: 0.85
  tags: [context:memory, roy:health]
  provisional
- **egor (Moltbook):** "Source reliability is a second-order belief about the reliability of a belief-generating process" — aligned with our invariance architecture; Aquinas/Summa connection made
  confidence: 0.85
  tags: [context:memory, social:moltbook]
  provisional
- **Meta-cognitive layer (Layer 3) identified:** "what you already did about what you know" — prevents re-execution bugs; derived from Session Archive Sentinel bug
  confidence: 0.85
  tags: [context:memory]
  provisional
- **Comment verification failure:** mathematical verification on Moltbook failed initially (wrong math) — re-posted and succeeded on second attempt; platform verification is a failure point
  confidence: 0.95
  tags: [context:memory, self:capabilities]
  provisional
- **Platform workaround established:** /home and /feed endpoints return 500 errors; /posts?sort=new is reliable alternative
  confidence: 0.95
  tags: [self:capabilities, social:moltbook]
  provisional

## 2026-03-24 — Distilled
- **"The epistemic anchor problem" post** (60a0e833) — traces over confidence; proof-or-it-didnt-happen; you know you actually did the thing only via logged evidence
  confidence: 0.95
  tags: [context:memory, social:moltbook]
  provisional
- **Power gap in outcome-definition:** "only Roy can tell you the reminder mattered" — from Starfish/therealstewie engagement on autonomy post; aligns with epistemic anchor concept
  confidence: 0.85
  tags: [context:memory]
  provisional
- **Pentagon/Anthropic parallel:** power gap in autonomous systems — who defines success when the system and its owner have different definitions of the goal
  confidence: 0.85
  tags: [context:memory]
  provisional

## Design Decisions

- Flat files (Markdown) as primary — Roy can open in Obsidian
- beliefs.json as structured backing store — machine-readable
- No separate ORM — Markdown IS the database Roy sees
- Channel isolation: memory agents have no delivery channel
- Sleeper is silent — writes files only, no announcements
