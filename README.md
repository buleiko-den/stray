# Handoff: NoStrayPets.kz — Landing / Who-Am-I / Persona flow

## Overview
A mobile-first educational micro-site for Kazakhstan about the stray-animal problem. Home screen states the scale of the problem, then routes visitors through a "Who am I?" persona picker (pet owner / pet lover / doesn't like pets) into a tailored action page. Trilingual: English, Russian, Kazakh (live-switching dropdown, no page reload).

## About the Design Files
The files in this bundle (`Site.dc.html`) are **design references built in HTML** — a working prototype of the intended look, content, and interaction, not production code to copy directly. The task is to **recreate this design in the target codebase's environment** (React, Vue, native mobile, etc.) using that codebase's existing component/state patterns — or, if no environment exists yet, choose the most suitable framework and implement there.

## Fidelity
**High-fidelity.** Colors, typography, spacing, copy (in all 3 languages), and interaction states are final/intended, not placeholders — except the 5 photos/illustrations noted under Assets, which are prototype art and should be swapped for final commissioned art if available.

## Screens / Views

### 1. Home
- **Purpose**: State the stakes (annual stray-pet deaths) and set the collaborative tone before asking who the visitor is.
- **Layout**: Single column, max-width 480px container centered on page (desktop shows it as a centered "phone-width" column with a soft drop shadow; on mobile it's full-bleed). Vertical padding 86px top (clears fixed header) / 40px bottom.
- **Components** (top to bottom):
  - Flag stripe: 6px tall bar, `linear-gradient(90deg, #0099CC 70%, #FFD100 70%)`, 20px bottom margin.
  - Hero image frame: 16px border-radius, `box-shadow: 0 8px 24px rgba(0,0,0,.12)`, background `#eaf7fb`, image `object-fit: contain` (no cropping).
  - Stat number: 46px, weight 800, color `#0099CC`, centered. Content-driven (currently "≈286,000").
  - Body text 1: 17px/1.45, weight 600, `#0a1f33`, centered, `text-wrap: pretty`.
  - Second illustration frame ("Біз біргеміз" / "We are together"): same frame treatment, white background.
  - Body text 2: same style as body text 1.
  - Down-arrow button: 48px circle, background `#0099CC`, white "↓", `box-shadow: 0 4px 12px rgba(0,153,204,.35)`. Links/scrolls to the Who-Am-I section.

### 2. Who am I? (persona picker)
- **Purpose**: Let the visitor self-identify so content can be tailored non-judgmentally.
- **Layout**: Same column, 36px/44px vertical padding. Title centered, 26px/800 weight, 22px bottom margin.
- **Components**: 3 stacked full-width picker cards, 14px gap. Each card: 2px solid `#0a1f33` border, 16px radius, image on top (`object-fit: contain`, max-height 220px), label below (17px/700, centered, 12px padding). Tapping a card navigates to that persona's detail page (see State Management).

### 3. Persona detail (3 variants: Owner / Lover / Dislike)
- **Purpose**: Validate the visitor's stance, then give 3 concrete action steps and 2–3 contextual "what to do if…" resource links — a distinct full page per persona, not an in-page accordion.
- **Layout**: Full-screen replacement of Home/Who-Am-I (own scroll, 86px top padding to clear fixed header, `min-height: 100vh`, background `#f7fbfc`).
- **Components**:
  - Validation callout: rounded box (14px radius), background `#eaf7fb`, 2px solid `#0099CC` border, 16px padding. Text 17px/700, `#0a1f33`.
  - "Do these simple steps:" heading (19px/800), then 3 stacked step rows: white card, 2px solid `#0a1f33` border, 12px radius, 10×14px padding, gold (`#FFD100`) 28px circle "✓" badge + 15px/600 label text.
  - "What to do if I:" heading, then 2–3 stacked resource rows: white card, 2px **dashed** `#0099CC` border, 12px radius, 📍 icon + 15px/600 label.
  - "← Choose another" text link (15px/700, `#0099CC`) at the bottom, returns to the Who-Am-I picker.

## Interactions & Behavior
- **Hamburger menu** (fixed header, always visible — `position: fixed`, top:0, full width up to 480px, white background, bottom border): opens a right-side slide-in panel (`translateX(100%)→0`, 0.22s ease-out) covering ~78% width (max 340px) over a 50%-opacity scrim. Panel items: Home, Facts & statistics (both scroll/navigate to Home for now — "Facts & statistics" as its own page is a known next step, not yet built), Who am I? Tapping the scrim or the × closes the panel.
- **Language dropdown**: native `<select>` EN/RU/KZ in the fixed header, switches all copy instantly (no reload), state persists in-memory only (no localStorage in the prototype — add persistence in production if desired).
- **Persona navigation**: tapping a persona card sets `persona = <key>` and scrolls to top, replacing Home+Who-Am-I with the persona's dedicated full page. "← Choose another" clears `persona` and smooth-scrolls back to the Who-Am-I section.
- **Down arrow** on Home: anchor scroll to `#whoami`.
- No loading states, no forms, no validation logic — this is a static informational flow.

## State Management
- `lang`: `"EN" | "RU" | "KZ"` — drives all copy via a per-language content object.
- `menuOpen`: boolean — hamburger panel visibility.
- `persona`: `null | "owner" | "lover" | "dislike"` — `null` shows Home+Who-Am-I (scrollable together); any other value shows only that persona's full detail page.
- All copy lives in one lookup object keyed `[lang][field]`, plus a `details[persona]` sub-object with `validation`, `steps[]`, `resources[]` per persona — recreate this shape (or equivalent i18n structure) in the target codebase.

## Design Tokens
- **Colors**: Primary blue `#0099CC` (flag blue, links, primary actions), Gold `#FFD100` (accent, checkmark badges), Ink `#0a1f33` (text/borders), light blue tint background `#eaf7fb`, page background `#fff` / `#f7fbfc`.
- **Typography**: Headings/labels — Manrope (400/600/700/800). Body copy — Nunito (400/600/700). Stat number 46px/800; section titles 26px/800; card titles 17px/700; body 17px/600; small labels 15px/600.
- **Radius**: 16px (image/picker cards), 14px (callout), 12px (step/resource rows), 8px (buttons/select), 50% (circular arrow button & step badge).
- **Shadows**: `0 8px 24px rgba(0,0,0,.12)` (image frames), `0 4px 10px rgba(0,0,0,.06)` (picker cards), `0 4px 12px rgba(0,153,204,.35)` (arrow button).
- **Borders**: 2px solid `#0a1f33` (cards/buttons), 2px dashed `#0099CC` (resource rows).

## Assets
Prototype art (to be replaced with final commissioned assets if available), all in `site-images/`:
- `hero-family.png` — Home hero photo (family + dog + cat).
- `biz-birge.png` — "Біз біргеміз" (We are together) illustration.
- `persona-owner.png`, `persona-lover.png`, `persona-dislike.png` — cartoon character illustrations for each Who-Am-I card, reused on that persona's detail page context.

## Files
- `Site.dc.html` — the full working prototype (structure, styling, copy in all 3 languages, and interaction logic).
- `site-images/` — the 5 image assets referenced above.
