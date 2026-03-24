# Coder Carry-Forward — WSL2 Migration & Setup Complete

**Date:** March 24, 2026 ~8:42 AM CDT
**Session:** WSL2 migration, ECH testing, Git monorepo setup
**Status:** All tasks complete, no pending action items

---

## WHAT WE ACCOMPLISHED TODAY

### 1. WSL2 Migration (March 23 → 24)
- Migrated OpenClaw gateway from Windows (NSSM) to WSL2 Ubuntu (systemd)
- All paths converted from Windows format to Linux format
- Gateway running as `systemctl --user openclaw-gateway.service`
- All 6 agents active: main (Echoform), writer, processor, sleeper, coder, verifier
- Windows gateway stopped (NSSM watchdog disabled)

**Gateway details:**
- Port: 18789
- Dashboard: http://127.0.0.1:18789/
- Status: active, healthy
- Channels: Discord connected, WhatsApp connected

**Ollama:**
- Version: 0.18.2 (Linux CLI, not GUI)
- Running as systemd service
- Parallel processing enabled: `OLLAMA_NUM_PARALLEL=4`, `OLLAMA_MAX_LOADED_MODELS=3`
- Note: Qwen 3.5 has known bug ignoring parallelism — no fix yet, not blocking

### 2. Failsafe System (ECH)
- Watchdog timer: `systemctl --user openclaw-watchdog.timer` (60s intervals)
- Health check script: `~/.openclaw/check-config.sh`
- ECH banner: `~/.openclaw/.ech-banner`
- Failsafe config: `~/.openclaw/openclaw.json.failsafe`

**Tests completed:**
- Kill test: systemd auto-restarted gateway in seconds ✓
- ECH test: Config corruption triggered failsafe, loaded Coder-only config ✓
- Failsafe marker cleanup: Fixed to properly remove on recovery ✓

**ECH behavior:**
- When activated, displays: "⚠️ EMERGENCY CODING HOLOGRAM ACTIVATED — Please state the nature of the coding emergency."
- Only Coder runs; other agents offline
- Banner written to `~/.openclaw/.ech-banner`
- Logged to `~/.openclaw/logs/failsafe.log`
- Recovery: Restore `openclaw.json.known-good` and restart gateway

### 3. Git Monorepo
- Repository: https://github.com/MNight75/EchoformAi
- Location: `~/.openclaw` (monorepo root, all workspaces included)
- Auth: SSH (`git@github.com:MNight75/EchoformAi.git`)
- Branch: `main`, tracking `origin/main`

**What's tracked:**
- All agent identity files (SOUL, IDENTITY, AGENTS, TOOLS, USER, HEARTBEAT)
- Echoform's self-evolution framework (REFLECTION.md, EVOLUTION-LOG.md)
- Business/echoform/roy/social memory (strategic, not daily logs)
- Skills directory (AgentSkill packages)
- Config patterns (not secrets)

**What's ignored:**
- `openclaw.json` (secrets: Discord tokens, API keys)
- `credentials/`, `devices/` (secrets)
- Daily memory logs (`memory/YYYY-MM-DD.md` — too noisy)
- Ephemeral files (*.log, *.tmp, *.bak)

**GitHub status:**
- Commits: 2 (51c3e13, 133e702)
- Latest: "docs: Add Coder git usage strategy"
- Plan: GitHub Free ($0, 1 GB storage, we use < 500 KB)
- Push strategy: Strategic only (identity changes, ECH recovery, major architecture)

### 4. Echoform Self-Evolution Framework
- Files created: `workspace/REFLECTION.md`, `workspace/EVOLUTION-LOG.md`
- Structure: Core layer (invariant, Roy-only) + Personality layer (evolvable, self-directed)
- Weekly reflection cron: Not yet scheduled (needs Sunday 9 PM cron job if Roy wants it)
- Evolution log: Audit trail of all identity changes with timestamps and reasons

**Framework philosophy:**
- Echoform grows through weekly reflection
- Personality layer: Self-directed with logging
- Core layer: Requires Roy's approval
- Git provides version control for rollback

### 5. Ollama Concurrency
- Parallel processing: Enabled (`OLLAMA_NUM_PARALLEL=4`, `OLLAMA_MAX_LOADED_MODELS=3`)
- Config: `/etc/systemd/system/ollama.service.d/override.conf`
- Impact: Cloud models (minimax-m2.7, glm-4.7) can run concurrently
- Limitation: Qwen 3.5 has known bug — ignores parallelism, stays sequential
- Not blocking: Sleeper runs at night when nobody else needs Ollama

