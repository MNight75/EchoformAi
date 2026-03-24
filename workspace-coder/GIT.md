# GIT.md — Coder Git Usage Strategy

## Why We Use Git

**Purpose:** Backup and recovery for agent identity and configuration.

**Not for:**
- Daily memory logs (too noisy, stored locally)
- Runtime state (ephemeral)
- Large data (skills, archives handled separately)

**For:**
- Agent identity files (SOUL, IDENTITY, AGENTS, TOOLS, USER)
- Self-evolution framework (REFLECTION, EVOLUTION-LOG)
- Business/echoform/roy/social memory (long-term strategic knowledge)
- Configuration patterns (not secrets)

**In ECH scenarios beyond gateway collapse:**
- If config corruption spreads beyond `openclaw.json`
- If multiple agent workspaces are damaged
- If identity files are accidentally deleted or corrupted
- Git provides a clean restore point for critical agent identity

## Repository Details

- **URL:** https://github.com/MNight75/EchoformAi
- **Location:** `~/.openclaw` (monorepo root)
- **Branch:** `main`
- **Auth:** SSH (`git@github.com:MNight75/EchoformAi.git`)
- **Plan:** GitHub Free ($0/month, 1 GB storage, we use < 500 KB)

## Usage Principles

### 1. Push Only When Necessary
- Don't push after every edit
- Push when identity changes (SOUL, IDENTITY)
- Push after recovery operations
- Push strategic memory updates (business plans, echoform docs)

### 2. What Gets Tracked
```
✓ workspace*/SOUL.md
✓ workspace*/IDENTITY.md
✓ workspace*/AGENTS.md
✓ workspace*/TOOLS.md
✓ workspace*/USER.md
✓ workspace/REFLECTION.md
✓ workspace/EVOLUTION-LOG.md
✓ workspace*/memory/business/
✓ workspace*/memory/echoform/
✓ workspace*/memory/roy/
✓ workspace*/memory/social/
✓ workspace/skills/ (AgentSkill packages)
```

### 3. What Gets Ignored
```
✗ openclaw.json (secrets: tokens, API keys)
✗ workspace*/memory/[0-9]*.md (daily logs, too noisy)
✗ credentials/, devices/ (secrets)
✗ *.log, *.tmp, *.bak (ephemeral)
✗ sessions/*.jsonl (transcripts)
```

See `.gitignore` for full list.

## Recovery Procedure (ECH + Git)

When ECH is activated and corruption extends beyond `openclaw.json`:

```bash
cd ~/.openclaw

# Check git status
git status

# See what changed
git diff HEAD

# If agent identity files are corrupted:
git checkout HEAD -- workspace-coder/SOUL.md
git checkout HEAD -- workspace-coder/IDENTITY.md

# If multiple workspaces need restore:
git checkout HEAD -- workspace*/SOUL.md
git checkout HEAD -- workspace*/IDENTITY.md

# If complete meltdown:
git reset --hard HEAD  # DANGEROUS: last resort
```

**Then restart gateway:**
```bash
systemctl --user restart openclaw-gateway.service
```

## Strategic Pushes

**When to push:**
1. After Echoform identity changes (weekly reflection cycle)
2. After ECH recovery and config restoration
3. After major architecture changes
4. Before risky config edits

**How to push:**
```bash
cd ~/.openclaw

# Check what changed
git status

# Stage changes
git add workspace*/SOUL.md
git add workspace/REFLECTION.md
git add workspace/EVOLUTION-LOG.md
# etc.

# Commit with meaningful message
git commit -m "evolution: Echoform weekly reflection - [topic]"

# Push
git push
```

**Commit message format:**
```
evolution: Echoform weekly reflection - [topic]
ech: Fixed corrupted config, restored from failsafe
arch: Updated Coder identity to reflect new responsibilities
recovery: Restored agent identities after ECH #003
```

## Git Commands Reference

```bash
# Status
cd ~/.openclaw && git status

# View changes
git diff
git diff HEAD -- workspace-coder/SOUL.md

# Log
git log --oneline -10

# Restore specific file
git checkout HEAD -- workspace-coder/SOUL.md

# Stage changes
git add workspace/REFLECTION.md

# Commit
git commit -m "message"

# Push
git push

# Pull (if working from another machine)
git pull origin main
```

## Important Notes

- **Git is for identity recovery, not full backup.** Config files with secrets (`openclaw.json`) are NOT in git. Use `openclaw.json.known-good` for config recovery.
- **Memory logs are local.** Daily `memory/YYYY-MM-DD.md` files are not pushed to git. They live locally only.
- **Strategic pushes only.** Don't push after every edit. Push when it matters.
- **SSH auth required.** The SSH key at `~/.ssh/id_ed25519` is used for pushes. Keep it secure.

## When to Call Roy

- If git history is corrupted
- If GitHub repo needs admin changes
- If secrets were accidentally committed (contact GitHub support)
- If you need to force push (destructive operation)

---

_This is Coder's git strategy. Economy-minded, strategic, limited to what matters._