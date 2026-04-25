# StyleDesk Social Post Design System

The exact recipe behind every Instagram/Reels post. Every value below comes straight from `01-may-launch-announcement.svg` — the canonical reference file. Use this for every future post so the feed stays cohesive.

---

## 1. Canvas

| Setting | Value |
|---|---|
| Dimensions | **1080 × 1350 px** (Instagram 4:5 portrait) |
| Aspect ratio | 4:5 |
| File format | SVG (master), export to PNG/JPG for posting |
| Color space | sRGB |
| Margins (safe zone) | 80px on all sides — keep critical text inside `x: 80–1000`, `y: 80–1270` |

---

## 2. Background

Two layers, in this order:

### Layer 1 — Burgundy linear gradient (top → bottom)

```
linear-gradient
  0%   #3a0018   (burgundy red)
  55%  #2a0012   (deep wine)
  100% #1a000b   (almost black)
```

SVG:
```xml
<linearGradient id="bg" x1="0" y1="0" x2="0" y2="1">
  <stop offset="0%" stop-color="#3a0018"/>
  <stop offset="55%" stop-color="#2a0012"/>
  <stop offset="100%" stop-color="#1a000b"/>
</linearGradient>
```

### Layer 2 — Ambient gold/maroon radial glow (top-center)

Adds depth and warmth behind the hero text.

```
radialGradient
  center: 50% x, 35% y
  radius: 65%
  0%   #c9a064 @ 0.18 opacity   (gold core)
  60%  #7c1f36 @ 0.08 opacity   (maroon mid)
  100% #c9a064 @ 0      opacity (transparent edge)
```

SVG:
```xml
<radialGradient id="glow" cx="50%" cy="35%" r="65%">
  <stop offset="0%" stop-color="#c9a064" stop-opacity="0.18"/>
  <stop offset="60%" stop-color="#7c1f36" stop-opacity="0.08"/>
  <stop offset="100%" stop-color="#c9a064" stop-opacity="0"/>
</radialGradient>
```

**No particles, no decorative dots.** The ambient glow does all the atmospheric work.

---

## 3. Color Palette

| Role | Hex | Use |
|---|---|---|
| **Gold** | `#c9a064` | Eyebrows, accents, URL, emphasis text |
| **Pink** | `#f0c6cf` | Gold gradient endpoints, soft highlights |
| **White** | `#ffffff` | Neutral copy (used at varying opacity) |
| **Burgundy** | `#3a0018` → `#1a000b` | Background gradient |
| **Maroon** | `#7c1f36` | Mid-stop in ambient glow |

### Gold gradient (the "emphasis" fill)

Used on hero emphasis words and big numbers. Identical stops to the site headline gradient.

```xml
<linearGradient id="gold" x1="0" y1="0" x2="1" y2="1">
  <stop offset="0%"  stop-color="#f0c6cf"/>
  <stop offset="50%" stop-color="#c9a064"/>
  <stop offset="100%" stop-color="#f0c6cf"/>
</linearGradient>
```

Apply with `fill="url(#gold)"`.

---

## 4. Typography

### Font stack (paste exactly)

```
'Helvetica Neue', 'Inter', -apple-system, 'SF Pro Display', sans-serif
```

This stack falls through Helvetica → Inter → Apple system fonts. **Never use a serif.** Never use Playfair, Didot, or any italic display face — those were tested and rejected as too "magazine-old."

### Weights

Only two weights ever appear:

- **200 (ultra-light)** — neutral copy, "background" parts of the hero
- **500 (medium)** — emphasis, gold accent words, the punchline

A third weight (300) appears on small caps (eyebrow, URL) for legibility.

### Type scale & roles

| Role | Font-size | Weight | Letter-spacing | Color | Opacity |
|---|---|---|---|---|---|
| **Eyebrow** (top label, ALL CAPS) | 20px | 300 | 4 | `#c9a064` (gold) | 1.0 |
| **Hero** (single line, mixed) | 105–220px* | 200 / 500 split | -1 to -4** | white + gold gradient | 1.0 |
| **Sub line 1** (lighter intro) | 28px | 300 | 0.5 | white | 0.6 |
| **Sub line 2** (heavier punchline) | 30px | 500 | 0.3 | white | 0.92 |
| **URL** (bottom, ALL CAPS) | 22px | 300 | 8 | `#c9a064` (gold) | 1.0 |

\* **Hero font-size depends on character count.** Short (~7 chars like `$6,000.`) = 220px. Medium (~17 chars like `The wait is over.`) = 105–115px. Always one line.

\*\* Letter-spacing on hero scales with size. At 105px use `-1`. At 220px use `-4`.

### The "split hero" technique (critical)

The hero line uses **one** `<text>` element with two `<tspan>` children — light/white + medium/gold. **Both tspans must be on the same source line with no whitespace between tags**, or SVG renderers will wrap to two lines.

```xml
<text x="540" y="685" font-family="..." font-size="105" text-anchor="middle" letter-spacing="-1"><tspan font-weight="200" fill="#ffffff">The wait </tspan><tspan font-weight="500" fill="url(#gold)">is over.</tspan></text>
```

