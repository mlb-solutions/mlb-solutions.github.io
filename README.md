# MLB Solutions website

Source of [mlb-solutions.github.io](https://mlb-solutions.github.io/), the public site for MLB Solutions' Android games. Static HTML, no build step, served by GitHub Pages from `main`.

## Pages

| URL | Purpose |
|-----|---------|
| `/` | Company landing page |
| `/warmer/` | Warmer landing page |
| `/warmer/privacy.html` | Warmer privacy policy (Play Console policy and data deletion URL) |
| `/warmer/c.html` | Warmer challenge link: Android App Link target, forwards to Google Play with the install referrer |
| `/bridgle/` | Bridgle landing page |
| `/bridgle/privacy.html` | Bridgle privacy policy |
| `/bridgle/s.html` | Bridgle challenge link, same mechanism as Warmer |
| `/.well-known/assetlinks.json` | Android App Links verification for both apps |
| `/app-ads.txt` | AdMob seller authorization |

## Layout

```
index.html, style.css, 404.html   company site
warmer/                           Warmer pages and theme
bridgle/                          Bridgle pages and theme
.well-known/assetlinks.json       one statement per app
app-ads.txt
.nojekyll                         required so Pages serves .well-known
```

## Maintaining

- `assetlinks.json` is only honored at the host root, so this must remain the organization's `*.github.io` repo. Add a statement per app; do not replace the file.
- Host and path constants in the apps (`ChallengeUrl.kt`) must match the pages above and the manifest `intent-filter`.
- When an app's data handling changes (ads, billing, leaderboards), update its `privacy.html`, bump "Last updated" and update the Play Data safety form.
- Verify after deploy:
  ```
  curl -s https://mlb-solutions.github.io/.well-known/assetlinks.json | python3 -m json.tool
  adb shell pm verify-app-links --re-verify com.warmer.app
  ```

## Contact

lstamenov.mlb@gmail.com
