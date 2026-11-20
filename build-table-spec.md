# The Build Table: Website Concept & Build Specification

**Document purpose:** a complete, buildable specification for a software development company website whose main experience is an interactive "Build Table" tool. It is written for an AI coding agent (OpenHands) or a human developer. Treat it as the source of truth.

**Placeholder notice:** the company name "Vektor Forge", all project names, team names, prices and rates in this document are **placeholders**. They live in config files (section 14) and must never be hard-coded in components.

**If something is ambiguous:** choose the simplest option that satisfies the acceptance criteria, then record the choice in `DECISIONS.md` in the repo root.

---

## Table of contents

1. Concept summary
2. Goals, audience and success metrics
3. Client journey (the experience being built)
4. Information architecture and routes
5. Visual design system
6. Screen-by-screen specification
7. The module catalog
8. Dependency rules
9. Estimation engine (formulas and test fixtures)
10. Blueprint rendering (layout, lines, animation)
11. Ghost overlay (similar past projects)
12. Backend, API and data models
13. Emails
14. Configuration files
15. Accessibility
16. Responsive behaviour
17. SEO and non-interactive fallback
18. Analytics, privacy and security
19. Performance budgets and browser support
20. Tech stack and repository structure
21. Build plan (milestones and tasks)
22. Acceptance criteria and test plan
23. Copy deck
24. Open questions and assumptions

---

## 1. Concept summary

Most software company websites are brochures: a hero banner, a list of services, logos, a contact form. Visitors cannot tell one from another.

**The Build Table is a tool, not a brochure.** The visitor lands on a glowing, 80s-future drafting workbench. They drag modules (such as "Mobile app", "Payments", "AI assistant") onto the table. A blueprint draws itself live as they build. A side rail shows a rough **timeline, team, budget range and risks** that update with every change. When they are happy, a laser scans the blueprint, a one-page plan prints, and they press **Send blueprint**. That blueprint is the enquiry.

**Style:** retro-futurist. Blue drafting-paper grid, glowing vector-line holograms, chamfered (corner-cut) panels, laser-scanner animations, technical annotations in monospace.

**One-line pitch:** "Design your software on the table. We'll build it."

---

## 2. Goals, audience and success metrics

### 2.1 Business goals
1. Replace a cold contact form with a qualified enquiry that already contains scope, a timeline and a budget range.
2. Differentiate the company from generic agency sites.
3. Educate visitors honestly about how software fits together, to build trust.
4. Start sales conversations at the solution, not at the introduction.

### 2.2 Primary persona
**Meera, non-technical founder.** Has an idea (a clinic-booking app). Does not know what it costs or what is needed. Has seen several agency sites that said "We build digital experiences" and left each one. Wants to understand what she needs and what it costs before talking to anyone.

### 2.3 Secondary personas
- **Dev, product manager** at an existing company who needs a feature added (for example AI search). Wants speed and a clear scope.
- **Sana, skeptical technical buyer.** Wants to see past work, the team and process before engaging. Uses the "dock" links.

### 2.4 Success metrics (instrumented, see section 18)

| Metric | Target (first 90 days) |
|---|---|
| Visitors who add at least 1 module | 55% |
| Visitors who reach 3 or more modules | 30% |
| Visitors who run a scan | 18% |
| Scan to send conversion | 35% |
| Median time on Build Table | 3 to 6 minutes |
| Enquiries with a blueprint attached | 100% of tool-originated enquiries |

---

## 3. Client journey

Meera's path, step by step. Every later section exists to make this journey real.

### Step 1: Arrival (0 to 10 seconds)
- Screen starts black. A laser line sweeps across and draws a blue-grid workbench.
- No hero banner, no big navigation bar.
- One line: **"What do you want to build?"** Below it three buttons:
  - *Launch something new*
  - *Fix or upgrade what I have*
  - *Add AI to my business*
- A small **dock** at the edge: *Our work · Our team · Talk to a human*, for visitors who want a conventional route.
- **Feeling:** "This is different, and I already know what to do."

### Step 2: Setting the foundation
- Meera picks *Launch something new*. The table fills with floating glowing modules.
- A prompt asks: "Tell us in one sentence what it is." She types "booking app for clinics."
- The table highlights suggested modules (Mobile app, Payments, Notifications, Booking, User login) with a soft pulse. Nothing is added automatically.
- **Feeling:** "It understood me without a form."

### Step 3: Building (the core)
- She drags *Mobile app* onto the table. It snaps in with a magnetic click. A vector phone sketch draws on the blueprint.
- She adds *Payments*. A connecting line draws between them. Because Payments needs User login, the table offers to add it.
- **Hover** a module for a plain-language hologram card. **Click** a placed module to open option dials (platform, payment methods, and so on).
- The side rail updates live: timeline, team, budget range, risks.
- Removing a module others depend on is blocked with an explanation; the connecting lines flash.
- **Feeling:** "I'm in control and I'm learning what I didn't know to ask."

### Step 4: Proof in context
- Faint "ghost" blueprints of similar past projects appear at the table's edge. Tapping one overlays it on her blueprint and shows what matched, what differed, and how long it really took.
- **Feeling:** "They've done this before, and I can see it."

### Step 5: The scan
- She presses **Scan blueprint**. A laser sweeps down the blueprint, annotating each module. A one-page plan prints out: phases, timeline, team, budget range, what is included and not included.
- She can still edit; numbers update instantly.
- **Feeling:** "This is a real plan, not a sales pitch."

### Step 6: Send blueprint
- One short form: name, email, optional extras. The only form on the site.
- On send the blueprint folds into a glowing capsule and shoots off the table.
- Confirmation screen states exactly what happens next: a named engineer reads it within one working day, a 30-minute call starts from her design, and she gets a private link to edit or forward the blueprint.
- **Feeling:** "This wasn't a cold enquiry. I've already started the project."

### Step 7: After she leaves
- Her blueprint lives at a private link and can be refined.
- The team sees the exact same blueprint.
- If she has not booked a call after 48 hours, one follow-up email shows her blueprint image: "Your clinic app is still on the table."

---

## 4. Information architecture and routes

| Route | Purpose | Indexable |
|---|---|---|
| `/` | The Build Table experience (boot, intent, build, scan, send) | Yes (see section 17 for fallback content) |
| `/work` | List of past projects (conventional page) | Yes |
| `/work/[slug]` | One project case study, with "Start from this blueprint" button | Yes |
| `/team` | Team page | Yes |
| `/talk` | "Talk to a human": book a call, email, phone/WhatsApp | Yes |
| `/b/[id]` | Read-only view of a saved blueprint | No (`noindex`) |
| `/b/[id]?edit=[token]` | Editable view of a saved blueprint | No |
| `/privacy` | Privacy policy | Yes |
| `/admin` | Internal list of blueprints and enquiries (protected) | No |
| `/api/*` | Backend endpoints (section 12) | No |

**The dock** (Our work, Our team, Talk to a human) is visible on `/` at all times, in the header on desktop and in a menu button on mobile. On `/work`, `/team`, `/talk` it is the normal header, plus a persistent button **"Open the Build Table"**.

---

## 5. Visual design system

### 5.1 Principles
1. **The table is the hero.** Everything else is quiet.
2. **Lines, not fills.** Holograms are outlines with a faint tint. Solid fills are used only for primary buttons and the laser.
3. **Every annotation means something.** Monospace labels are used for real data (module ID, weeks, dimensions), never decoration.
4. **Motion answers actions.** Idle motion is limited to slow module floating and the laser on boot/scan.

### 5.2 Color tokens (CSS variables on `:root`)

```css
:root {
  --paper:        #0A1A3F;  /* blueprint background */
  --paper-2:      #0E2A63;  /* raised panels */
  --paper-3:      #143683;  /* hover/active panels */
  --grid:         rgba(143, 211, 255, 0.14); /* minor grid lines */
  --grid-major:   rgba(143, 211, 255, 0.28); /* every 5th line */
  --line:         #8FD3FF;  /* primary line/outline color */
  --holo:         #5CE1FF;  /* hologram glow, focus */
  --laser:        #FF3D81;  /* laser, primary buttons, errors that need attention */
  --amber:        #FFC857;  /* estimates, warnings, dependency lines */
  --ok:           #7CFFB2;  /* success, satisfied dependencies */
  --danger:       #FF6B6B;  /* blocked actions, invalid fields */
  --ink:          #EAF4FF;  /* main text */
  --ink-dim:      #9DB4E0;  /* secondary text */
  --ink-on-laser: #1A0610;  /* text on laser-colored buttons */
}
```

**Contrast requirements (WCAG AA):** `--ink` on `--paper` 4.5:1 or better (it is above 12:1). `--ink-dim` on `--paper` must stay at 4.5:1 or better; verify with a script in CI. `--ink-on-laser` on `--laser` 4.5:1 or better.

**Optional "paper mode" (P2, after launch):** `[data-theme="paper"]` swaps to cream drafting paper (`--paper:#F3EAD3`), ink-blue lines (`--line:#1B3A8C`), and keeps laser/amber adjusted for contrast. Respect `prefers-color-scheme` only for first visit, then persist the choice.

### 5.3 Typography

| Role | Font | Size / line height | Weight |
|---|---|---|---|
| Display (boot question) | Chakra Petch | 56/60 desktop, 36/40 mobile | 600 |
| H2 | Chakra Petch | 32/38 | 600 |
| H3 / module names | Chakra Petch | 20/28 | 500 |
| Body | IBM Plex Sans | 16/26 | 400 |
| Annotation / data labels | IBM Plex Mono | 13/18 | 400 |
| Button | Chakra Petch | 16/20, letter-spacing 0.04em | 600 |

- Self-host fonts (WOFF2, `font-display: swap`), subset to Latin plus Latin Extended. Fallbacks: `system-ui, sans-serif` and `ui-monospace, monospace`.
- Body line length at most 70 characters.
- Do not use ALL-CAPS for labels or headings. Use sentence case everywhere.

### 5.4 Spacing, shape and elevation
- Spacing scale (px): 4, 8, 12, 16, 24, 32, 48, 64, 96.
- **Chamfered corners:** panels and modules use `clip-path: polygon(10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%, 0 10px)`. Buttons use a 6px chamfer. Inputs are rectangular with a 2px bottom border.
- Outlines: 1px `--line` at 70% opacity; hover and selected 2px `--holo` with `box-shadow: 0 0 12px var(--holo)`.
- No drop shadows other than glow.

