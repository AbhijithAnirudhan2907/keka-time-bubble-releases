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
| 2.27.0 | 2026-10-29 | **My Team** tab: press + to search anyone in the company and keep your own list of people with their status today (leave, in / out / not in yet, remote); your team on leave and working remotely, your peers on leave and **peers right now** (in / out). Keka only shares leave and in/out for your team and peers. **Half-day leave** halves the day's target (4h 15m of 8h 30m), the week's target counts it and the week's average weighs it as half a day; a **Half day** button on Today for leave Keka does not have yet. Leaves tab: **Upcoming** holidays (public / optional) and your applied leave. Dashboard settings (look, theme, media, target, WFH templates, My Team) are also saved to disk and come back if lost. WFH is now the second tab; Watch face is the default style. Includes 2.26.2-2.26.4 (Leaves tab, team photos, approved leave in week targets, a celebration when the day is done). |
| 2.26.1 | 2026-10-28 | Media controls: the song's timeline is now a **sound wave** (each song its own shape; the played part lights up). **Scroll on it** to skip 5 s back or forward, or click to jump; scroll on the speaker for the volume. While you scroll the wave swells and a label shows the time or level, and for the volume the wave turns into a rising ramp. **Dynamic work from home**: a new Dynamic template starts the request at the moment you apply and makes it as long as the time still needed for your Daily target, rounded up to the next half hour (1h 20m short -> 1h 30m, 1h 45m -> 2 hours); any template can be made dynamic in its editor (Starts: When I apply; For: Time still needed). |
| 2.26.0 | 2026-10-28 | **Media controls** (Windows, on by default; Settings > Widget > Media controls): a player above the widget for whatever is playing (YouTube in a browser, Spotify, VLC...), with the artwork, title, artist, progress and previous / play-pause / next (plus shuffle and repeat where the player supports them; click the bar to seek). It shows while something plays or is paused, in frosted glass tinted by the artwork. Layout: **Horizontal** (a bar above the widget, as wide as it) or **Vertical** (a pill to its left, as tall as it); narrow or short widgets keep just the essentials. The speaker button mutes; scroll on it for the volume. **The chameleon opens its mouth**: on a Tongue trip the Golden Chameleon's mouth opens, the tongue flicks out of it to catch the fly, reels the widget in until its mouth reaches the fly, then slurps it up and shuts, all smoothly timed. Themes can say where the mouth is (`art.mouth`). |
| 2.25.0 | 2026-10-28 | **The chameleon changes colour**: Golden Chameleon slowly cycles yellow, green, blue, pink and back, smoothly (the eyes stay blue), and the timer's accent changes with it. Themes can now ask for a colour cycle (`art.hue`: seconds, plus ovals that keep their colour). |
| 2.24.1 | 2026-10-28 | Fix: on the Watch face with the LCD readout (custom themes, or a wide font from Settings > Text) the time spilled out, the date wrapped and the IN / BREAK / DONE / LEFT cells overlapped. The readout now shrinks as a whole to fit the theme's slot. |
| 2.24.0 | 2026-10-28 | **16 new fonts** for the widget's times (Settings > Widget > Text): signature and brush scripts (Great Vibes, Alex Brush, Allura, Sacramento, Parisienne, Pinyon, Mr Dafoe, Kaushan, Yellowtail, Pacifico, Dancing, Satisfy, Caveat), Lobster, a Gothic blackletter and tall Bebas; built into the app, so they work on every PC. **Blur** slider for the frosted widget, and the widget now darkens itself over a bright (white) background so the times stay readable. |
| 2.23.0 | 2026-10-28 | **Frosted widget** (Windows): with See-through black on, the desktop behind the widget is blurred, like frosted glass (Settings > Widget > Background & outline > Blur behind, on by default). The app copies the screen behind the widget a few times a second, so while it is on the widget does not appear in screenshots or screen sharing. |
| 2.22.3 | 2026-10-28 | **See-through black** (Settings > Widget > Background & outline, on by default): the widget has no dark card behind it, and the black in the theme picture lets the desktop show through (animated pictures keep moving). Switch it off to get the solid card back. |
| 2.22.2 | 2026-10-28 | Easier to read: the Glass dashboard is now nearly solid by default, so busy windows behind it no longer show through the text. Settings > Dashboard look > **Glass opacity**: See-through, Frosted or Solid. |
| 2.22.1 | 2026-10-28 | Removed the system blur added in 2.22.0: on newer Windows 11 builds it drew a black box over the whole widget window (around and between the dashboard and the widget) instead of blurring. The Glass look is back to the see-through tint of 2.21.0. |
| 2.21.0 | 2026-10-28 | **Redesigned dashboard.** A slim top bar replaces the sidebar: pill tabs Today, Week, WFH and Themes, a status chip, refresh and a Settings gear, so pages get the full width. Settings is grouped into Widget, Dashboard look, Work day, Keka account and App. One design system (spacing, corners, type, colours) for Glass and Classic, readable with light themes too; big light numbers without the seconds clutter, a clearer week chart. **Time on the taskbar**: the effective time written next to the clock (Windows; green when the target is met, grey when out). Fix: Sign in to Keka on Today no longer also opens the browser. |
| 2.20.0 | 2026-10-28 | New **Glass** look (Settings > Look): a smoky, see-through dashboard with no shadow, pill navigation with a cream active pill, light big numbers and cream buttons; Classic stays one click away. **Widget** settings: turn its background and shadow off, and add a dark or light outline so the times read on any picture or desktop. **Text** settings: font, weight, italic and colour for the big time, the other times and the labels, on every style. The Watch face shows the time still needed: "1h 02m to go · done 7:31p" under the bar, and a **LEFT** cell in place of WEEK on themes with the LCD readout (Thor, Loki, Moon Knight…). It follows Settings > Daily target (e.g. 8h 30m). Fix: theme pictures over ~1.5 MB (Joker, Moon Knight) did not show, because Chromium drops CSS URLs over 2M characters; big pictures now go to CSS as blob: URLs. Themes: a **Refresh** button fetches the newest themes from the library (the list also refreshes itself after 10 minutes, and downloads skip the CDN cache). |
| 2.19.0 | 2026-10-27 | Three new ways to travel. **Crescent dart** (Moon Knight): rain sweeps over the screen, a silver crescent dart spins out and sticks in the spot with a cold flash, and the bubble glides after it under a streaming cape. **Wild card** (Joker): the bubble bursts into a deck of cards that fly to the spot, swirl round it and deal the bubble back out with a "HA HA HA". **Map** (Dora): a dotted trail draws out to a red X, the bubble hops along it and lands in a burst of stars. New themes: Moon Knight (pouring rain, glowing eyes, lightning in the clouds), Joker (a failing cell light, dust in the beam) and Dora & Boots (they blink). All three are in Make your own theme too. **Work from home**: a new page with your own hourly request templates (name, start time, length, note); Apply today checks Keka (working day, no leave, no request yet), shows exactly what will be sent and sends it only when you confirm; tick **Time still needed for 8h 30m** to make the request as long as today still lacks. **Daily target** (Settings): count down to Keka's shift length, or a fixed 8h, 8h 30m or 9h; every style, the taskbar readout and Done at follow it (leave days keep Keka's figure). The templates are also in the tray menu (Work from home today). **No extension needed**: Settings > Keka sign-in opens Keka in a window of the app; sign in once and it stays signed in, hidden, renewing its own login (the Chrome extension still works too). Fix: pressing Esc while aiming Miss Minutes no longer leaves the travel overlay stuck. |
| 2.18.1 | 2026-10-22 | Fix: during Miss Minutes' travel (and Doctor Strange's portal) the bubble could stay visible before the door opened, because Windows does not redraw the bubble while the travel overlay covers it. The bubble window is now hidden while it travels and shown again as it comes out of the door. |
| 2.18.0 | 2026-10-22 | Smoother travel. **Miss Minutes** (Loki): the bubble fades away as she pops up, she rolls with a gentle bob and leans into the start, rocks to a stop, and the TVA door opens while she is still arriving; the bubble grows out of the door once it is fully open, she gives you a look and a blink, then vanishes in a smaller, single-colour star blink (no sparkle when she appears). The whole trip is about a second shorter. **Every travel**: animations run at the same speed on any monitor refresh rate, the screen dim no longer lags or flickers round the bubble's edge, Doctor Strange's portal exit grows the bubble back smoothly, and the overlay does much less drawing per frame. |
| 2.17.0 | 2026-10-22 | Loki's travel is now **Miss Minutes**: she pops up beside the bubble, rolls like a wheel to the spot you click (her eyes look around and blink), opens an orange TVA door there, and the bubble steps out of it once it is fully open; then she vanishes in a star blink and the door closes. |
| 2.16.0 | 2026-10-21 | Two new ways to travel. **Mjölnir**: Thor throws his hammer wrapped in lightning, it strikes the spot with a flash and a thunder ring, and the bubble glides after it (new Thor theme, with flickering lightning). **Time threads**: green time-threads weave out to the spot, the bubble glides along them and steps out through a golden TVA door (new Loki theme: the throne, the Sacred Timeline and the TVA door fading into one another). Both are in Make your own theme too. Every travel moves more smoothly, and watch-face text stays crisp on light pictures. |
| 2.15.0 | 2026-10-21 | Spider-Man's web is now a braided rope of silk fibres that frays into a fan where it sticks. New travel: **Tongue**, where a fly buzzes at the cursor and the chameleon's sticky tongue catches it and reels the bubble in (the new Golden Chameleon theme uses it; also in Make your own theme). |
| 2.14.0 | 2026-10-21 | **Travel** for the Marvel themes: click the new button on the bubble, then any spot on the screen. Spider-Man web-swings there, Doctor Strange opens a sling-ring portal, Iron Man flies on repulsors (Update those themes in **Themes**). Make your own theme gets a Travel choice. |
| 2.13.0 | 2026-10-21 | **Make your own theme**: in **Themes**, pick a picture from your computer, choose a watch face or round shape, drag to place the time, and save. It stays on your computer. Animated WebP pictures play (the Spider-Man themes now blink). |
| 2.12.0 | 2026-10-21 | A dot on **Updates** (and on the bubble's gear) shows when a new version is out. Themes can have a tune: the Spider-Man themes play the Homecoming theme from the ▶ button next to the gear (Get the update for those themes in **Themes**). |
| 2.11.0 | 2026-10-21 | Theme library: open **Themes** in the dashboard to browse and search themes and **Get** the ones you want (only those are downloaded; gallery at abhijithanirudhan2907.github.io/keka-time-bubble-themes). Spider-Man Casio gets an LCD readout with in, break, done and week. |
| 2.10.0 | 2026-10-20 | Themes: pick one under Settings › Theme (Midnight and Paper included), plus a new tall Watch face style. Optional artwork theme packs can be added per person. |
| 2.9.0 | 2026-10-16 | Seven new watch-style looks: Flight, Gauge, Week bars, Countdown, Timeline, Sunset and Meter. |
| 2.8.5 | 2026-10-16 | Previous / next day arrows (and arrow keys) on a day opened from This week, with Today to go back. Agenda style lists every work and break stretch and scrolls. |
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
