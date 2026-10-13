# Bridgle site (GitHub Pages)

Static pages for Bridgle: privacy policy, store landing page and the challenge-link landing page.
Designed to be the root of the organization Pages repo `mlb-solutions/mlb-solutions.github.io`, served at `https://mlb-solutions.github.io/`.

| URL | File | Use |
|-----|------|-----|
| `/bridgle/` | `bridgle/index.html` | landing page |
| `/bridgle/privacy.html` | `bridgle/privacy.html` | Play Console privacy policy URL |
| `/bridgle/s.html` | `bridgle/s.html` | challenge link; App Link target, forwards to Play with the install referrer |
| `/.well-known/assetlinks.json` | `.well-known/assetlinks.json` | Android App Links verification |

## Deploy
1. Create the repo `mlb-solutions/mlb-solutions.github.io` (public) and copy the **contents** of this folder into its root, including `.nojekyll` (without it Pages hides `.well-known`).
2. Repo Settings, Pages, deploy from branch `main`, folder `/ (root)`.
3. Replace `REPLACE_WITH_PLAY_APP_SIGNING_SHA256` in `.well-known/assetlinks.json` with the app-signing SHA-256 from Play Console (App integrity). Add the upload key too if you test release builds locally. If the host already serves an `assetlinks.json` (for example Warmer's), append a statement to its array instead of replacing the file.
4. Verify: `make site-check`, then `curl -s https://mlb-solutions.github.io/.well-known/assetlinks.json | python3 -m json.tool` and on a device `adb shell pm verify-app-links --re-verify com.lyudmil.bridgle.app`.

`assetlinks.json` is only honored at the host root, which is why this must be the organization's `*.github.io` repo (or a custom domain).

## Keep in sync with the app
- Host and path constants live in `ChallengeUrl.kt` (phase 07): host `mlb-solutions.github.io`, path `/bridgle/s.html`, and the manifest `intent-filter`.
- Update `bridgle/privacy.html` before shipping ads (phase 12), billing (phase 12) or Play Games (phase 13), then bump the "Last updated" date and update the Play Data safety form.