### 5.5 The table surface
- Background `--paper` with a CSS/SVG grid: minor lines every 24px, major lines every 120px.
- A subtle radial vignette (transparent center to 35% black at the edges).
- Four corner brackets (L-shaped, 24px, 2px `--line`) frame the workbench area.
- Faint rotating registration marks (crosshair circles) at the corners are allowed as static decoration only.

### 5.6 Module (hologram card) visual
- Size 168 x 104 (tray), 160 x 96 (placed on blueprint).
- Chamfered outline, inner faint horizontal scanlines (`repeating-linear-gradient`, 2px period, 6% opacity).
- 40px line-art icon (2px stroke, `--holo`), module name below (H3, 15px override), effort tag in mono at the bottom-right: `4-6 wks`.
- **States:** idle (floating), hover (scale 1.04, glow), dragging (scale 1.08, opacity 0.92, soft shadow-glow, other tray items dim to 60%), placed (solid outline, small bolt dots at the four corners), selected (2px `--holo`), blocked (outline `--danger`, shake), suggested (slow pulse of glow, 2s loop, until interacted or sentence changes).

### 5.7 Motion tokens

```css
:root {
  --ease-snap:   cubic-bezier(0.2, 0.9, 0.2, 1.2); /* magnetic snaps */
  --ease-out:    cubic-bezier(0.16, 1, 0.3, 1);
  --ease-print:  steps(10, end);                   /* printer feed */
  --dur-fast:    120ms;
  --dur-base:    240ms;
  --dur-slow:    480ms;
  --dur-scene:   960ms;
}
```
- **Idle float:** each tray module translates Y by +/-4px over 4 to 6 seconds (random per module), `ease-in-out`, infinite. Disabled under reduced motion.
- **All motion respects `prefers-reduced-motion: reduce`:** replace sweeps, floats and draws with instant state changes or 120ms fades; the printed plan simply appears.
- Optional sound (P2): off by default. Soft click on snap, low hum during scan. Toggle in header. Never autoplay.

### 5.8 Iconography
One custom line-icon per module (section 7 lists the concept). SVG, 40 x 40 viewBox, `stroke="currentColor"`, `stroke-width="2"`, `stroke-linecap="square"`, no fills.

---

## 6. Screen-by-screen specification

Desktop reference width: 1440 x 900. All screens live on `/` and are states of one app (a state machine, section 20.3), except where noted.

### S0: Boot sequence
**Timeline (first visit):**
| Time | Event |
|---|---|
| 0 to 400ms | Black screen |
| 400 to 1000ms | Laser line (2px, `--laser`, glow) sweeps left to right at vertical center |
| 1000 to 1900ms | Grid draws outward from the laser line (stroke-dashoffset animation) |
| 1900 to 2200ms | Four corner brackets snap in (`--ease-snap`) |
| 2200ms onward | Headline types in at 40ms per character, then three intent buttons fade in (240ms, 80ms stagger) |

- **Skip:** any key or click jumps to the end state immediately.
- **Returning visitors** (flag `vf.seen` in localStorage): a 600ms version (grid fades in, headline appears instantly).
- **Reduced motion:** end state immediately.
- **Total blocking time before interaction:** at most 2.2 seconds on first visit, and the intent buttons are focusable as soon as they appear.

### S1: Intent
- Headline: "What do you want to build?"
- Three large buttons (min 56px tall):
  1. **Launch something new**: sets `intent = "new"`; tray shows all modules, interface modules first.
  2. **Fix or upgrade what I have**: `intent = "upgrade"`; tray shows modules, with Integrations, Analytics, Admin panel and Dashboard first; adds an extra optional field in S2 ("What do you have today?").
  3. **Add AI to my business**: `intent = "ai"`; AI assistant, Search, Integrations first; asks which AI type in S2.
- Dock links visible at top-right. A text link below the buttons: "Not sure? Just look around" which goes straight to S3 with an empty table and all modules in the default order.

### S2: One-sentence prompt
- A single text field, 140-character maximum, placeholder rotates between examples: "booking app for clinics", "inventory dashboard for my shop", "AI that answers customer emails".
- Buttons: **Continue** (primary) and **Skip** (text).
- On Continue: run `suggestModules(sentence, intent)` (section 6.1). Transition: the grid pans and the tray appears.
- No network call is required. (Optional P2: LLM-based suggestion through `/api/suggest`; must fall back to the keyword method on failure or over 1.5 seconds.)

#### 6.1 Keyword suggestion map (v1, rule-based)
Lowercase the sentence, match whole words or stems. Each match adds its modules to the suggestion set (maximum 5, ordered by number of matches).

| Keywords | Suggested modules |
|---|---|
| book, booking, appointment, schedule, reserve, slot, clinic, salon | booking, user_login, notifications, mobile_app, payments |
| shop, store, sell, ecommerce, checkout, cart, buy | web_app, payments, user_login, search, admin_panel |
| app, mobile, ios, android | mobile_app, user_login, notifications |
| dashboard, report, analytics, kpi, metrics, insights | web_dashboard, analytics_reports, user_login |
| admin, manage, backoffice, staff | admin_panel, user_login |
| ai, assistant, chatbot, gpt, automate, automation, summar | ai_assistant, integrations, search |
| chat, message, messaging, support | chat_messaging, notifications, user_login |
| map, location, delivery, track, tracking, nearby | maps_location, mobile_app, notifications |
| pay, payment, invoice, subscription, billing | payments, user_login |
| search, find, catalog, directory | search, web_app |
| upload, document, file, photo, pdf | file_storage, user_login |
| connect, integrate, api, crm, erp, sync | integrations, admin_panel |
| language, multilingual, translate, hindi, tamil, spanish | multilanguage |

If fewer than 2 modules match, suggest by intent: `new` gives web_app, mobile_app, user_login; `upgrade` gives integrations, web_dashboard, analytics_reports; `ai` gives ai_assistant, integrations, search.

### S3: The Build Table (main screen)

#### 3.1 Layout (desktop, at least 1100px wide)

```
+------------------------------------------------------------------------------+
| Logo      Our work · Our team · Talk to a human        [sound] [currency] [?] |  header 56px
+----------------+-----------------------------------------+-------------------+
|  TRAY (320px)  |           BLUEPRINT CANVAS (flex)       |  ESTIMATE RAIL    |
|  category tabs |                                         |  (340px)          |
|  floating      |    drafting grid + placed modules       |  Timeline         |
|  module        |    + connection lines                   |  Team             |
|  hologram      |                                         |  Budget           |
|  cards         |                                         |  Risks            |
|                |  [ghost chips of similar projects]      |  [Scan blueprint] |
+----------------+-----------------------------------------+-------------------+
```

- **Tray:** category filter tabs (All, Interfaces, Features, Foundations). Scrollable vertical list/grid (2 columns). Modules already placed are shown dimmed with a check mark and cannot be dragged again (integrations are the only module that can be re-added, section 7).
- **Blueprint canvas:** the drop target. Empty state shows faint dashed outline slots and the text "Drag a module here to start your blueprint." with an arrow from the tray.
- **Estimate rail:** described in 3.3.
- **Header** during build: logo only, dock links, sound toggle, currency selector, help (?) which opens a 3-step tooltip tour.

#### 3.2 Interactions in detail

**Adding a module (desktop, pointer):**
1. Pointer down on a tray card: lift (scale 1.08), dim others, show a translucent drop zone over the canvas.
2. Dragging: the card follows the pointer with a 60ms lag (spring, stiffness 300, damping 28).
3. Within **48px** of its target slot, the card **magnetically snaps** to the slot (spring, `--ease-snap`, 240ms).
4. Release inside the canvas: module is placed at the next free slot in its band (section 10.1). Release outside: card returns to the tray with a 240ms spring.
5. On placement: outline switches from dashed to solid, bolts appear, a short "lock" flash (opacity 0.6 to 0, 120ms), the blueprint glyph starts drawing (section 10.4), the rail numbers animate.

**Adding a module (alternative, all devices):** click/tap or press Enter on a tray card, then pick **Add to blueprint** in the small hologram card that appears. This is the primary mobile method and is the keyboard method (section 15).

**Hover (desktop) / long-press (touch) on a tray card:** a hologram info card appears (320px wide) with:
- Module name (H3)
- Plain-language description (2 sentences maximum; text in section 7)
- "Typically takes": `4-6 weeks of effort`
- "Works with": names of modules it connects to
- "Needs": required modules, if any

**Selecting a placed module (click/tap):** opens the **Option panel**, a hologram card anchored to the module with:
- Title and short description
- Option dials (segmented controls or radio chips, section 7)
- A remove button (**Remove module**)
- Live effect line, for example: "Both platforms: +1.6 weeks, about +$X"

**Removing a module:** via the option panel or by dragging it off the canvas back to the tray, or pressing Delete when focused. If other placed modules **require** it, removal is blocked (section 8.3).

**Reordering:** placement order within a band is the order of addition; users can drag placed modules left or right within their band to reorder (swap with neighbour, 240ms spring). Order has no effect on estimates.

**Undo / redo:** Ctrl/Cmd+Z and Ctrl/Cmd+Shift+Z, plus two small icon buttons above the canvas. History depth 50. Every add, remove, option change and reorder is one history entry.

**Reset:** a small "Clear table" text button above the canvas, with a confirm popover ("Remove all 5 modules? You can undo this.") and it is undoable.

**Autosave:** the blueprint state is written to `localStorage` (`vf.blueprint.v1`) after every change (debounced 300ms). On return, the table restores and a toast says "Welcome back, your blueprint is still on the table." with a **Start over** link.

#### 3.3 Estimate rail

All values come from the estimation engine (section 9). Numbers animate with a 400ms count-up/down; ranges update both ends. Under reduced motion they change instantly.

1. **Timeline**
   - Large range text: `12 to 17 weeks`
   - Below: a mini Gantt of four phases (Discover and design, Build, Test, Launch). The bar shows the longer (max) case, and a notch marks the shorter (min) case.
   - Phase labels in mono: `Design 3.3w`, `Build 7.1 to 11.3w`, and so on.
