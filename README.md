# Mundial 2026 Predictor — Design System

Brand and UI design system extracted from the **Predictor Mundial 2026** web app, an
internal interactive tool by **Transformación ExO** that lets users predict every
match of the 2026 FIFA World Cup and (optionally) sync their picks to a Google Sheet.

> **Tagline (from the product):** _"Predictor de Resultados • Transformación ExO"_

The product is a single-page, no-backend web app. It covers all 104 matches across
five phases (Groups → Round of 32 → Quarters → Semis → Final + 3rd-place), an
explorer of 16 host stadiums, a points system, and CSV export. UI copy is in
**Spanish (Latin America)**.

---

## Sources

| What | Where |
|---|---|
| Source repo | `alzatejuanc-eng/mundial2026` (GitHub, default branch `main`) |
| Source HTML | `source/index.html` (full single-file app, ~37KB) |
| Apps Script reference | `source/apps-script.js` |
| Author / org | Transformación ExO — `transformacionexo.com` |

The repo also contains `README.md`, `QUICK_START.md`, `DEPLOY.md`, `vercel.json`,
`LICENSE`. There is **no Figma file**, **no design tokens file**, **no component
library**, and **no font assets** — every visual decision lives inline in
`source/index.html`. This design system is the codified version of those choices.

---

## Index

```
README.md                  ← you are here
SKILL.md                   ← skill manifest for Claude Code use
colors_and_type.css        ← design tokens (CSS vars) + base type styles

source/                    ← imported original (do not edit)
  index.html
  apps-script.js

assets/                    ← logos, illustrations, icons (project-owned)
  flags-readme.md          ← note on flag emoji approach

preview/                   ← Design System tab cards (700×N)
  type-display.html
  type-scale.html
  ...

ui_kits/
  predictor/               ← the only product surface
    index.html             ← interactive click-thru of the predictor
    Header.jsx
    StatCard.jsx
    MatchCard.jsx
    StadiumCard.jsx
    ConfigModal.jsx
    Alert.jsx
    NavTabs.jsx
    Button.jsx
    README.md
```

---

## CONTENT FUNDAMENTALS

**Language.** Spanish (Latin America register). All UI copy, alerts, labels, and
microcopy are in Spanish. No English appears in the product UI itself — only in
file names and code identifiers.

**Voice.** Direct, friendly, action-oriented. The product addresses the user
informally with the **tú** form (`Tu nombre`, `Estás seguro?`, `tus predicciones`)
and never the formal *usted*. It uses the imperative for primary actions
(`Guardar`, `Exportar`, `Reiniciar`, `Configura`) and exclamations for delight
(`¡Listo!`, `¡Que disfrutes prediciendo el Mundial 2026!`).

**Casing.**
- **Buttons / CTAs:** Title Case in Spanish — `Guardar Predicción`, `Nuevo despliegue`.
- **Stat labels & nav tabs:** UPPERCASE with letterspacing —
  `PUNTOS TOTALES`, `📋 GRUPOS (72)`.
- **Headings:** Sentence case — `Configuración de Almacenamiento`.
- **Inline help / descriptions:** Sentence case, full sentences with periods.

**Punctuation.**
- Spanish opening marks (`¿`, `¡`) are used in alerts and confirms.
- Em-dashes are uncommon; sentences are short.
- Sections in marketing/docs copy use friendly headers like
  `🚀 Instalación Rápida`, `📋 Configuración de Google Sheets`,
  `🐛 Troubleshooting` (an English loanword).

**Emoji usage — heavy, by design.** Emoji are part of the brand voice, not
decoration. Every primary action carries a glyph:

| Emoji | Used for |
|---|---|
| ⚽ 🏆 | The product itself / branding |
| ⚙️ 📥 🔄 | Configuration, export, reset |
| 💾 ✅ ❌ | Save / confirm / cancel |
| 📋 🎯 🔥 👑 🏆 | Phase tabs (Groups → R32 → Q → SF → F) |
| 🏟️ 📍 👥 🏗️ | Stadium meta (name, location, capacity, year) |
| 📌 ⚠️ 🐛 💡 | Alert types (info, warning, bug, tip) |
| 🇲🇽 🇧🇷 🇦🇷 … | National flags as team identifiers |

**Numbers & units.** Stadium capacity uses `toLocaleString()` so it appears as
`87,523` (English locale separators happen to match Spanish here). Points are
shown as bare integers. Phase counts go in parentheses on tabs: `Grupos (72)`.

**Tone examples (verbatim from product):**
- Empty state nudge: `📌 Configura una hoja de cálculo para sincronizar tus predicciones automáticamente`
- Confirm dialog: `⚠️ ¿Estás seguro? Se borrarán todas las predicciones`
- Validation: `⚠️ Por favor completa ambas predicciones`
- Success toast: `✅ Configuración guardada` / `✅ Guardado`

