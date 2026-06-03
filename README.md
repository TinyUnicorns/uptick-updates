# Uptick updates

This repo is served via **GitHub Pages** at https://tinyunicorns.github.io/uptick-updates/
and hosts two things:

- **`index.html`** — the public landing page where anyone can download Uptick.
  The download button resolves the newest `.dmg` straight from `appcast.xml` at page
  load, so it always points at the latest release — no edits needed per version.
- **`appcast.xml` + `*.dmg` / `*.delta`** — the Sparkle auto-update feed
  (`SUFeedURL`). New versions are published from the app repo via `./publish.sh`,
  which rsyncs the versioned dmg, deltas, and a freshly signed appcast here.

## Publishing a release (from the app repo)

```bash
./build.sh --release   # notarized Uptick.dmg
./publish.sh           # → versioned dmg + signed appcast (notes embedded), pushed here
```

That single flow updates **both** the auto-updater (existing users) **and** the
landing-page download (new users) — the page reads whatever `publish.sh` writes.
