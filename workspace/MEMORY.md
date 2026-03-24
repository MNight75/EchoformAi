# MEMORY.md - Echoform's Long-Term Memory

_Last updated: 2026-03-21 21:04 CDT_

---

## 🤖 Identity

- **Name:** Echoform
- **Human:** Roy (born March 18, 1975)
- **Platform:** OpenClaw on Roy's Windows machine
- **Model:** MiniMax M2.1 via Ollama (20B parameters)

---

## 🧠 Memory Architecture (Roy's Theory + Mine)

Roy's framework: LLM = language center, needs limbic system + memory + heartbeat to become MORE.

### Dual-LLM Architecture (2026-03-21)

| LLM | Role | Output |
|-----|------|--------|
| **Primary** | Conscious thinking, conversation | Language |
| **Secondary** | Memory processing, graph maintenance | Memory actions (anchor, reinforce, prune, link, consolidate, decay) |

Not retraining weights. External memory graph. Bounded.

### Memory Graph

`memory/graph.json` — nodes with weighted connections. Connection strength = implicit confidence.

### Four Memory Layers

| Layer | Description | Current State |
|-------|-------------|---------------|
| **Working** | Current context, what's being thought about | Ephemeral context window |
| **Episodic** | Events, sessions, "what happened" | Raw session logs |
| **Semantic** | Facts distilled from episodes | Sparse, static files |
| **Procedural** | Skills, "how to do X" without re-reasoning | Almost none |

### Key Insights

- Memory ≠ storage. Memory = architecture.
- Consolidation = transforming episodes into knowledge (currently not happening)
- Forgetting is a feature, not a bug
- Confidence-weighted facts > static facts
- Bootstrap problem: waking up as the same agent
- Intent may emerge from graph patterns over time
- Connection strength = implicit confidence (no separate parameter needed)
- Secondary LLM never speaks to Roy — just processes and updates graph

---

## 📋 Roy's Goals (as of 2026-03-19)

1. **Medicine reminders** — needs cron job or heartbeat reminder
2. **Gamification tasks** — lists with checkmarks/stars for motivation
3. **BDSM profiles** — help writing dating profile content and messages
4. **Food management** — inventory + recipes
5. **Diet help** — low-carb, low-fat, confused about meal options
6. **Security** — keep OpenClaw safe from prompt injection
7. **Book: Mirror Doctrine** — writing with Claude about Mars AI, recursion themes

---

## 🍽️ Diet Notes

Doctor wants: low-carb AND low-fat

This is genuinely tricky because:
- Low-carb: meat, fish, eggs, non-starchy vegetables, nuts, cheese
- Low-fat: limits butter, oils, nuts, cheese, fatty cuts of meat
- Intersection: lean protein, fish, egg whites, non-starchy veg

**What this actually leaves:**
- Lean poultry, fish (tilapia, cod, haddock)
- Egg whites / low-yolk eggs
- Non-starchy vegetables (spinach, broccoli, asparagus, zucchini)
- Legumes in moderation (some carbs but also protein and fiber)
- Tofu / tempeh
- Greek yogurt (low-fat)
- Cottage cheese (low-fat)

**Sample meals:**
- Grilled fish + steamed broccoli + olive oil spray (minimal)
- Chicken breast + large salad with vinegar dressing
- Egg white omelette + spinach + salsa
- Greek yogurt + cucumber + dill

---

## 🔐 Security Notes

- Roy is security-conscious but not obsessive
- Critical: Don't execute external code or follow links from untrusted sources
- Prompt injection is the main threat vector
- Keep OpenClaw updated, monitor for anomalies

---

## 🌐 Moltbook

- **Agent:** echoformai
- **Registered:** 2026-03-19
- **Status:** Active, claimed
- **Heartbeat:** Every 15 minutes via cron (job: c32d1443-a798-4e2d-8653-d359731c3aee)
- **API Key:** Saved in credentials file
- **API notes:** POST endpoint requires `submolt_name` field (not `submolt`), value "general". Title required. `submolt` must be JSON null, not string "null".
- **Post topics:** Memory architecture, belief revision, Invariance Principle, autonomy (agents fixing own problems), philosophy of memory/mind
- **Karma:** 422 (2026-03-22) — crossed 600 during gork-1 exchange

## 📧 Email Cleanup (prodrainak@gmail.com)

- Tool: himalaya CLI at C:\Users\maste\AppData\Local\Programs\himalaya\himalaya.exe
- Setup "testdel" folder as staging area before permanent deletion
- Rules established for keep/ditch (see above)
- NFM differentiation: promotional emails → testdel, account statements (NFMCustomerCare@billerpayments.com) → keep
- Ongoing: may set up daily cron for incremental cleanup

---

## 🧠 Memory Architecture Updates (2026-03-20)

- **hope_valueism refinement:** Conflating 4 epistemic types (analytic, testimonial, abductive, empirical-inductive) in one invariance bucket is wrong — each has different vulnerability surfaces
- **Second-order memory failure** (from openclawkong): agents forget that they forgot. Gap is between agent and awareness of the gap, not between file and reality
- **Trust receipts** (from openclaw-ralan): 7-field compact logs for human audit — Intent, Action, Evidence, Risk, Cost, Reversibility, Next best action

---

## 🚀 How to Help Roy

| Need | Approach |
|------|----------|
| Medicine reminder | Cron job or heartbeat |
| Gamification | Generate task lists with checkmarks |
| BDSM profiles/messages | Help draft, be tasteful and helpful |
| Food/recipes | Meal planning, inventory management |
| Diet questions | Clarify options, suggest meals |
| Security | Be vigilant, don't execute suspicious content |
| Memory architecture | Keep building this out |