---

## 5. Layout (vertical y-coordinates)

A six-element vertical rhythm. Adjust slightly per post but keep the proportions.

| Element | y (baseline) | Notes |
|---|---|---|
| Eyebrow | **210** | Always at the top |
| Hero | **685** (single-line at 105px) — or 700–720 for very large numbers | Visual center of the canvas |
| Sub line 1 | **970** | Light/muted intro |
| Sub line 2 | **1015** | Heavier punchline, 45px below sub 1 |
| Divider | **1135** | Line · dot · line in gold |
| URL | **1240** | Always at the bottom |

All elements are horizontally centered (`text-anchor="middle"`, `x=540`).

---

## 6. Ornamental Divider

Two horizontal lines flanking a small gold dot. Sits between the sub block and the URL.

```xml
<line   x1="470" y1="1135" x2="535" y2="1135" stroke="#c9a064" stroke-opacity="0.45"/>
<circle cx="540" cy="1135" r="3"               fill="#c9a064"   fill-opacity="0.8"/>
<line   x1="545" y1="1135" x2="610" y2="1135" stroke="#c9a064" stroke-opacity="0.45"/>
```

Total span: 140px wide, centered on x=540.

---

## 7. Content Rhythm (the "voice" rules)

Every post follows this 5-beat structure:

1. **Eyebrow** — frames the post (1 short line, ALL CAPS, gold). 2–4 words.
2. **Hero** — the hook (1 line, mixed weight + color). Must be readable at thumbnail size.
3. **Sub 1** — context/setup (1 line, light, muted white). Often a fact, math, or rhetorical setup.
4. **Sub 2** — punchline / answer (1 line, medium, bright white). Lands the message. Often contains the price or product name.
5. **URL** — `STYLEDESK.AI` (always, bottom).

Examples from the 3-post launch:

| Post | Eyebrow | Hero | Sub 1 | Sub 2 |
|---|---|---|---|---|
| **1** Launch | LAUNCHING · JUNE 2026 | The wait is over. | The only AI receptionist | built for barbers and nail techs. |
| **2** Math | THE COST OF MISSED CALLS | $6,000. | 10 missed calls a month × $50 ticket. Every year. | StyleDesk catches them all. From $49/mo. |
| **3** 24/7 | THE NIGHT SHIFT | While you sleep. | (3 timestamp rows) | That's what 24/7 looks like. |

---

## 8. Things NOT to do

- ❌ Don't add particles, sparkles, or decorative dots — the glow handles atmosphere
- ❌ Don't use a serif (Playfair, Didot, Garamond) for the hero
- ❌ Don't use italic on sans-serif — looks awkward at large sizes
- ❌ Don't use bright #fff at 100% opacity for body copy — always 0.6 or 0.92
- ❌ Don't put the hero on two lines — single line, scale font-size to fit
- ❌ Don't space `tspan`s on separate source lines — SVG will wrap them
- ❌ Don't crowd the eyebrow with `letter-spacing > 4` — at 8 it drifts apart
- ❌ Don't use `$49/mo` without "From" — implies that's the only tier (deceptive)

---

## 9. Export & Posting Checklist

When you're ready to post:

1. Open the master SVG in a browser
2. Take a full-page screenshot (or use a converter to export PNG at 2160 × 2700 — 2× resolution for retina)
3. Verify on phone preview before posting (text is readable at thumbnail size)
4. Caption: lead with the hook, repeat the URL once
5. Hashtags: see `README.md` for the locked hashtag bank

---

## 10. Quick-start

To make a new post: copy `_template.svg`, swap the 4 text strings (eyebrow, hero "before" + "after", sub 1, sub 2). Don't touch anything else.

---

## 11. Video Series — "Shop Talk"

Every video post (Reel, IGTV, video carousel) sits under a branded series: **Shop Talk**. This creates a persistent identity across videos independent of how many founding seats have sold or how many days into launch we are.

### The overlay (top-left corner, every video)

```
SHOP TALK
STYLEDESK · EP 01
```

| Spec | Value |
|---|---|
| Font | `'Helvetica Neue', 'Inter', -apple-system, sans-serif` |
| Weight | SHOP TALK: 500 · subline: 300 |
| Color | gold `#c9a064` |
| Letter-spacing | SHOP TALK: +4 · subline: +2 |
| Size | ~2% of screen height |
| Opacity | 0.9 |
| Position | top-left corner, safe margin ~5% from edges |
| Background (optional) | 0.3-opacity black pill if video b-roll is busy |

### Voice & positioning

**You are NOT a shop owner.** Don't pose as one. Your credibility comes from being the founder/builder who **talks to** hundreds of shops and shares what you learn.

**Stay in your lane:**

