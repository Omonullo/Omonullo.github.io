# Arcade "About Me" Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the entire `omonullo.github.io` repo contents with a single static, retro-arcade-styled "about me" page for Omonullo Abdullaev.

**Architecture:** One self-contained `index.html` with all CSS and JS inline. The only external dependency is the "Press Start 2P" pixel font from Google Fonts. No build step — GitHub Pages serves the file directly. Old HTML5 UP template files are deleted.

**Tech Stack:** Plain HTML5, CSS3 (inline `<style>`), vanilla JavaScript (inline `<script>`), Google Fonts.

---

## File Structure

- `index.html` — the entire page (replaces old company site). Sections: title screen, character stats, class & abilities, soundtrack, quest log. Inline CSS in `<head>`, inline JS before `</body>`.
- `README.md` — short description of the page (replaces old `README.txt`).
- Deleted: `elementselements.html`, `left-sidebar.html`, `no-sidebar.html`, `right-sidebar.html`, `README.txt`, `LICENSE.txt`, `assets/`, `images/`, `.idea/`.
- Removed before final commit: `docs/` (the spec + plan folder).

Verification for a static page is manual: open `index.html` in a browser and confirm the described behavior. Each task ends with a concrete check and a commit.

---

## Task 1: Delete old template files

**Files:**
- Delete: `index.html`, `elementselements.html`, `left-sidebar.html`, `no-sidebar.html`, `right-sidebar.html`, `README.txt`, `LICENSE.txt`, `assets/`, `images/`, `.idea/`

- [ ] **Step 1: Remove the old files**

```bash
cd /tmp/omonullo.github.io
git rm -r index.html elementselements.html left-sidebar.html no-sidebar.html right-sidebar.html README.txt LICENSE.txt assets images
rm -rf .idea
```

- [ ] **Step 2: Verify only kept files remain**

Run: `git status --short && ls -A`
Expected: staged deletions for all listed files; `ls -A` shows only `.git`, `.gitignore`, `docs` (and `.superpowers` if the brainstorm session left it — that is fine, it is gitignored or removed later).

- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "Remove old HTML5 UP company-site template"
```

---

## Task 2: Page skeleton, theme, and title screen

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create `index.html` with the head, theme CSS, and title screen**

Create `/tmp/omonullo.github.io/index.html` with this exact content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Omonullo Abdullaev</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #2b1a4a;
    --bg-2: #1f1238;
    --yellow: #ffe14d;
    --pink: #e0357b;
    --teal: #4dffd0;
    --text: #efe9ff;
    --muted: #b9a9e6;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Press Start 2P', monospace;
    line-height: 1.9;
    image-rendering: pixelated;
    padding-bottom: 60px;
  }
  section {
    max-width: 720px;
    margin: 0 auto;
    padding: 48px 24px;
  }
  h1, h2 { line-height: 1.4; }
  .screen-label {
    color: var(--teal);
    font-size: 10px;
    margin-bottom: 18px;
  }
  /* Title screen */
  #title {
    text-align: center;
    padding-top: 90px;
    padding-bottom: 70px;
  }
  #title h1 {
    color: var(--yellow);
    font-size: 26px;
    text-shadow: 3px 3px 0 var(--pink);
  }
  #title .tagline {
    color: var(--teal);
    font-size: 10px;
    margin-top: 28px;
  }
  #title .blink {
    color: var(--muted);
    font-size: 9px;
    margin-top: 36px;
    animation: blink 1.1s steps(1) infinite;
  }
  @keyframes blink { 50% { opacity: 0; } }
</style>
</head>
<body>

<section id="title">
  <h1>OMONULLO ABDULLAEV</h1>
  <p class="tagline">With a slow pace you can swim against the flow.</p>
  <p class="blink">scroll down to continue</p>
</section>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Run: `open /tmp/omonullo.github.io/index.html`
Expected: Deep-purple page; yellow pixel-font name with pink drop-shadow; teal tagline; blinking "scroll down to continue" line.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Add page skeleton, arcade theme, and title screen"
```

---

## Task 3: Character stats panel

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add stats-panel CSS**

In `index.html`, inside `<style>`, immediately before the closing `</style>` tag, add:

```css
  /* Stats panel */
  .stat { margin-bottom: 22px; }
  .stat-label {
    font-size: 9px;
    margin-bottom: 8px;
    display: flex;
    justify-content: space-between;
  }
  .stat-label .val { color: var(--yellow); }
  .bar {
    background: var(--bg-2);
    border: 2px solid var(--muted);
    height: 20px;
    padding: 2px;
  }
  .bar-fill {
    background: var(--teal);
    height: 100%;
    width: 0;
    transition: width 1.1s ease-out;
  }
```

- [ ] **Step 2: Add the stats section markup**

In `index.html`, immediately after the closing `</section>` of `#title`, add:

```html
<section id="stats">
  <p class="screen-label">// CHARACTER STATS</p>
  <div class="stat">
    <div class="stat-label"><span>&#128692; SPEED</span><span class="val">85</span></div>
    <div class="bar"><div class="bar-fill" data-fill="85%"></div></div>
  </div>
  <div class="stat">
    <div class="stat-label"><span>&#9917; FOOTWORK</span><span class="val">78</span></div>
    <div class="bar"><div class="bar-fill" data-fill="78%"></div></div>
  </div>
  <div class="stat">
    <div class="stat-label"><span>&#129504; STRATEGY</span><span class="val">90</span></div>
    <div class="bar"><div class="bar-fill" data-fill="90%"></div></div>
  </div>
  <div class="stat">
    <div class="stat-label"><span>&#127798; SPICE TOLERANCE</span><span class="val">95</span></div>
    <div class="bar"><div class="bar-fill" data-fill="95%"></div></div>
  </div>
  <div class="stat">
    <div class="stat-label"><span>&#128516; HUMOR</span><span class="val">88</span></div>
    <div class="bar"><div class="bar-fill" data-fill="88%"></div></div>
  </div>
</section>
```

- [ ] **Step 3: Add the scroll-reveal script**

In `index.html`, immediately before the closing `</body>` tag, add:

```html
<script>
  // Fill stat bars when they scroll into view
  var bars = document.querySelectorAll('.bar-fill');
  var io = new IntersectionObserver(function (entries) {
    entries.forEach(function (e) {
      if (e.isIntersecting) {
        e.target.style.width = e.target.dataset.fill;
        io.unobserve(e.target);
      }
    });
  }, { threshold: 0.4 });
  bars.forEach(function (b) { io.observe(b); });
</script>
```

- [ ] **Step 4: Verify in browser**

Run: `open /tmp/omonullo.github.io/index.html`
Expected: Below the title, a "// CHARACTER STATS" section with 5 labeled bars (SPEED, FOOTWORK, STRATEGY, SPICE TOLERANCE, HUMOR). Each teal bar animates from empty to its value when scrolled into view.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "Add character stats panel with scroll-reveal bars"
```

---

## Task 4: Class & abilities section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add abilities CSS**

In `index.html`, inside `<style>`, immediately before the closing `</style>` tag, add:

```css
  /* Class & abilities */
  #class .class-line {
    font-size: 10px;
    color: var(--text);
    margin-bottom: 28px;
  }
  #class .class-line b { color: var(--pink); }
  .chips { display: flex; flex-wrap: wrap; gap: 12px; }
  .chip {
    background: var(--bg-2);
    border: 2px solid var(--teal);
    color: var(--teal);
    font-size: 9px;
    padding: 8px 12px;
    transition: transform 0.1s ease-out, background 0.1s ease-out;
  }
  .chip:hover {
    transform: translate(-2px, -2px);
    background: var(--teal);
    color: var(--bg);
  }
```

- [ ] **Step 2: Add the class section markup**

In `index.html`, immediately after the closing `</section>` of `#stats`, add:

```html
<section id="class">
  <p class="screen-label">// CLASS &amp; ABILITIES</p>
  <p class="class-line"><b>CLASS:</b> Clojure / Java Developer &mdash; employed at a secret company &#129323;</p>
  <div class="chips">
    <span class="chip">Clojure</span>
    <span class="chip">Java</span>
    <span class="chip">Leiningen</span>
    <span class="chip">SQL</span>
    <span class="chip">Git</span>
    <span class="chip">Azure</span>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

Run: `open /tmp/omonullo.github.io/index.html`
Expected: A "// CLASS & ABILITIES" section with the class line (pink "CLASS:" label) and 6 teal-bordered skill chips. Hovering a chip nudges it up-left and inverts its colors.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "Add class and abilities section"
```

---

## Task 5: Soundtrack panel

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add soundtrack CSS**

In `index.html`, inside `<style>`, immediately before the closing `</style>` tag, add:

```css
  /* Soundtrack */
  .track {
    display: flex;
    align-items: center;
    gap: 14px;
    font-size: 9px;
    padding: 12px 0;
    border-bottom: 2px solid var(--bg-2);
  }
  .track .num { color: var(--pink); }
  .track .name { color: var(--text); flex: 1; }
  .track .eq { color: var(--teal); letter-spacing: 2px; }
```

- [ ] **Step 2: Add the soundtrack section markup**

In `index.html`, immediately after the closing `</section>` of `#class`, add:

```html
<section id="soundtrack">
  <p class="screen-label">// SOUNDTRACK</p>
  <div class="track"><span class="num">01</span><span class="name">Classic</span><span class="eq">||||</span></div>
  <div class="track"><span class="num">02</span><span class="name">Epic</span><span class="eq">|||||</span></div>
  <div class="track"><span class="num">03</span><span class="name">Inspiring</span><span class="eq">||||</span></div>
  <div class="track"><span class="num">04</span><span class="name">Rock</span><span class="eq">|||||</span></div>
</section>
```

- [ ] **Step 3: Verify in browser**