The vibe is **enthusiastic but practical** — closer to a fan-club tool than a
corporate dashboard.

---

## VISUAL FOUNDATIONS

### Color
A **deep navy** primary anchors the brand, with a **teal** accent doing nearly all
the interactive work. Cyan, coral, and purple are present in the token set but
appear sparingly — coral on destructive confirms, the others reserved for future
data viz / illustration.

| Token | Hex | Used for |
|---|---|---|
| `--color-primary` | `#1a3a52` | Header bg, headings, stat values |
| `--color-primary-2` | `#1e5a7a` | Header gradient stop |
| `--color-teal` | `#00c9a7` | Primary CTA, accents, focus, stat-card border |
| `--color-teal-hover` | `#00a88f` | CTA hover |
| `--color-cyan` | `#00d9ff` | Tertiary accent (gradients) |
| `--color-coral` | `#ff6b5a` | Destructive confirms |
| `--color-purple` | `#9d4edd` | Tertiary accent (illustrations) |

Backgrounds are a **soft cool gradient** (`#f5f7fa → #e9ecf1`) — never pure white
for the page. Cards sit on white. The product uses **3 named gradients**:
the page wash, the navy header, and a navy → teal feature gradient on stadium
tile placeholders.

### Typography
- **Family.** Originally `'Segoe UI', Tahoma, Geneva, Verdana, sans-serif`. We
  load **Inter** (Google Fonts) as a metric-compatible fallback so non-Windows
  previews look identical. **🚩 SUBSTITUTION FLAGGED** — if the brand has a
  sanctioned typeface, please share font files and I'll swap.
- **Scale.** 10 / 12 / 14 / 16 / 20 / 28 / 32 — see `colors_and_type.css`.
- **Weights.** 400 / 500 / 600 / 700.
- **Tracking.** Headings tighten (`-0.5px`); micro-labels and the header subtitle
  open up (`1px` and `2px` respectively) — this is the system's most identifiable
  type signature.
- **Numerics.** Stat values are `32px / 700`, in navy (`--color-primary`); the
  "Puntos Totales" stat instead picks up the teal accent.

### Spacing
A loose 4-step rhythm: `4 / 8 / 10 / 12 / 16 / 20 / 24 / 30 / 40` px.
Cards are padded `20px`; container max-width is `1200px` with `30px / 20px`
horizontal padding.

### Backgrounds
- **Page:** subtle cool linear gradient (no images).
- **Hero / sticky header:** navy gradient, full-bleed.
- **Stadium tiles:** placeholder gradient block (navy → teal) with a `🏟️` glyph
  centered. **🚩 No real stadium photos** — see Caveats.
- No textures, no patterns, no hand-drawn illustrations, no full-bleed photos.
  The product is a **flat, gradient-accented dashboard**.

### Animation & motion
- All transitions are `all 0.3s ease` — uniform across cards, buttons, inputs.
- **Hover lift:** cards translate `-4px`; buttons translate `-2px`. Combined with
  shadow-up, this is the system's signature interaction.
- **Modal entry:** `slideIn` keyframe — `translateY(-50px) → 0`, opacity 0 → 1,
  300ms ease.
- **Loading:** classic 360° spinner, 1s linear infinite.
- No bounces. No spring physics. No scroll-triggered animation.

### Hover & press states
- **Buttons (primary):** background darkens (teal → `#00a88f`), translate up `-2px`,
  teal-tinted shadow appears.
- **Buttons (secondary):** transparent → white fill, text flips from white to navy.
- **Cards:** translate up `-4px`, shadow grows from `--shadow-card` to
  `--shadow-hover`, and on `.match-card` the transparent border becomes teal.
- **Inputs on focus:** `border-color` → teal, background → `--color-teal-tint`
  (`#f0fffe`), outline removed.
- **Saved-state button:** background flips to `#4caf50` (green), label becomes
  `✅ Guardado` for 2s before reverting.
- No explicit press/active state defined; the product relies on the hover-lift
  reverting.

### Borders
- **Default border:** `2px solid var(--color-border)` (`#e0e0e0`) on inputs,
  separators sometimes use `1px`.
- **Stat card accent:** `border-left: 4px solid var(--color-teal)` — the system's
  one use of the "colored left rule" pattern.
- **Tab underline:** `border-bottom: 3px solid` — teal when active, transparent
  when not.
- **Match card hover ring:** `2px solid var(--color-teal)` — promoted from a
  `2px solid transparent` resting state to avoid a layout shift on hover.

### Shadows
Three-tier system, all neutral / non-colored except the CTA shadow which
reuses the teal hue at 30% alpha:

