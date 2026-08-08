# Adding Projects & Presentations

A step-by-step guide for publishing new work to this site. Keep this file in the
repo as your reference.

## The mental model

Every project is a **folder inside `projects/`**. That folder holds two files:

- `index.html` — the project **write-up page**: title, description, tech tags,
  a short write-up, and buttons linking out to the source repo and notebook.
- `presentation.html` — your **rendered Quarto deck**, embedded in a responsive
  16:9 frame on the write-up page.

Your source code and notebooks live in their **own separate GitHub repos**. The
project page doesn't host them — it just links to them. A working example ships
at `projects/credit-risk-eda/`.

```
projects/
  credit-risk-eda/
    index.html          # the write-up page
    presentation.html   # the rendered Quarto deck (or a Power BI embed)
  <your-next-project>/
    index.html
    presentation.html
```

## Adding a Quarto presentation

### 1. Render the deck to a single self-contained file

In your project's Quarto folder:

```bash
quarto render deck.qmd --to revealjs --embed-resources
```

`--embed-resources` inlines all the CSS, JS, and images into **one** HTML file,
so it works as a standalone embed. Without it, Quarto also produces a
`deck_files/` folder that you'd have to copy alongside the HTML for the deck to
find its assets.

### 2. Create the project folder

Copy the example folder and rename it:

```
projects/credit-risk-eda/  ->  projects/loan-default-model/
```

### 3. Drop in your deck

Move your rendered deck into the new folder, renamed to **`presentation.html`**,
replacing the placeholder file that's already there.

### 4. Edit the write-up page

Open the new folder's `index.html` and update:

- the page `<title>` and the `<h1>` project title
- the description paragraph and the tech-stack chips
- the three buttons near the top — **Open presentation fullscreen**,
  **Source code**, and **Notebook** — pointing at your repos
- the write-up prose lower down (Overview / What I did / Key findings / Links)

Leave the `../../styles.css`, `../../index.html` etc. links as they are — they
already point two levels up to the shared files.

### 5. Add a card on the projects page

So people can find it, open `projects.html` and copy one of the existing
`<a class="card"> ... </a>` blocks into the right category group. Then:

- point its `href` at your new folder, e.g. `projects/loan-default-model/index.html`
- set `data-type` to one of: `notebook`, `quarto`, `powerbi`, `sql`, `excel`
  (this drives the filter tabs and their counts)

### 6. Commit, push, refresh

```bash
git add .
git commit -m "Add loan default project"
git push
```

Wait for the green check in the repo's **Actions** tab, then hard-refresh the
live page with **Ctrl+F5** (browsers cache aggressively).

## Adding a Power BI dashboard

Same as above, but instead of a Quarto file:

1. In the Power BI service: **File → Embed report → Publish to web (public)**.
2. Copy the `<iframe>` snippet it gives you.
3. Paste it inside the `.embed-frame` div on the project's `index.html`, in
   place of the existing Quarto `<iframe>`.

> ⚠️ **Publish-to-web is fully public** — anyone with the link can view it.
> Only use it for non-sensitive / demo data. Keep dashboards to one or two.

## SQL & Excel projects

These usually don't need an embed. Give the project page a good write-up and link
the repo or file with the action buttons. You can delete the `.embed-frame`
section from that page's `index.html` and keep just the prose and buttons.

## Adding a preview image to a card (optional)

- **Featured block** (home + projects pages): save a screenshot at
  `img/<name>.png`, then in the `.featured-media` div swap the placeholder
  `<span>` for the commented-out `<img>` tag.
- Cards themselves are text-only by default — keep them clean, or add your own
  `<img>` at the top of a `.card` if you want thumbnails.

## Quick checklist

- [ ] Deck rendered with `--embed-resources`
- [ ] New folder under `projects/` with `index.html` + `presentation.html`
- [ ] Write-up page edited (title, description, tags, buttons, prose)
- [ ] Card added on `projects.html` with correct `href` and `data-type`
- [ ] Committed, pushed, Actions green, hard-refreshed

## The one recurring gotcha

After any push, if the live site looks unchanged or half-broken, it's almost
always the **browser cache**, not a real problem. Hard-refresh (**Ctrl+F5**) or
open an incognito window before assuming anything's wrong.
