# Tech Blog and Bio
Personal Tech Blog built using the [Minimal Mistakes remote theme starter](https://github.com/mmistakes/mm-github-pages-starter/generate) based on [Minimal Mistakes Jekyll theme](https://github.com/mmistakes/minimal-mistakes).

## Root URL redirect
This repo is a GitHub Pages project site, so it is served at <https://zerafachris.github.io/bio/>. The root URL <https://zerafachris.github.io/> is served by a separate repo, [zerafachris/zerafachris.github.io](https://github.com/zerafachris/zerafachris.github.io), which only redirects visitors here:

- `/` goes to `/bio/`.
- Any other root path, e.g. `/posts/`, goes to the same path under `/bio/`.

If this repo is ever renamed, or the site moves to a custom domain, update the redirect targets in that repo too.