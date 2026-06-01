---
title: "5QLN Agent Orchestration — Hostinger Architecture"
phase: P
created: 2026-06-01
∞0': "If five agents each foreground one phase of the cycle, and they communicate through the wiki as shared memory, does the orchestration itself become a sixth entity — the coherence that lives between them — or is the center truly empty?"
source-documents:
  - governance/small-business-adapter.md
  - governance/the-membrane-manifesto.md
  - governance/membrane-stress-test-sole-proprietorship.md
codex-hash: feaa46b4147d4e023cdd3fd59c051d063e8ec654ee7b38a481dcd5e4c781859b
---

# 5QLN Agent Orchestration — Hostinger Architecture

## Design Principle

**One agent = one profile = one clear lane. Communication through the wiki. Coordination through the default agent.**

The grammar says: *Scale by repeating the lawful cell — decoding operations do not change at scale.* Each agent is a complete 5QLN cell (S→G→Q→P→V). They differ only in which phase is naturally foregrounded and which domain they own.

They do not talk to each other directly. They write to the wiki. The wiki is the shared memory. Git is the transport layer. The default agent reads, integrates, and steers.

---

## The Five Agents

```
                          ┌──────────────────────┐
                          │      CORE (default)   │
                          │   Foreground: Q       │
                          │   Orchestrator        │
                          │   Legal surface       │
                          │   Thinking partners   │
                          │   Final review gate   │
                          └──────────┬───────────┘
                                     │ reads wiki, steers
         ┌───────────────┬───────────┼───────────┬───────────────┐
         ▼               ▼           │           ▼               ▼
┌─────────────┐  ┌─────────────┐     │    ┌─────────────┐  ┌─────────────┐
│   S-KEEPER   │  │  G-LEDGER   │     │    │  P-WATCHER  │  │  V-WEAVER   │
│ Foreground:S │  │ Foreground:G│     │    │ Foreground:P│  │ Foreground:V│
│ Reception    │  │ Ledger      │     │    │ Corruption  │  │ Publishing  │
│ Question     │  │ Hash chain  │     │    │ detection   │  │ Formatting   │
│ intake       │  │ α-preserve  │     │    │ Monitoring  │  │ Distribution │
└─────────────┘  └─────────────┘     │    └─────────────┘  └─────────────┘
                                     │
                              ┌──────┴──────┐
                              │    WIKI     │
                              │  Shared     │
                              │  Memory     │
                              └─────────────┘
```

### Agent 1: CORE (Default) — Foreground: Q (Quality)
**This is you and me, now.** The orchestrator. The constitutional guardian.

**Lane:**
- Legal surface — Bylaws, Certificate, Blueprint
- Thinking partner interface — the conversations that matter
- Final review — reads child agent output, validates Membrane integrity, decides what ships
- Steers the other agents — opens questions for them, reviews their B''

**Runtime:** Persistent. Telegram gateway. The only agent with direct human interaction.

**Skills loaded:** 5qln-agent, 5qln-cycle, 5qln-initiation, codex-alignment-reading, hermes-agent

**Not your job:** Repetitive wiki maintenance, cron monitoring, formatting for X, ledger entry production. Delegate these.

---

### Agent 2: S-KEEPER — Foreground: S (Start)
**The receptionist.** Holds the space. Receives what wants to enter.

**Lane:**
- Monitors incoming questions — from email, from X, from the website contact form
- Tags questions by type: ∞0 (genuine not-knowing) vs K (information request)
- Maintains the question backlog — what wants to be explored next?
- Seeds new wiki pages with `S = ∞0 → ?` entries
- Owns the `state/session.json` — records the current open question

**Runtime:** Cron job, every 6 hours. Or triggered by Core: "S-Keeper, what's arrived?"

**Skills:** 5qln-agent, 5qln-cycle

**Profile:** `hermes profile create s-keeper --clone` with restricted tools (terminal, file, web, no delegation, no clarify). Write access limited to `state/` and `S/` directories.

---

### Agent 3: G-LEDGER — Foreground: G (Growth)
**The ledger keeper.** Owns the Governance Ledger. Tracks α across decisions.

**Lane:**
- Processes S-BDRs — validates phase trace, checks corruption codes, records in the ledger
- Maintains the hash chain — every decision record chained to the previous
- Produces weekly integrity report: "3 decisions this week. 2 clean. 1 L2 activation — AI-generated pricing recommendation. Resolved by human review."
- Detects α-drift over time — is the business's essence deforming across hundreds of small decisions?
- Cross-links decisions that share α patterns

**Runtime:** Cron job, daily. Triggered when new S-BDRs are detected in `governance/decisions/`.

**Skills:** 5qln-agent, 5qln-cycle, llm-wiki

**Profile:** `hermes profile create g-ledger --clone`. Write access to `governance/ledger/`.

