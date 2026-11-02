# Adding Projects and Presentations

This guide covers publishing new work to the site. Keep it in the repo as a reference.

## The structure

Each project is a folder inside `projects/`, containing an `index.html` project page. Some projects also contain one or more presentations (self-contained Quarto renders) that the page embeds.

```
projects/
  pd-model/              # multi-stage project: one page, several presentations
    index.html
    eda.html
    pd.html
  vintage-analysis/      # single-page project
    index.html
```

## Conventions

Follow the conventions in the README. In short: outcome-first copy, no status badges, the
standard **View Project →** and **Repository ↗** labels, no em dashes in visible copy, and
no placeholder controls. If a project has no repo yet, leave out the Repository link.

## Adding a Quarto presentation

### 1. Render a self-contained file

```bash
quarto render deck.qmd --to revealjs --embed-resources
```

`--embed-resources` packs the CSS, JavaScript and images into one HTML file, so the deck works as a single embed.

### 2. Copy it into the project folder

Name it for its stage, for example `eda.html`, and copy it into the matching project folder. Use PowerShell from the deck folder:

```powershell
copy 01_eda.html "E:\Dev\smallchuch.github.io\projects\pd-model\eda.html" -Force
```

### 3. Link it from the project page

On a single-deck page, point the embed at the file. On the multi-stage PD page, add the stage to the `STAGES` list in `projects/pd-model/index.html` (see below).

## Adding a stage to the PD model page

Open `projects/pd-model/index.html` and find the `STAGES` list near the bottom of the file. Add an entry for the stage:

```js
{
  id: "lgd",
  stage: "05",
  title: "LGD model",
  desc: "Loss given default estimates and recovery assumptions.",
  file: "lgd.html",
  ready: true
}
```

Add a stage only once its presentation exists in the folder. Don't list stages that aren't rendered yet.

## Adding a project to the site

Add a panel to `projects.html` (copy an existing `<article class="project-panel">`) and point its **View Project →** link at the project's `index.html`. Include **Repository ↗** only if the repo exists.

Add a row to `index.html` (copy an existing `<article class="proj-row">` inside `.proj-rows`). Include the one-line description, the toolchain line, and the same two links. Remove the Repository link if there isn't one.

## Adding a Power BI dashboard

1. In the Power BI service, choose **File → Embed report → Publish to web (public)**.
2. Copy the `<iframe>` snippet it gives you.
3. Paste it inside the `.embed-frame` div on the project page, in place of the Quarto iframe.

> Publish-to-web is fully public. Anyone with the link can view it. Use it only for non-sensitive or demo data.

## SQL and Excel projects

These usually don't need an embed. Give the project page a clear write-up and link the repo or file. Remove the `.embed-frame` section and keep the prose and buttons.

## Checklist

- [ ] Deck rendered with `--embed-resources` (if there is one)
- [ ] Project folder created under `projects/`, with `index.html`
- [ ] Project page edited: title, description, tags, links and write-up
- [ ] Stage added to the `STAGES` list (multi-stage projects)
- [ ] Panel added to `projects.html`
- [ ] Row added to `index.html`
- [ ] No status labels, em dashes or placeholder controls left in visible copy
- [ ] Committed, pushed, Actions green, and hard-refreshed (Ctrl+F5)

## The one recurring gotcha

If the live site looks unchanged or half-broken after a push, it's almost always the browser cache. Hard-refresh with **Ctrl+F5**, or try an incognito window, before assuming something is wrong.