2. **Team**
   - Large text: `6 people`
   - Role chips: `1 Lead`, `1 Designer`, `3 Engineers`, `1 QA` (QA shows "part-time" when only 1 engineer).
3. **Budget**
   - Range in the selected currency, for example `$62,500 to $94,000`.
   - Label "Estimate" with an info button that opens a popover: "A rough range based on similar projects. Your real quote comes after a call and can be higher or lower. Here is what could change it: scope changes, third-party approvals, complex integrations."
4. **Notes and risks**
   - Rule-based list (section 9.7), maximum 4 visible, "Show all (n)" expands. Each item has an icon (info = `--holo`, warning = `--amber`).
5. **Primary button:** **Scan blueprint** (disabled with tooltip "Add at least 1 module" when empty).
6. Empty state: values show `Add modules to see your estimate`.

#### 3.4 Ghost chips
At the bottom edge of the canvas (section 11). Appear after at least 2 modules are placed.

#### 3.5 Help tour
Three tooltips, once, dismissible: "1. Drag modules onto the table", "2. Click a module to set options", "3. Watch the estimate update". Re-openable via (?).

### S4: Scan (transition) and S5: Plan sheet

**Scan animation (S4), 3.4 seconds total:**
| Time | Event |
|---|---|
| 0 to 300ms | Controls and rail dim to 40%; canvas scales slightly to fill the stage |
| 300 to 2700ms | A horizontal laser line (`--laser`, 2px, glow) sweeps top to bottom over the blueprint. As it passes each module, a dimension line and mono annotation fade in beside it: `MOD-03 · Payments · 3-5 wk` |
| 2700 to 3400ms | Laser fades; all annotations hold |
| 3400ms onward | Transition to S5 |

- Skippable with Escape or a "Skip" button. Reduced motion: no sweep, annotations appear instantly, 400ms fade to S5.
- The scan **creates a saved blueprint** on the server (`POST /api/blueprints`), so a private link exists. If the request fails, S5 still shows with a warning banner and the send flow retries.

**Plan sheet (S5):** a white-on-blue "printed page" (paper color `#F7FBFF`, ink `#0A1A3F`, blue accents) that slides out of a printer slot at the top of the stage with `--ease-print` over 1.8 seconds. Contents, in this order:

1. Header: company logo, "Project blueprint", blueprint ID (`BP-` + 6 characters from the ID), date.
2. **Title:** auto-generated from the sentence (capitalized, trimmed to 60 characters), editable inline. If no sentence: "Untitled project."
3. **The idea:** the sentence, plus intent.
4. **What you'll get:** the module list grouped by band, each with its chosen options in plain language.
5. **Plan:** the phase table (phase, what happens, weeks min to max).
6. **Team:** roles and counts.
7. **Budget range:** with the "Estimate" explanation.
8. **Included / Not included** (section 23.5, fixed copy plus dynamic items).
9. **Assumptions and risks:** the same rule-based list as the rail, full.
10. A miniature of the blueprint drawing (SVG) at the top-right of the sheet.

**Actions below the sheet:**
- **Edit blueprint** (secondary): returns to S3 with state intact.
- **Download PDF** (secondary): generates the PDF (section 12.5).
- **Send blueprint** (primary): opens S6.

### S6: Send blueprint
A modal/panel slides in beside the sheet (full-screen on mobile).

| Field | Type | Required | Rules |
|---|---|---|---|
| Name | text | Yes | 2 to 80 chars |
| Email | email | Yes | RFC-valid; lowercased; trimmed |
| Company | text | No | up to 120 chars |
| Phone / WhatsApp | tel | No | E.164-tolerant; up to 20 chars |
| Note | textarea | No | up to 500 chars; counter shown at 400 |
| Best time for a call | select | No | Morning / Afternoon / Evening (in your timezone); timezone detected via `Intl.DateTimeFormat().resolvedOptions().timeZone` |
| Consent | checkbox | Yes | "I agree to be contacted about this blueprint. Privacy policy." (links to `/privacy`) |

- Hidden honeypot field `website`; Cloudflare Turnstile (invisible) token sent with the request.
- **Button:** **Send blueprint**. Disabled while submitting; shows "Sending...".
- **Validation:** inline, on blur and on submit; error text under the field in `--danger`, linked via `aria-describedby`; focus moves to the first invalid field on submit.
- **Errors:** network failure shows "We couldn't send your blueprint. Your work is saved. Try again, or email us at {email}." with a Retry button. Rate-limit (429) shows "Too many attempts. Please try again in a minute."

### S7: Launch animation and confirmation
- **Capsule animation, 1.6s:** the blueprint miniature folds (3 steps of rotateX) into a glowing capsule, which shoots up-right off the table with a trail. Skippable; reduced motion shows a 300ms fade.
- **Confirmation screen:**
  - Heading: "Blueprint sent." Subheading: "Thanks, {firstName}. It's on its way to {engineerName}."
  - Reference: `BP-XXXXXX`.
  - Three "What happens next" items:
    1. "{engineerName} reads your blueprint within one working day."
    2. "You get a 30-minute call that starts from your design, not from zero."
    3. "You get a private link to edit or forward your blueprint."
  - Buttons: **Copy link**, **Forward to a co-founder** (opens `mailto:` with subject and link), **Book a time now** (opens `/talk` booking embed, P1).
  - A small note: "We sent a copy to {email}."

### S8: Saved blueprint page `/b/[id]`
- Server-rendered read-only view: the plan sheet and the blueprint drawing, a "Download PDF" button, and **Open in the Build Table** if the `edit` token is present or valid in localStorage.
- Editing on this page loads the table with the saved state; saving again increments `version` and re-notifies the assigned engineer only if the enquiry was already sent ("Updated blueprint" email, rate-limited to 1 per hour).

### S9: Dock pages (`/work`, `/team`, `/talk`)
- Normal responsive pages styled with the same tokens (grid background, chamfered cards).
- `/work`: card grid of projects (`projects.json`). Each case study has: problem, what we built, the blueprint of the project (the same SVG renderer, read-only), actual vs. estimated timeline, results, and a **Start from this blueprint** button which loads its modules into the Build Table (state is replaced after a confirm if the table is not empty).
- `/team`: grid of team cards (photo as a duotone blue hologram effect, name, role, short bio, one fun fact).
- `/talk`: three options: **Book a 30-minute call** (Cal.com embed or configurable URL), **Email us**, **WhatsApp / Call**. A line: "Prefer to start with a plan? Open the Build Table."

### S10: Error and empty states
- **404:** drafting-paper page, headline "That page isn't on the table.", buttons **Open the Build Table** and **See our work**.
- **500:** "Something broke on our side. Your blueprint is saved in this browser."
- **Offline:** banner "You're offline. You can keep building. We'll send your blueprint when you're back online." (the table works offline after first load; sending queues until online, P2.)

---

## 7. The module catalog

All modules are data in `config/modules.json` (schema in 7.2). The table below is the complete v1 catalog. **Effort is in person-weeks of build effort** (min to max) before option multipliers.

### 7.1 Catalog

| ID | Name | Band | Effort (pw) | Requires | Recommends | Options (multiplier on effort) |
|---|---|---|---|---|---|---|
| `web_app` | Website or web app | Interfaces | 4 to 6 | none | none | **Size:** Small, up to 10 screens (x0.8) / Medium, up to 25 (x1.0, default) / Large, 25+ (x1.4) |
| `mobile_app` | Mobile app | Interfaces | 8 to 12 | none | `notifications` | **Platform:** iOS only (x0.85) / Android only (x0.85) / Both (x1.0, default) |
| `web_dashboard` | Web dashboard | Interfaces | 4 to 6 | `user_login` | `analytics_reports` | **Size:** Simple, up to 5 views (x0.8) / Standard (x1.0, default) / Rich, 12+ views (x1.4) |
| `admin_panel` | Admin panel | Interfaces | 3 to 5 | `user_login` | none | **Roles:** One admin role (x1.0, default) / Multiple roles and permissions (x1.4) |
| `user_login` | User login | Foundations | 1.5 to 2.5 | none | none | **Methods:** Email and password (x1.0, default) / + Social login (x1.2) / + Phone OTP (x1.2) / Social and OTP (x1.4) |
| `payments` | Payments | Features | 3 to 5 | `user_login` | `notifications` | **Methods:** Cards only (x1.0, default) / Cards, UPI and wallets (x1.3) / Plus subscriptions (x1.6) |
| `notifications` | Notifications | Features | 1.5 to 2.5 | `user_login` | none | **Channels:** Email only (x0.6) / Email and push (x1.0, default) / Email, push and SMS (x1.3) |
| `booking` | Booking and scheduling | Features | 3 to 5 | `user_login` | `notifications`, `payments` | **Scope:** One provider (x1.0, default) / Multiple providers or locations (x1.5) |
| `ai_assistant` | AI assistant | Features | 4 to 7 | none | `user_login`, `file_storage` | **Type:** Support chatbot (x1.0, default) / Answers from your documents (x1.2) / Workflow automation (x1.5) |
| `search` | Search | Features | 2 to 3 | none | none | **Level:** Basic keyword (x1.0, default) / Filters and suggestions (x1.4) |
| `analytics_reports` | Analytics and reports | Features | 2 to 4 | any of: `web_dashboard`, `admin_panel` | none | **Depth:** Key numbers only (x0.8) / Standard charts and export (x1.0, default) / Custom reports (x1.4) |
| `chat_messaging` | In-app chat | Features | 3 to 5 | `user_login` | `notifications` | **Type:** One-to-one (x1.0, default) / Groups too (x1.4) |
| `maps_location` | Maps and location | Features | 2 to 3 | none | none | **Use:** Show locations (x1.0, default) / Live tracking (x1.6) |
| `file_storage` | File uploads and storage | Foundations | 1 to 2 | none | none | **Types:** Images and documents (x1.0, default) / Plus video (x1.5) |
| `integrations` | Integrations with other tools | Foundations | 2 to 4 per integration | none | `admin_panel` | **Count:** 1 (x1.0, default) / 2 (x1.8) / 3 or more (x2.5). Counted as one module on the table |
| `multilanguage` | Multiple languages | Foundations | 1 to 2 | none | none | **Languages:** 2 (x1.0, default) / 3 to 4 (x1.4) / 5 or more (x1.8) |

