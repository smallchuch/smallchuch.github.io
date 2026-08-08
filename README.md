# Chuch — Portfolio Website

A bold, single-page portfolio built with plain HTML + CSS (no build step, no
frameworks). Designed to showcase data & analytics projects: Jupyter notebooks,
Quarto presentations, Power BI dashboards, SQL, and Excel work.

## Files

```
index.html    # all the content and structure
styles.css    # all the styling (colors, layout, animations)
cv.pdf        # your CV — add this file so the Download CV button works
README.md     # this file
```

## Customising it

Everything you need to edit is in `index.html`:

- **Hero text** — the headline and intro paragraph at the top.
- **Projects** — each project is a `<article class="card">`. To add one, copy an
  existing card and change the title, description, tag, and links. Set the
  `data-type` attribute to one of `notebook`, `quarto`, `powerbi`, `sql`, or
  `excel` so the filter buttons work.
- **Links** — replace the `href="#"` placeholders with real links (GitHub repo,
  nbviewer/HTML export of a notebook, published Power BI report, etc.).
- **About / CV / Contact** — plain text and links near the bottom.

Colors live at the top of `styles.css` under `:root` — change the `--grad-*`
variables to reshape the whole palette.

### Tips for linking each project type

- **Jupyter notebooks** — commit the `.ipynb` to the repo (GitHub renders it), or
  export to HTML (`jupyter nbconvert --to html`) and link the HTML file. You can
  also link an [nbviewer](https://nbviewer.org) URL.
- **Quarto** — render to HTML (`quarto render`) and drop the output into the repo;
  link the generated `.html`.
- **Power BI** — use "Publish to web" in the Power BI service to get an embed/link
  URL, then link or `<iframe>` it. (Note: publish-to-web is public — don't use it
  for sensitive data.)
- **SQL / Excel** — link the file in the repo, or write a short markdown/HTML
  writeup and link that.

## Deploying to GitHub Pages (free)

1. **Create the repo.** Sign in to GitHub and make a new repository. For a
   personal site at `https://<username>.github.io`, name it exactly
   `<username>.github.io`. Any other name works too — it'll just live at
   `https://<username>.github.io/<repo-name>/`.

2. **Add these files** to the repo (drag-and-drop in the browser, or use git):

   ```bash
   git init
   git add .
   git commit -m "Initial portfolio"
   git branch -M main
   git remote add origin https://github.com/<username>/<repo>.git
   git push -u origin main
   ```

3. **Turn on Pages.** In the repo, go to **Settings → Pages**. Under "Build and
   deployment", set **Source: Deploy from a branch**, pick branch **main** and
   folder **/ (root)**, then Save.

4. **Wait ~1 minute**, then visit the URL Pages shows you. Done. Every push to
   `main` republishes automatically.

### Custom domain (optional)

If you buy a domain (e.g. `chuch.dev`):

1. In **Settings → Pages → Custom domain**, enter your domain and Save. This
   creates a `CNAME` file in the repo.
2. At your domain registrar, add DNS records:
   - Four `A` records pointing to GitHub's IPs: `185.199.108.153`,
     `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - For a `www` subdomain, a `CNAME` record pointing to `<username>.github.io`
3. Back in Pages, tick **Enforce HTTPS** once the certificate is issued.

## Local preview

Just open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
# then open http://localhost:8000
```
