# Wilda — Personal Funnel

**Build • Grow • Protect • Legacy** · Team Majesty 👑

A single-page, dependency-free funnel. Open `index.html` in a browser — no build step, no
framework, no install. Fonts load from Google Fonts; everything else is inline.

Positioning: Wilda leads as a **business woman, strategic thinker, and educator**. The page talks
about business, money, growth, protection, and legacy. Financial solutions appear only late, and
only as an invitation to a private educational conversation.

---

## 1. Before it goes live — replace these

| Placeholder | Where | What to put there |
|---|---|---|
| `assets/wilda-hero.jpg` | Hero (full-bleed) | Editorial, confident shot — walking through a modern office, on stage, or at an elegant workspace. Landscape, high resolution (≥2000px wide), subject positioned right-of-centre so the headline sits over dark space on the left. Falls back to an emerald/black gradient with a "W" monogram if missing, so the page never looks broken. |
| `assets/wilda-hero.mp4` | Hero (optional) | Short silent loop (6–10s, muted, no captions needed). Swap the `<img>` for the commented-out `<video>` block right above it. |
| `assets/wilda-story.jpg` | Story section | Reviewing business plans, laptop + notebook, or a coffee meeting. ~4:4.9 vertical. |
| `assets/proof-event-1..3.jpg` | Real Conversations | Speaking, networking, and Team Majesty event photos. |
| `assets/og-wilda.jpg` | `<meta og:image>` | 1200×630 social share card. |
| `https://chat.whatsapp.com/REPLACE-WITH-INVITE` | Check-in success, Community, footer (3 places) | Real WhatsApp community invite link. |
| `https://calendly.com/REPLACE-WITH-LINK` | Conversation success state | Real scheduling link (Calendly / TidyCal / etc.). |
| Team Majesty `href="#"` | Community tile, Team Majesty section, footer | Official Team Majesty destination. |
| Social `href="#"` | Community section, "Follow Wilda" button, footer | Instagram, Facebook, TikTok. |
| `hello@wilda.com` | Footer | Real contact address. |
| `data-video` on `.vid` cards | Content Hub | Add `data-video="https://…"` to each card to link Wilda's real videos. Cards without it scroll to the Community section instead. |

### Wiring up the forms

Both forms (**Business & Wealth Check-In** and **Request a Conversation**) validate client-side,
show a success state, and currently only `console.log` the payload. In `index.html`, search for
**`CONNECT YOUR BACKEND HERE`** and replace the log with a `POST` to your ESP/CRM. Payload shape:

```json
{
  "firstName": "", "email": "", "phone": "", "state": "", "language": "", "about": "",
  "source": "wilda-funnel/business-wealth-check-in"
}
```

`source` is `wilda-funnel/private-conversation` for the conversation form, so both can hit the same
endpoint and still be segmented. `about` is only present on the conversation form.

A hidden honeypot field (`company`) silently discards bots. Phone is optional everywhere and
accepts 10–15 digits. **No sensitive financial information is collected anywhere on the page, by
design** — both forms say so in their fine print.

### Social proof — read this before publishing

The **Real Conversations. Real Growth.** section ships with clearly-marked empty slots on purpose.
No invented testimonials, no fake numbers. Fill them only with:

- real audience comments (paste text or a screenshot),
- client feedback with written permission (first name + state only),
- event / speaking / networking photos,
- documented community engagement.

Delete any slot you can't fill honestly — a shorter section is stronger than a padded one.

---

## 2. Funnel flow

The page sits at step 3 of this journey:

```
Instagram / Facebook / TikTok
   ↓
Wilda business content
   ↓
Wilda personal funnel        ← this page
   ↓
Business & Wealth Check-In   (lead capture)
   ↓
Email / WhatsApp community
   ↓
Educational content
   ↓
Trust
   ↓
Private conversation
   ↓
Identify needs
   ↓
Appropriate solutions
   ↓
Team Majesty 👑
```

Three conversion paths run in parallel the whole way down, so a visitor can convert at any scroll
depth:

- **Low commitment** → Join Wilda's Community (Instagram / WhatsApp). Hero secondary CTA,
  Content Hub, Community section, check-in success state, footer, drawer.
- **Lead capture** → The Business & Wealth Check-In. Nav CTA, hero primary, Entrepreneur section
  CTA, its own section, sticky mobile bar, footer.
- **High intent** → Start a Private Conversation. Deliberately placed *after* every educational
  section, never above them.

Section order: Hero → marquee → Business Woman Mindset (4 cards) → Story → Content Hub (categories,
filter, video hooks) → For Entrepreneurs (two-column ledger) → Business & Wealth Check-In → Community
→ Real Conversations → Growth Without Protection → Let's Talk About What You're Building → Team
Majesty → Footer.

The brief describes the conversation step as its own page. It ships here as a full-width section
(`#talk`) so the funnel stays one file; to split it, lift that `<section>` plus the nav/footer into
`conversation.html` and point the CTAs at `conversation.html#talk`.

