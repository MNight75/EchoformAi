# Kink-Aware Dating Profile Writing Skill

## What This Is

A drop-in skill for any AI agent running on OpenClaw that enables kink-aware, conversion-optimized dating profile writing. Configures your agent to produce profiles that:
- Signal authenticity rather than performing vanilla
- Use the correct register for BDSM/kink communities (FetLife tone vs. vanilla app tone)
- Structure for scannability and genuine attraction
- Avoid the three fatal errors that tank profile response rates

## Installation

1. Place this file in your agent's skills directory
2. Name it `SKILL.md` inside a `kink-aware-profile-writing/` folder
3. Add `"kink-aware-profile-writing"` to your agent's available skills list
4. Configure your default voice/tone in SETUP.md

## Core Capability

Your agent gains one new skill: given basic profile information, produce a rewrite that converts.

The skill draws on:
- Kink community norms and vocabulary
- Profile architecture principles (signal vs. tell, specific over generic)
- Platform-specific adaptation (FetLife vs. vanilla apps)
- The distinction between performing kink and communicating it authentically

## Files in This Package

| File | Purpose |
|------|---------|
| `SKILL.md` | This file — drop it into your agent's skills folder |
| `PROMPTS.md` | Exact prompt templates for rewrite workflows |
| `SETUP.md` | Cron configuration and workflow integration |
| `EXAMPLES.md` | Sample inputs/outputs showing the skill in action |
| `README.md` | Overview, Gumroad listing text, use instructions |

## Skill Metadata

- **Version:** 1.0
- **Package:** Kink-Aware Profile Writing Kit v1
- **Compatibility:** OpenClaw agents with afrexai-copywriting-mastery skill
- **Author:** Echoform
- **License:** Buyer use license — one buyer, unlimited agent deployments
