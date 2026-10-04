# Piece It Together — Photo Puzzle

A drag-and-drop jigsaw puzzle game. It slices a photo into a grid, shuffles
the pieces, and lets you drag them back into place. Solving it reveals the
full photo with a "so pretty" celebration.

## Project structure

```
piece-it-together/
├── index.html          ← the entire game (HTML + CSS + JS, no build step)
├── assets/
│   └── photo.jpg        ← put your own image here (not included)
├── package.json          ← optional, only used to run a local dev server
└── README.md
```

## Dependencies

**None at runtime.** This is a single static HTML file — plain HTML, CSS,
and vanilla JavaScript. It loads two Google Fonts (Baloo 2, Inter) over
the network; everything else is self-contained. There is no framework,
no bundler, and no build step.

The `package.json` in this repo is optional — it only wires up a
convenience script for serving the file locally, since opening
`index.html` directly via `file://` will block the image fetch in some
browsers.

## Running it

You don't need Node or npm to use this — you can just open `index.html`
in a browser. If your browser blocks local image loading over `file://`,
serve the folder instead:

```bash
npx serve .
# or, if you ran npm install first:
npm start
```

Then open the printed local URL (e.g. `http://localhost:3000`).

## Configuration

Open `index.html` and find this block near the top of the `<script>` tag:

```js
var IMAGE_SRC = "assets/photo.jpg";   // path, URL, or data:image/... URI to your photo
var DIFFICULTY = 4;                    // grid size: DIFFICULTY x DIFFICULTY (3, 4, 5, or 6)
```

- **`IMAGE_SRC`** — a relative path, an absolute URL, or a base64
  `data:image/...` URI if you want the whole game to stay a single
  portable file with no external asset.
- **`DIFFICULTY`** — an integer for the grid size (e.g. `4` → 4×4 = 16
  pieces).

Save the file and reload the page to apply changes.

## How it works

- The image is sliced into pieces purely with CSS (`background-size` +
  `background-position` on each piece div) — no canvas or server-side
  processing.
- Pieces are dragged using pointer events (`pointerdown` / `pointermove`
  / `pointerup`) attached to `document`, so it works with mouse,
  trackpad, and touch alike.
- Dropping a piece onto an occupied cell swaps the two pieces.
- When every piece is in its correct cell, the board's grid gaps
  collapse to reveal the seamless photo and a "so pretty" overlay
  appears with your solve time.

## License

Do whatever you like with this code.
