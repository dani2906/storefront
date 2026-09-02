# Storefront

A single-file, client-side store screenshot builder. Upload a screenshot, add a headline above or below it, export every size the App Store and Google Play accept. No server, no upload — everything happens on the canvas in the browser.

## Deploy to GitHub Pages

Create an empty repo called `storefront` on GitHub, then from the folder holding `index.html`:

```bash
git init
git add index.html README.md
git commit -m "Storefront"
git branch -M main
git remote add origin https://github.com/dani2906/storefront.git
git push -u origin main
```

Then Settings → Pages → Source: **Deploy from a branch** → `main` / `/ (root)`. Live in a minute or two at:

**https://dani2906.github.io/storefront/**

If you name the repo `dani2906.github.io` instead, it serves from the root: `https://dani2906.github.io/`.

Only external dependency is JSZip from cdnjs (for the zip download) and Archivo from Google Fonts. If either is blocked, the app still works — exports just fall back to downloading files one at a time.

## Sizes included

**App Store — iPhone**

| Class | Pixels | Notes |
|---|---|---|
| 6.9″ (17/16 Pro Max) | 1320 × 2868 | primary; Apple scales down from here |
| 6.9″ (Plus, older Pro Max) | 1290 × 2796 | |
| 6.9″ (iPhone Air) | 1260 × 2736 | |
| 6.5″ | 1284 × 2778 | required if you skip 6.9″ |
| 6.3″ | 1206 × 2622 | |
| 6.1″ | 1179 × 2556 | |
| 5.5″ | 1242 × 2208 | |

**App Store — iPad:** 13″ 2064 × 2752 (required if the app runs on iPad), 12.9″ 2048 × 2732.

**Google Play:** phone 1080 × 1920 (min 2, max 8), phone hi-res 1440 × 2560, 7″ tablet 1080 × 1920, 10″ tablet 1600 × 2560, feature graphic 1024 × 500 (required).

Play enforces 320–3840 px per side and an aspect ratio between 1:2 and 2:1 — which is why Apple's 9:19.5 iPhone files can't be reused there.

## Alpha channel

Both stores reject images with an alpha channel. Canvas PNGs are always 32-bit RGBA even when fully opaque, so if a file is rejected on upload, switch the export format to JPEG.

## Extending

Presets live in the `PRESETS` array at the top of the `<script>` block:

```js
{g:'App Store — iPhone', dir:'AppStore/iPhone-6.9', label:'6.9″', w:1320, h:2868, on:true, req:true}
```

`dir` is the folder path inside the exported zip. Add Watch, Mac, tvOS or Chromebook entries the same way — the renderer is resolution-independent, so nothing else needs to change.
