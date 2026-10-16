# Keka Time Bubble

A small floating bubble that shows your live Keka attendance time (effective hours done, time
left, when you can log off, breaks and swipes) without opening Keka. It sits on top of your other
windows, with a tray / menu-bar readout too.

This repo only hosts the installers and the update file. **Download the latest version from
[Releases → Latest](https://github.com/AbhijithAnirudhan2907/keka-time-bubble-releases/releases/latest).**

## Which file do I download?

| Your computer | Download |
|---|---|
| Windows 10 / 11 | `keka-time-bubble_<version>_x64-setup.exe` |
| Mac with Apple Silicon (M1, M2, M3, M4…) | `keka-time-bubble_<version>_aarch64.dmg` |
| Mac with an Intel processor | `keka-time-bubble_<version>_x64.dmg` |
| Ubuntu / Debian Linux | `keka-time-bubble_<version>_amd64.deb` |
| Any other Linux (64-bit) | `keka-time-bubble_<version>_amd64.AppImage` |
| **Everyone, also** | `keka-time-bubble-extension.zip` (the Chrome extension) |

Not sure which Mac you have? Apple menu → **About This Mac**: "Chip Apple M…" means Apple Silicon,
"Processor Intel…" means Intel.

The `.app.tar.gz` files and `latest.json` are used by the app's automatic updates; you don't need
to download them.

## Supported devices

| Platform | Supported | Notes |
|---|---|---|
| **Windows 10 / 11 (64-bit)** | Yes | Needs Microsoft Edge WebView2, which comes with Windows 11 and current Windows 10. The installer downloads it if it's missing. |
| **macOS 10.15 Catalina or later** | Yes, from v2.8.4 | Apple Silicon and Intel. Lives in the menu bar (no Dock icon). |
| **Linux (64-bit, x86_64)** | Yes, from v2.8.4 | Ubuntu 22.04 or later, Debian 12 or later, or a similarly recent distro. Works best in an X11 session (see below). |
| Windows on ARM | Not officially | The Windows installer may run under emulation; not tested. |
| Linux on ARM (e.g. Raspberry Pi) | No | |
| Android / iPhone | No | |

**Browser:** the app gets your Keka login from a small Chrome extension, so you also need
**Google Chrome, Microsoft Edge, Brave** or another Chromium-based browser. Firefox and Safari
aren't supported.

## Install

### 1. The app

**Windows.** Run the `.exe`. If Windows SmartScreen says it protected your PC, click
**More info → Run anyway** (the installer isn't code-signed). No admin rights are needed.

**macOS.** Open the `.dmg` and drag **Keka Time Bubble** into Applications. The app isn't signed by
Apple, so the first time macOS says it "can't be opened" or "is damaged". Fix it once, either way:
- Right-click the app in Applications → **Open** → **Open**, or
- In Terminal, run:
  ```sh
  xattr -cr "/Applications/Keka Time Bubble.app"
  ```

**Linux.** Install the package:
```sh
sudo apt install ./keka-time-bubble_<version>_amd64.deb
```
or run the AppImage directly, no install needed:
```sh
chmod +x keka-time-bubble_<version>_amd64.AppImage
./keka-time-bubble_<version>_amd64.AppImage
```

### 2. The Chrome extension

1. Unzip `keka-time-bubble-extension.zip`.
2. Open `chrome://extensions` (or `edge://extensions`) and turn on **Developer mode**.
3. Click **Load unpacked** and choose the unzipped folder.
4. Open your Keka attendance page once. The extension connects to the app by itself, and your time
   appears in the bubble within a few seconds.

The extension only talks to the app on your own computer (`127.0.0.1`); your Keka token never
leaves your machine.

## Using it

- **Click** the bubble to open the dashboard (Today, This week, Settings).
- **Drag** to move it; drag the top-left corner to resize.
- The **gear** opens Settings: style, display mode (bubble, tray or both), start at login, updates.
- The **tray / menu-bar icon** has the same options, plus Refresh and Quit.

Your time refreshes every 10 minutes and whenever you open Keka in Chrome.

## Updates

The app updates itself. Use **Updates** in the dashboard, or **Check for updates…** in the tray
menu. When a new version is out, it asks, downloads and installs it. Every update is signed, and
the app rejects anything that isn't.

| Installed from | Automatic updates |
|---|---|
| Windows installer | Yes |
| macOS `.dmg` | Yes |
| Linux AppImage | Yes |
| Linux `.deb` | No: download and install the new `.deb` |

## Linux notes

- **Wayland:** Wayland doesn't let apps position their own windows, so the bubble may not drag or
  remember its spot. Log in with an X11 session (e.g. "Ubuntu on Xorg"), or start the app with
  `GDK_BACKEND=x11`.
- **Tray icon:** needs AppIndicator support. On GNOME that's the *AppIndicator and
  KStatusNotifierItem Support* extension (already included on Ubuntu). If clicking the tray icon
  doesn't bring the bubble back, use the tray menu instead.
- **Round, see-through bubble:** needs a desktop with compositing, which GNOME, KDE, Cinnamon and
  Xfce have by default.

## Release history

| Version | Date | What changed |
|---|---|---|
| 2.8.4 | 2026-10-13 | Percent keeps counting past the target (110%, 120%… for extra time). macOS and Linux versions added on 2026-10-16. |
| 2.8.3 | 2026-10-13 | Layout fixes so times with seconds fit in every style. |
| 2.8.2 | 2026-10-13 | Seconds on every duration and clock time, in every style. |
| 2.8.1 | 2026-10-09 | Seconds in the dashboard and an exact "Done at" time. |
| 2.8.0 | 2026-10-09 | New styles: Battery, Dots, Flip clock and Split. Starburst styles removed. |
| 2.7.1 | 2026-10-09 | Agenda shows each break's length and your total break; Summary shows Done at. |
| 2.7.0 | 2026-10-09 | New dashboard (Today, This week with an hours chart, Settings) and the Summary style. |
| 2.6.0 | 2026-10-09 | New expanded view and settings menu; fixes for missed swipes, weekend targets and offline states. |
| 2.5.0 | 2026-10-09 | Expanded view with streak, Mon–Sun circles and swipes. |
| 2.4.0 | 2026-10-09 | Click a day in This week to see its hours and swipes. |
| 2.3.0 | 2026-10-09 | This week: hours per day, week total and what's left. |
| 2.2.1 | 2026-10-08 | Test release confirming automatic updates. |
| 2.2.0 | 2026-10-08 | First release with automatic updates. |

## Problems?

- **Bubble shows no time:** open your Keka attendance page in Chrome once, and check the extension
  is enabled in `chrome://extensions`.
- **Time looks old:** use **Refresh now** in the tray menu.
- **Anything else:** contact Abhijith.
