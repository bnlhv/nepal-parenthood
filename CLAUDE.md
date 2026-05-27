# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this is

A single-page, Hebrew **RTL** portfolio/business website for **נפאל מנה-להב** — Educational Counselor (M.A, Bar-Ilan), B.Ed in Education & Special Education for Early Childhood, graduate of the "Parenting Pentagon" program at Tel Aviv University. The site is targeted at Israeli parents seeking emotional therapy, parenting instruction, or social groups for children.

Tone: warm, empathetic, professional, therapeutic. Avoid corporate or clinical language.

## Stack

- **HTML5** only — no framework, no build step.
- **Tailwind CSS via CDN** (`cdn.tailwindcss.com`) with a custom theme defined inline in `<script>tailwind.config = {...}</script>`.
- **Google Fonts**: Assistant (primary) + Heebo (fallback) — both support Hebrew.
- **Vanilla JS** for: mobile menu toggle, scroll-aware navbar, footer year stamp. No JS frameworks.
- **Formspree** for the contact form (action attribute, currently placeholder).
- **No package.json, no node_modules.** Deployment is a static file drop (Vercel).

## File structure

```
/
├── index.html              # The entire site — single source of truth
├── images/
│   ├── nepal-logo.png      # Logo (used as favicon + navbar + footer)
│   ├── nepal-profile.png   # Profile photo (About section)
│   ├── nepal-warmth-1.png  # Family playing (Moments section)
│   └── nepal-warmth-2.png  # Mother & daughter reading (Moments section)
├── .gitignore
└── CLAUDE.md
```

Image filenames are normalized; do NOT reintroduce AI-generator names like `Gemini_Generated_Image_*`.

## Site sections (in DOM order)

1. **Header / Navbar** — sticky, blur-on-scroll, mobile hamburger menu.
2. **Hero** (`#home`) — name, credentials, CTA "תיאום שיחת ייעוץ".
3. **About** (`#about`) — bio + credential pills + stats. Profile photo on the right (RTL: left of bio in source).
4. **Moments** (`#moments`) — two warmth photos with Hebrew captions. Sits between About and Services. Not in the navbar — intentional.
5. **Services** (`#services`) — 4 color-coded cards: ייעוץ חינוכי (sage), הדרכת הורים (sky), טיפול רגשי (lavender), מנחת קבוצות (butter).
6. **Contact** (`#contact`) — Formspree form + email card + phone card + WhatsApp card.
7. **Footer** — logo, nav, contact, credentials line, copyright with auto-updating year.
8. **Floating WhatsApp button** — bottom-left, soft pulse animation.

## Design system (Tailwind theme extensions)

Custom palette in the inline `tailwind.config`:

| Token | Use |
|---|---|
| `cream-50/100/200/300` | Page + section backgrounds |
| `sage-50…900` | Primary brand color (greens) |
| `sky-50…700` | Pastel accent #1 (blues) — Parenting card |
| `lavender-50…700` | Pastel accent #2 (purples) — Emotional Therapy card |
| `butter-50…700` | Pastel accent #3 (yellows) — Social Groups card |
| `blush-50…600` | Reserved pastel — currently unused, keep for future |
| `warm-300…600` | Earthy/sandy text accents |
| `charcoal` (DEFAULT/light/muted) | Body text. **Never use pure `black` — too harsh.** |

Custom shadows: `shadow-soft`, `shadow-card`, `shadow-card-hover`. Custom radius: `rounded-4xl` (2rem).

## RTL & Hebrew conventions

- `<html lang="he" dir="rtl">` — global RTL is in effect, do not flip the document direction.
- For phone numbers and Latin/email strings inside a Hebrew block, wrap with `dir="ltr"` to keep correct visual order.
- Hebrew copy uses quotation conventions: `"text"` is fine; for emphasis prefer `<strong class="text-charcoal font-semibold">…</strong>`.
- When adding icons or arrow CTAs, remember that `→` visually points "forward" in RTL, but our `<svg>` arrows in CTAs use left-pointing chevrons (which read as "forward" in Hebrew). Keep that convention.

## Integration placeholders that may still need replacement

Search the file for these strings before deploy:

- `https://formspree.io/f/your-id` — replace with the real Formspree endpoint.
- `972526969121` — WhatsApp number (appears in floating button, contact-section WhatsApp card). Format: country code, no `+`, no leading 0.
- `tel:+972526969121` and the displayed `+972 52-696-9121` — phone link in contact card + footer.
- `nepal.parenthood@gmail.com` — email (mailto in contact card + footer).

Each placeholder has a `<!-- TODO -->` comment nearby.

## Coding rules for this project

- **Keep `index.html` as a single, self-contained file.** Do not introduce a build step, npm dependencies, or split into multiple HTML files.
- **No emojis** in source or copy unless the user explicitly asks.
- **Don't add comments** that describe what code does — well-named Tailwind classes are self-documenting. Only comment on non-obvious WHY (e.g., the `<!-- TODO: replace WhatsApp number -->` markers).
- **Preserve the warm, calming aesthetic.** New components should fit the pastel palette and rounded-2xl/3xl/4xl language. Avoid harsh borders, pure black, or aggressive shadows.
- **Mobile-first.** Most visitors will be on phones. Test every change at narrow widths.
- **Accessibility:** maintain `aria-label`, `aria-expanded`, `aria-controls` on the mobile menu and form labels. Keep visible focus rings (`:focus-visible` style is defined in `<style>`).

## Local preview

```bash
open index.html
# or, if you need a local server (e.g., to test absolute paths):
python3 -m http.server 8000
# then http://localhost:8000
```

No build, no install, no dev server needed.

## Deployment

Static site → **Vercel** (drag-and-drop, or `vercel` CLI). The whole site is `index.html` + `images/`. No vercel.json needed unless adding redirects.

## Git / auth

Remote uses HTTPS with a username-scoped URL to keep credentials separate from the user's work account on the same machine:

```
origin = https://bnlhv@github.com/bnlhv/nepal-parenthood.git
credential.useHttpPath = true
```

PAT lives in macOS Keychain under `https://bnlhv@github.com/bnlhv/nepal-parenthood`. Do not embed tokens in `.git/config` or in chat.

## What NOT to do

- Don't rename or move files in `images/` without updating all references in `index.html`.
- Don't convert the site to a framework (React/Next/Vue/etc.) without explicit instruction.
- Don't add tracking pixels, analytics, or third-party widgets without asking.
- Don't change the Hebrew copy tone toward marketing-aggressive language. The brand is therapeutic, not "high-converting funnel."
- Don't introduce LTR-only assumptions (e.g., `ml-auto`, `text-left`) — use logical equivalents (`me-auto`, `text-start`) when the layout should flip with RTL.