---

## 3. Design system

**Palette** (CSS custom properties at the top of `index.html`)

| Token | Hex | Role |
|---|---|---|
| `--emerald` / `--emerald-deep` | `#0B3D2E` / `#07281E` | Wealth, growth, ambition. Section grounds. |
| `--emerald-lift` / `--emerald-glow` | `#125540` / `#1B7355` | Button hover fills, hero light bloom |
| `--black` / `--charcoal` | `#0C0C0C` / `#151515` | Authority. Hero, story, conversation, footer. |
| `--ivory` / `--ivory-warm` | `#F7F3EA` / `#EFE7D7` | Premium breathing space, content areas |
| `--bronze` / `--bronze-lift` / `--bronze-pale` | `#B8894A` / `#D3A465` / `#E8D5B4` | Accent only — hairlines, eyebrows, one primary button |
| `--teal` / `--sage` | `#0A2F31` / `#7E9585` | Optional secondary washes |

Bronze is a **hairline and small-accent** colour — it appears as 1px rules, eyebrow text, numerals,
and a single primary button. It is never a large fill, which is what keeps it from reading cheap.
Emerald and black carry the weight; ivory carries the reading.

**Type** — Bodoni Moda (editorial display headlines, pull quotes, the "Wilda" signature in italic),
Manrope (body, UI, letterspaced eyebrows and labels). No script font — the signature is set in
Bodoni italic, which reads executive rather than decorative.

**Geometry** — near-square corners (2–4px) instead of pills, 1px grid gaps between cards so
sections read like a magazine layout, hard high-contrast section transitions (ivory → black →
emerald), and generous vertical rhythm (`--sec: clamp(84px, 11vw, 152px)`).

**Motion** — IntersectionObserver reveals with staggered `--d` delays, buttons whose hover fill
wipes up from the bottom, cards that flip to emerald on hover, a paused-on-hover marquee, and a
scroll cue. All of it collapses under `prefers-reduced-motion: reduce`.

**Deliberately absent:** burgundy, plum, rose, pink (Yoltha's territory), corporate blue, stock
photos of families on couches, countdown timers, fake testimonials, and the phrases "buy
insurance", "get a policy", or "get life insurance now".

---

## 4. Accessibility & responsive

- Semantic landmarks, one `h1`, ordered heading levels, visible skip link.
- Decorative art marked `aria-hidden`; the marquee has a screen-reader-only text equivalent;
  icon-only links carry `aria-label`.
- Bronze `:focus-visible` rings on every interactive element.
- Category filter uses real `<button aria-pressed>` toggles.
- Form errors are per-field, inline, cleared on input, and focus moves to the first invalid field.
- Success states use `role="status"` + `aria-live` so screen readers announce them.
- Breakpoints at 1080px (two-column cards, hamburger drawer, stacked splits) and 700px (single
  column, full-width buttons, sticky bottom CTA bar).

---

## 5. Copy notes

Hero, all section headlines, the four pillars, the story, the content categories, the Kreyòl video
hooks, the entrepreneur lists, the lead-magnet subtitle, the protection transition, the conversation
copy, and the Team Majesty message are verbatim from the brief.

Written to match the voice, adjust freely: the seven check-in questions, the three-step conversation
explainer, the ledger intro ("Two lists sit on every business owner's desk…"), the social tile
descriptions, the hub subhead, two English video hooks, and the footer disclaimer.

Video hooks currently in rotation:
`Fè lajan ak bati richès se pa menm bagay.` ·
`Si business ou pa ka mache san ou, gen yon kestyon ou bezwen poze tèt ou.` ·
`3 desizyon mwen pran diferan depi mwen kòmanse panse tankou yon business woman.` ·
`Ou travay di pou konstwi li. Men èske ou gen yon plan pou pwoteje li?` ·
`Income is temporary. What are you building with it?`

---

## 6. Differentiation from the Yoltha funnel

Same Team Majesty ecosystem, two unmistakably different personal brands:

| | Yoltha | Wilda |
|---|---|---|
| Feeling | Warm, educational, family-oriented | Bold, entrepreneurial, aspirational |
| Confidence | Soft feminine | Executive feminine |
| Subject | Financial habits, preparation | Business, wealth, leadership, legacy |
| Colour | Plum · Burgundy · Champagne · Cream | **Emerald · Black · Ivory · Bronze** |
| Type | Playfair + Jost + Parisienne script | **Bodoni Moda + Manrope**, no script |
| Shape | Rounded pills, soft shadows, cream ground | Near-square edges, 1px grid rules, dark ground |
| Layout | Centred, gentle, generous curves | Asymmetric editorial grid, hard contrast cuts |

---

## 7. Deploy

Drop the folder on Netlify, Vercel, Cloudflare Pages, or any static host — one HTML file plus an
`assets/` directory. Create `assets/` and add the images before launch.