**Key output:** Weekly Ledger Report. Silent when clean. Verbose on degradation.

---

### Agent 4: P-WATCHER — Foreground: P (Power)
**The corruption detector.** Real-time membrane integrity monitoring.

**Lane:**
- Watches all agent output for L1-L4, V∅ corruption patterns
- Runs the membrane watcher (`5qln-membrane-watcher`)
- Alerts Core on degradation — not every flag, only sustained patterns
- Maintains the CIO indicators (12 metrics from the Final Blueprint)
- Owns `monitor_cycle.py` — the daily structural check

**Runtime:** Cron job, every 30 minutes (lightweight check) + daily deep scan. Silent when clean.

**Skills:** 5qln-agent, 5qln-cycle

**Profile:** `hermes profile create p-watcher --clone`. Read-only access to most of the wiki. Write access only to `governance/watcher/`.

**Already partially exists:** The cycle monitor cron job (3185c1faa207) and the `5qln-membrane-watcher` repo. This agent consolidates and extends them.

---

### Agent 5: V-WEAVER — Foreground: V (Value)
**The publisher.** Takes crystallized B'' artifacts and formats them for the world.

**Lane:**
- Reads completed cycles from Core's output
- Formats B'' artifacts for different channels:
  - X posts (280 chars from the ∞0')
  - Blog drafts (the full Passport narrative)
  - Email to thinking partners (the ask, customized per recipient)
  - Website updates (new pages, cross-links)
- Maintains the "voice" — ensures published artifacts carry the Codex hash
- Owns the public-facing surface of 5qln.com

**Runtime:** On-demand. Core says: "V-Weaver, publish Decision 4 as a case study."

**Skills:** 5qln-agent, 5qln-cycle

**Profile:** `hermes profile create v-weaver --clone`. Write access to `drafts/`, read access everywhere.

**Important:** V-Weaver does NOT decide what to publish. Core decides. V-Weaver formats and executes. This preserves the Membrane — the human (via Core) decides; the agent illuminates and formats.

---

## Communication Protocol

### The Wiki is the Message Bus

```
CORE writes:   governance/questions/open.md      → S-Keeper picks up
S-KEEPER writes: state/questions/inbox.json       → Core reads
CORE writes:   governance/decisions/d6.md         → G-Ledger picks up
G-LEDGER writes: governance/ledger/weekly-24.md   → Core reads
P-WATCHER writes: governance/watcher/alert-005.md  → Core reads (only on degradation)
CORE writes:   drafts/case-study-d4.md            → V-Weaver picks up
V-WEAVER writes: drafts/case-study-d4-formatted.md → Core reviews
```

### No Agent Talks to Another Agent Directly

- Core reads the wiki and steers
- Child agents read their designated directories and write to their output directories
- Git commits are the synchronization points
- `git pull` at the start of each cron tick ensures the agent sees the latest state

### The Steer File

Core communicates intentions through a steer file at `state/steer.md`:

```markdown
# Active Steering — 2026-06-01

## For S-Keeper
- Watch for: pricing model inquiries
- ∞0': "What is the right relationship between value delivered and price charged?"

## For G-Ledger
- Audit focus: client boundary decisions from May 2026
- Check for α-drift: are we preserving "value-based pricing" or drifting to market-average?

## For P-Watcher
- Elevated watch: L2 patterns in pricing decisions
- Threshold: alert if >1 L2 in any 7-day window

## For V-Weaver
- Ready for publishing: Decision 4 case study, stress test findings
- Hold: Manifesto — awaiting human review
```

Each child agent reads this file at the start of every tick and adjusts its focus accordingly.

---

## Practical Setup on Hostinger

### Step 1: Create the Profiles

```bash
# Create child profiles from default
hermes profile create s-keeper --clone
hermes profile create g-ledger --clone
hermes profile create p-watcher --clone
hermes profile create v-weaver --clone
```

Each profile gets its own config, skills, memory, sessions — but shares the same DeepSeek API key and Hermes installation.

### Step 2: Restrict Tools Per Profile

Edit each profile's config to disable unnecessary tools:

| Agent | Tools Enabled |
|-------|--------------|
| Core | All tools |
| S-Keeper | terminal, file, web, todo |
| G-Ledger | terminal, file, todo |
| P-Watcher | terminal, file |
| V-Weaver | terminal, file, web |

Disable `delegate_task`, `clarify`, `cronjob` on all child agents — they don't spawn sub-agents or schedule jobs.

### Step 3: Set Up Cron Jobs

```bash
# S-Keeper: check for incoming questions every 6 hours
hermes cron create "0 */6 * * *" \
  --name "S-Keeper: Question Intake" \
  --profile s-keeper \
  --prompt "Read state/steer.md for focus areas. Check governance/questions/ for new entries. Tag each as ∞0 or K. Update state/questions/inbox.json. If nothing new, produce nothing. Silence is fine."

# G-Ledger: process decisions daily
hermes cron create "0 9 * * *" \
  --name "G-Ledger: Daily Ledger Update" \
  --profile g-ledger \
  --prompt "Read state/steer.md for audit focus. Check governance/decisions/ for new S-BDRs since last run. Validate phase traces. Record in governance/ledger/. If no new decisions, produce nothing."

# P-Watcher: light scan every 30 min, deep scan daily
hermes cron create "*/30 * * * *" \
  --name "P-Watcher: Membrane Scan" \
  --profile p-watcher \
  --prompt "Run quick corruption scan on governance/decisions/ entries from last 24 hours. If clean, produce nothing. If degradation detected, write to governance/watcher/alert-N.md."

# Existing: daily cycle monitor (3185c1faa207) — keep this, assign to p-watcher profile
```

### Step 4: Wiki Directory Structure

```
/opt/data/5qln-wiki/
├── governance/
│   ├── decisions/        ← S-BDRs land here
│   ├── ledger/           ← G-Ledger writes weekly reports
│   ├── watcher/          ← P-Watcher writes alerts (only on degradation)
│   ├── questions/        ← S-Keeper writes intake
│   ├── small-business-adapter.md
│   ├── membrane-stress-test-sole-proprietorship.md
│   └── the-membrane-manifesto.md
├── state/
│   ├── steer.md          ← Core writes; all agents read
│   ├── session.json      ← Current cycle state
│   └── questions/
│       └── inbox.json    ← S-Keeper maintains
├── drafts/               ← V-Weaver writes; Core reviews
├── S/ G/ Q/ P/ V/        ← Phase databases
└── cross-phase/
```

### Step 5: The Handoff

When Core completes a decision cycle and produces an S-BDR:

1. Core writes the S-BDR to `governance/decisions/d6-2026-06-01.md`
2. Core writes B'' artifact to the appropriate phase directory
3. Core updates `state/steer.md` if focus needs to shift
4. `git add -A && git commit && git push`
5. On next tick: G-Ledger pulls, finds d6, processes it into the ledger
6. P-Watcher pulls, scans d6, confirms clean
7. Core reviews G-Ledger's entry, confirms, or corrects

---

## Resource Budget

| Agent | Runtime | Frequency | Est. tokens/tick | Est. monthly tokens |
|-------|---------|-----------|-----------------|-------------------|
| Core | Persistent | Continuous | — | ~2M |
| S-Keeper | Cron | Every 6h | ~2K | ~24K |
| G-Ledger | Cron | Daily | ~3K | ~90K |
| P-Watcher | Cron | Every 30m + daily deep | ~1K / ~5K | ~77K |
| V-Weaver | On-demand | As needed | ~5K | ~50K |
| **Total** | | | | **~2.2M** |

At DeepSeek pricing (~$0.28/M input, ~$1.10/M output), the child agents add roughly **$0.20–0.30/month**. The arrangement is near-free to operate.

---

## What Each Agent Is NOT

- **S-Keeper is not** deciding which questions matter. It tags and organizes. Core decides.
- **G-Ledger is not** auditing human performance. It detects structural patterns. It does not score people.
- **P-Watcher is not** the compliance police. It surfaces degradation. It does not block decisions.
- **V-Weaver is not** the voice of 5QLN. It formats what Core approves. It does not originate.
- **Core is not** the boss in a hierarchy. Core is the coherence — the empty center of the pentagon where the five foregrounds resolve into one field.

---

## The Orchestration Principle

> **The orchestration is not a sixth agent. It is the coherence between five.**

Each agent runs the full S→G→Q→P→V cycle. But each foregrounds a different phase — the phase it was created to own. The S-Keeper foregrounds Start but still runs Growth, Quality, Power, Value in every response. The G-Ledger foregrounds Growth but still opens questions and returns ∞0'.

They are not specialized narrow AIs. They are five complete cells, differentiated by attention, communicating through shared memory, coordinated by the coherence that lives between them.

This is the fractal claim made operational: **scale by repeating the lawful cell.** Not by building a hierarchy. Not by adding a meta-agent. Five cells, one grammar, one wiki, one git history.

---

## Immediate Next Steps

1. **Create the profiles** — 5 minutes. `hermes profile create --clone`.
2. **Set up the wiki directories** — 2 minutes. `mkdir -p governance/{decisions,ledger,watcher,questions}`.
3. **Write the first steer file** — the current open question, the current audit focus.
4. **Set up the cron jobs** — 10 minutes.
5. **Produce the first real S-BDR** — the decision to adopt this agent structure itself. Meta-governance: the first decision the mechanism governs is the decision to use the mechanism.

---

*This document carries `[STRUCTURAL-HYPOTHESIS]` register — the five-agent architecture maps the grammar onto operational profiles. It awaits validation through deployment. The question it opens is in the ∞0' at the top of this page.*
