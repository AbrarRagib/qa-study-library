# QA Study Library

A single-page reading room for all your study PDFs. Open one guide in a built-in
viewer, search across them, or switch to **Read all** to scroll every PDF on one page.

It's one file (`index.html`) with no build step and no dependencies to install.

---

## How to put it online (GitHub Pages)

1. **Create a repo** on GitHub (e.g. `qa-study-library`). Make it **Public**.
2. **Add your files** to the repo root:
   - `index.html`
   - `.nojekyll`
   - all your `.pdf` files (drop them right next to `index.html`)
3. **Enable Pages**: repo → **Settings → Pages** → *Source: Deploy from a branch* →
   Branch: `main`, Folder: `/ (root)` → **Save**.
4. Wait ~1 minute, then open the link GitHub shows, e.g.
   `https://YOURNAME.github.io/qa-study-library/`

That's it. Every `.pdf` in the repo shows up automatically.

> Tip: You can drag-and-drop the PDFs straight into the repo on the GitHub website
> (**Add file → Upload files**) — no git commands needed.

---

## Adding or removing PDFs later

Just add or delete `.pdf` files in the repo. The list **rebuilds itself** on the next
page load — you don't edit any code. (It reads the repo's file list from GitHub.)

---

## Good to know

- **Categories** (SQA Theory, Tools, Programming, Career…) are worked out automatically
  from each filename, so keep filenames descriptive.
- **One filename in your screenshot was cut off** —
  `Software_Development_Methodologies.pdf`. Make sure the real file uses that exact name,
  or rename it; the auto-list uses whatever the actual filename is, so this only matters
  for the offline preview list inside `index.html`.
- The `.md` file (`istqb_ctfl_prep.md`) is skipped — only PDFs are shown. Its PDF version
  (`istqb_ctfl_prep.pdf`) is included.
- Sharing a link with `#file=Selenium-Viva-Prep-Guide.pdf` opens straight to that guide.
- Works on phones too (the sidebar becomes a menu).

## Optional tweaks (top of `index.html`)

```js
const CONFIG = {
  siteTitle: "QA Study Library",   // heading
  tagline:   "Viva & interview prep",
  pdfDir:    "",                   // set to "pdfs" if you keep PDFs in a /pdfs subfolder
  ...
};
```

If you ever host it somewhere that isn't GitHub Pages, it falls back to the `manualList`
of filenames in that same CONFIG block.
