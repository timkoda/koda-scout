# Client Brief Template — Claude Design Input Format

Use this template to structure every extracted brief. Output as Markdown, paste the `CLAUDE DESIGN INPUT` block into Claude Design.

---

## 1. Project Identity

```yaml
client_name: ""
project_title: ""
deadline: "YYYY-MM-DD"
budget: ""  # leave empty if not stated
priority: "low | medium | high"
```

## 2. Brand System

```yaml
primary_colors:
  - "#HEX1  # name / role"
  - "#HEX2  # name / role"
  - "#HEX3  # name / role"

typography:
  primary: "Font Name — weights used"
  secondary: "Font Name — weights used"

voice_tone:
  - "descriptor 1"  # e.g. "confident"
  - "descriptor 2"  # e.g. "warm"
  - "descriptor 3"  # e.g. "technical"

logo_files:
  - path: "projects/client-<name>/refs/logo.svg"
    usage: "primary"
  - path: "projects/client-<name>/refs/logo-mark.png"
    usage: "icon / favicon"
```

## 3. Deliverables

List every output the client expects. Use Claude Design terminology so the handoff is clean.

```yaml
deliverables:
  - type: "landing_page"
    details: "hero + 3 feature sections + CTA + testimonials"
  - type: "pitch_deck"
    details: "12 slides — brand story, market, product, traction, team, ask"
  - type: "brand_kit"
    details: "logo lockups, color palette, typography sheet, stationery"
  - type: "social_campaign"
    details: "5 IG posts, 3 stories, 1 carousel"
  - type: "email_template"
    details: "responsive HTML welcome email"
```

## 4. References & Inspiration

```yaml
competitor_sites:
  - "https://..."  # what they like / don't like

moodboard:
  - "projects/client-<name>/refs/inspiration-1.jpg"
  - "projects/client-<name>/refs/inspiration-2.jpg"

brand_deck:
  - "projects/client-<name>/brief/brand-guidelines.pdf"

live_site:
  - "https://clientsite.com"  # for Claude Design web capture
```

## 5. Constraints

```yaml
must_include:
  - "Primary logo always top-left"
  - "Legal footer on every page"
  - "CTA button always matching brand red #E32020"

must_avoid:
  - "Stock photography of people"
  - "Competitor's aesthetic (<competitor name>)"
  - "Sans-serif secondary typography"

technical:
  - "Mobile-first responsive"
  - "WCAG 2.1 AA accessibility"
  - "Max page weight 2MB"
```

## 6. Open Questions for Client

If the email missed critical info, list the questions to send back BEFORE starting the design work. Don't guess.

```yaml
open_questions:
  - "Are there existing brand fonts licensed, or should we pick?"
  - "What's the primary CTA destination URL?"
  - "Is the logo available in vector format?"
```

## 7. Claude Design Input Block (ready to paste)

This is the final block the skill outputs. Copy-paste into Claude Design's brief input.

```
Project: <project_title>
Client: <client_name>

Brand system:
- Colors: #HEX1 (primary), #HEX2 (secondary), #HEX3 (accent)
- Typography: <primary font>, <secondary font>
- Voice: <tone descriptors>
- Logo: attached

Deliverables:
- <list of deliverables, 1 per line>

References:
- Competitor inspiration: <urls>
- Moodboard: attached
- Live site to mirror: <url> (use web capture)

Constraints:
- Must include: <list>
- Must avoid: <list>
- Technical: <list>

Deadline: <date>

Generate the full visual system locked to this brand. Ship every deliverable in one canvas.
```

---

## Notes on parsing

- **Color extraction**: if the brand deck is a PDF, look for hex codes in the text layer. If only visual, extract from logo pixels using color picker mentally (or flag as open question if uncertain).
- **Typography**: fonts are usually named explicitly. If only shown visually, flag as open question.
- **Tone/voice**: extract adjectives from the email body. Don't invent.
- **Deliverables**: parse explicit lists. If the client says "we need marketing materials", ask for specifics.
- **Deadlines**: extract dates from email. If relative ("next week"), convert to absolute.
