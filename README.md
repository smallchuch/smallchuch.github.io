# Chuch — Portfolio Website

A hand-built, no-framework portfolio (plain HTML + CSS + a little JS) for
showcasing credit-risk and data-analytics work: Quarto presentations, Jupyter
notebooks, Power BI dashboards, SQL, and Excel projects. Styled with my own
brand design system (jacaranda / gold / olive on warm off-white — Inter, DM
Sans, JetBrains Mono), ported from `python_style_util.py`.

## Structure

```
index.html                         # home / landing page
projects.html                      # projects index (filter tabs + cards)
styles.css                         # shared design system — edit colors here
cv.pdf                             # your CV (add this file)
img/                               # screenshots for cards/featured (optional)
projects/
  credit-risk-eda/
    index.html                     # a project detail page (copy this per project)
    presentation.html              # the rendered Quarto deck (replace placeholder)
```

Each project lives in its own folder under `projects/` with an `index.html`
(the write-up page) and a `presentation.html` (the embedded Quarto deck). Source
code and notebooks stay in **separate GitHub repos** — the project page just
links out to them.

## Adding a new project

1. **Copy** `projects/credit-risk-eda/` to `projects/<your-project>/`.
2. **Edit** `projects/<your-project>/index.html` — title, description, tech
   chips, the write-up prose, and the three action buttons (presentation,
   source repo, notebook). The links to `../../styles.css`, `../../index.html`
   etc. already point two levels up, so leave those as-is.
3. **Add a card** on `projects.html`: copy an existing `<a class="card" ...>`
   block into the right category group, point its `href` at your new folder,
   and set `data-type` to one of `notebook`, `quarto`, `powerbi`, `sql`, or
   `excel` (this drives the filter tabs and their counts).

### Embedding a Quarto presentation

Render your deck to a **self-contained** HTML file so it works as a single
embed:

```bash
quarto render deck.qmd --to revealjs --embed-resources
```

`--embed-resources` inlines the CSS/JS/images into one HTML file. Rename the
output to `presentation.html` and drop it in the project folder, replacing the
placeholder. The project page embeds it in a responsive 16:9 frame; the "Open
presentation fullscreen" button opens it on its own.

> Tip: if you don't use `--embed-resources`, Quarto also creates a
> `deck_files/` folder — commit that alongside `presentation.html` so the deck
> can find its assets.

### Embedding a Power BI dashboard

In the Power BI service, use **File → Embed report → Publish to web (public)**
to get an `<iframe>` snippet, then paste it inside the `.embed-frame` div on the
project page in place of the Quarto iframe. Note: publish-to-web is **public** —
never use it for confidential data. Keep dashboards to "at most one or two," as
you planned.

### SQL / Excel projects

These usually don't need an embed — give the project page a write-up and link
the repo/file. You can drop the `.embed-frame` section entirely and keep just
the prose + action buttons.

## Colors & fonts

Everything is driven by CSS variables at the top of `styles.css` under
`:root`, mirroring your Python palette (`jacaranda`, `gold`, `olive`,
`charcoal`, `off_white` at shades 100–500). Change a hex there and it updates
site-wide. Fonts load from Google Fonts (Inter, DM Sans, JetBrains Mono).

## Deploying (GitHub Pages)

Your repo `smallchuch.github.io` is already set to deploy from `main` / root.
Just commit and push these files to the root of that repo:

```bash
git add .
git commit -m "New portfolio site"
git push
```

The site publishes at **https://smallchuch.github.io** within ~1 minute of each
push. Optionally add an empty `.nojekyll` file at the root to tell GitHub Pages
to serve the files as-is (no Jekyll processing).

### A note on placeholders

Search the files for `smallchuch`, `chuchdeveloper@proton.me`, "Chuch", and the
LinkedIn `href="https://www.linkedin.com/"` and swap in your real name, GitHub
handle, email, and profile links.

## Local preview

```bash
python -m http.server 8000
# open http://localhost:8000
```
