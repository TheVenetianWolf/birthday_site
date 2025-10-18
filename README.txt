# Happy Birthday Web 🎂🎉

A tiny, single-file party page that sings “Happy Birthday,” highlights lyrics karaoke-style, floats balloons, fires confetti, and lets you blow out animated candles. Built with plain HTML/CSS/JS—no build tools, no dependencies.

## Quick start

1. Create a new folder.
2. Save the provided code as `index.html` in that folder.
3. Open `index.html` in your browser.

## Personalise it

- Fastest: add `?name=Aoife` to the URL, e.g. `index.html?name=Aoife`.
- Default name in code:
  ```js
  const person = params.get('name')?.trim() || 'Sister';