| Token | Value | Where |
|---|---|---|
| `--shadow-header` | `0 4px 15px rgba(0,0,0,.10)` | Sticky header |
| `--shadow-card` | `0 2px 8px rgba(0,0,0,.05)` | Cards / panels at rest |
| `--shadow-hover` | `0 8px 20px rgba(0,0,0,.10)` | Cards on hover |
| `--shadow-cta` | `0 6px 12px rgba(0,201,167,.30)` | Primary button hover |

No inner shadows. No layered/elevation systems beyond these three.

### Corner radii
- `4px` — micro pills (phase badges)
- `6px` — buttons, inputs
- `8px` — alerts
- `10px` — stat cards
- `12px` — match cards, modals, stadium cards (the "default" container radius)

### Cards (the canonical card)
White background, `12px` radius, `--shadow-card` at rest, `20px` padding, hover
lifts `-4px` and grows shadow to `--shadow-hover`. Optional `2px transparent →
teal` border treatment is the highlight pattern for "this is interactive."

### Layout rules
- **Container:** `max-width: 1200px`, centered, `30px 20px` padding.
- **Sticky header:** position sticky at `top:0`, `z-index: 100`.
- **Grid behavior:** Auto-fit / minmax — match cards collapse from 3-up at desktop
  to 1-up below 768px; stadiums collapse from 4-up to 1-up. No named breakpoints
  beyond `768px` (mobile).
- **Modal:** centered flex overlay, `rgba(0,0,0,.5)` scrim, max-width `400px`,
  20px padding around content area.

### Transparency & blur
None used. The modal scrim is the only translucent surface (`rgba(0,0,0,.5)`).
**No `backdrop-filter` anywhere.**

### Color vibe of imagery
There is no imagery in the source — no photos, no illustrations, no SVG art.
The system reads as **clean, light, gradient-accented** with energetic emoji
acting as visual color. If the brand later adds photography, treat the navy →
teal gradient as a duotone reference.

---

## ICONOGRAPHY

**Iconography in this product is built on Unicode emoji.** There is **no icon
font, no SVG sprite, no PNG icon set, no Lucide / Heroicons / Material Icons**
import — every glyph in the UI is a native emoji rendered by the system font.
This is intentional: it keeps the app a single zero-dependency HTML file.

**Categorical mapping** (locked across the product):

```
⚽ 🏆        — Brand / product
⚙️           — Configuration / settings
📥 🔄        — Export / reset
💾 ✅ ❌     — Save / confirm / cancel
📋 🎯 🔥 👑 🏆  — Tournament phases (Groups → R32 → Q → SF → F)
🏟️ 📍 👥 🏗️  — Stadium meta (name, city, capacity, year)
📌 ⚠️ 🐛 💡  — Alert types
🇽🇽 (regional indicator pairs) — Team flags
```

**Substitution policy.** When building screens that need an icon NOT covered
above (a chevron, a hamburger, a checkmark next to text), use **Lucide via CDN**
at default 24px / `stroke-width: 2`. Lucide's geometric, slightly rounded line
style is the closest open-source match to the product's clean, gradient-light
aesthetic. **🚩 This is a substitution, not a brand-sanctioned set** — if the
team adopts a real icon system, we'll swap it.

```html
<script src="https://unpkg.com/lucide@latest"></script>
<i data-lucide="chevron-right"></i>
<script>lucide.createIcons();</script>
```

**Logos & brand marks.** The product has **no wordmark, no monogram, no SVG
logo** — the brand presents as the literal string `⚽ MUNDIAL 2026` in a 28px
semibold heading, with the eyebrow `Predictor de Resultados • Transformación
ExO`. We've reproduced this as a text-only "logo" in
`assets/wordmark.html`. **🚩 Please share an actual Transformación ExO logo
file** if one exists.

**Generic illustrations / background images.** None exist in the source. We've
not invented any — the design system stays photo-free per the original.

---

## CAVEATS & ASKS

1. **No real Transformación ExO logo.** The product uses a text wordmark only.
   Please drop a logo SVG/PNG in `assets/` if you have one.
2. **Inter is substituted for Segoe UI.** The original uses a Windows-default
   stack. If Transformación ExO has a sanctioned typeface, please share files.
3. **No icon system.** Lucide is wired up as a CDN fallback for any need beyond
   emoji. Confirm this is acceptable, or point me at the brand's icon library.
4. **No stadium photography.** The product fakes it with a navy → teal gradient
   tile + 🏟️ emoji. We replicated that. Real photos would massively upgrade
   the stadiums view.
5. **Spanish is hardcoded.** Strings in this design system match the source
   exactly. If localization is on the roadmap, surface that and I'll structure
   the kit for i18n.
6. **The 16-of-Final ("16vos") fixture list in the source has duplicates** (last
   four entries repeat the first four) — we preserved the bug in the UI kit's
   data so the visuals match. Worth flagging to engineering.
