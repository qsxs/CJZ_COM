# 纯记账 (Chunjizhang) — Website

## What this is

GitHub Pages static site for the Android app **纯记账**.
Landing page: `index.html` (pure HTML+JS, not a Jekyll template). Help docs (`help/*.md`) use the Jekyll layout in `_layouts/default.html`.

The Android app source code is **not in this repo** — only the website and APK binaries are.

## Release workflow

1. Drop new APK into `update/` (name pattern: `chunjizhang_Official_release_<VERSION>_<DATE>.apk`; alpha/beta builds use e.g. `chunjizhang_4.0.0_alpha2_<DATE>.apk`)
2. Update `update/app_version.json` with new versionCode, versionName, updateLog, apkUrl
3. The homepage `index.html` (`#dl-android`) and redirect page `index/jump.htm` read `update/app_version.json`: display and download Beta only when its `versionCode` is greater than Official's; otherwise use Official (including equal version codes). Alpha is distributed through the in-app update channel only. Variants `index_glass.html` / `index_flat.html` have their own links if in use.
4. Commit and push — GitHub Pages auto-deploys

## Key files

| File | Purpose |
|---|---|
| `index.html` | Main landing page (download, donate, contact) |
| `_config.yml` | Jekyll site config (title, description) |
| `CNAME` | Custom domain (`www.chunjizhang.com`) |
| `update/app_version.json` | In-app update check payload |
| `update/update_log.md` | Changelog (linked from navbar) |
| `other/announcement.json` | In-app announcement banner (set `enable: false` to hide) |

## Notes

- No build tooling, no package manager, no tests — pure static site
- Landing page is `index.html` (`.htm` extension no longer used; `index_old.htm` is the legacy page)
- APK download link in `index.html:713` (`#dl-android`); variants `index_glass.html` / `index_flat.html` have their own links if used
- WeChat users get redirected to `index/jump.htm` (prompts to open in browser)