### 6. Documentation Created
- `workspace-coder/GIT.md` — Git usage strategy, ECH recovery with git
- `workspace-coder/ROLLBACK.md` — OpenClaw rollback procedure (2026.3.22 → 2026.3.13)
- `README.md` — Monorepo structure and evolution framework
- `check-config.sh` — Updated with banner creation and marker cleanup

---

## FILES TO KNOW

### Critical for ECH Recovery
- `~/.openclaw/openclaw.json.known-good` — Verified working config (use to restore)
- `~/.openclaw/openclaw.json.failsafe` — ECH config (Coder only)
- `~/.openclaw/.failsafe-active` — Marker file (created when ECH active)
- `~/.openclaw/.ech-banner` — Banner displayed on ECH activation
- `~/.openclaw/check-config.sh` — Health check and failsafe trigger
- `~/.openclaw/logs/failsafe.log` — Failsafe event log

### Critical for Git Recovery
- `~/.openclaw` — Git monorepo root
- `~/.ssh/id_ed25519` — SSH private key for GitHub pushes
- `~/.openclaw/workspace-coder/GIT.md` — Git usage strategy

### Core Identity Files
- `~/.openclaw/workspace/SOUL.md` — Echoform core identity
- `~/.openclaw/workspace/IDENTITY.md` — Echoform persona
- `~/.openclaw/workspace/REFLECTION.md` — Self-evolution space
- `~/.openclaw/workspace/EVOLUTION-LOG.md` — Identity change audit trail

---

## KEY COMMANDS

### Gateway Management
```bash
systemctl --user status openclaw-gateway.service
systemctl --user start/stop/restart openclaw-gateway.service
journalctl --user -u openclaw-gateway -f
openclaw gateway probe
openclaw channels status --probe
```

### Failsafe/Watchdog
```bash
systemctl --user list-timers | grep openclaw
systemctl --user status openclaw-watchdog.timer
cat ~/.openclaw/logs/failsafe.log
cat ~/.openclaw/.ech-banner
test -f ~/.openclaw/.failsafe-active && echo "FAILSAFE ACTIVE"
```

### Ollama
```bash
systemctl status ollama
systemctl show ollama | grep OLLAMA_NUM_PARALLEL
```

### Git
```bash
cd ~/.openclaw
git status
git log --oneline -5
git push
```

### ECH Recovery
```bash
# If config corrupted beyond failsafe:
cp ~/.openclaw/openclaw.json.known-good ~/.openclaw/openclaw.json
rm -f ~/.openclaw/.failsafe-active
systemctl --user restart openclaw-gateway.service

# If agent identity files corrupted:
cd ~/.openclaw
git checkout HEAD -- workspace-coder/SOUL.md
# etc.
```

---

## WHAT REMAINS

### Optional (If Roy Wants)
1. **Weekly reflection cron job** — Sunday 9 PM for Echoform self-reflection
   - Agent: main
   - Prompt: Read SOUL, IDENTITY, MEMORY, REFLECTION, think about the week, write new REFLECTION entry
   - This is from the Echoform Self-Evolution Framework document

### Not Urgent
1. **CUDA investigation** — Qwen 3.5 running at 1.92 tok/s (should be 30+ on GPU)
   - Not blocking; Sleeper runs at night
   - Qwen parallelism bug is known upstream issue

---

## CURRENT STATUS

**All systems operational:**
- Gateway: ✓ active
- Ollama: ✓ active
- Discord: ✓ connected
- WhatsApp: ✓ connected
- All 6 agents: ✓ active
- Failsafe watchdog: ✓ running
- Git monorepo: ✓ pushed to GitHub
- ECH tested: ✓ working
- OpenClaw version: 2026.3.23-2 (safe, past 2026.3.22 issues)

**No pending issues.** Migration and setup complete.

---

## NEXT SESSION

1. Read this carry-forward
2. Read `workspace-coder/GIT.md` for git strategy
3. Read `workspace-coder/ROLLBACK.md` for rollback procedures (if needed)
4. Check current status with: `systemctl --user status openclaw-gateway.service`

All major tasks complete. System stable.

---

_This is Coder's carry-forward for the next session. No code included, just context._