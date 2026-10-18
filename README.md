# facelessrekt-web

Static site for facelessrekt.com. No build step, no framework, no dependencies —
plain HTML and CSS. Any static host works.

## Layout

```
index.html              landing: apps + security summary
404.html
assets/
  style.css             the whole design system
  apps/                 app icons used by the cards
calcvault/
  index.html            app page
  privacy.html          privacy policy  <- URL Play Store needs
adem/
  index.html            app page
security/
  index.html            security research portfolio + disclosure policy
_template/
  privacy.html          skeleton for the next app
```

## Deploy

### GitHub Pages (free, ~5 minutes)

```bash
cd ~/.omp/engagements/facelessrekt-web
git init
git add -A
git commit -m "facelessrekt site"
gh repo create facelessrekt-web --public --source=. --push
```

Repo → **Settings → Pages → Source: Deploy from a branch → main / (root)**.

URL: `https://<username>.github.io/facelessrekt-web/`

### Custom domain

Add a `CNAME` file containing `facelessrekt.com`, then a DNS `CNAME` record
pointing at `<username>.github.io`. Result:
`https://facelessrekt.com/calcvault/privacy.html`

## Adding an app

```bash
cp -r calcvault newapp
```

Edit the copy, drop a 512×512 icon into `assets/apps/`, add an `<li>` to the
apps list in `index.html`. Keep the section order in the privacy policy — Play
reviewers expect permissions, third parties and deletion to be findable.

## Paths are relative, deliberately

Every `href` and `src` is relative (`assets/style.css`, `../security/`), never
root-relative (`/assets/style.css`). Root-relative paths break two common cases:

- opening the file directly (`file://…`), where `/` is the filesystem root
- GitHub Pages on a project repo, where the site lives under `/<repo>/`

Verified: all pages render correctly from `file://`, and every internal link
resolves.

## Design notes

One accent colour, one monospace face for metadata, one sans for prose. Sections
are numbered in the `h2` so the page reads as a document rather than a stack of
cards. Severity chips are colour-coded but also labelled in text, so the meaning
survives greyscale and colour-blind readers.

No JavaScript beyond the copyright year. No web fonts — system stack only, so
there is nothing to block first paint and no third-party request.
