# Aurora for Apple TV

Aurora is an open-source game streaming client for Apple TV, built on the [Moonlight](https://github.com/moonlight-stream/moonlight-ios) protocol. It lets you stream your full library of games and apps from a powerful desktop PC to your Apple TV over your local network — with low latency, high quality, and a native tvOS interface.

Aurora supports both [Sunshine](https://github.com/LizardByte/Sunshine) (recommended, open source) and NVIDIA GeForce Experience (GFE) as the host server.

---

## Features

### Streaming
- **Video codecs:** H.264, HEVC (H.265), and AV1 — automatically selected based on what your Apple TV hardware can decode
- **Resolutions:** 720p, 1080p, 1440p (QHD), and 4K
- **Frame rates:** 30, 60, and 120 fps
- **Bitrates:** 5 Mbps to 500 Mbps, adjustable in-app
- **HDR support** for HEVC and AV1 streams on capable hardware
- **Frame pacing** for smoother playback
- **Performance stats overlay** showing live bitrate, frame rate, and latency during a stream

### Audio
- Stereo, 5.1, and 7.1 surround sound
- Optional simultaneous audio playback on the host PC

### Controllers & Input
- Full MFi and Xbox/PlayStation controller support
- Multi-controller support (up to 4 gamepads)
- Optional A/B and X/Y button swap for non-Xbox layouts
- Optimize Game Settings mode to adjust host display and audio for streaming

### Host Management
- **Automatic discovery** of Sunshine and GFE hosts on the local network via Bonjour/mDNS
- **Manual host entry** by IP address or hostname
- **Wake on LAN** to wake sleeping PCs from the couch
- Persistent host list with per-host pairing and certificate storage

### Pairing
- Secure PIN-based pairing using the Limelight cryptographic exchange
- Mutual TLS authentication with pinned server certificates
- Detects and handles unpairing from the PC side

### App Grid
- Full app and game library fetched from the host, sorted by most recently launched
- **Pin to Top** — long-press any game to pin it to the front of the shelf; pinned games sort alphabetically before all others
- Box art downloaded and cached automatically
- "Now Playing" badge on the currently running game
- Blurred box art background when no hero art is available
- Quit-and-switch confirmation when launching a different game while one is running

### SteamGridDB Artwork
When a [SteamGridDB](https://www.steamgriddb.com) API key is configured, Aurora fetches high-quality artwork from the community database. This is especially useful for non-Steam games, emulators, and custom shortcuts where the host has no cover art.

- **Hero art** — full-screen background image that fades in behind the shelf when a game is focused
- **Logo art** — transparent PNG logo displayed above the shelf in place of the game title
- **Animated artwork** — GIF/animated images are supported for both hero and logo art
- **Per-game artwork cycling** — long-press any game to open the Artwork menu:
  - **Try Different Cover Art** — cycles to the next SteamGridDB result for the box art
  - **Try Different Background** — cycles to the next hero image
  - **Try Different Logo** — cycles to the next logo image
  - **Use Local Artwork** — blocks SteamGridDB for this game and falls back to the host-provided box art immediately
  - **Restore SteamGridDB Artwork** — re-enables SteamGridDB for a game after using local artwork

To get a free API key, visit [steamgriddb.com/profile/preferences/api](https://www.steamgriddb.com/profile/preferences/api).

### Settings
- All settings are in-app under the gear icon — no system Settings app required
- Video, audio, controller, artwork, and debug sections

---

## Requirements

- Apple TV HD or Apple TV 4K (tvOS 17 or later)
- A PC running [Sunshine](https://github.com/LizardByte/Sunshine) or NVIDIA GeForce Experience on the same local network

---

## Building

1. Install Xcode from the [Mac App Store](https://apps.apple.com/us/app/xcode/id497799835)
2. Clone the repo with submodules:
   ```
   git clone --recursive https://github.com/coderwg/aurora-tvos.git
   ```
   If you already cloned without `--recursive`:
   ```
   git submodule update --init --recursive
   ```
3. Open `Aurora.xcodeproj` in Xcode
4. To run on a real Apple TV, update the signing settings:
   - Select the project in the sidebar → **Signing & Capabilities** → **Aurora TV** target
   - Set your **Team** and change the **Bundle Identifier** to something unique (repeat for the **Aurora Top Shelf Extension** target)
   - Select your Apple TV as the run destination and press **Run**

---

## Credits

Aurora is a fork of [Moonlight for iOS/tvOS](https://github.com/moonlight-stream/moonlight-ios), created by [Cameron Gutman](https://github.com/cgutman) and the Moonlight contributors. The underlying streaming engine is [moonlight-common-c](https://github.com/moonlight-stream/moonlight-common-c).

Aurora removes the iOS/iPadOS target and replaces the tvOS interface with a fully native SwiftUI app purpose-built for the Apple TV experience.

The Moonlight project is licensed under the [GNU General Public License v3](https://www.gnu.org/licenses/gpl-3.0.html). Aurora inherits this license.

### Related Projects
- [Moonlight iOS/tvOS](https://github.com/moonlight-stream/moonlight-ios) — the upstream project this is forked from
- [Sunshine](https://github.com/LizardByte/Sunshine) — open-source GameStream host server (recommended)
- [Moonlight PC](https://github.com/moonlight-stream/moonlight-qt) — desktop client
- [Moonlight Android](https://github.com/moonlight-stream/moonlight-android) — Android client