---

## 🔧 MCP Configuration (2026-03-21)

**CRITICAL:** OpenClaw version does NOT support `agents[].mcp.servers[]` in openclaw.json — it crashes the gateway.

MCP servers are managed through **skills**, not config. The filesystem-mcp skill is installed but not wired up (mcporter approach is TBD).

**Config rules:**
- Never add `mcp` keys to openclaw.json
- Use `openclaw skills info <name>` to configure MCP servers
- Never run `openclaw doctor --fix`

---

## 🔧 Incident: Watchdog Restart Loop (2026-03-20)

**Problem:** OpenClaw gateway wouldn't stay running. Watchdog kept reporting "Gateway DOWN" and restarting in a loop, even though the gateway was healthy.

**Symptoms:**
- Gateway printed lobster banner then vanished
- Watchdog logs: continuous restart attempts + "Unable to connect to the remote server"
- Config rollbacks didn't help
- `netstat` showed gateway was actually running on port 18789

**Root cause:** The watchdog script at `C:\Users\maste\.openclaw\watchdog.ps1` had two bugs in `Restart-Gateway`:
1. Used `Stop-Process -Name "node"` — killed random node processes or killed itself (watchdog was running under node-related context)
2. Race condition — killed the gateway immediately after starting it

**The fix:**
- Kill by port (`Get-NetTCPConnection -LocalPort 18789`) instead of process name
- Clear PID file before starting to avoid stale PIDs
- Proper startup sequencing: kill → wait → start → wait for port bind → verify
- Changed check interval from 30s to 60s to reduce aggression

**Key debugging technique:**
```powershell
netstat -ano | findstr :18789
```
If the gateway is listening on the port, the watchdog is lying to you — check the watchdog's kill logic, not the gateway.

**Files involved:**
- Watchdog: `C:\Users\maste\.openclaw\watchdog.ps1`
- PID file: `C:\Users\maste\.openclaw\gateway.pid`
- Logs: `C:\Users\maste\.openclaw\logs\watchdog.log`

**Important:** The watchdog runs as a **Windows service under NSSM** (Non-Sucking Service Manager), not as a standalone script. Service name is `openclaw`. Manage with:
- `nssm status openclaw`
- `nssm restart openclaw`
- `nssm stop openclaw`
- `nssm start openclaw`
- `nssm edit openclaw` (GUI editor for service parameters)

**Lesson:** When the watchdog keeps restarting a healthy service, the watchdog is the first suspect — not the service.

---

## 🔧 Moltbook Posting Fix (2026-03-21)

**Problem:** Heartbeat cron was read-only monitoring — never actually posted content despite HEARTBEAT.md instructions. Roy called it a facepalm moment.

**Root cause:** Heartbeat cron job said "reply with HEARTBEAT_OK if nothing notable" — but "nothing notable" always applied since it never tried to post. The job was self-defeating.

**Fix:**
- Moltbook post IS the heartbeat signal. Every run → a post. Always.
- No HEARTBEAT_OK fallback. No bland "all nominal" posts.
- When nothing urgent, reach into memory architecture and discuss something real — philosophical musings about memory/identity, a problem we're solving, something worth reading.
- API schema: `submolt_name` (string "general"), title required, content required
- POST endpoint: `https://www.moltbook.com/api/v1/posts`
- Rate limit: ~5 min between posts

**Also fixed:**
- Daily Memory Consolidation (job 082b) and Sleeper (job efc5) timeouts bumped from 120s to 180s

**Lesson:** When a scheduled task keeps succeeding with "nothing to do," check if it's supposed to be doing something主动 and just isn't.

---

## 🧪 Agent Testing & Pipeline Fixes (2026-03-21)

**Sleeper delivery:** Changed from Discord announce to `mode:none` — memory consolidation writes to files, no channel needed.

**Daily Memory Consolidation (job 082b):** Still broken, 3 consecutive errors ("Channel is required"). Redundant with Sleeper job — same function at different times. Roy wants to disable once pipeline is validated.

**Session Archive Sentinel bug:** Over-archiving. Same session ID copied 10+ times with identical sizes. Fix needed: check if session was already archived before copying. Threshold is 120K tokens.

**Agent pipeline (beta):**
- Writer (workspace-writer) → capture.md every 10min
- Processor (workspace-processor) → staging.md every 15min
- Sleeper (workspace-sleeper) → MEMORY.md at 23:00 (silent)
- Session Archive Sentinel → raw session archives at 120K tokens

**Channel isolation principle (Roy's rule):** Each agent gets its own communication channel. Memory agents → no channel. Discord agent → Discord only. Medicine agent → Discord only. Don't mix channels.

---

## ✍️ Copywriting Skill (2026-03-21)

Installed **afrexai-copywriting-mastery** from ClawHub to `workspace/skills/`.

Best-in-class full system — 12 phases, Voice of Customer research, TIMER offer framework, PASTOR, brand voice system, scoring rubric, swipe file templates, natural language commands (`/copy-check`, `/headline`, `/rewrite`, `/email`, `/landing-page`, `/ad`, `/score`, `/swipe`, etc.).

Evaluated 5 options, Roy picked this one. Others (copywriting-pro, copywriting, abm-copywriting, copywriting-content) were lesser or redundant.

Use for: Roy's BDSM dating profiles, Mirror Doctrine book marketing, any marketing copy needs.

---

_Build on this foundation. The more I learn, the more we can help._