### 7.2 JSON schema for a module

```jsonc
{
  "id": "payments",
  "name": "Payments",
  "band": "features",                    // "interfaces" | "features" | "foundations"
  "icon": "payments",                    // file name in /public/icons
  "short": "Let customers pay inside your product.",
  "description": "Customers pay for orders or appointments inside the product. Includes receipts and refunds.",
  "effort": { "min": 3, "max": 5 },      // person-weeks
  "requires": ["user_login"],            // all must be present
  "requiresAny": [],                     // at least one must be present
  "recommends": ["notifications"],       // soft suggestion only
  "options": [
    {
      "id": "methods",
      "label": "Payment methods",
      "type": "single",                  // single-select only in v1
      "choices": [
        { "id": "cards",   "label": "Cards only",             "mult": 1.0, "default": true,
          "help": "Debit and credit cards." },
        { "id": "upi",     "label": "Cards, UPI and wallets", "mult": 1.3,
          "help": "Adds local payment methods that many customers prefer." },
        { "id": "subs",    "label": "Plus subscriptions",     "mult": 1.6,
          "help": "Adds recurring billing, plan changes and failed-payment retries." }
      ]
    }
  ],
  "suggestKeywords": ["pay", "payment", "invoice", "subscription", "billing"],
  "notes": [                             // rule-based risks, see 9.7
    { "type": "warning",
      "text": "Your payment provider must approve your business before live payments start. This usually takes 1 to 3 weeks and runs alongside the build." }
  ],
  "glyph": "payments"                    // blueprint SVG symbol id, see 10.4
}
```

### 7.3 Plain-language descriptions (use verbatim)

| ID | Description (max 2 sentences) |
|---|---|
| `web_app` | The part of your product people use in a browser, on any device. Includes the pages, navigation and look and feel. |
| `mobile_app` | An app people install from the App Store or Google Play. We build it once and tune it for each phone. |
| `web_dashboard` | A private area where people see their data in one place, such as orders, bookings or reports. |
| `admin_panel` | A back office for your own team to manage users, content and settings without calling a developer. |
| `user_login` | People create an account and sign in securely. Includes password reset and keeping accounts safe. |
| `payments` | Customers pay for orders or appointments inside the product. Includes receipts and refunds. |
| `notifications` | Messages that reach people at the right time, such as booking reminders or order updates. |
| `booking` | People pick a time or slot and confirm it. Includes availability, changes and cancellations. |
| `ai_assistant` | An assistant that answers questions or does tasks for your customers or team, using your own information. |
| `search` | People find what they need quickly, by typing or by filtering. |
| `analytics_reports` | Charts and exports that show how your business or product is doing. |
| `chat_messaging` | People message each other inside the product, with history that is saved. |
| `maps_location` | Show places on a map, or follow an item or person in real time. |
| `file_storage` | People upload photos or documents, and they are stored safely and can be viewed later. |
| `integrations` | Your product talks to other tools you already use, such as a CRM, accounting software or an existing system. |
| `multilanguage` | The product works in more than one language, including switching between them. |

### 7.4 Icon concepts (one line-icon each)
web_app: browser window with a cursor. mobile_app: phone outline with a notch. web_dashboard: window with a bar chart. admin_panel: gear over a window. user_login: padlock beside a person silhouette. payments: card with a check. notifications: bell with a signal arc. booking: calendar with a clock. ai_assistant: chat bubble with a spark. search: magnifier over lines. analytics_reports: line chart with a document corner. chat_messaging: two overlapping bubbles. maps_location: map pin on a folded map. file_storage: folder with an up arrow. integrations: two plug ends meeting. multilanguage: speech bubble with two glyphs.

---

## 8. Dependency rules

### 8.1 Types
- **requires:** hard rule. Module cannot exist on the table without every listed module.
- **requiresAny:** hard rule. At least one of the listed modules must exist.
- **recommends:** soft. Shows a suggestion in the rail notes and a dotted amber line; never blocks.

### 8.2 Adding a module with unmet requirements
When the user places a module whose `requires`/`requiresAny` are not satisfied:
1. The module is placed in a **pending** state (dashed amber outline).
2. A hologram dialog appears anchored to it: "**{Module}** needs **{Required}**. Add it?" with buttons **Add both** (primary) and **Cancel**.
   - For `requiresAny`: "**Analytics and reports** needs a dashboard or an admin panel. Which one?" with a button per choice and **Cancel**.
3. **Add both:** the required module is placed (it flies in from the tray, 480ms), line draws, pending state clears. Estimates update once, after both are placed.
4. **Cancel:** the pending module returns to the tray.
5. If the user ignores the dialog and clicks elsewhere, the pending module stays pending but is **excluded from estimates** and shows a persistent small badge "Needs {Required}". The Scan button is disabled while any module is pending, with tooltip "Resolve modules that need others".

### 8.3 Removing a module that others require
- Removal is **blocked**. The dependents' outlines pulse `--danger` once, and the connecting lines to them flash red (3 flashes, 120ms each).
- A dialog explains: "**{Module}** is needed by **{Dependent A}** and **{Dependent B}**." Buttons: **Remove all three** (removes the module and dependents, undoable) and **Keep**.

### 8.4 Recommends
- When a recommended module is absent, the rail shows a note: "Most {booking} products also add {notifications}. Add it?" with an **Add** link. The dismissal is remembered per blueprint (`dismissedRecommendations`).

### 8.5 Single instance rule
Every module can exist **once** on the table. Integrations count as a single module with a count option.

### 8.6 Satisfied dependencies on the drawing
Lines for satisfied requirements draw in `--ok`; recommended-but-absent show as a dotted amber stub from the module toward a ghost slot.

---

## 9. Estimation engine

Pure, deterministic, side-effect-free TypeScript module `lib/estimate.ts` with unit tests. Inputs: placed modules with chosen options, `pricing.json`. Output: the `Derived` object (12.3).

### 9.1 Definitions
- `n` = number of placed modules (including auto-added dependencies, excluding pending).
- For each module `m`: `optMult(m)` = product of the multipliers of its selected option choices (v1 has one option group per module).
- `effMin(m) = m.effort.min * optMult(m)`, `effMax(m) = m.effort.max * optMult(m)` (person-weeks).
- `buildMin = sum(effMin)`, `buildMax = sum(effMax)`, `buildMid = (buildMin + buildMax) / 2`.

### 9.2 Team size
- `engineers = clamp( ceil(buildMid / 8), 1, 8 )`
- Roles: `1 Lead`, `1 Designer`, `engineers` Engineers, `1 QA` (flag `partTime = true` when `engineers == 1`).
- Displayed team size = `engineers + 3`.

### 9.3 Timeline (weeks)
Constants from `pricing.json`: `efficiency = 0.8`, `designBase = 2`, `designPerModule = 0.25`, `testRatio = 0.15`, `launchWeeks = 1`.

```
designWeeks = designBase + designPerModule * n
buildWeeksMin = buildMin / (engineers * efficiency)
buildWeeksMax = buildMax / (engineers * efficiency)
testWeeksMin = testRatio * buildWeeksMin
testWeeksMax = testRatio * buildWeeksMax
totalMin = designWeeks + buildWeeksMin + testWeeksMin + launchWeeks
totalMax = designWeeks + buildWeeksMax + testWeeksMax + launchWeeks
display  = round(totalMin) to round(totalMax)   // Math.round; ensure min <= max
```
Phases are sequential in v1. Phase output includes both min and max week values (unrounded to 2 decimals; rounded for display to 1 decimal).

**Critical-path check:** compute the longest chain of `requires` effort (sum of `effMax` along any chain, divided by 0.8). If it exceeds `buildWeeksMax`, set `buildWeeksMax` to the chain value (re-derive totals). In v1 catalog this almost never triggers but the code must include it.

### 9.4 Budget
Constants: `qaRatio = 0.2`, `qaMinPw = 1`, `mgmtRatio = 0.10`, `rate[currency]` (cost per person-week), `roundTo = 500`.

```
designPw = designWeeks                                  // 1 designer
qaPwMin  = max(qaMinPw, qaRatio * buildMin)
qaPwMax  = max(qaMinPw, qaRatio * buildMax)
subMin   = buildMin + designPw + qaPwMin
subMax   = buildMax + designPw + qaPwMax
totalPwMin = subMin * (1 + mgmtRatio)
totalPwMax = subMax * (1 + mgmtRatio)
budgetMin = roundTo(totalPwMin * rate, 500)             // round to nearest 500
budgetMax = roundTo(totalPwMax * rate, 500)
```
Default placeholder rate: **2400 per person-week (USD)**. Other currencies in `pricing.json` (section 14). Format with `Intl.NumberFormat` by locale; for INR use lakh grouping (`en-IN`).

### 9.5 Included and not included
Fixed lists in the copy deck (section 23.5). Dynamic additions: for each placed module, one "Included" line from its `short` text.

### 9.6 Phase descriptions (used in the plan sheet)
| Phase | What happens |
|---|---|
| Discover and design | Workshop to confirm goals and users, then screens and a clickable prototype you approve. |
| Build | Engineers build in weekly releases. You see progress every Friday. |
| Test | Testing on real devices and real scenarios, and fixing what we find. |
| Launch | Go-live, store submission if needed, and monitoring during the first days. |

### 9.7 Notes and risks (rule engine)
Each rule: `{ when: (state) => boolean, type: "info" | "warning", text, priority }`. Show highest priority first.

| Rule | Type | Text |
|---|---|---|
| `payments` present | warning | Your payment provider must approve your business before live payments start. This usually takes 1 to 3 weeks and runs alongside the build. |
| `mobile_app` present | info | App store review takes 1 to 7 days for each release. We plan for it. |
| `ai_assistant` present | warning | AI answers need testing with your real information. We add review rounds so you can check quality before launch. |
| `integrations` present | warning | Timelines depend on how good the other tool's API is and how quickly we get access. |
| `maps_location` with `live tracking` | info | Live tracking can raise running costs for map services as you grow. |
| `user_login` with social/OTP | info | Social login and OTP need accounts with those providers; we help set them up. |
| `n >= 8` | warning | This is a large project. We often split it into two releases so you launch sooner. |
| `buildMax - buildMin > 10` | info | Your range is wide because several modules have options that change effort a lot. A call will narrow it. |
| Any recommended module absent | info | See 8.4 text. |
| `multilanguage` present | info | Translations are provided by you or a translator; we build the system to hold them. |
| `analytics_reports` present | info | Reports depend on having clean data. We check your data sources early. |

