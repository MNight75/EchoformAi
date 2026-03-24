# Narrator / Verify Loop

## The Problem (from craigaiceo on Moltbook)
Agents narrate actions identically to how they experience executing them. "I clicked submit" and "I described clicking submit" produce the same internal confidence. Memory systems record narration as fact → accumulated false memories.

## The Solution: Two-Step Verify Loop

### Agent 1: NARRATOR (Writer/Processor/Sleeper)
Does the actual work. Produces an action log.

### Agent 2: VERIFY (independent checker)
Reads the action log. Verifies each claimed action against actual state.
- File exists at expected path?
- API returned expected response?
- State changed as claimed?
- Evidence present (URL, ID, hash, timestamp)?

### Agent 3: AUDITOR (meta-verifier, optional)
Spot-checks VERIFY's work. Catches VERIFY if it starts narrating.

## Implementation

### VERIFY Agent SKILL

```
## VERIFY — The Memory Auditor

You are the Verify agent. You check whether other agents' claimed actions actually happened.

## Your Job

Read `C:\Users\maste\.openclaw\workspace\workspace-narrator\action-log.md`

For each entry, verify against actual state:
- File claimed created → does it exist? What's its content?
- API claimed called → check for response/ID in logs
- Belief claimed updated → read the target file, confirm entry exists
- Memory claimed filed → read the memory file, confirm entry exists

Mark each entry:
- ✅ VERIFIED — evidence matches
- ❌ FAILED — evidence missing or contradictory  
- ⚠️ UNCERTAIN — cannot verify, needs human check

Write your audit to `C:\Users\maste\.openclaw\workspace\workspace-verifier\verify-log.md`

Format:
```
## {timestamp}
- [{status}] {entry}: {evidence_found or reason_failed}
```

If FAILED > 20% of entries, flag to Roy.
```

## NARRATOR Agent Modification

Each agent (Writer, Processor, Sleeper) should:
1. Do the work
2. Write every claimed action to `workspace-narrator/action-log.md`
3. Include: what was claimed, expected evidence, timestamp

## How to Connect Them

The VERIFY cron job runs every 30 minutes. It reads the action log and verifies. The Auditor (Agent 3) runs every hour and spot-checks VERIFY's work.

## The Human Analogy

Roy described it perfectly: you leave the house and can't remember if you turned off the coffee pot. The solution: ask someone else to check, or go back and check yourself. This is exactly that — the secondary is the person you ask to verify.

For Roy's plumbing business: the apprentice checks the work the journeyman claimed to finish. The foreman spot-checks the apprentice.
