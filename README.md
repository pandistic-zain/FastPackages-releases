# FastPackages ERP — Releases

Built by [SalwaDev](https://salwadev.com) — Developer: [Zain Ul Abideen](https://webbyzain.online)

This repo hosts nothing but published installer downloads for the
**FastPackages ERP desktop app**, under this repo's [Releases][releases]
tab. There is no source code here on purpose — the real source lives in a
separate, private repository.

## Why a separate repo

The desktop app checks this repo automatically (via `electron-updater`) to
find and download newer versions. Keeping it separate from the private
source repo means:

- This repo can be **public** (required for the app to check it with no
  credentials baked into the installer — see below), while the actual
  source code stays private.
- No GitHub access token ever has to ship inside the installed app. A
  token embedded in a distributed app would be extractable by anyone with
  access to an installed PC; a plain public repo needs none.

## What goes here

Nothing, manually. Every release is published by running
`electron-builder --publish always` from the `fastpackages-pos` repo's
`apps/desktop` folder (see `docs/shipping-a-windows-installer.md` there),
which creates a tagged GitHub Release here with the installer (`.exe`) and
its update metadata (`latest.yml`, `.blockmap`) attached automatically.

Don't manually create releases, edit assets, or delete/rename existing
releases here — every installed app is actively polling this repo, and
editing a release out from under a partially-downloaded update can break
that update for whoever's mid-download.

## Setup checklist (one-time)

1. Create this repo on GitHub as **public**, under the same
   `pandistic-zain` account, named exactly `FastPackages-releases`
   (must match `build.publish` in `apps/desktop/package.json`).
2. `git remote add origin https://github.com/pandistic-zain/FastPackages-releases.git`
3. `git push -u origin main`
4. From then on, publishing a new app version is just the
   `electron-builder --publish always` step above — nothing further to do
   in this repo directly.

[releases]: https://github.com/pandistic-zain/FastPackages-releases/releases
