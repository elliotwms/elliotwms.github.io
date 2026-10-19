# CLAUDE.md

Personal site for Elliot Williams, served at https://elliot.wales via GitHub Pages.

## Stack

- [Hugo](https://gohugo.io) (extended), version pinned by `HUGO_VERSION` in `.github/workflows/gh-pages.yml`. Use that exact version locally; bump it there when upgrading.
- No theme or submodules: templates live in `layouts/`, CSS in `assets/css/` (vendored from the etch theme, MIT, see `LICENSE-etch`). Edit them directly.
- No Node, Sass or other build tooling.

## Layout

- `content/_index.md` homepage intro; `content/posts/` blog posts (the only main section, so they're listed on the homepage and in the RSS feed); `content/talks/` talks; `about.md`, `projects.md`, `wishlist.md` standalone pages.
- `layouts/_default/baseof.html` page skeleton; `layouts/partials/head.html` meta, CSS bundle, Open Graph/Twitter cards and `<title>` (`Page · Site`, site title alone on the homepage).
- `layouts/partials/goatcounter.html` GoatCounter analytics, only rendered when `hugo.IsProduction`.
- `layouts/partials/subscribe.html` Buttondown signup form (username in `params.buttondown`). Checkboxes apply the `posts` and `newsletter` tags. Shown at the end of every post (`single.html`) and on `content/subscribe.md` via the `{{< subscribe >}}` shortcode. New-post emails come from Buttondown's RSS-to-email reading `/posts/index.xml`, so keep that feed's URL stable.
- `layouts/_default/list.html` generic list for sections and taxonomies; `layouts/index.html` homepage.
- `hugo.toml` site config and the main menu. `markup.goldmark.renderer.unsafe = true`, so raw HTML in Markdown is allowed.

## Content conventions

- British English (`locale = "en-GB"`).
- Every page needs a `title` in front matter; it feeds the `<title>`, the page `<h1>`, and list entries.
- Posts and talks need a `date`. New content starts as `draft: true` (see `archetypes/default.md`).
- Embed videos with the built-in `{{< youtube ID >}}` shortcode.

## Checking a change

```sh
hugo --gc --minify --panicOnWarning   # same as CI; must exit cleanly
hugo server -D                         # eyeball it locally
```

After a build, grep `public/` for the thing you changed rather than assuming. Delete `public/` and `resources/_gen/` afterwards; both are gitignored.

## Git and deploys

- Default branch is `master`. Pushes to it deploy; PRs only build.
- Commit messages are short and imperative, often with a conventional prefix (`fix:`, `chore:`).
- Work on a branch and open a PR rather than pushing to `master`.
