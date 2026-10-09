# Carlos Gallego-Moll: academic website

Quarto website (HTML, light/dark theme). Public content only.

## Build

```bash
quarto preview      # live preview at http://localhost:4200 (or the port Quarto prints)
quarto render       # builds _site/
```

Requires Quarto >= 1.4 and R with the `bib2df` package (`install.packages("bib2df")`).

## How content is organised

| Page | File | Source of content |
|---|---|---|
| Home | `index.qmd` | Written by hand (about + news) |
| Research | `research.qmd` | Agenda, work in progress and projects by hand; **publications and working papers are generated** |
| Presentations | `presentations.qmd` | By hand |
| Teaching | `teaching.qmd` | By hand |
| CV | `cv.qmd` | By hand (online CV, no PDF download yet) |
| Contact | `contact.qmd` | Email lives in `_variables.yml` |

### Publications

`scripts/build_publications.R` runs before every render (`pre-render` in `_quarto.yml`). It reads `data/own-bib.bib` and writes `_generated/publications.md` (journal articles, grouped by year) and `_generated/working-papers.md` (`@techreport` entries). Do not edit `_generated/` by hand.

If the private CV repo sits next to this folder (`../Carlos_Gallego___CV/own-bib.bib`), the script copies that bibliography over `data/own-bib.bib` first, so the CV stays the source of truth. Elsewhere it simply uses `data/own-bib.bib`.

Notes on the generated lists:

- Your name is shown in bold. Lists longer than 8 authors are cut to the first three, your name and "et al."
- Titles are shown exactly as written in the `.bib`.
- Each title links to the DOI (or to `url` when there is no DOI), which is how working papers are redirected to their source.

## Before going public: checklist

- [ ] Set the institutional email in `_variables.yml`.
- [ ] Add a portrait: put `assets/photo.jpg` (square) and uncomment `image:` in `index.qmd`.
- [ ] When a custom domain exists, update `site-url` in `_quarto.yml`, `url` in `assets/structured-data.html` and the `Sitemap:` line in `robots.txt`.
- [ ] CV download is **intentionally not offered**. When ready, add the link in `cv.qmd` (see the comment at the top).
- [ ] Submit the sitemap in Google Search Console.

## Publishing (GitHub Pages)

1. Create a **public** repository named `cgallegom.github.io` under the `cgallegom` account.
2. In this folder: `git init`, add the remote, commit and push to `main`.
3. `quarto publish gh-pages` (renders locally and pushes `_site/` to the `gh-pages` branch), then set Pages to serve that branch.
4. For a custom domain: add it in the repository's Pages settings and create the DNS records the registrar needs. GitHub redirects the old `github.io` address to the new one.
