# ▶ SwiftPlay – Auto Video Speed

> Automatically plays every video at **2× speed**. Adds a sleek on-video overlay to adjust speed in **0.25× steps**. Works on YouTube, Netflix, Vimeo, Twitter, Twitch, and everywhere else.

![Chrome Web Store](https://img.shields.io/badge/Chrome%20Web%20Store-Available-brightgreen?logo=googlechrome)
![Manifest V3](https://img.shields.io/badge/Manifest-V3-blue)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## Install

**[→ Add to Chrome / Edge from the Chrome Web Store](https://chromewebstore.google.com/detail/swiftplay/YOUR-EXTENSION-ID)**

Or install manually — see [Manual Installation](#manual-installation) below.

---

## What It Does

Most video sites cap playback speed at 2× or hide the option behind menus. SwiftPlay fixes that:

- **Auto 2× on every video** — the moment a video loads, it plays at 2× automatically. No clicks needed.
- **On-video speed overlay** — a minimal frosted-glass control appears in the top-right corner of every video with `−` and `+` buttons to adjust speed by **0.25× steps**.
- **Global popup panel** — click the extension icon to set or reset speed across all tabs at once.
- **Persistent** — your preferred speed is saved and synced across all your devices via `chrome.storage.sync`.
- **Aggressive enforcement** — works on sites like YouTube and Netflix that normally block external speed changes.

---

## Speed Range

| Minimum | Default | Maximum |
|---------|---------|---------|
| 0.25×   | 2.00×   | 4.00×   |

---

## Screenshots

| On-video overlay | Popup panel |
|---|---|
| ![Overlay](store-assets/screenshot-1-overlay.png) | ![Popup](store-assets/screenshot-2-popup.png) |

---

## Compatibility

Works on any Chromium-based browser:

- ✅ Google Chrome
- ✅ Microsoft Edge
- ✅ Brave
- ✅ Opera
- ✅ Vivaldi

---

## Permissions

SwiftPlay requests the minimum permissions needed:

| Permission | Why it's needed |
|---|---|
| `storage` | Saves your preferred speed via `chrome.storage.sync` |
| `scripting` | Applies your saved speed to videos when changed from the popup |
| `host_permissions` | Injects the speed overlay on any page that contains a video element |

**No data is collected.** See the full [Privacy Policy](privacy-policy.html).

---

## Manual Installation

If you want to install directly from this repo without the Chrome Web Store:

1. Click the green **Code** button → **Download ZIP**
2. Unzip the folder
3. Open Chrome and go to `chrome://extensions`
4. Enable **Developer Mode** (toggle in the top-right)
5. Click **Load unpacked** and select the unzipped `swiftplay-v2` folder

For Microsoft Edge:
1. Go to `edge://extensions`
2. Enable **Developer Mode** (toggle in the bottom-left)
3. Click **Load unpacked** and select the folder

---

## File Structure

```
swiftplay-v2/
├── manifest.json       # Extension config (Manifest V3)
├── content.js          # Core logic — auto-speed + overlay injection
├── content.css         # Overlay styles
├── popup.html          # Popup UI
├── popup.js            # Popup logic (chrome.storage.sync)
├── privacy-policy.html # Privacy policy (hosted via GitHub Pages)
└── icons/
    ├── icon16.png
    ├── icon48.png
    └── icon128.png
```

---

## How It Works

1. `content.js` runs on every page and watches for `<video>` elements — including dynamically loaded ones.
2. When a video is found, it immediately sets `playbackRate` to the saved speed (default 2×).
3. An overlay is injected and absolutely positioned over the video's top-right corner.
4. Speed changes in the popup write to `chrome.storage.sync`, which `content.js` listens to via `chrome.storage.onChanged` — no page refresh needed.
5. For stubborn players (YouTube, Netflix), speed is re-enforced on 8 video events plus an 800ms interval.

---

## Changelog

### v1.0.0 — Initial release
- Auto 2× speed on all videos
- On-video `+` / `−` overlay (0.25× steps)
- Global popup panel
- `chrome.storage.sync` for cross-device persistence
- Aggressive enforcement for YouTube / Netflix / Twitch

---

## License

MIT — free to use, modify, and distribute.

---

## Privacy

SwiftPlay collects **zero data**. The only thing stored is your playback speed preference — a single number saved locally via Chrome's built-in storage API.

Full privacy policy: [privacy-policy.html](privacy-policy.html)
