# Happy Birthday Web – README

A tiny, single-file party page that **sings “Happy Birthday,”** highlights lyrics karaoke-style, floats balloons, fires confetti, and lets you **blow out** animated candles. Built with plain HTML/CSS/JS—no build tools, no dependencies.

---

## 1) Quick start

1. Create a new folder.
2. Save the provided code as `index.html` in that folder.
3. Open `index.html` in your browser (double-click it).

That’s it—you’ve got a birthday site.

---

## 2) Personalise it (name, message)

### A) Fastest (via URL)

Add `?name=Aoife` (or any name) to the page URL:

```
index.html?name=Aoife
```

This updates the headline and the “dear ___” lyric.

### B) Change the default name (in code)

Search for:

```js
const person = params.get('name')?.trim() || 'Sister';
```

Replace `'Sister'` with your default, e.g. `'Aoife'`.

### C) Custom headline text

Search for:

```js
headline.textContent = `Happy Birthday, ${person}! 🎉`;
```

Change the string however you like.

---

## 3) Colours & dark theme

Colours are controlled by CSS variables at the top of the stylesheet:

```css
:root{
  --bg1:#06070e; --bg2:#101321; --ink:#e8e8f2;
  --accent:#ff5faf; --accent2:#ffda65;
  --cake:#f88ca5; --icing:#fff2f8; --candle:#ffc93c;
  --flame:#ff7b00; --flame2:#ffeaa7;
}
```

* **Background:** `--bg1`, `--bg2`
* **Text:** `--ink`
* **Highlight gradient:** `--accent`, `--accent2`
* **Cake & candles:** `--cake`, `--icing`, `--candle`, `--flame*`

Change these to suit your palette.

---

## 4) Candles, balloons, confetti

### A) Candles

* Click/tap a candle to **blow it out** (toggle flame).
* When **all** are out, confetti pops.
* We fixed placement so they sit on the icing:

```css
.candles { position:absolute; top:-12%; left:50%; transform:translateX(-50%); z-index:2; }
```

### B) Balloons

Balloons float with strings **below** the balloon (fixed via `::after`):

```css
.balloon::after { top:100%; left:50%; transform:translateX(-50%); height:22vh; }
```

Adjust how many appear by editing this loop in JS:

```js
for(let i=0; i<14; i++){ /* increase/decrease */ }
```

### C) Confetti

* Click the **🎊 Confetti** button any time.
* Automatically bursts on first play and when all candles are out.
* Particle count is the function argument:

```js
launchConfettiBurst(220);
```

---

## 5) The music (Web Audio)

* The melody is generated with the **Web Audio API** (no files to host).
* Tempo is set by `bpm`:

```js
const bpm = 88; // change this for faster/slower
```

* Overall volume:

```js
masterGain.gain.value = 0.14; // 0.0–1.0
```

**Note on autoplay:** Modern browsers block audio until user interaction. The page provides a **Play** button to comply.

---

## 6) Add a background photo (optional)

Replace the `body` background with your own image:

```css
body{
  color:var(--ink);
  background:
    linear-gradient(180deg, #000000aa, #000000aa),            /* dark overlay */
    url("images/your-photo.jpg") center/cover no-repeat fixed; /* your image */
}
```

Keep a dark overlay so text and graphics remain readable.

---

## 7) Deployment

* **Share locally:** send the whole folder; recipients open `index.html`.
* **GitHub Pages:** commit the folder to a public repo → Settings → Pages → set branch → use the generated URL (`…/index.html?name=Aoife`).
* **Netlify / Vercel:** drag-and-drop the folder in their dashboards.
* **Any static host** works; there’s no server logic.

---

## 8) Accessibility & keyboard

* **Candles:** focusable; press **Enter/Space** to toggle.
* **Play/pause:** press **K** or **Space** to start playback when focused on the page.
* Text contrast and hit targets are tuned for dark backgrounds.

---

## 9) Common tweaks

* **Change number of candles:** duplicate/remove `.candle` elements inside:

  ```html
  <div class="candles" id="candles">
    <div class="candle">…</div>
    <div class="candle">…</div>
    <div class="candle">…</div>
  </div>
  ```
* **Lyrics text size:** adjust `.line { font-size: clamp(16px, 3vw, 28px); }`
* **Disable motion for all users:** wrap key animations in `@media (prefers-reduced-motion: no-preference)` or set `animation: none;`.

---

## 10) Troubleshooting

* **No sound?** You must click **Play** once (browser autoplay policy).
* **Balloons’ string above balloon?** Ensure your `.balloon::after` uses `top:100%`.
* **Candles too low/high?** Tweak `.candles { top: -12%; }` slightly (-10% to -15%).
* **Looks washed out over a bright photo?** Add/strengthen a dark overlay on `body` (`#000000cc`).

---

## 11) Legal note

The melody is browser-synthesised; no audio files included. “Happy Birthday” is widely considered public domain in many jurisdictions since 2016, but if you publish commercially, do your own local check.

---

## 12) Ideas to extend

* Microphone “**blow to snuff**” (Web Audio input amplitude).
* **Name capture form** on page instead of URL param.
* **Aurora / starfield** background.
* **Share link** generator that appends `?name=` automatically.

---

Enjoy the party page, ship it, light it, confetti it.