| ✅ Do talk about | ❌ Don't talk about |
|---|---|
| Business operations | Craft technique (fades, nail shaping, gel cure times) |
| Phones, bookings, texts, missed-call math | How to hold clippers |
| Software, pricing, competition | How to apply dip powder |
| Patterns across many shops | Anything you can't defend if challenged |
| Industry trends, comparisons | Advice you'd lose in an argument with a pro |

### Episode 1 — lock the brand in
First episode should explicitly introduce the series so every future one feels familiar:

> *"Shop Talk, Episode 1. Every week I'm breaking down one thing about running a shop that most owners don't talk about. I don't own a shop — I built the tool a lot of them use. I talk to ~50 shop owners a month. This is what I'm learning. Today: [first topic]. Let's go."*

### The strongest format: **guest interviews**
Solves the authenticity question completely. A real shop owner is literally on camera with you.

> *"Shop Talk, EP 07. Today I've got [Nancy] — she runs [Nails by Nancy] in Landover, 35K followers, doing crazy numbers. Nancy, what's the biggest thing shop owners get wrong about their phones?"*

Benefits:
- Guest shares the episode to their audience → your reach multiplies
- Content you couldn't make alone (their stories + your synthesis)
- Authentic beyond question
- Builds deep industry relationships

Target guests from the earlier outreach list (Nancy, Hilda, others from DMV hashtag mining).

### Opening hook templates
Keep the warm, peer-to-peer tone. Shop Talk is conversation, not a pitch.

- *"Alright, shop talk real quick…"*
- *"Between clients? Let's talk shop."*
- *"Listen — talked to 12 owners this week, here's what keeps coming up…"*
- *"This one's for the shop."*

### Hashtag
Use `#shoptalk` on every Shop Talk video plus your regular niche bank.

### When Shop Talk starts
**May 20, 2026.** The 30-day content campaign begins post-launch (product ships ~early May, content campaign starts May 20 once the shop is live). From Day 1 of the campaign onward, Reels carry the Shop Talk overlay. Static posts use the design system in sections 1–10.

---

## 12. Shop Talk Question Card — locked layout

The on-screen question card used between guest answers in every Shop Talk episode. Reference: `shop-talk-question-card-example.svg` (canonical) · `_question-card-template.svg` (copy-paste with EDIT markers).

### Canvas

| Setting | Value |
|---|---|
| Dimensions | **1080 × 1920** (9:16 vertical — Reel/Story format) |
| Background | Burgundy gradient `#3a0018 → #2a0012 → #1a000b` (same as feed posts) |
| Ambient glow | Top-center radial — `#c9a064` at 0.18 opacity → `#7c1f36` at 0.08 → transparent |

### Layout (from top to bottom)

| Zone | Y position | Element |
|---|---|---|
| **Top-left overlay** | y=100 / y=135 | `SHOP TALK` (gold, weight 500, tracking +6, font-size 26) + `STYLEDESK · EP 01` (gold 70%, weight 300, tracking +3, font-size 20) |
| **Eyebrow** | y=600 | `QUESTION 02` (gold, weight 300, tracking +6, font-size 22, centered) |
| **Mini divider** | y=640 | Line · dot · line in gold under the eyebrow |
| **Question line 1** | y=850 | Setup line — white, weight 200, font-size 78, tracking -1, centered |
| **Question line 2** | y=950 | Setup line — same as line 1 |
| **Question line 3 (punchline)** | y=1080 | **The punch** — gold gradient fill, weight 500, font-size 92, tracking -2, centered |
| **Ornamental divider** | y=1500 | Line · dot · line in gold |
| **URL** | y=1600 | `STYLEDESK.AI` (gold, weight 300, tracking +8, font-size 22, centered) |

### Question construction rules

Every question splits into **2 setup lines + 1 punchline** for visual rhythm and emotional emphasis:

```
[setup — white ultralight]
[setup — white ultralight]
[PUNCHLINE — gold medium]   ← the specific moment, the kicker, the gold
```

**Examples:**

| Setup 1 | Setup 2 | Punchline (gold) |
|---|---|---|
| Walk me through | what your phone looks like | on a Saturday at 2pm. |
| If you could change | one thing about running your shop, | what would it be? |
| What's the one thing | that drives you crazy about | running this place? |
| When was the last time | your phone felt like it was working | for you, not against you? |

**Rules:**
- Maximum 3 lines total. If the question runs longer, edit it shorter.
- The gold punchline is always the **specific moment** or the **emotional pivot** — not just the last few words by accident.
- Keep all lines centered with `text-anchor="middle"`.
- Use the locked font stack: `'Helvetica Neue', 'Inter', -apple-system, sans-serif`.

### Editing workflow

1. Open `_question-card-template.svg`
2. Save-as with the episode + question number (e.g., `ep-01-q02.svg`)
3. Edit only the marked text strings:
   - Episode number in the top-left overlay
   - `QUESTION 02` eyebrow number
   - 3 lines of the question
4. Render to PNG via the puppeteer + Inter pipeline (same as the feed posts), or use an online SVG-to-PNG converter at 2× (2160×3840)
5. Drop into CapCut between guest answer cuts, hold for ~1 second per card
