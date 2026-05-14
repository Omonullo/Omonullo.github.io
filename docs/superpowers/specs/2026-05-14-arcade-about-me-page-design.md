# Arcade "About Me" Page — Design

## Goal

Replace the entire `omonullo.github.io` repo (currently a Russian-language
porcelain-insulator company site built on the HTML5 UP "Landed" template) with
a single, fun, static "about me" page for Omonullo Abdullaev. No career résumé
content beyond a deliberate, playful framing.

## Style

Retro arcade / pixel-game aesthetic. Deep-purple background, bright accent
colors (yellow, pink, teal), pixel font ("Press Start 2P" from Google Fonts).
One scrolling page.

## Page sections (`index.html`)

1. **Title screen (hero)**
   - Pixel-font name: "OMONULLO ABDULLAEV"
   - Tagline as game subtitle: *"With a slow pace you can swim against the flow."*
   - Static — no "Press Start" interaction.

2. **Character stats panel** — interests shown as an RPG character sheet.
   Each stat is a labeled pixel bar that animates filling when scrolled into view:
   - 🚴 SPEED — bicycle + walking
   - ⚽ FOOTWORK — futbol
   - 🧠 STRATEGY — dota
   - 🌶️ SPICE TOLERANCE — spicy food
   - 😄 HUMOR — jokes

3. **Class & abilities** — the developer line.
   - `CLASS: Clojure / Java Developer — employed at a secret company 🤫`
   - Equipped abilities (skill chips): Clojure, Java, Leiningen, SQL, Git, Azure
   - No real company name, no résumé detail.

4. **Soundtrack panel** — music taste shown like a game's sound/playlist menu:
   classic, epic, inspiring, rock.

5. **Quest log: See the world** — the dream to travel the world (never traveled
   yet). A simple pixel world map. Hosts the easter egg.

## Interactivity

- **Stat bars** animate on scroll into view.
- **Konami code easter egg**: typing `↑ ↑ ↓ ↓ ← → ← → B A` reveals a hidden
  confession near the world map / quest log:
  *"SECRET: I still love football… I just don't play it anymore."*
- Light arcade-style CSS hover effects on chips/cards. No sound effects, no
  mini-game, no "Press Start" screen (not requested).

## Repo cleanup

**Delete:**
- `index.html` (old company site)
- `elementselements.html`, `left-sidebar.html`, `no-sidebar.html`, `right-sidebar.html`
- `README.txt` (old template readme)
- `LICENSE.txt` (HTML5 UP template license — template removed)
- `assets/` (template CSS/JS/fonts)
- `images/` (insulator product photos)
- `.idea/` (IDE config)

**Keep:** `.git/`, `.gitignore`

**Add:**
- New self-contained `index.html` — all CSS and JS inline, only external
  dependency is the Google Fonts pixel font. No build step.
- New short `README.md` describing the page.

## Constraints

- Fully static. Must work as a GitHub Pages site with no build.
- Self-contained `index.html`; no local asset files required.
- No career/résumé content beyond the playful "secret company" class line and
  the skill chips.
