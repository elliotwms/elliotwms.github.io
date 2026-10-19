# elliotwms.github.io

A [Hugo](https://gohugo.io) site which powers https://elliot.wales

## Running locally

Install the Hugo version pinned in [`.github/workflows/gh-pages.yml`](.github/workflows/gh-pages.yml) (`HUGO_VERSION`), then:

```sh
hugo server -D   # serve with drafts at http://localhost:1313
hugo             # production build into ./public
```

New posts: `hugo new content posts/my-post.md`

## Deployment

Pushes to `master` build and deploy to GitHub Pages. Pull requests are built (with `--panicOnWarning`) but not deployed.

## Theme

The templates in `layouts/` and styles in `assets/css/` started life as the [etch](https://github.com/LukasJoswiak/etch) theme by Lukas Joswiak, vendored in and modified. See [`LICENSE-etch`](LICENSE-etch).