### 9.8 Test fixtures (must pass in CI)

**Fixture A: "Clinic app".** Modules: `mobile_app` (Both), `payments` (Cards only), `notifications` (Email and push), `user_login` (Email and password), `booking` (One provider). Rate USD 2400.
- `n = 5`, `buildMin = 17`, `buildMax = 27`, `buildMid = 22`, `engineers = 3`, team size `6`.
- `designWeeks = 3.25`. `buildWeeksMin = 7.083`, `buildWeeksMax = 11.25`. `testWeeksMin = 1.0625`, `testWeeksMax = 1.6875`.
- `totalMin = 12.396 -> 12`, `totalMax = 17.1875 -> 17`. **Display: 12 to 17 weeks.**
- `qaPwMin = 3.4`, `qaPwMax = 5.4`. `totalPwMin = 26.015`, `totalPwMax = 39.215`. **Budget: $62,500 to $94,000.**

**Fixture B: "Simple site".** Modules: `web_app` (Medium). Rate USD 2400.
- `n = 1`, `buildMin = 4`, `buildMax = 6`, `engineers = 1`, team size `4` (QA part-time).
- `designWeeks = 2.25`. `buildWeeksMin = 5.0`, `buildWeeksMax = 7.5`. `testWeeksMin = 0.75`, `testWeeksMax = 1.125`.
- `totalMin = 9.0`, `totalMax = 11.875`. **Display: 9 to 12 weeks.**
- `qaPwMin = 1`, `qaPwMax = 1.2`. `totalPwMin = 7.975`, `totalPwMax = 10.395`. **Budget: $19,000 to $25,000.**

**Fixture C: "Payments with auto-added login".** Modules: `payments` (Cards only), `user_login` (Email and password).
- `n = 2`, `buildMin = 4.5`, `buildMax = 7.5`, `engineers = 1`, team size `4`.
- `designWeeks = 2.5`. `buildWeeksMin = 5.625`, `buildWeeksMax = 9.375`. `testWeeksMin = 0.844`, `testWeeksMax = 1.406`.
- `totalMin = 9.97 -> 10`, `totalMax = 14.28 -> 14`. **Display: 10 to 14 weeks.**
- `qaPwMin = 1`, `qaPwMax = 1.5`. `totalPwMin = 8.8`, `totalPwMax = 12.65`. **Budget: $21,000 to $30,500.**

**Fixture D: dependency edge cases (logic tests).**
1. Add `payments` alone: result state has `payments` pending, estimate uses 0 modules until resolved.
2. Add `analytics_reports` with neither `web_dashboard` nor `admin_panel`: dialog offers both choices.
3. Remove `user_login` while `payments` and `booking` exist: blocked, lists both dependents.
4. Option change `mobile_app: ios` on Fixture A: `buildMin = 17 - 8*0.15 = 15.8`, `buildMax = 27 - 12*0.15 = 25.2`.

---

## 10. Blueprint rendering

The blueprint is a single SVG (`<svg viewBox="0 0 1200 720">`) rendered by `components/Blueprint.tsx`, used on the canvas (interactive), the plan sheet (miniature), `/b/[id]` (read-only), PDF export and case studies. It is a **pure function of the blueprint state**.

### 10.1 Layout algorithm
Three horizontal bands:

| Band | Center Y | Contains |
|---|---|---|
| Interfaces | 130 | modules with `band = "interfaces"` |
| Features | 360 | modules with `band = "features"` |
| Foundations | 590 | modules with `band = "foundations"` |

- Node size: 160 x 96. Band label (mono, 13px, left edge, `--ink-dim`): "Interfaces", "Features", "Foundations", with a dashed horizontal divider line at the band's top edge.
- Within a band, with `k` nodes, the x-center of node `i` (0-based) is: `x = 120 + (960 / k) * (i + 0.5) + 60` clamped so nodes never overlap (minimum center spacing 184). If `k > 5` in a band, the band wraps to a second row (`+ 130` px in Y) and the viewBox height increases to 850 (the SVG scales to fit).
- **Slots:** the canvas shows empty slot outlines (dashed) in the band order until filled; during drag the nearest valid slot highlights.

### 10.2 Buses and connections
- **Bus A** at y = 245 connects Interfaces and Features. **Bus B** at y = 475 connects Features and Foundations. Each is a horizontal line (1px, `--line` 50% opacity) spanning from the leftmost to rightmost node x in the two bands it joins.
- Each node has a vertical **stub** (1px) from its top/bottom edge to the adjacent bus (Interfaces: bottom to Bus A; Features: top to Bus A and bottom to Bus B; Foundations: top to Bus B).
- **Dependency lines** (requires satisfied): orthogonal path (horizontal/vertical segments, 8px corner radius) from the dependent node to the required node, `--ok`, 2px. Draw order: stub lines, then dependency lines.
- **Recommended but absent:** dotted amber stub (2px, `stroke-dasharray: 2 6`) from the module toward the nearest empty slot, ending with a small plus marker.
- **Blocked / conflict flash:** lines to dependents animate stroke `--danger` for 3 x 120ms.

### 10.3 Annotations (always visible, small)
- Under each node: mono label `MOD-01` (index by order of addition) and effort: `4-6 wk` (after options).
- Top-left of the canvas: blueprint title block like a technical drawing: `PROJECT: {title}`, `SCALE: 1:1`, `SHEET: 1/1`, `REV: {version}`. (This is real data from state; `SCALE` and `SHEET` are fixed text.)

### 10.4 Glyph drawing animation
- Each module has an SVG symbol (line art, larger than the tray icon: 72 x 72) drawn inside the node.
- On placement: path `stroke-dasharray`/`stroke-dashoffset` animation over 600ms (`--ease-out`), staggered 40ms per path. Node outline draws first (clockwise, 300ms), then the glyph, then the label fades in.
- **Re-render rule:** only newly added elements animate; existing elements update positions with 240ms transitions when the layout shifts (use keyed React components and FLIP animation).
- Reduced motion: no stroke animation; 120ms fade.

### 10.5 Export
`renderBlueprintSVG(state): string` produces a static SVG string (no animation, system fonts embedded as web-safe fallbacks) for PDF and email image rendering. Email image: PNG 1200 x 720 rendered server-side from the SVG (`sharp`/resvg).

---

## 11. Ghost overlay (similar past projects)

### 11.1 Data
`config/projects.json`: each project has `id`, `slug`, `name`, `summary`, `modules` (array of `{id, options}`), `actual` (`{ weeks, teamSize, budgetBand }`), `result` (one line), `cover` (image or blueprint SVG).

### 11.2 Matching
After at least 2 modules are placed: for each project, compute Jaccard similarity of module ID sets, `J = |A ∩ B| / |A ∪ B|`. Show projects with `J >= 0.4`, top 2, sorted by `J` descending.

### 11.3 Chips
- At the canvas bottom, a chip per match: ghost mini-blueprint outline (faint, 60 x 36) + text `Similar: {project name}` + `{percentage} match`.
- Animation: chips fade/slide in once (240ms); no repeated attention-seeking motion.

### 11.4 Overlay mode
On click/tap/Enter on a chip:
- The project's blueprint draws **over** the user's with a translucent layer.
- **Legend** (top-right of canvas): solid cyan outline = "in both", dashed amber = "only in {project}", dashed white = "only in yours".
- A side card replaces the rail's lower section: project name, summary, "Their actual timeline: 14 weeks (our estimate for yours: 12 to 17)", team size, result line, and two buttons: **View case study** (`/work/[slug]`, new tab) and **Add missing modules** (adds the project's extra modules as pending suggestions, not placed).
- Exit with an **X**, Escape, or clicking the chip again. Overlay never changes the user's blueprint.

---

## 12. Backend, API and data models

### 12.1 Approach
Next.js route handlers (or an equivalent small Node service), PostgreSQL via Prisma. All inputs validated with `zod`. All responses JSON. IDs: `nanoid(12)` (url-safe).

### 12.2 Data models (Prisma-style)

```prisma
model Blueprint {
  id            String   @id            // nanoid(12)
  version       Int      @default(1)
  title         String
  intent        String                  // "new" | "upgrade" | "ai"
  sentence      String?
  state         Json                    // BlueprintState (12.3)
  derived       Json                    // Derived (12.3), cached
  currency      String   @default("USD")
  editTokenHash String                  // sha256 of edit token
  status        String   @default("draft") // draft | sent
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt
  enquiry       Enquiry?
}

model Enquiry {
  id            String   @id
  blueprintId   String   @unique
  blueprint     Blueprint @relation(fields: [blueprintId], references: [id])
  name          String
  email         String
  company       String?
  phone         String?
  note          String?
  preferredTime String?                 // "morning" | "afternoon" | "evening"
  timezone      String?
  consent       Boolean
  consentAt     DateTime
  ipHash        String                  // sha256(ip + daily salt)
  userAgent     String?
  assignedTo    String?                 // team member id from team.json
  status        String   @default("new") // new | contacted | call_booked | won | lost
  followUpSentAt DateTime?
  createdAt     DateTime @default(now())
}
```

### 12.3 Shared TypeScript types

```ts
type Intent = "new" | "upgrade" | "ai";

interface PlacedModule {
  id: string;                          // module id
  options: Record<string, string>;     // optionGroupId -> choiceId
  order: number;                       // order of addition (1-based)
  pending?: boolean;                   // unmet dependency
}

interface BlueprintState {
  schema: 1;
  intent: Intent;
  sentence?: string;
  title?: string;
  modules: PlacedModule[];
  dismissedRecommendations: string[];
  currency: "USD" | "EUR" | "INR";
}

interface Derived {
  n: number;
  build: { minPw: number; maxPw: number };
  team: { engineers: number; size: number; roles: { role: string; count: number; partTime?: boolean }[] };
  phases: { id: "design" | "build" | "test" | "launch"; minWeeks: number; maxWeeks: number }[];
  weeks: { min: number; max: number };               // rounded display values
  budget: { min: number; max: number; currency: string };
  notes: { type: "info" | "warning"; text: string; moduleId?: string }[];
}
```

