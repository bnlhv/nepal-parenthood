# Nepal Mane-Lahav · Personal Practice Website

A single-page, Hebrew (RTL) portfolio site for **Nepal Mane-Lahav** — Educational Counselor, Parenting Instructor, Emotional Therapist, and Social Group Facilitator for children.

**Live:** https://nepal-tawny.vercel.app

---

## Tech Stack

| Layer | Choice | Why |
|---|---|---|
| **Markup** | HTML5 | Single static file (`index.html`). No build step. |
| **Styling** | [Tailwind CSS](https://tailwindcss.com/) via CDN | Custom pastel palette (sage / sky / lavender / butter) configured inline. No PostCSS / no compile step. |
| **Fonts** | [Google Fonts](https://fonts.google.com/) — Assistant + Heebo | Hebrew-first typefaces with strong weights for headings. |
| **Scripting** | Vanilla JavaScript (no framework) | Mobile menu toggle, scroll-aware navbar, footer year. ~30 lines total. |
| **Forms** | [Formspree](https://formspree.io/) | Hosted form backend; POSTs from the static page get emailed to `nepal.parenthood@gmail.com`. Free tier (50 submissions/month). |
| **Hosting** | [Vercel](https://vercel.com/) | Static hosting + global CDN. Auto-deploys on every push to `main`. |
| **Source control** | GitHub | Repo: [`bnlhv/nepal-parenthood`](https://github.com/bnlhv/nepal-parenthood) (private). |
| **WhatsApp** | [`wa.me`](https://wa.me/) deep links | Floating button + contact card open WhatsApp with a pre-filled Hebrew greeting. |

**Intentionally not used:** no React/Vue/Next/Astro, no npm dependencies for the site itself, no analytics, no tracking pixels, no CMS, no backend.

---

## Project Structure

```
/
├── index.html        # The entire site — single source of truth
├── images/
│   ├── nepal-logo.png        # Brand logo (favicon + navbar + footer)
│   ├── nepal-profile.png     # Profile photo (About section)
│   ├── nepal-warmth-1.png    # Family playing (Moments section)
│   └── nepal-warmth-2.png    # Mother & daughter reading (Moments section)
├── CLAUDE.md         # Internal guidance for Claude Code sessions
├── README.md         # You are here
└── .gitignore
```

---

## Sections

1. **Hero** — name, credentials, primary CTA
2. **About** — bio + credential pills (B.Ed, M.A Bar-Ilan, Parenting Pentagon TAU) + stats
3. **Moments** — two photo cards with Hebrew captions about connection and presence
4. **Services** — 4 color-coded cards: ייעוץ חינוכי · הדרכת הורים · טיפול רגשי · מנחת קבוצות ילדים
5. **Contact** — Formspree form + email / phone / WhatsApp direct-contact cards
6. **Floating WhatsApp button** — bottom-left, soft pulse animation

---

## Local Development

No install required.

```bash
git clone https://github.com/bnlhv/nepal-parenthood.git
cd nepal-parenthood
open index.html
```

Or, if you need a local HTTP server (e.g., to test absolute paths):

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

---

## Deployment

Vercel is connected to this repo. **Any push to `main` automatically triggers a production deploy** — no CLI needed.

Manual deploy from the CLI (rarely needed):

```bash
vercel --prod
```

The Vercel project lives at:
https://vercel.com/benlahav1990-5904s-projects/nepal

---

## Third-Party Services

| Service | Purpose | Credential location |
|---|---|---|
| **Formspree** | Receives contact form submissions | Form endpoint hardcoded in `index.html` (`action="https://formspree.io/f/maqkaprg"`). Dashboard: https://formspree.io/forms |
| **Vercel** | Hosting + CDN + auto-deploy | Vercel CLI auth in `~/.local/share/com.vercel.cli/`. Owner: `benlahav1990-5904s-projects`. |
| **GitHub** | Source + Vercel integration | HTTPS remote, PAT stored in macOS Keychain under `https://bnlhv@github.com/bnlhv/nepal-parenthood`. |
| **Google Fonts** | Web fonts (Assistant, Heebo) | None — public CDN. |
| **WhatsApp** | Direct messaging link | None — `wa.me` deep link with phone `972526969121`. |

---

## Contact Info Wired Into the Site

| Channel | Value |
|---|---|
| Email | `nepal.parenthood@gmail.com` |
| Phone | `+972 52-696-9121` |
| WhatsApp | `+972 52-696-9121` (with pre-filled Hebrew message) |

---

## Design System

Custom Tailwind theme extensions (defined inline in `index.html`):

- **`cream`** — page + section backgrounds (off-white)
- **`sage`** — primary brand color (greens)
- **`sky`** — pastel accent (Parenting card)
- **`lavender`** — pastel accent (Emotional Therapy card)
- **`butter`** — pastel accent (Social Groups card)
- **`blush`** — reserved pastel
- **`warm`** — earthy text accents
- **`charcoal`** — body text (never pure black)

Custom radii: `rounded-4xl` (2rem). Custom shadows: `shadow-soft`, `shadow-card`, `shadow-card-hover`. WhatsApp pulse uses a CSS keyframe `pulse-ring`.

---

## License

Private project. All content and imagery © Nepal Mane-Lahav.
