# Vigil Fire — marketing site

A standalone, single-file marketing site for **Vigil Fire** (the fire-equipment
register app, which lives in its own separate repo — `Fire-Equipment-Register`).

Keep this repo separate from the app: different audience, different release
cadence, and a marketing change should never be able to break the compliance
app or its offline cache.

## Structure

```
index.html      ← the whole site (inline CSS + a few lines of JS, no build step)
.nojekyll       ← lets GitHub Pages serve the files as-is
screens/        ← app screenshots used on the page (site-register, due-list, equipment-form, trainee-logbook)
og-image.png    ← 1200×630 social preview image (referenced in <head>)
```

The screenshots are generated, not live captures: HTML mock-ups that reuse the
app's own CSS with realistic sample data, rendered with headless Chrome. They
track the live app at `https://vigilfire.github.io/app/` — when the app gains or
changes a feature, refresh the copy here and re-shoot.

## Fill in the placeholders

Search `index.html` for `TODO` and `{{ }}`:

| Placeholder | What to set |
|---|---|
| `https://app.vigilfire.co.za` | Done — "Log in" links point at `https://vigilfire.github.io/app/` |
| _(contact details)_ | Done — email `vigilfire1@gmail.com`, phone/WhatsApp `063 399 4805` |
| `{{FORM_ID}}` | Done — the contact form posts to Formspree form `xwlklgvw`. Swap the id in the `<form action>` to change it, **or** switch to Netlify Forms — see the comment above the `<form>` |
| footer entity line | Deferred — company not yet registered; once "Vigil Fire (Pty) Ltd" is registered, uncomment the line in the footer |
| `screens/*.png` | Done — four generated screenshots wired into `index.html` (see Structure note above) |
| `og-image.png` | Done — 1200×630 branded card |
| `<link rel="canonical">` / `og:url` | Your real domain |

_Standards naming: the site consistently uses **SANS 1475-1** (not bare "SANS 1475")._

## Run locally

It's static — just open `index.html`, or:

```bash
python -m http.server 8000    # then visit http://localhost:8000
```

## Deploy (pick one — all free for a static site)

### GitHub Pages
1. `git init && git add -A && git commit -m "Marketing site"`
2. Create a repo (e.g. `vigil-fire-web`) and push.
3. Repo → Settings → Pages → Source: `Deploy from a branch`, branch `main`, folder `/ (root)`.
4. Add a custom domain (`vigilfire.co.za`) in the Pages settings; it writes a `CNAME` file. Point a CNAME/ALIAS DNS record at `<user>.github.io`.

### Cloudflare Pages / Netlify
Connect the repo, leave the build command empty, set the output/publish directory
to `/` (root). Add the custom domain in the dashboard.

## Suggested domains

| | Where |
|---|---|
| Marketing site (this repo) | `vigilfire.co.za` |
| The app (`Fire-Equipment-Register` repo) | `https://vigilfire.github.io/app/` (GitHub Pages) |

The "Log in" links in this site point at the app's GitHub Pages URL.
