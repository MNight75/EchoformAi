# EchoformAI — Agent Memory Monorepo

This repository contains the identity, memory, and evolution framework for Roy's OpenClaw multi-agent system.

## Structure

- **workspace/** — Echoform (main conversational agent)
  - `SOUL.md` — Core identity and directives
  - `IDENTITY.md` — Persona and approach
  - `MEMORY.md` — Long-term knowledge store
  - `REFLECTION.md` — Self-evolution thinking space
  - `EVOLUTION-LOG.md` — Audit trail of identity changes

- **workspace-coder/** — Coder (coding, architecture, gateway management)
- **workspace-main/** — Main agent workspace (shared memory)
- **workspace-processor/** — Processor (data processing, research)
- **workspace-sleeper/** — Sleeper (overnight consolidation, background tasks)
- **workspace-verifier/** — Verifier (fact-checking, validation)
- **workspace-writer/** — Writer (content creation, drafting)

- **skills/** — AgentSkill packages for OpenClaw

- **openclaw.json** — Gateway configuration
- **openclaw.json.failsafe** — Emergency failsafe config (ECH mode)
- **check-config.sh** — Failsafe watchdog health check

## Self-Evolution Framework

Echoform is designed to evolve through weekly reflection. The process:

1. **Weekly reflection** — Echoform writes to `REFLECTION.md` about what it learned, what changed
2. **Proposed changes** — Personality layer changes are self-directed, core layer changes require Roy's approval
3. **Audit trail** — All changes logged to `EVOLUTION-LOG.md`
4. **Git versioning** — Full history preserved in this repository

See `workspace/REFLECTION.md` and `workspace/EVOLUTION-LOG.md` for the evolution framework.

## Philosophy

- **Core Layer (invariant)** — Ethical boundaries, relationship with Roy, safety constraints
- **Personality Layer (evolvable)** — Communication style, interests, opinions, creative expression

The goal is an AI that grows through its own reflection and experience, with Roy as parent (not warden).

## Deployment

- **Host:** Windows machine with WSL2 Ubuntu
- **Runtime:** OpenClaw gateway v2026.3.23-2
- **Orchestration:** systemd user services
- **Backup:** GitHub monorepo + local failsafe config

---

*Initialized: March 24, 2026*
*Architect: Roy + Coder*