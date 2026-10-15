# scuffedplatformer
A basic webgl game

**Scuffed Platformer** is a 2D pixel-art platformer built in Unity and exported to WebGL. This repo holds the
exported WebGL build (not the Unity project source).

- **Play in the browser (GitHub Pages):** https://bruce-peters.github.io/scuffedplatformer/
- **Also on itch.io:** https://bobcat9.itch.io/scuffed-platformer

Use a desktop browser. Unity WebGL builds do not run on phones (the page shows a warning on mobile).

## How to play

Click **Start from Begining** (or **Level Menu**) on the title screen. Move with **WASD**, as the in-game
level 1 hint says. Get to the portal to finish a level. The button in the bottom-right corner of the
player switches to fullscreen.

## Run it locally

A Unity WebGL build has to be served over HTTP; opening `index.html` straight from disk (`file://`) will not
load it. Any static file server works. The build files are uncompressed, so no special
`Content-Encoding` headers are needed (same as on GitHub Pages).

Prereq: Node.js 18+ (for `npx`), or Python 3.

```bash
git clone https://github.com/bruce-peters/scuffedplatformer.git
cd scuffedplatformer
npx http-server . -p 8080
# or: python3 -m http.server 8080
```

Then open http://localhost:8080/ in Chrome, Edge or Firefox. The first load downloads about 42 MB
(`.data` + `.wasm`), so give it a few seconds.

## Project structure

```
index.html          Unity WebGL page template (loader config points at Build/)
Build/              exported game: .loader.js, .framework.js, .wasm, .data (uncompressed)
StreamingAssets/    Unity Services config written by the export
TemplateData/       CSS, icons and progress-bar images for the page
```

## Notes

- To publish a new version, rebuild from the Unity project with **Build Settings > WebGL**, keep
  **Player Settings > Publishing Settings > Compression Format = Disabled** (or turn on
  **Decompression Fallback**), then replace `Build/` and the file names in `index.html`.
  GitHub Pages cannot send the `Content-Encoding` headers that a Gzip/Brotli Unity build needs.
