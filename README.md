# MediaMini

Local macOS app that compresses website images and videos using perceptual quality analysis. Crawls a URL or accepts drag-and-drop files, converts to WebP/WebM, and delivers a zip mirroring the original site structure. Everything runs locally — no files leave your machine.

---

## Features

- Crawls a full site or single page and fetches every image and video
- Drag-and-drop mode for processing local files without a URL
- Classifies images by content type (hero, photograph, graphic, icon, background) and compresses each to the highest quality that still achieves meaningful size reduction
- SSIM scoring validates every output against the original pixel-by-pixel
- VP9/WebM video encoding with CRF floors tuned per content type
- Output zip mirrors the original URL folder hierarchy exactly
- No cloud APIs, no accounts, no data leaves your computer
- One double-click to launch — no terminal interaction required

---

## Requirements

- macOS (Ventura or later recommended)
- [Node.js LTS](https://nodejs.org ) — install once, never think about it again

---

## Installation

1. Download **MediaMini.zip** from the [latest release](../../releases/latest)
2. Unzip it and move the `MediaMini` folder wherever you like
3. Install [Node.js LTS](https://nodejs.org ) if you haven't already

---

## First launch (one-time only)

macOS blocks unsigned apps by default. To allow MediaMini to run:

1. Double-click **Start MediaMini** — when the warning appears, click **Done**
2. Open **System Settings → Privacy & Security**
3. Scroll down to *"Start MediaMini was blocked…"* and click **Open Anyway**
4. Enter your Mac password and click **Open Anyway** again
5. Double-click **Start MediaMini** — it opens normally from here on

On first launch, MediaMini installs its dependencies and downloads a browser engine (~100 MB). This takes 1–2 minutes and never happens again.

---

## Usage

1. Double-click **Start MediaMini** — a Terminal window opens in the background
2. Your browser opens automatically to `http://localhost:5173`
3. Choose a tab:
   - **Optimize a Website** — paste a URL, choose Full Site or Single Page, click Run
   - **Optimize Local Files** — drag files into the drop zone, choose output formats, click Run
4. When the job finishes, the optimized zip downloads automatically
5. Close the Terminal window when you're done

---

## Output structure

The zip mirrors your site's URL hierarchy exactly:

```
your-site.com/
  page-name/
    image.webp
    video.webm
  section/
    sub-page/
      image.webp
```

Drop the folders directly into your site's asset directory as replacements.

---

## How compression works

| Category | Examples | Compression approach |
|---|---|---|
| Hero Image | Large banner photos | Very conservative — highest quality floor |
| Photograph | Portfolio, editorial images | High quality, moderate reduction |
| Graphic / Illustration | Flat artwork, logos | Moderate — prioritises file size |
| Icon / UI Element | Small or simple images | Aggressive |
| Background Texture | Large, low-detail fills | Aggressive |

A binary search finds the lowest WebP quality setting that still passes the SSIM threshold for that category. Videos use VP9 CRF encoding with per-content-type quality floors.

---

## Limitations

- macOS only
- Videos must be hosted directly on the site — YouTube, Vimeo, and other embedded players are not supported
- Pages behind authentication or bot-detection may not be crawlable

---

## License

MIT