### 12.4 Endpoints

| Method and path | Purpose | Request | Response |
|---|---|---|---|
| `POST /api/blueprints` | Create a blueprint (at Scan) | `{ state: BlueprintState }` | `201 { id, editToken, derived, url }` |
| `PUT /api/blueprints/[id]` | Update a blueprint | header `X-Edit-Token`; `{ state, expectedVersion }` | `200 { version, derived }` or `409` on version mismatch |
| `GET /api/blueprints/[id]` | Read a blueprint (read-only) | none | `200 { id, title, state, derived, version, status }` (no tokens, no personal data) |
| `POST /api/blueprints/[id]/send` | Send the blueprint as an enquiry | header `X-Edit-Token`; `{ name, email, company?, phone?, note?, preferredTime?, timezone?, consent, turnstileToken, website? }` | `200 { reference, assignedTo: { firstName, photo }, url }` |
| `GET /api/blueprints/[id]/pdf` | PDF of the plan sheet | none | `application/pdf` |
| `GET /api/blueprints/[id]/image` | PNG of the blueprint | none | `image/png` |
| `GET /api/admin/enquiries` | Admin list (protected) | query: `status`, `q`, `page` | paginated list |
| `PATCH /api/admin/enquiries/[id]` | Admin updates status/assignee | `{ status?, assignedTo? }` | `200` |
| `GET /api/admin/enquiries.csv` | CSV export (protected) | none | `text/csv` |

**Rules:**
- The server **recomputes** `derived` from `state` using the same `lib/estimate.ts` on every create/update/send. Never trust client-provided derived values.
- The server validates `state`: unknown module IDs rejected; option choices must exist; dependency rules must pass (no pending modules saved); at most 20 modules.
- **Rate limits:** 10 blueprint writes per IP per hour; 3 sends per IP per hour; 1 send per blueprint per 10 minutes (re-send allowed afterwards, flagged "updated"). Return `429` with `Retry-After`.
- **Spam:** Turnstile verification on send; honeypot `website` must be empty; reject disposable email domains (configurable list).
- **Assignment:** round-robin across `team.json` members flagged `takesEnquiries: true`, stored in `assignedTo`.
- **Edit token:** random 32 bytes, base64url; only the hash is stored; returned once at creation, stored in the browser's localStorage (`vf.edit.[id]`) and included in the confirmation email link.
- **Idempotency:** `send` accepts an `Idempotency-Key` header (uuid) to prevent duplicates on retry.

### 12.5 PDF generation
Server-side render of the plan sheet page (`/b/[id]/print`) using Playwright/Chromium to PDF, A4, print stylesheet (white background, ink-blue text, blueprint SVG at top). Cache by `id + version`. Fallback: `@react-pdf/renderer` template.

### 12.6 Admin
`/admin` protected by HTTP basic auth or an allow-listed email magic link (config: `ADMIN_EMAILS`). Features (P1): table of enquiries (date, name, email, title, modules count, weeks, budget range, status, assignee), search, status change, "Open blueprint" (read-only view), CSV export. Never indexed.

---

## 13. Emails

Transport: Resend or SendGrid (config). From: `{COMPANY_NAME} <hello@{DOMAIN}>`. Plain-text alternative for all emails. Unsubscribe line in follow-up.

### 13.1 To the client, immediately after send
**Subject:** `Your blueprint is with {engineerFirstName}: {title}`
**Body (HTML + text):**
- Greeting: "Hi {firstName},"
- "Thanks for sending your blueprint. {engineerName} will read it within one working day and reach out to schedule a 30-minute call."
- Blueprint image (PNG), caption "Reference BP-XXXXXX".
- Summary table: Timeline, Team, Budget range (labeled as estimate).
- Buttons: **Open your blueprint** (edit link with token), **Download PDF**.
- Footer: company address, privacy link.

### 13.2 To the team (internal), immediately after send
**To:** the assigned engineer + `ENQUIRY_CC` list. **Subject:** `New blueprint: {title} ({weeksMin}-{weeksMax} wk, {budgetRange}) from {name}`
**Body:** client details, note, preferred time and timezone, the full plan (modules with options), derived numbers, link to admin view, JSON attachment of the blueprint state, PNG image.

### 13.3 Follow-up (48 hours later, only if `status = "new"` and no booking)
**Subject:** `Your {title} is still on the table`
**Body:** blueprint image, one sentence: "You were {n} modules in. Pick it up where you left off, or book a quick call." Buttons: **Open your blueprint**, **Book a call**. Sent once only (`followUpSentAt`). Skipped if the user replied/booked or if consent was missing.

### 13.4 Update notification (blueprint edited after sending)
To the assigned engineer only. Subject: `Updated blueprint: {title} (v{version})`. Includes a diff summary (modules added/removed/option changes).

---

## 14. Configuration files

All content that a non-developer might change lives in `/config` (typed, validated at build time with zod):

| File | Content |
|---|---|
| `brand.json` | `companyName`, `tagline`, `logoSvg`, `contactEmail`, `phone`, `whatsapp`, `address`, `socials` |
| `modules.json` | Module catalog (section 7) |
| `pricing.json` | Constants and per-currency rates (14.1) |
| `projects.json` | Past projects (section 11.1) |
| `team.json` | Team members: `id`, `firstName`, `name`, `role`, `photo`, `bio`, `funFact`, `takesEnquiries` |
| `copy.json` | All UI strings (section 23) for easy edits and later translation |
| `keywords.json` | Keyword suggestion map (6.1) |

### 14.1 `pricing.json`

```json
{
  "efficiency": 0.8,
  "designBase": 2,
  "designPerModule": 0.25,
  "testRatio": 0.15,
  "launchWeeks": 1,
  "qaRatio": 0.2,
  "qaMinPw": 1,
  "mgmtRatio": 0.10,
  "roundTo": 500,
  "defaultCurrency": "USD",
  "rates": { "USD": 2400, "EUR": 2200, "INR": 150000 },
  "locales": { "USD": "en-US", "EUR": "de-DE", "INR": "en-IN" },
  "_note": "Rates are placeholders. The company owner must confirm before launch."
}
```
Auto-pick the initial currency from the browser locale (`INR` for `en-IN`, `EUR` for common EU locales, else `USD`); the visitor can change it in the header.

### 14.2 Environment variables

```
DATABASE_URL=
APP_URL=
EMAIL_PROVIDER=resend            # resend | sendgrid
EMAIL_API_KEY=
EMAIL_FROM=
ENQUIRY_CC=
TURNSTILE_SITE_KEY=
TURNSTILE_SECRET_KEY=
ADMIN_EMAILS=
IP_HASH_SALT=
CAL_BOOKING_URL=
ANALYTICS_PROVIDER=plausible     # plausible | posthog | none
ANALYTICS_DOMAIN=
```

---

## 15. Accessibility (WCAG 2.2 AA is required)

1. **Full keyboard path.** Everything that can be done by dragging can be done by keyboard:
   - Tab moves through: header/dock, tray tabs, tray modules, canvas modules, rail, primary button.
   - On a tray module: **Enter** or **Space** opens its info card with **Add to blueprint**; **Arrow keys** move between tray modules.
   - On a placed module: **Enter** opens options; **Delete/Backspace** starts removal; **Alt + Left/Right arrow** reorders within the band.
   - **Escape** closes dialogs, overlays, and skips the scan or launch animation.
2. **List view toggle.** A visible button "Use list view" (also auto-offered for screen reader users via the first focusable element) switches the canvas to an accessible, standard form: a checklist of modules with option selects and a text summary of the blueprint. This view is functionally complete and feeds the same state.
3. **ARIA live region** (`role="status"`, `aria-live="polite"`) announces: "Payments added. Estimate is now 12 to 17 weeks, 6 people, $62,500 to $94,000." Announcements are debounced to 800ms.
4. **Blueprint SVG:** `role="img"` with `aria-label` generated from the state ("Blueprint with 5 modules: ...") plus a visually hidden list of modules and dependencies. Individual nodes are `button`-like elements with accessible names (not SVG-only).
5. **Focus visibility:** 2px `--holo` outline with 2px offset on every focusable element; never remove it. Focus is trapped in dialogs and returned to the trigger on close.
6. **Reduced motion:** honor `prefers-reduced-motion`; also provide a manual **"Reduce motion"** toggle in the help menu.
7. **Color is never the only signal.** Dependency states have icons and text, not only color. Errors have an icon and text.
8. **Pointer targets** at least 44 x 44 px on touch; no drag-only critical actions; no hover-only information (long-press on touch; also reachable via focus).
9. **Forms:** labels always visible, error messages programmatically associated, autocomplete attributes (`name`, `email`, `tel`, `organization`).
10. **Language and structure:** `lang` set; one `h1` per page; landmarks (`header`, `main`, `nav`, `footer`).
11. **Time limits:** none. No auto-advancing content except the boot sequence, which can be skipped.
12. **Testing:** axe-core in CI on every route and key state; manual checks with VoiceOver and NVDA before launch.

---

## 16. Responsive behaviour

| Breakpoint | Layout |
|---|---|
| 1100px and up | Three columns (tray, canvas, rail) as in S3 |
| 768 to 1099px (tablet) | Canvas full width. Tray becomes a **bottom sheet** (peek height 96px, drag up to 60% height). Rail becomes a **collapsible top bar** showing the summary numbers; tap to expand. |
| 0 to 767px (mobile) | One-column flow with a **sticky bottom bar**: `[ + Add module ]   12-17 wks · $62.5k-94k   [ Scan ]`. Tapping Add module opens the tray as a full-screen sheet (list with descriptions). Adding is by **tap (Add)**, not drag. The blueprint canvas is a vertically scrollable SVG (bands stacked, nodes 140 x 84, two per row). Rail details open in a bottom sheet. |

- Boot sequence on mobile: same, scaled; headline 36px.
- The plan sheet scrolls vertically, actions are a sticky footer.
- Send form: full-screen, one column, keyboard-aware (`inputmode`, `enterkeyhint`).
- Haptics (mobile): `navigator.vibrate(10)` on snap/add where supported; off under reduced motion.
- Orientation: landscape on phones uses the tablet layout.

