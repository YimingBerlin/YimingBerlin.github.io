# yimingliuecon.com

Personal academic homepage for Yiming Liu, hosted free on **GitHub Pages**.
Static HTML/CSS — no build step, no framework, no platform fees.

## How it is served

- Repository: `YimingBerlin/YimingBerlin.github.io` (a GitHub *user site*).
- GitHub Pages serves the contents of the `main` branch at
  `https://yimingberlin.github.io` and, once the custom domain is attached,
  at `https://www.yimingliuecon.com`.
- `.nojekyll` tells GitHub to serve the files as-is (no Jekyll processing).

## Files

| Path | What it is |
|------|------------|
| `index.html` | The homepage (research, publications, courses). |
| `styles.css` | All styling. Recreates the old Weebly "Birdseye" look. |
| `404.html` | Friendly not-found page. |
| `uploads/1/2/2/7/122790501/…` | The CV, paper PDFs, and profile photo. **These paths deliberately match the old Weebly URLs**, so existing links to your papers (SSRN, Google Scholar, other people's pages) keep working after the move. |
| `CNAME` | Added at cutover; contains the custom domain. |

## Editing the site

1. Edit `index.html` (add a paper, change your title, etc.).
2. To add a new paper PDF, drop it in `uploads/1/2/2/7/122790501/` and link to it.
3. Commit and push to `main`:
   ```bash
   git add -A && git commit -m "Update site" && git push
   ```
4. GitHub rebuilds within ~1 minute. Hard-refresh the browser to see changes.

You can also edit any file directly on github.com (pencil icon) if you don't
want to touch the command line.

## Custom domain

See `DOMAIN-SETUP.md` for the full walkthrough of pointing
`yimingliuecon.com` at this site.
