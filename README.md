# QA Study Library

A single-page reading room for all your QA / software-testing study PDFs.
Built to be **hassle-free**: you drop a PDF into one folder, push, and it shows up.
No build step, no dependencies to install, no code to edit.

**Live site:** `https://abrarragib.github.io/qa-study-library/`

---

## The one rule: to add a guide, drop a PDF in `pdfs/`

1. Put your `.pdf` file into the **`pdfs/`** folder.
2. Push (or use GitHub's **Add file → Upload files** and drag it into `pdfs/`).
3. Done. The list rebuilds itself and the new guide appears on the site.

Removing a guide is the same — delete the PDF from `pdfs/` and push.
You never touch `index.html` for this.

> Filenames become titles automatically, and each guide is sorted into a
> category (SQA Theory, Tools & Automation, Programming & DSA, Database, Career)
> from its filename — so keep names descriptive, e.g.
> `Selenium-Viva-Prep-Guide.pdf`.

---

## Folder layout

```
qa-study-library/
├── index.html                 ← the app (never needs editing)
├── .nojekyll                  ← makes GitHub Pages serve files as-is
├── README.md
├── assets/
│   └── pdfjs/                 ← the PDF viewer engine, bundled locally
│       ├── pdf.min.js            (no CDN — it can't break if a CDN is down)
│       └── pdf.worker.min.js
├── .github/
│   └── workflows/
│       └── build-index.yml    ← auto-updates the list when PDFs change
└── pdfs/                      ← ★ PUT ALL YOUR PDFs HERE ★
    ├── index.json                (auto-generated list — don't edit by hand)
    ├── Database-SQL-Viva-Prep-Guide.pdf
    ├── Selenium-Viva-Prep-Guide.pdf
    └── … all your other guides
```

---

## First-time setup (about 3 minutes)

**1. Push these files to your repo** (`AbrarRagib/qa-study-library`).
Replace the old contents with this folder's contents so everything is fresh.

**2. Turn on GitHub Pages**
Repo → **Settings → Pages** → *Source: Deploy from a branch* →
Branch: `main`, Folder: `/ (root)` → **Save**.
After ~1 minute your site is live at the URL above.

**3. Let the auto-list update itself** (one-time permission)
Repo → **Settings → Actions → General** → *Workflow permissions* →
choose **Read and write permissions** → **Save**.
This lets the included Action keep `pdfs/index.json` in sync on every push.

> Even if you skip step 3, the site still works — it falls back to reading the
> repo's file list directly. Step 3 just makes it faster and rate-limit-proof.

---

## How the list stays in sync (three safety nets)

The site finds your PDFs using the first of these that works, so it never
ends up with an empty list:

1. **`pdfs/index.json`** — regenerated automatically by the GitHub Action
   every time you add/remove a PDF. Fast, and no rate limits.
2. **GitHub file listing** — if the JSON isn't there yet, it reads the repo's
   `pdfs/` folder live.
3. **Built-in list** inside `index.html` — a final fallback for offline use.

This triple fallback is what fixes the old "the list broke and I couldn't fix
it" problem: if one method is unavailable, the next one takes over.

---

## Features

- **Proper PDF viewer** rendered with PDF.js (bundled locally, not from a CDN).
- **Light / dark theme** — the moon/sun button, top-right. Your choice is remembered.
- **Dark PDF** — the half-moon button in the toolbar darkens the PDF itself for
  night reading (on by default in dark theme; toggle it off for colourful diagrams).
- **Reading mode** — the **Read** button switches to continuous scroll of every
  page and hides the sidebar for distraction-free reading. (Keyboard: `R`.)
- **Zoom** — toolbar `+ / −`, or the `+` / `−` keys.
- **Page navigation** — arrows in the toolbar, or the `←` / `→` keys.
- **Search** the sidebar to filter guides by name.
- **Open in browser viewer** (top-right toolbar icon) if you want native
  find-in-page, printing, or text selection.
- **Download** button for saving any guide.
- **Deep links** — share `…/qa-study-library/#file=Selenium-Viva-Prep-Guide.pdf`
  to open straight to one guide.
- Remembers your last-read guide, theme, zoom, and mode.
- Works on phones (the sidebar becomes a slide-in menu).

---

## Optional tweaks

Only the small `CONFIG` block at the top of `index.html` is meant to be edited,
and only if you want to change the title or tagline:

```js
const CONFIG = {
  siteTitle: "QA Study Library",
  tagline:   "Viva & interview prep",
  pdfDir:    "pdfs",     // keep as "pdfs"
  owner: "", repo: "",   // auto-detected — leave blank
  manualList: [ ... ]    // last-resort offline fallback; leave as is
};
```

That's the whole system. Add PDFs to `pdfs/`, push, read.
