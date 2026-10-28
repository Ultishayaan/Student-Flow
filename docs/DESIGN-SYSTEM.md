# StudentFlow — Design System

Generated with the `ui-ux-pro-max` skill for a **student productivity app (high-school, ages 13–18)**. Style: **Flat Design**. This is the **current primary direction**; two alternates are pending (see README §8).

## Primary direction: "Flat / Teal + Orange"

| Token | Value | Use |
|-------|-------|-----|
| Primary | `#0D9488` (teal) | Brand, active nav, primary buttons |
| On Primary | `#000000` | Text/icon on primary |
| Secondary | `#14B8A6` (light teal) | Supporting accents |
| Accent / CTA | `#EA580C` (orange) | FAB, high-priority, call-to-action |
| Background | `#F0FDFA` (mint-white) | App background |
| Foreground | `#134E4A` (dark teal) | Primary text |
| Card | `#FFFFFF` | Cards/surfaces |
| Muted | `#E8F1F4` | Inactive chips, subtle fills |
| Muted Foreground | `#475569` | Secondary text |
| Border | `#99F6E4` | Dividers, card borders |
| Destructive | `#DC2626` | Delete, overdue |

- **Font:** Plus Jakarta Sans (300–800). Friendly, modern, great for productivity.
  - Google Fonts: `https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap`
- **Icons:** Phosphor (`@phosphor-icons/react`) — use `ph-fill` for active, `ph` (outline) for inactive. Consistent stroke, no emojis as icons.
- **Effects:** No gradients/shadows in the base style. Simple hover/press (color/opacity shift), fast transitions 150–200ms.

## Subject color-coding (data-coding only, NOT brand)
Used to visually distinguish classes. Keep these separate from the brand palette.
- Math → violet `#8B5CF6`
- Biology → emerald `#10B981`
- History → amber `#F59E0B`
- English → pink `#EC4899`
- Chemistry → blue `#3B82F6`

## Accessibility rules (must follow)
- Body text contrast ≥ 4.5:1 in light AND dark mode.
- Focus states visible for keyboard nav.
- Respect `prefers-reduced-motion`.
- Touch targets ≥ 44pt (iOS) / 48dp (Android).
- Color is never the only indicator of state (pair with icon/text).
- Responsive breakpoints: 375px, 768px, 1024px, 1440px.

## Alternate directions (now built — see `design/`)

Both alternates are built as standalone HTML mockups showing **mobile + web dashboard** for each, so the owner can compare all three directions side by side.

### A — "Aurora / Vibrant" (Gen‑Z energetic)
- **File:** `design/alternate-a-aurora.html`
- **Style:** Aurora UI + vibrant block-based. Mesh gradients, flowing 12s animation, bold blocks, large friendly type.
- **Colors:** Purple `#BF00FF` · Pink `#FF1493` · Blue `#0080FF` · Cyan `#00FFFF` · Background lavender‑white `#FBF7FF` · Foreground deep indigo `#1E1B4B`
- **Font:** Fredoka (headings) + Nunito (body)
- **Effects:** Gradient cards/buttons (`background-size:300%`, 12s loop), soft purple-tinted shadows on cards. Honors `prefers-reduced-motion`.
- **Accessibility:** Dark indigo text on light lavender bg (high contrast); white text only on saturated gradient blocks; priority/state always paired with a text label, never color alone.

### B — "Dark Focus" (night‑study)
- **File:** `design/alternate-b-dark-focus.html`
- **Style:** OLED dark, low light emission, eye-comfort for late study sessions.
- **Colors:** Deep black `#000000` · Surface `#121212` · Midnight blue `#0A0E27` · Neon cyan `#22D3EE` · Green `#4ADE80` · Gold `#FBBF24`
- **Font:** Plus Jakarta Sans (same as primary — reads well on dark)
- **Effects:** Minimal neon glow (`text-shadow`/`box-shadow` sparingly), cyan→green progress gradient. `color-scheme: dark`. Honors `prefers-reduced-motion`.
- **Accessibility:** Near-white text `#F5F5F5` on black (≈16:1); muted text kept at `#A3A3A3` (not lower); glow used only as a secondary cue alongside clear text/icons.

## Web dashboard (primary direction)
- **File:** `design/web-dashboard-primary.html` — the primary teal/orange flat style applied to the web dashboard (sidebar + topbar + progress/week/due‑today/subjects), matching the mobile screens. Flat design rules apply: no gradients/shadows, borders + solid color only.

## Prototype
- `design/ui-screens.html` — primary **mobile** prototype, 6 screens: Onboarding/Login, Today, Assignments, Add Assignment, Calendar, Subjects.
- `design/web-dashboard-primary.html` — primary **web** dashboard.
- `design/alternate-a-aurora.html` — Direction A, mobile + web.
- `design/alternate-b-dark-focus.html` — Direction B, mobile + web.
- All are standalone HTML (CDN Tailwind + Phosphor + Google Fonts) — no build step to view.