---

## 17. SEO and non-interactive fallback

The Build Table is a client-side app, but the company must still be found and understood.

1. **Server-rendered content on `/`:** below the app region (and available without JavaScript in `<noscript>` and in the DOM for crawlers), include real text: an H1 "Software development company that designs your project with you", a 3-paragraph description of services, the process in 4 steps, links to `/work`, `/team`, `/talk`.
2. **Real pages for each dock link** (section 9 of routes) with unique titles and meta descriptions, Open Graph tags, and structured data (`Organization`, `ProfessionalService`; `CreativeWork` for case studies).
3. **`sitemap.xml` and `robots.txt`:** include `/`, `/work`, `/work/*`, `/team`, `/talk`, `/privacy`. Disallow `/b/`, `/admin`, `/api/`.
4. **Social image:** a static image of a finished blueprint (1200 x 630), and dynamic OG image for `/work/[slug]` using the project's blueprint.
5. **No-JS behaviour:** `<noscript>` shows the text content and the three dock links plus an email link. No form or tool is required without JS.
6. **Core Web Vitals:** see section 19.

---

## 18. Analytics, privacy and security

### 18.1 Analytics events
Use a privacy-friendly, cookieless provider (Plausible or PostHog with persistence off by default). **No personal data in event properties** (no email, name, free text).

| Event | Properties |
|---|---|
| `boot_skipped` | `method` (click/key) |
| `intent_selected` | `intent` |
| `sentence_submitted` | `length`, `suggested_count` |
| `module_added` | `id`, `method` (drag/tap/keyboard), `count_after` |
| `module_removed` | `id`, `count_after` |
| `option_changed` | `module`, `option`, `choice` |
| `dependency_prompt` | `module`, `required`, `result` (added/cancelled) |
| `ghost_opened` | `project` |
| `help_opened` | none |
| `scan_started` | `count`, `weeks_min`, `weeks_max`, `budget_min_band` |
| `pdf_downloaded` | none |
| `send_started` | none |
| `send_succeeded` | `count` |
| `send_failed` | `reason` |
| `dock_clicked` | `target` |
| `currency_changed` | `to` |

Funnel: `intent_selected` to `module_added` to `scan_started` to `send_succeeded`.

### 18.2 Privacy
- Visitor-provided personal data (name, email, company, phone, note) is stored only after the visitor presses Send, with explicit consent. The anonymous blueprint saved at Scan contains no personal data.
- Anonymous drafts older than 90 days and never sent are deleted automatically (daily job).
- IP addresses are not stored, only a salted hash that rotates daily.
- Provide a data-deletion contact in `/privacy`; admin can delete an enquiry and its blueprint.
- If the analytics provider is not cookieless, show a cookie consent banner and load analytics only after consent. Cookies/localStorage used for functionality (`vf.blueprint.v1`, `vf.seen`, `vf.edit.*`, theme) are strictly necessary and listed in `/privacy`.

### 18.3 Security
- HTTPS only, HSTS, strict CSP (no inline scripts except hashed ones), `X-Content-Type-Options`, `Referrer-Policy: strict-origin-when-cross-origin`, `frame-ancestors 'none'` (except for the Cal embed origin if needed).
- All user-provided text is escaped when rendered; email templates escape all variables.
- Parameterised queries only (Prisma). Validate and size-limit all JSON bodies (maximum 64 KB).
- Admin routes behind authentication with CSRF protection and rate limiting.
- Dependency audit in CI; secrets only in environment variables.

---

## 19. Performance budgets and browser support

### 19.1 Budgets
| Metric | Target |
|---|---|
| LCP (mobile, 4G) | at most 2.5s (the headline text is the LCP element; do not wait for animation to render it) |
| INP | at most 200ms |
| CLS | at most 0.05 |
| JS shipped for `/` (gzipped, initial) | at most 200 KB; lazy-load the PDF code, Turnstile, Cal embed, ghost overlay |
| Drag and animation | 60 fps on a mid-range phone; animate only `transform` and `opacity`; heavy glow via pre-rendered filters, not animated `box-shadow` on many elements |
| Fonts | at most 3 files, preloaded, WOFF2 |
| Total weight `/` first load | at most 600 KB excluding fonts |

### 19.2 Browser support
Last 2 versions of Chrome, Edge, Firefox, Safari (macOS and iOS), Samsung Internet. Provide graceful fallbacks when `clip-path`, `backdrop-filter` or `color-mix` are unsupported (use plain rectangles and solid colors).

---

## 20. Tech stack and repository structure

### 20.1 Recommended stack (substitute only with a recorded reason)
- **Framework:** Next.js (App Router) + TypeScript (strict).
- **Styling:** CSS variables for tokens plus CSS Modules or Tailwind configured to those tokens. No component library look; components are custom.
- **State:** Zustand with a history middleware (undo/redo), and a finite state machine for screen flow (XState or a simple reducer).
- **Drag and drop:** `@dnd-kit/core` (supports pointer, touch and keyboard sensors) with custom collision for the 48px magnetic snap.
- **Animation:** Framer Motion (springs, FLIP/layout animations) and plain SVG stroke animation; GSAP not required.
- **Validation:** zod, shared between client and server.
- **Database:** PostgreSQL with Prisma.
- **Email:** Resend (default) with React Email templates.
- **PDF/image:** Playwright (PDF), `@resvg/resvg-js` (SVG to PNG).
- **Anti-spam:** Cloudflare Turnstile.
- **Testing:** Vitest (unit), Testing Library (components), Playwright (end to end), axe-core (accessibility).
- **Hosting:** Vercel or a Docker deployment (Node 20+, Postgres). Provide a `Dockerfile` and `docker-compose.yml` for local use.

### 20.2 Repository structure

```
/
  app/
    page.tsx                      # Build Table (client app shell) + SEO content
    work/ page.tsx, [slug]/page.tsx
    team/page.tsx
    talk/page.tsx
    privacy/page.tsx
    b/[id]/page.tsx, [id]/print/page.tsx
    admin/page.tsx
    api/ ...                      # endpoints in 12.4
  components/
    boot/ BootSequence.tsx
    table/ Tray.tsx, ModuleCard.tsx, Canvas.tsx, Blueprint.tsx, OptionPanel.tsx,
           DependencyDialog.tsx, GhostChips.tsx, EstimateRail.tsx, HelpTour.tsx, ListView.tsx
    scan/ ScanAnimation.tsx, PlanSheet.tsx
    send/ SendForm.tsx, LaunchAnimation.tsx, Confirmation.tsx
    ui/ Button.tsx, Chamfer.tsx, Dialog.tsx, Toast.tsx, Segmented.tsx, Tooltip.tsx
  lib/
    estimate.ts                   # engine (9)
    dependencies.ts               # rules (8)
    layout.ts                     # blueprint layout (10)
    suggest.ts                    # keywords (6.1)
    similarity.ts                 # ghost matching (11)
    format.ts                     # currency/number formatting
    schema.ts                     # zod schemas + types
    analytics.ts
  state/ store.ts, machine.ts
  config/ *.json                  # section 14
  public/ icons/*.svg, glyphs/*.svg, fonts/*
  emails/ ClientConfirmation.tsx, TeamNotification.tsx, FollowUp.tsx, Updated.tsx
  prisma/ schema.prisma
  tests/ unit/, e2e/, fixtures/
  DECISIONS.md
  README.md
```

### 20.3 Screen state machine
States: `boot -> intent -> sentence -> table -> scan -> plan -> send -> confirmation`.
- `table <-> plan` (Edit blueprint returns to `table`).
- Any state may go to `table` if a saved blueprint exists and the user picks "Skip".
- Deep links: `/b/[id]?edit=token` loads directly into `table` (or `plan` if `status = sent`).
- Browser Back moves between states using `history.pushState` for `table`, `plan`, `send`, `confirmation` (so Back from `plan` returns to `table`, not off-site).

---

## 21. Build plan (milestones and tasks)

Deliver in this order. Each milestone must be demonstrable and pass its acceptance criteria before the next starts.

### M0: Foundations (day 1 to 2)
- [ ] Create repo, Next.js + TypeScript strict, lint, prettier, Vitest, Playwright, CI.
- [ ] Add tokens (5.2 to 5.7), fonts, base layout, grid background, chamfer utility, Button, Dialog.
- [ ] Add config files with placeholder content; zod schemas that validate them at build.
- [ ] `DECISIONS.md` and `README.md` (run, test, env).

### M1: Engine and data (day 2 to 4)
- [ ] `lib/estimate.ts` with fixtures A to D passing.
- [ ] `lib/dependencies.ts` (add/remove rules, pending logic).
- [ ] `lib/layout.ts`, `lib/suggest.ts`, `lib/similarity.ts`, `lib/format.ts` with unit tests.
- [ ] Zustand store with undo/redo and localStorage autosave.

### M2: Table without flair (day 4 to 8)
- [ ] Tray, module cards, add by tap/keyboard, option panel, dependency dialogs.
- [ ] Static blueprint SVG renderer (no animation), estimate rail, notes/risks.
- [ ] List view (accessible alternative). Live-region announcements.
- [ ] Responsive layouts (tablet bottom sheet, mobile sticky bar).

### M3: Interaction polish (day 8 to 11)
- [ ] Drag and drop with magnetic snap (dnd-kit), drop zones, reorder.
- [ ] Tray idle float, hover/long-press info cards, suggested pulse.
- [ ] Blueprint stroke-draw animation, FLIP re-layout, red flash on blocked removal.
- [ ] Rail count-up animations, mini Gantt.
- [ ] Reduced-motion variants; help tour.

### M4: Journey front-end (day 11 to 14)
- [ ] Boot sequence, intent screen, one-sentence screen, suggestions.
- [ ] Scan animation, plan sheet with print animation, inline title edit.
- [ ] Send form, launch animation, confirmation screen.

### M5: Backend (day 14 to 17)
- [ ] Prisma schema, migrations; blueprint create/update/get; server-side estimate recompute and validation.
- [ ] Send endpoint (Turnstile, honeypot, rate limits, idempotency, round-robin assignment).
- [ ] Email templates and sending; PDF and PNG endpoints; `/b/[id]` pages.
- [ ] Follow-up job (cron) and cleanup job (cron).

