# Koda Scout — A Claude Code Skill for Claude Design

A Claude Code skill that turns your Gmail inbox into an automated client intake pipeline for Claude Design.

Built by [@timkoda_](https://instagram.com/timkoda_) for solo AI studios, freelancers, and agencies running client work on Claude Design and Claude Code.

---

## What it does

When installed, this skill teaches Claude Code to:

- **Browse your Gmail inbox** via the Gmail MCP and detect incoming client briefs
- **Read the full email thread** and download every relevant attachment (brand decks, moodboards, style guides, reference images)
- **Extract the design brief** into a structured format: brand colors, typography, voice, deliverables, references, constraints, deadlines
- **Output a ready-to-paste block** for Claude Design at `claude.ai/design`
- **Flag open questions** when the client's email is missing critical info (so you ask the right follow-ups before designing)

The skill is **Layer 1 — the Intake** of the Solo AI Studio Stack:

```
Intake (this skill) → Design (Claude Design) → Ship (Claude Code)
```

---

## Install

### Option 1 — User-scope (available in every Claude Code project)

```bash
git clone https://github.com/timkoda/koda-scout.git ~/.claude/skills/koda-scout
```

Restart Claude Code. The skill loads automatically whenever you mention client briefs, email intake, or Claude Design input.

### Option 2 — Manual

```bash
mkdir -p ~/.claude/skills/koda-scout/references
curl -fsSL https://raw.githubusercontent.com/timkoda/koda-scout/main/SKILL.md \
  -o ~/.claude/skills/koda-scout/SKILL.md
curl -fsSL https://raw.githubusercontent.com/timkoda/koda-scout/main/references/brief-template.md \
  -o ~/.claude/skills/koda-scout/references/brief-template.md
```

---

## Prerequisites

- **Claude Code** installed (cli.anthropic.com)
- **Gmail MCP** connected to your Claude.ai account (goes through Claude.ai native Gmail integration)
- **Claude Design** access (included in Claude Pro, Max, Team, Enterprise plans)

---

## Usage

Once installed, just talk to Claude Code naturally:

> *"Extract the latest client brief from my inbox"*

> *"Pull the design brief from that Mercury Studios email and format it for Claude Design"*

> *"Parse the brand deck attached to yesterday's email with Kavy and structure it"*

Claude Code will query your Gmail, download attachments, parse the brief, and output a ready-to-paste block for `claude.ai/design`.

---

## The output structure

Every extracted brief follows a 7-section format (see `references/brief-template.md`):

1. **Project identity** — client name, project title, deadline, budget
2. **Brand system** — colors (hex), typography, voice, logo files
3. **Deliverables** — structured list ready for Claude Design
4. **References** — competitor sites, moodboard images, brand decks
5. **Constraints** — must-include, must-avoid, technical requirements
6. **Open questions** — what to ask the client before designing
7. **Claude Design input block** — copy-paste ready

---

## Why this exists

For the first time, AI creators can run a full design studio solo. Claude Design handles the designs. Claude Code ships the code. But the **intake step** — reading client emails, downloading attachments, parsing brand info — is still manual friction.

This skill kills that friction. Every client email becomes a structured design brief in seconds.

---

## Part of the Solo AI Studio Stack

This skill is one layer of a complete system:

- **Layer 1 — Intake**: this skill (Gmail → structured brief)
- **Layer 2 — Design**: Claude Design workspace (`claude.ai/design`)
- **Layer 3 — Ship**: Claude Code handoff bundle (live URL)

Full system walkthrough → [timkoda.com](https://timkoda.com) or comment "SOLO" on [@timkoda_](https://instagram.com/timkoda_) Instagram.

---

## Credits

Built and tested by [Tim Koda](https://instagram.com/timkoda_) — French AI creative director.

If this skill saves you time, [leave a tip](https://timkoda.com/tip) or follow for more creator AI systems.

---

## License

MIT — use it, fork it, remix it. Just keep the credit.
