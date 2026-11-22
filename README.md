# Tom & Jerry: Hide & Seek 3D — packaging

One game file (`www/index.html`, Three.js inlined, works offline) packaged three ways.

## 1) Laptop / any browser
Open `web-pwa/index.html` directly (double-click) or host the `web-pwa/` folder on any static host
(GitHub Pages, Netlify, Cloudflare Pages). Hosted over https it is installable (Chrome/Edge "Install app",
Android "Add to Home screen", iOS Safari "Add to Home Screen") and runs fullscreen/offline.

## 2) Android APK (no Android Studio needed)
1. Create a GitHub repo and upload everything in this folder (keep the `.github` folder).
2. Open the repo's **Actions** tab -> "Build Android APK" -> run it (it also runs on every push).
3. When it finishes, download the artifact **TomJerry-HideSeek-debug-apk** -> `app-debug.apk`.
4. Copy to your phone, allow "install unknown apps", open it. Landscape + immersive fullscreen are preconfigured.

Or build locally (Android Studio / JDK 17 + Android SDK):
```
npm install
npx cap sync android
cd android && ./gradlew assembleDebug      # -> android/app/build/outputs/apk/debug/app-debug.apk
```
(For the Play Store you need a signed release build/AAB: `npx cap open android` -> Build > Generate Signed Bundle.)
Change the app id/name in `capacitor.config.json` and `android/app/src/main/res/values/strings.xml` before publishing.

## 3) iOS
Needs a Mac: `npm i @capacitor/ios && npx cap add ios && npx cap open ios`, then build in Xcode.
Without a Mac, use the PWA install from Safari.

## Controls
WASD/arrows move · Space/E hide or search · P pause · V camera zoom · on phones: touch & drag anywhere to move (floating stick), quick tap = hide/search.

## v3 – Levels & maps
4 themed maps cycle by level (House, Haunted Mansion, SuperMart, Snowy Camp), with collectibles, combos, 1–3 star ratings and unlockable start levels.

## v4 – Online 2-player
Menu → 👥 Play Online. One player hosts and sends a code; the friend pastes it, sends back a reply code, and the game starts. Peer-to-peer (WebRTC), no game server. Roles swap each round.

## Online play needs a real web page
The claude.ai preview blocks WebRTC. Either open `web-pwa/index.html` directly in Chrome on a laptop, or push this folder to GitHub, enable Settings > Pages > Source: GitHub Actions, and run the "Deploy web version" workflow. You get an https link both players can open on phones.

## v6
Online play now uses a 4-character room code (free public PeerJS matchmaking; game data then flows directly between players). Manual codes remain as a fallback. New realistic cat and mouse models.
