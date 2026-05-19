# Media Now Playing

`Media Now Playing` is a Windows app that shows your current media in OBS through a local browser source.

It started as a Spotify overlay, but it now supports broader Windows media session tracking and a much more flexible overlay builder.

## Features

- Local OBS browser source URL
- Works with Spotify, YouTube, YouTube Music, browsers, Twitch, and other compatible media-session sources
- Auto, Spotify-only, or YouTube-preferred source modes
- Source priority ordering for mixed setups
- Live preview and popout preview window
- In-app updates from GitHub releases

### Overlay customization

- Built-in layout modes:
  - `Classic`
  - `Compact`
- Custom layout editor for:
  - card size
  - element positions
  - element sizes
  - visibility
- Show or hide:
  - cover art
  - media source label
  - playback state
  - progress bar
  - elapsed time
  - remaining time
  - watermark
  - title
  - artist
- Background modes:
  - `Full Card`
  - `Text Only`
  - `None`
- Optional card border toggle
- Optional full-size background behavior when elements are hidden
- Text alignment:
  - `Left`
  - `Center`
  - `Right`
- Adjustable overlay padding

### Title and artist display

- `Separate Lines`
- `Title - Artist`
- `Artist - Title`
- Combined-line vertical positioning:
  - `Title Line`
  - `Centered`
  - `Artist Line`
- Title scroll modes:
  - `Bounce`
  - `Loop`
  - `Off`

### Cover art and styling

- Cover shapes:
  - `Square`
  - `Rounded`
  - `Circle`
- Optional spinning cover art
- Configurable spin speed and direction
- Presets and custom color themes
- Auto-theme from album art
- Adjustable opacity
- Optional blurred cover background
- Adjustable blur strength and background image opacity
- Dark mode for the desktop app

### Visibility timing

- Hide when paused
- Show only for the first `X` seconds after a track starts
- Show only for the last `Y` seconds before a track ends

### Logging and troubleshooting

- Built-in logs window
- Logging levels:
  - `Errors Only`
  - `Standard`
  - `Verbose`
- Media session debug views
- Debug bundle export
- Reconnect button for media-session refresh
- Built-in troubleshooting help

## OBS Setup

The app gives you a local browser source URL like:

```text
http://127.0.0.1:17342/media-card.html
```

Add that URL to an OBS Browser Source.

Older setups that still use the legacy route should also continue to work:

```text
http://127.0.0.1:17342/spotify-card.html
```

## Installation

1. Download the latest `MediaNowPlayingApp.exe` from the GitHub Releases page.
2. Put it in its own folder.
3. Run it.
4. Copy the OBS browser source URL from the app into OBS.

## Updating

The app supports built-in updates from GitHub releases.

When an update is accepted, the app will:

1. Download the new version
2. Close the current app
3. Replace the current EXE in place
4. Relaunch from the same location

If you are coming from a much older pre-rebrand build, a clean reinstall may still be the safer option.

## Chat Command Triggers

The app supports a simple local trigger URL for chat bots and automation tools.

Base trigger URL:

```text
http://127.0.0.1:17342/show-nowplaying
```

Optional duration parameter:

```text
http://127.0.0.1:17342/show-nowplaying?duration=10
```

There is also an in-app helper under:

```text
Settings > General > Chat Triggers
```

That section lets you:

- set the default trigger duration
- copy the base trigger URL
- copy an example trigger URL with duration included

### Streamer.bot example

For a simple `!nowplaying` trigger in Streamer.bot:

- Action: `Fetch URL`
- Method: `GET`
- URL: `http://127.0.0.1:17342/show-nowplaying?duration=10`
- `Parse Results as JSON`: off
- `Auto-Type non-JSON Result`: off
- `Variable Name`: leave blank
- `Headers`: leave empty

### Important note for cloud bots

This trigger works best with tools running on the same PC as the app, such as Streamer.bot.

Cloud-hosted bots like Nightbot cannot normally call `127.0.0.1` on your computer directly, so they would need some kind of relay or local companion tool.

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

- Media tracking still depends on Windows media session behavior, so reliability can vary depending on the app being tracked.
- Updating in place works best from a normal user-writable folder rather than a protected location like `Program Files`.
