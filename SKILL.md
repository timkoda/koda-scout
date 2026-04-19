---
name: koda-scout
description: "Koda Scout — the AI intake scout for Claude Design. Browses your Gmail inbox, detects incoming client briefs, and extracts the full design brief (brand system, references, constraints, style guides, deliverables) into a structured output ready to paste into Claude Design. Uses the Gmail MCP to read emails + attachments. Use this skill whenever a solo AI studio receives a new client email and needs a design brief formatted for Claude Design. Triggers on: 'koda scout', 'scout my inbox', 'extract brief', 'client brief', 'new client email', 'pull brief from inbox', 'design brief from email', 'parse client', 'brand brief extract', 'gmail brief', 'claude design brief', 'client intake'."
---

# Koda Scout — AI Intake Scout for Claude Design

Koda Scout turns your Gmail inbox into an automated client intake pipeline for Claude Design. Every client email becomes a structured design brief, ready to paste into Claude Design with one click.

Built for solo AI studios, freelancers, and agencies running client work on the Claude stack.

---

## When to use

- A new client email lands with a design brief, brand deck, or reference files
- You want to start a Claude Design project and need the full brief extracted from an email thread
- You want to auto-generate the design prompt for Claude Design from a client's existing materials
- A prospect pings you with "here's what we need" and you need to ship a first draft fast

---

## The Workflow

### Step 1 — Scout the inbox

Use the Gmail MCP to list recent unread messages, or search by sender / subject.

```
mcp__claude_ai_Gmail__gmail_search_messages({
  q: "from:<client_domain> OR subject:(brief OR project OR design OR campaign) newer_than:7d",
  maxResults: 10
})
```

Common queries:
- `from:<client_domain> has:attachment newer_than:14d` — emails with attached brand decks
- `subject:(brief OR RFP OR project) is:unread` — new project intakes
- `"brand guidelines" OR "style guide" OR "moodboard"` — style reference emails

### Step 2 — Read the client email + attachments

For each relevant message, read the full thread:

```
mcp__claude_ai_Gmail__gmail_read_message({ messageId: "<id>" })
mcp__claude_ai_Gmail__gmail_read_thread({ threadId: "<id>" })
```

Download attachments to a project folder:
- Brand decks (PDF, PPTX) → `projects/client-<name>/brief/`
- Reference images → `projects/client-<name>/refs/`
- Style guides (DOCX) → `projects/client-<name>/brief/`
- Existing website URLs → note them for Claude Design web capture

### Step 3 — Extract the brief into structured output

Parse the email body + attachments and output a structured brief using the template in `references/brief-template.md`.

### Step 4 — Format for Claude Design

Paste the structured brief into Claude Design's input field. Attach all reference files (images, brand decks). Point Claude Design at the client's website URL if available (web capture tool).

The output is Claude Design ready with:
- Full project description
- Brand system (colors, typography, tone)
- Reference materials
- Deliverables list
- Constraints + deadlines

---

## The Output Structure

Every extracted brief follows this structure (see `references/brief-template.md` for the full template):

### Project identity
- Client name
- Project title
- Deadline
- Budget (if mentioned)

### Brand system
- Primary colors (hex codes extracted from brand deck or logo analysis)
- Typography (fonts explicitly named, or inferred from brand deck)
- Voice / tone (from existing website copy or brief)
- Logo files location

### Deliverables requested
Explicit list of what the client wants shipped. Common formats:
- Landing page
- Pitch deck
- Brand kit
- Social campaign (IG posts, stories, carousels)
- Email template
- Prototype / app UI

### References provided
- Competitor websites mentioned
- Moodboard images
- Existing brand assets
- Inspiration links

### Constraints
- Must-include elements (legal, logo placement, CTAs)
- Things to avoid (competitors' look, banned colors)
- Technical requirements (mobile-first, accessibility)

### Open questions for the client
If the email is missing critical info, list the questions Tim should ask back (not guessed).

---

## Example Flow

```
User: Extract the client brief from that Mercury Studios email
→ skill runs:
  1. Gmail search: from:mercurystudios.com newer_than:7d
  2. Reads the latest thread
  3. Downloads 2 attachments (brand deck PDF, moodboard JPG)
  4. Parses brief → outputs structured brief.md
  5. Returns: "Brief ready in projects/client-mercury/brief/brief.md — paste into Claude Design at claude.ai/design"
```

---

## Rules & Tips

### Rules
- **Never guess brand colors if unstated** — flag as open question instead
- **Always preserve exact client wording** for brand voice / tone
- **Download attachments** into a per-client folder — don't paste big files inline
- **If the email thread is long**, read the FULL thread (not just latest message) to catch earlier brief context
- **Verify the client email is real** — if sender is suspicious, flag before auto-processing

### Tips
- If the client shares a website URL, note it explicitly. Claude Design's web capture tool can pull the design system from the live site — that's often richer than the brand deck.
- For pitch decks specifically, check if the email mentions "slides" or "deck" — that triggers a different Claude Design template.
- If the brief is ambiguous on "what", ship 2-3 concept variants in Claude Design instead of guessing one.

---

## Handoff to Claude Design

Once the brief is extracted, the skill outputs a ready-to-paste block:

```
CLAUDE DESIGN INPUT:

Project: <title>
Client: <name>
Brand colors: <hex1>, <hex2>, <hex3>
Typography: <font>
Tone: <voice descriptors>
Deliverables: <list>
References: <urls + attached images>
Constraints: <list>
Deadline: <date>

Start generating assets following this brand system. Reference images attached.
```

The user then:
1. Opens claude.ai/design
2. Creates a new project
3. Pastes the block into the brief input
4. Attaches the downloaded reference files
5. Points Claude Design at the client's website (web capture)
6. Generates

The Claude Skill's job ends when the Claude Design input is ready. Claude Design takes over from there.

---

## Integration with the Solo AI Studio Stack

This skill is **Layer 1 — the Intake** of Tim Koda's Solo AI Studio Stack:

```
Intake (this skill) → Design (Claude Design) → Ship (Claude Code)
```

See `~/.claude/skills/claude-design-workflow/` (if exists) for the Step 2 design skill, and `~/.claude/skills/claude-code-deploy/` for the Step 3 shipping skill.

---

## Credits

Built by Tim Koda (@timkoda_) — French AI creative director.

Part of the **Solo AI Studio Stack** lead magnet.
