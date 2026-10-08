# demo-apps

Public download page for small **demo** apps (plugin demos, experiments). Scan a QR code → install on Android.

Site: https://tucarmd.github.io/demo-apps/

| App | Page | Source |
|---|---|---|
| AppVersion Demo | [app-version/](https://tucarmd.github.io/demo-apps/app-version/) | `capacitor-app-version/example-app` (private) |

## Rules

- **Demo apps only.** Never publish company / production apps (e.g. CarMD Connect) here: this repo and its
  releases are public, anyone with the link can download them.
- **No binaries in git.** APKs live as GitHub **Release assets**, one fixed tag per app
  (`<app>-latest`), so the download URL — and the QR code — never changes:
  `https://github.com/tucarmd/demo-apps/releases/download/<app>-latest/<app>-demo.apk`
- iOS is not published: an installable `.ipa` needs signing (ad hoc UDIDs or TestFlight).

## How an app gets updated

The app's own repo builds the APK on CI and uploads it to this repo's release with `--clobber`:

```bash
gh release upload app-version-latest app-version-demo.apk --repo tucarmd/demo-apps --clobber
```

The source repo needs a secret `DEMO_APPS_TOKEN`: a fine-grained PAT with access to **only** `tucarmd/demo-apps`,
permission **Contents: Read and write**.

## Add a new demo app

1. Create the release once: `gh release create <app>-latest --repo tucarmd/demo-apps --title "<App> (latest)" --notes "Built by CI"`.
2. Copy `app-version/` to `<app>/`, change `TAG`, `FILE` and the texts.
3. Add a card to `index.html` and a row to the table above.
4. Add the upload step to the app repo's workflow and the `DEMO_APPS_TOKEN` secret.
