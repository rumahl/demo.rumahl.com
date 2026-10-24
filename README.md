# demo.rumahl.com

Static deployment of the rumahl OS demo. The repository contains the built
frontend; no build step is needed on Vercel.

## Vercel

Import this repository as a static project:

- Framework preset: **Other**
- Build command: none (or use the committed `package.json` no-op script)
- Output directory: `public`
- Domain: `demo.rumahl.com`

`vercel.json` already sets those values, adds the `/apps/*` and `/widgets/*`
rewrites, cache headers for hashed assets and the frame CSP for the demo host.

The `/apps/*` and `/widgets/*` frames allow the demo to be embedded on the
website (`rumahl.com`, `*.rumahl.com`) and on localhost. Add any other parent
origin to `frame-ancestors` there, otherwise the nested app and widget frames
are blocked by the browser.

## Rebuilding

From a rumahl checkout:

```sh
pnpm --dir frontend/packages/shell build:demo
rsync -a --delete frontend/packages/shell/dist-demo/ /path/to/demo.rumahl.com/public/
rm -rf /path/to/demo.rumahl.com/public/.vite
```

Then commit the updated `public/` directory.

The demo keeps its state in the browser (`localStorage`). Clear the site data to
reset apps, files, settings and the workspace.
