📸 I got tired of iPhone photos (HEIC) not opening on Windows, so I built a free image converter. 🚀

It started as a Python script for converting folders on my laptop. Then I turned it into a web app anyone can use, with no install and no sign-up.

🔗 Try it: https://shrey-iitk.github.io/heic2any/

**What it does:** \
🔄 Converts HEIC, HEIF, JPG, PNG, WebP, GIF, BMP and AVIF into JPG, PNG, WebP or PDF \
🔒 100% private: conversion runs in your browser, so your photos never leave your device and nothing is uploaded \
⚡ Batch mode: drop in many photos at once \
🎚️ Adjustable quality slider for smaller or sharper files \
📄 Merge several photos into one multi-page PDF \
📦 One-click ZIP download for everything you converted \
🖼️ Instant thumbnails with before and after file sizes \
📱 Works on desktop and mobile
💸 Free forever

**Built with:** HTML, CSS, vanilla JavaScript, heic2any, jsPDF and JSZip, all hosted for free on GitHub Pages.

The biggest lesson was that a lot of useful tools don't need a backend. If the browser can do the work, your users' data stays with them, and you pay nothing for servers.

# How the Conversion Works

Everything below happens inside the visitor's browser. No photo is ever uploaded.

## Steps

1. **Choose settings.** The visitor picks an output format (**JPG, PNG, WebP or PDF**), sets the quality, and drops in photos.
2. **Read the file.**
   - **HEIC / HEIF:** the **heic2any** library decodes it into a normal image first.
   - **JPG, PNG, WebP, GIF, BMP, AVIF:** the browser reads them directly.
3. **Draw on a canvas.** The image is drawn onto a hidden `<canvas>`. For JPG and PDF the canvas gets a white background first, because those formats can't store transparency.
4. **Export in the chosen format.**
   - **JPG / WebP:** exported from the canvas using the quality slider.
   - **PNG:** exported from the canvas losslessly, so the quality slider is ignored.
   - **PDF:** the **jsPDF** library places the image on a page sized to the photo.
5. **Show the result.** A thumbnail is created, and a **Download** button appears with the before and after file sizes.
6. **Download.**
   - **Single file:** saved directly.
   - **ZIP:** **JSZip** packs all converted files into one archive.
   - **Merged PDF:** jsPDF joins all converted pages into one multi-page PDF.

## Flow diagram

```
Drop photos
    │
    ▼
HEIC / HEIF? ──yes──► heic2any decodes to an image
    │ no                       │
    └──────────────────────────┘
                 ▼
     Draw on hidden canvas
     (white background for JPG / PDF)
                 ▼
   Export as JPG / PNG / WebP / PDF
                 ▼
  Thumbnail + Download button
                 ▼
   Single file · ZIP · Merged PDF
```

## Limitations

- Output formats are limited to what browsers can export (no HEIC, AVIF or TIFF output).
- Animated GIFs and multi-image HEIC files convert only their first frame.
- Very large batches depend on the visitor's device memory.