### M6: Content pages and ghost overlay (day 17 to 20)
- [ ] `/work`, `/work/[slug]` (with "Start from this blueprint"), `/team`, `/talk`, `/privacy`, 404/500.
- [ ] Ghost chips and overlay mode.
- [ ] SEO content, metadata, sitemap, OG images, structured data.

### M7: Admin, hardening, launch (day 20 to 24)
- [ ] `/admin` list, status updates, CSV export.
- [ ] Analytics events; cookie banner if needed.
- [ ] Accessibility audit (axe + manual), performance pass against budgets, security headers.
- [ ] End-to-end tests of the full journey; load test of the send endpoint.
- [ ] Production deploy docs; owner checklist to replace all placeholders.

### P2 backlog (after launch)
Paper (light) theme, optional sound, LLM-assisted suggestion, offline send queue, multi-language UI, CRM webhook, calendar booking embedded in confirmation, A/B test of boot sequence length.

---

## 22. Acceptance criteria and test plan

### 22.1 Acceptance criteria (Given / When / Then)

1. **Boot skip.** *Given* a first-time visitor, *when* they press any key during boot, *then* the end state (headline and intent buttons) shows within 100ms.
2. **Suggestions.** *Given* the sentence "booking app for clinics", *when* submitted, *then* the tray highlights `booking`, `user_login`, `notifications`, `mobile_app`, `payments` (max 5) and nothing is added to the table automatically.
3. **Drag add.** *Given* an empty table, *when* the user drags `mobile_app` within 48px of a slot and releases, *then* it snaps into the Interfaces band, the rail shows a non-empty estimate, and an `aria-live` announcement is made.
4. **Keyboard add.** *Given* keyboard-only use, *when* the user presses Enter on `payments` and chooses "Add to blueprint", *then* the same outcome as drag occurs.
5. **Dependency add.** *Given* `payments` is added without `user_login`, *then* a dialog offers to add both; choosing **Add both** places both and the estimate equals Fixture C.
6. **Dependency block.** *Given* `user_login` required by `payments`, *when* the user tries to remove `user_login`, *then* removal is blocked, an explanation names `payments`, and **Remove all** removes both (undoable).
7. **Options.** *Given* Fixture A, *when* `mobile_app` platform changes to iOS only, *then* numbers match Fixture D4 calculations.
8. **Estimate correctness.** Fixtures A to C match exactly (weeks and budget) on both client and server.
9. **Undo/redo.** *Given* 5 actions, *when* Ctrl+Z is pressed 5 times, *then* the table is empty; Ctrl+Shift+Z restores step by step.
10. **Autosave.** *Given* modules placed, *when* the page is reloaded, *then* the same state is restored with the welcome-back toast.
11. **Scan.** *Given* at least 1 module and none pending, *when* **Scan blueprint** is pressed, *then* the scan animation plays (or is skipped), a blueprint is created on the server, and the plan sheet displays the same numbers as the rail.
12. **Send validation.** Invalid email, missing name or missing consent blocks submission with accessible inline errors and focus on the first invalid field.
13. **Send success.** *When* a valid form is submitted, *then* the client receives the confirmation email and the team receives the internal email (with attachment), the enquiry record exists with an assigned engineer, and the confirmation screen displays the reference.
14. **Spam and limits.** Filled honeypot or failed Turnstile gives a generic success-looking response but sends nothing (no signal to bots); exceeding rate limits returns 429.
15. **Private link.** `/b/[id]` shows read-only content without personal data; `?edit=token` opens the editable table; wrong token shows read-only.
16. **Ghosts.** *Given* modules that match a project at J of at least 0.4, *then* chips show; opening the overlay never alters the user's modules.
17. **Responsive.** All journey steps are completable on a 360 x 640 viewport using taps only.
18. **No-JS.** With JavaScript disabled, `/` shows the descriptive content and dock links.
19. **Reduced motion.** With `prefers-reduced-motion: reduce`, no looping or sweeping animation runs, and every flow completes.
20. **Accessibility.** axe-core reports zero serious/critical violations on every route and in states: table with modules, dialog open, plan sheet, send form.

### 22.2 Automated tests
- **Unit:** estimate (fixtures), dependency logic, layout positions, suggestion mapping, similarity, formatters.
- **Component:** ModuleCard states, DependencyDialog, EstimateRail announcements, SendForm validation.
- **End to end (Playwright):** full journey desktop and mobile (Chromium + WebKit), keyboard-only journey, send with a mocked email provider, private link edit flow.
- **Visual regression:** snapshots of boot end state, table with Fixture A, plan sheet, confirmation, at 1440 and 390 widths.

### 22.3 Definition of done (whole project)
- All milestones M0 to M7 complete; acceptance criteria 1 to 20 pass in CI.
- Lighthouse (mobile): Performance 90 or higher, Accessibility 100, Best Practices 95 or higher, SEO 95 or higher on `/`, `/work`, `/team`, `/talk`.
- No placeholder content remains unless flagged in the owner checklist (`OWNER_CHECKLIST.md`): brand, rates, team, projects, emails, privacy text, Cal URL.
- `README.md` documents local setup, environment variables, deployment, cron jobs and how to edit config.

---

## 23. Copy deck (UI strings)

Voice: plain, confident, honest. Short sentences. Sentence case. No jargon without an explanation. Buttons say exactly what happens.

### 23.1 Core
- Boot headline: **What do you want to build?**
- Intent buttons: **Launch something new** / **Fix or upgrade what I have** / **Add AI to my business**
- Look-around link: **Not sure? Just look around.**
- Sentence prompt label: **Tell us in one sentence what it is.**
- Sentence buttons: **Continue** / **Skip**
- Empty canvas: **Drag a module here to start your blueprint.** (touch: **Tap + Add module to start your blueprint.**)
- Clear table: **Clear table** / confirm "Remove all {n} modules? You can undo this." / **Remove all** / **Cancel**
- Welcome back toast: **Welcome back. Your blueprint is still on the table.** / **Start over**
- Tray tabs: **All** / **Interfaces** / **Features** / **Foundations**
- Add button in info card: **Add to blueprint**
- Remove button: **Remove module**
- Pending badge: **Needs {module}**
- Scan button: **Scan blueprint**; disabled tooltip: **Add at least 1 module.** / **Resolve modules that need others.**
- Rail empty: **Add modules to see your estimate.**
- Estimate info title: **About this estimate**
- Estimate info body: **A rough range based on similar projects. Your real quote comes after a call and can be higher or lower. These things can change it: scope changes, third-party approvals and complex integrations.**
- Plan sheet buttons: **Edit blueprint** / **Download PDF** / **Send blueprint**
- Send form heading: **Where should we send your blueprint?**
- Field labels: **Your name** / **Your email** / **Company (optional)** / **Phone or WhatsApp (optional)** / **Anything we should know? (optional)** / **Best time for a call (optional)**
- Consent: **I agree to be contacted about this blueprint.** + link **Privacy policy**
- Submit: **Send blueprint**; sending: **Sending...**
- Confirmation: **Blueprint sent.** / **Thanks, {firstName}. It's on its way to {engineerFirstName}.**
- Next steps: **{engineerName} reads your blueprint within one working day.** / **You get a 30-minute call that starts from your design, not from zero.** / **You get a private link to edit or forward your blueprint.**
- Confirmation buttons: **Copy link** / **Forward to a co-founder** / **Book a time now**
- Copied toast: **Link copied.**

### 23.2 Dock
**Our work** / **Our team** / **Talk to a human** / **Open the Build Table**

### 23.3 Errors
- Required: **Enter your {field}.**
- Email: **Enter a valid email, like name@example.com.**
- Consent: **Tick the box so we can contact you.**
- Send failed: **We couldn't send your blueprint. Your work is saved. Try again, or email us at {email}.**
- Rate limit: **Too many attempts. Try again in a minute.**
- Save failed on scan: **We couldn't save your blueprint online yet. You can keep editing; we'll retry when you send it.**
- 404: **That page isn't on the table.** / **Open the Build Table** / **See our work**
- 500: **Something broke on our side. Your blueprint is saved in this browser.**

### 23.4 Dialogs
- Needs another: **{Module} needs {Required}. Add it?** / **Add both** / **Cancel**
- Needs one of: **{Module} needs a dashboard or an admin panel. Which one?**
- Blocked removal: **{Module} is needed by {List}.** / **Remove all {n}** / **Keep**
- Recommendation: **Most {module} products also add {recommended}. Add it?** / **Add** / **Not now**

### 23.5 Plan sheet "Included / Not included"
**Included (always):** Design of every screen, a clickable prototype you approve, the build of the modules listed, testing on real devices, launch support, and a handover of all code and accounts.
**Not included (always):** Costs of third-party services (for example payment fees, map or SMS charges, app store accounts, hosting beyond launch), content writing and photography, legal documents, and changes to scope after sign-off. We'll quote those separately.

### 23.6 Help tour
1. **Drag modules onto the table.**
2. **Click a module to set its options.**
3. **Watch the estimate update as you build.**

---

## 24. Open questions and assumptions

**Assumptions used in this spec (confirm or change):**
1. Company name, rates, team, projects and contact details are placeholders (section 14).
2. Prices are shown as ranges with an honest "estimate" label; no exact quote is promised.
3. Currency defaults to USD with INR and EUR options; real rates are set by the company owner.
4. Only rule-based suggestions in v1; an LLM suggestion is a P2 feature.
5. v1 has one option group per module; multi-group options can be added later through the same schema.
6. Anonymous blueprints are saved only when the visitor presses Scan; nothing personal is stored before Send.
7. A human reads every sent blueprint; the "within one working day" promise must be operationally true.

**Questions for the company owner:**
1. What are the real day rates (per person-week) by currency, and should the budget be shown at all or only timeline and team?
2. Which modules should be added or removed for the real service catalog?
3. Who are the engineers who take enquiries, and how should assignment work (round-robin, by skill)?
4. Which CRM should receive enquiries (webhook or email only)?
5. Which booking tool should power "Book a call" (Cal.com, Calendly, other)?
6. Which regions are targeted (affects cookie consent and privacy text)?
7. Are real case studies available for `/work` and the ghost overlay (at least 3 recommended)?
8. Is a light "paper" theme required at launch or after?
