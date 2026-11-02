# Evan Reynolds · Portfolio Website

A hand-built portfolio in plain HTML, CSS and a little JavaScript, with no framework. It
showcases applied credit-risk and portfolio analytics work. Styled with a brand design system
(jacaranda / gold / olive on warm off-white; Inter, DM Sans, JetBrains Mono).

## Structure

```
index.html                         # home page
projects.html                      # projects index (one panel per project)
styles.css                         # shared design system; edit colours here
cv.pdf                             # CV
image/                             # headshot and other images
projects/
  pd-model/
    index.html                     # Credit Risk PD Model page (multi-stage)
    eda.html, pd.html, ...         # stage presentations (self-contained renders)
  vintage-analysis/
    index.html                     # Mortgage Vintage Analysis page
```

Source code and notebooks live in separate GitHub repositories. The project pages link out to them.

## Adding a project

See [ADDING-PROJECTS.md](ADDING-PROJECTS.md).

## Conventions

These apply across the whole site:

- **Outcome-first copy.** Describe the work and what it shows. Avoid "upskilling", "moving into" and "in progress" language.
- **No status badges.** Don't add "coming soon", "live" or "in progress" labels. If a link has no destination, remove the control.
- **Standard CTAs.** Use **View Project →** for a project page and **Repository ↗** for source code.
- **No em dashes in visible copy.** Use a colon, comma or full stop instead. HTML comments are fine.
- **Concise.** One or two sentences per description. Say each point once.
- **Decision support.** Frame lending-decision language as decision support, never as an automated approval or decline.
- **Consistent names.** Use the same model, stage and metric names on every page and in every presentation.

## Colours and fonts

Colours are CSS variables at the top of `styles.css` under `:root`. Change a hex value there and it updates across the site. Fonts load from Google Fonts (Inter, DM Sans, JetBrains Mono).

## Deploying (GitHub Pages)

The repo `smallchuch.github.io` deploys from `main` at the root. Commit and push to publish:

```bash
git add .
git commit -m "Update portfolio"
git push
```

The site publishes at **https://smallchuch.github.io** within about a minute of each push. To serve files as-is without Jekyll processing, add an empty `.nojekyll` file at the root.

## Local preview

```bash
python -m http.server 8000
# open http://localhost:8000
```
