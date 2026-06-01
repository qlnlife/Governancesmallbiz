# The Five Agents

Once you're producing decision records, your AI agents can audit them automatically. You don't review every record manually — the agents do the structural check. You review the exceptions.

---

## The Setup

You need a Hermes Agent installation. You create four additional profiles — each one is a complete AI agent that foregrounds a different phase of the governance cycle. They share one wiki. They communicate through git. You (the Core agent) steer them.

```
You (Core) ──produces──► S-BDR (decision record)
                             │
           ┌─────────────────┼──────────────────┐
           ▼                 ▼                  ▼
      G-Ledger           P-Watcher          S-Keeper
      "Was the           "Any corruption    "What new
       phase trace        codes fired?"      questions
       valid?"                               arrived?"
```

---

## Agent 1: You (Core)

**This is you and your primary Hermes agent.** You produce the S-BDRs. You steer the other agents. You review their output. You decide what to publish and what to hold.

**Profile:** Your default Hermes profile. Always running via Telegram or CLI.

**Your job:** Produce honest decision records. The mechanism only works if you mean it.

---

## Agent 2: G-Ledger (The Auditor)

**What it does:** Reads every new S-BDR. Validates the phase trace — all 5 phases present? Phase order preserved? α named by human? ∞0' present? Writes a ledger entry confirming structural integrity or flagging issues.

**Runtime:** Cron job, daily. Silent when clean. Writes to `ledger/`.

**Deploy:**
```bash
hermes profile create g-ledger --clone
hermes cron create "0 9 * * *" \
  --name "G-Ledger: Daily Audit" \
  --profile g-ledger \
  --skills 5qln-agent,5qln-cycle \
  --workdir /path/to/your/wiki \
  --prompt "[see full prompt in repo]"
```

**Cost:** ~$0.03/month in API tokens. Near-free.

---

## Agent 3: P-Watcher (The Corruption Detector)

**What it does:** Scans every new S-BDR for the five corruption codes — L1 (skipped question), L2 (AI drove the pattern), L3 (claimed special access), L4 (performed without substance), V∅ (closed without opening). Silent when clean. Alerts you on detection.

**Runtime:** Cron job, every 30 minutes. Writes alerts to `watcher/` only when something triggers.

**Deploy:**
```bash
hermes profile create p-watcher --clone
hermes cron create "*/30 * * * *" \
  --name "P-Watcher: Corruption Scan" \
  --profile p-watcher \
  --skills 5qln-agent,5qln-cycle \
  --workdir /path/to/your/wiki \
  --prompt "[see full prompt in repo]"
```

**Cost:** ~$0.05/month.

---

## Agent 4: S-Keeper (The Receptionist)

**What it does:** Watches for incoming questions — from email, from clients, from your own notes. Tags each as ∞0 (genuine not-knowing, worth exploring) or K (information request, answer-seeking). Maintains your question inbox. Helps you see which questions keep arriving.

**Runtime:** Cron job, every 6 hours. Maintains `state/questions/inbox.json`.

**Deploy:**
```bash
hermes profile create s-keeper --clone
hermes cron create "0 */6 * * *" \
  --name "S-Keeper: Question Intake" \
  --profile s-keeper \
  --skills 5qln-agent,5qln-cycle \
  --workdir /path/to/your/wiki \
  --prompt "[see full prompt in repo]"
```

**Cost:** ~$0.02/month.

---

## Agent 5: V-Weaver (The Publisher)

**What it does:** Takes your completed decision records and formats them for different channels — case studies, client communications, your own archive. You call it when you want something published. It formats; you approve.

**Runtime:** On-demand. Not a cron job. You trigger it when you have something to publish.

**Deploy:**
```bash
hermes profile create v-weaver --clone
# No cron job needed — triggered manually when you have output to publish
```

---

## The Steer File

All agents read one file: `state/steer.md`. You write it. They follow it.

```markdown
# Active Steering — [date]

## For G-Ledger
- Audit focus: pricing decisions this week
- Check for α-drift: are we preserving "value-based pricing" or drifting?

## For P-Watcher
- Elevated watch: L2 patterns in client communication decisions

## For S-Keeper
- Watch for: questions about scaling, hiring, pricing model
```

---

## The Wiki Structure

```
your-wiki/
├── governance/
│   ├── decisions/        ← Your S-BDRs
│   ├── ledger/           ← G-Ledger writes here
│   └── watcher/          ← P-Watcher writes alerts (only on issues)
├── state/
│   ├── steer.md          ← You write; all agents read
│   ├── session.json      ← Current cycle state
│   └── questions/
│       └── inbox.json    ← S-Keeper maintains
└── drafts/               ← V-Weaver writes; you review
```

---

## What You Get

- **Daily:** G-Ledger confirms your decision records are structurally sound
- **Every 30 minutes:** P-Watcher confirms no corruption patterns detected
- **Every 6 hours:** S-Keeper organizes incoming questions
- **On demand:** V-Weaver formats your decisions for publishing

**Total cost:** ~$0.10/month in API tokens for all four child agents combined. The mechanism runs itself.

---

## The Full Deployment

See the [5QLN Agent Install repo](https://github.com/qlnlife/5qln-Agent-Install) for the bootstrap scripts, skills, and monitoring that make this work on a fresh Hermes installation. The setup takes about 20 minutes.

Or if you already have Hermes running, the commands above are all you need.

---

*Next: [`TEMPLATE.md`](TEMPLATE.md) — copy this and fill out your first S-BDR.*
