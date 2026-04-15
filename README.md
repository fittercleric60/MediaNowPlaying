# Media Now Playing

`Media Now Playing` is a Windows app for showing currently playing media in OBS through a local browser source.

It began as a Spotify-focused overlay tool, but it now supports broader Windows media session tracking and a much more customizable overlay.

## Features

- Local OBS browser source URL
- Tracks current media from supported Windows media sessions
- Works well with Spotify, YouTube, YouTube Music, browsers, Twitch, and other compatible sources
- Customizable overlay layout, colors, and visibility
- Cover art styling:
  - square
  - rounded
  - circle
  - optional spinning cover art
- Title and artist display modes:
  - separate lines
  - `Title - Artist`
  - `Artist - Title`
- Title scrolling modes:
  - bounce
  - loop
  - off
- Optional blurred cover background
- Auto-theme from album art
- Hide when paused
- Optional timed display windows:
  - show for the first `X` seconds after a track starts
  - show for the last `Y` seconds before a track ends
- Live preview and popout preview
- In-app updates

## OBS Setup

The app gives you a local browser source URL like:

```text
http://127.0.0.1:17342/media-card.html
```

Add that URL to an OBS Browser Source to use the overlay.

Older setups that still use the legacy route should also continue to work:

```text
http://127.0.0.1:17342/spotify-card.html
```

## Installation

1. Download the latest `MediaNowPlayingApp.exe` from the GitHub Releases page.
2. Put it in its own folder.
3. Run it.
4. Copy the OBS browser source URL from the app.

## Updating

The app supports built-in updates from GitHub releases.

When an update is accepted, the app will:

1. Download the new version
2. Close the current app
3. Replace the current EXE in place
4. Relaunch from the same location

If you are coming from a very old pre-rebrand build, a clean reinstall may still be the safer option.

## Requirements

- Windows 10 or Windows 11
- OBS Studio if you want to use the browser source overlay
- WebView2 runtime for embedded preview features

## Donations

If you want to support development:

```text
https://paypal.me/FitterclericStreams
```

## Notes

- Media tracking still depends on Windows media session behavior, so reliability can vary a bit depending on the app being tracked.
- Updating in place works best from a normal user-writable folder rather than a protected location like `Program Files`.
