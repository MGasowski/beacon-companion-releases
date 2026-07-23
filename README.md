# Beacon Companion — release feed

Private distribution channel for the **Beacon** macOS companion app. This repo
holds no source: it exists so `electron-updater` has a stable place to read
releases from.

- Source lives in `MGasowski/qa-companion` (`apps/qa-companion`).
- Each release carries the signed + notarized `.dmg` and `.zip`, their
  `.blockmap`s (used for differential updates), and `latest-mac.yml`, which the
  updater reads to discover the newest version.
- The app authenticates to this private repo with a read-only fine-grained PAT
  baked in at build time. A token that cannot read this repo returns **404**,
  which the updater surfaces as "no update available" rather than an error.
- Assets are named by `build.mac.artifactName` / `build.dmg.artifactName`.
  Never rename them by hand: the updater fetches the exact `path:` recorded in
  `latest-mac.yml` and 404s on any mismatch.
