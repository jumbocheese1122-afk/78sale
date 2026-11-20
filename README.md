# 78 RPM Record Collection

A static, searchable catalog of a 78 RPM record collection for sale. No backend —
just HTML/JS/JSON, so it hosts for free on GitHub Pages.

## Hosting on GitHub Pages

1. Create a new GitHub repo (public or private) and push these files to it:

   ```bash
   git init
   git add .
   git commit -m "Initial catalog"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```

2. On GitHub, go to the repo's **Settings → Pages**, set **Source** to the `main`
   branch and `/ (root)` folder, then save.
3. After a minute or two the site is live at
   `https://<your-username>.github.io/<your-repo>/`.

Any time you edit `index.html`, `data.js`, or `sold.json` and push to `main`,
GitHub Pages redeploys automatically within a minute or so.

## Marking items as sold

The site has no server, so "marking sold" works like this:

1. Open the live site and append `?owner=1` to the URL once
   (e.g. `https://<you>.github.io/<repo>/?owner=1`). This unlocks **Owner Mode**
   for your browser and is remembered there — you won't need the `?owner=1`
   again on that device/browser. A small "owner" link in the bottom-right
   corner also toggles it, and exiting is one click ("Exit").
2. In Owner Mode, every card gets a **Mark sold / Mark available** button.
   Click it for any records you've sold — the card dims and gets a "Sold"
   ribbon immediately, just in your browser, as you go.
3. When you're done, click **Export sold.json** in the Owner Mode panel. Your
   browser downloads an updated `sold.json` listing every sold claim number.
4. Replace the repo's `sold.json` with the downloaded file and push:

   ```bash
   git add sold.json
   git commit -m "Mark records sold"
   git push
   ```

   Once GitHub Pages redeploys, every visitor sees the updated sold status.

Buyers can check **Hide sold** in the toolbar to only browse what's still
available.

## Regenerating the catalog data

`data.js` is generated from the original Discogs export CSV plus a one-time
Discogs API pass that pulls label photos and genre/style tags (see the
`build.py` / `fetch_images.py` scripts used to produce it, if you have them).
`sold.json` and any local Owner Mode state are independent of that
regeneration — regenerating `data.js` will not affect sold markings.