Run: `open /tmp/omonullo.github.io/index.html`
Expected: A "// SOUNDTRACK" section listing 4 tracks (Classic, Epic, Inspiring, Rock) with pink track numbers and teal equalizer bars.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "Add soundtrack panel"
```

---

## Task 6: Quest log section (world map) and footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add quest-log and footer CSS**

In `index.html`, inside `<style>`, immediately before the closing `</style>` tag, add:

```css
  /* Quest log */
  #quest .quest-text {
    font-size: 10px;
    color: var(--text);
    margin-bottom: 24px;
  }
  .map {
    background: var(--bg-2);
    border: 2px solid var(--muted);
    padding: 28px;
    text-align: center;
    color: var(--muted);
    font-size: 9px;
    letter-spacing: 1px;
  }
  .secret {
    margin-top: 24px;
    padding: 16px;
    border: 2px dashed var(--pink);
    color: var(--yellow);
    font-size: 9px;
    text-align: center;
    display: none;
  }
  .secret.shown { display: block; animation: blink 0.4s steps(1) 3; }
  footer {
    text-align: center;
    color: var(--muted);
    font-size: 8px;
    margin-top: 20px;
  }
  .hint { color: var(--bg-2); font-size: 8px; text-align: center; margin-top: 14px; }
```

- [ ] **Step 2: Add the quest section and footer markup**

In `index.html`, immediately after the closing `</section>` of `#soundtrack`, add:

```html
<section id="quest">
  <p class="screen-label">// QUEST LOG</p>
  <p class="quest-text">MAIN QUEST: See the world. Status &mdash; not started. Never traveled yet, but the map is waiting.</p>
  <div class="map">[ &#127757; WORLD MAP &mdash; 0 / 195 COUNTRIES VISITED ]</div>
  <div class="secret" id="secret">SECRET UNLOCKED: I still love football&hellip; I just don't play it anymore.</div>
  <p class="hint">psst &mdash; the old games had codes</p>
</section>

<footer>&#9733; Omonullo Abdullaev &mdash; built for fun &#9733;</footer>
```

- [ ] **Step 3: Verify in browser**

Run: `open /tmp/omonullo.github.io/index.html`
Expected: A "// QUEST LOG" section with the travel quest text, a bordered "WORLD MAP" box, a barely-visible hint line, and a centered footer. The secret box is not visible yet.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "Add quest log section and footer"
```

---

## Task 7: Konami code easter egg

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add the Konami code listener**

In `index.html`, inside the existing `<script>` block, immediately before the closing `</script>` tag, add:

```javascript
  // Konami code -> reveal secret
  var konami = ['ArrowUp','ArrowUp','ArrowDown','ArrowDown','ArrowLeft','ArrowRight','ArrowLeft','ArrowRight','b','a'];
  var pos = 0;
  document.addEventListener('keydown', function (e) {
    var key = e.key.length === 1 ? e.key.toLowerCase() : e.key;
    pos = (key === konami[pos]) ? pos + 1 : (key === konami[0] ? 1 : 0);
    if (pos === konami.length) {
      document.getElementById('secret').classList.add('shown');
      pos = 0;
    }
  });
```

- [ ] **Step 2: Verify in browser**

Run: `open /tmp/omonullo.github.io/index.html`
Expected: Scroll to the QUEST LOG section, then type on the keyboard: Up, Up, Down, Down, Left, Right, Left, Right, B, A. The dashed-pink secret box appears with "SECRET UNLOCKED: I still love football… I just don't play it anymore." and blinks briefly.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Add Konami code easter egg"
```

---

## Task 8: New README and final cleanup

**Files:**
- Create: `README.md`
- Delete: `docs/`

- [ ] **Step 1: Create `README.md`**

Create `/tmp/omonullo.github.io/README.md` with this exact content:

```markdown
# omonullo.github.io

A small, static, retro-arcade "about me" page for Omonullo Abdullaev.

Single self-contained `index.html` — no build step. The only external
dependency is the "Press Start 2P" font from Google Fonts.

There is a hidden easter egg on the page. The old games had codes. 🙂
```

- [ ] **Step 2: Remove the docs folder (spec + plan)**

```bash
cd /tmp/omonullo.github.io
git rm -r docs
```

- [ ] **Step 3: Verify the repo is just the page**

Run: `git status --short && ls -A`
Expected: `ls -A` shows only `.git`, `.gitignore`, `README.md`, `index.html` (and possibly `.superpowers` from the brainstorm session, which is not committed). Staged changes: new `README.md`, deleted `docs/`.

- [ ] **Step 4: Commit**

```bash
git add -A
git commit -m "Add README and remove design docs"
```

- [ ] **Step 5: Push to GitHub**

```bash
git push origin main
```

Expected: push succeeds. Within a minute or two, https://omonullo.github.io shows the new arcade page.

---

## Self-Review Notes

- **Spec coverage:** Title screen (Task 2), character stats panel (Task 3), class & abilities with the 6 skill chips (Task 4), soundtrack panel (Task 5), quest log / world map (Task 6), Konami easter egg with the football confession (Task 7), repo cleanup — old files (Task 1) and docs removal (Task 8), new README (Task 8). All spec sections covered.
- **No placeholders:** every code step contains the full content to insert.
- **Consistency:** the secret element id `secret` is created in Task 6 Step 2 and referenced in Task 7 Step 1; the `.bar-fill` / `data-fill` pair is defined and consumed within Task 3; CSS variables defined in Task 2 are reused throughout.
