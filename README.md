# Media Now Playing

`Media Now Playing` is a Windows desktop app for showing currently playing media in OBS through a local browser source.

It started as a Spotify-focused overlay tool, but it now supports broader Windows media session tracking, customizable overlay layouts, theming, cover art styling, and in-app updates.

## What It Does

- Creates a local OBS browser source URL for your now playing card
- Tracks current media through Windows media sessions
- Supports Spotify, YouTube, YouTube Music, Twitch, browsers, and other compatible media sources
- Shows title, artist, cover art, progress, playback state, source label, and watermark
- Lets you fully customize layout, colors, visibility, and timing behavior
- Includes a live preview and popout preview window
- Supports in-app updating from GitHub releases

## Main Features

### Overlay and Layout

- Multiple layout modes and custom layout editing
- Show or hide:
  - cover art
  - media source
  - playback state
  - progress bar
  - time labels
  - watermark
  - title
  - artist
- Title and artist display modes:
  - separate lines
  - `Title - Artist`
  - `Artist - Title`
- Title scrolling modes:
  - bounce
  - loop
  - off
- Text alignment:
  - left
  - center
  - right
- Background modes:
  - full card
  - text only
  - none

### Cover Art

- Cover shapes:
  - square
  - rounded
  - circle
- Optional spinning cover art
- Configurable spin speed and direction
- Optional blurred cover background

### Visibility Rules

- Hide when paused
- Show only for the first `X` seconds after a track starts
- Show only for the last `Y` seconds before a track ends

### Styling

- Built-in presets
- Custom presets
- Auto-theme from album art
- Custom gradient, bar, and text colors
- Adjustable opacity
- Dark mode for the app UI

### Source Handling

- Source mode:
  - auto
  - Spotify
  - YouTube
- Custom source priority order
- Text filter modes:
  - off
  - slurs only
  - slurs + swears

### Troubleshooting and Logs

- Built-in log window
- Logging levels:
  - errors only
  - standard
  - verbose
- Media session debug view
- Debug bundle export

## How It Works With OBS

The app hosts a local overlay page and gives you a browser source URL like:

```text
http://127.0.0.1:17342/media-card.html
```

Add that URL to an OBS Browser Source to show the overlay.

Legacy compatibility is also preserved for older setups that still use:

```text
http://127.0.0.1:17342/spotify-card.html
```

## Installation

### Simple install

1. Download the latest `MediaNowPlayingApp.exe` from GitHub Releases.
2. Put it in its own folder.
3. Run it.
4. Copy the OBS browser source URL from the app.

### Data storage

The app stores writable data in:

```text
%LocalAppData%\MediaNowPlayingApp\
```

This includes:

- `settings.json`
- `theme.json`
- `nowplaying.json`
- `window-state.json`
- logs
- cover files
- update staging files
- migration/normalization state

If an older portable install stored files beside the EXE, the app will try to copy them forward automatically.

## Updating

### Supported updater path

The current app supports in-app updates from GitHub releases.

When an update is accepted, the app will:

1. Download the new EXE
2. Close the current app
3. Replace the current EXE in place
4. Relaunch from the same location

The updater keeps only a small rollback window in:

```text
%LocalAppData%\MediaNowPlayingApp\updates\
```

Older staged updates are automatically cleaned up so the folder does not grow forever.

### Important compatibility note

Pre-rebrand `SpotifyNowPlayingApp` era builds are not guaranteed to update cleanly through the in-app updater.

If someone is coming from a very old build:

- a clean reinstall is recommended
- newer post-rebrand builds are the intended target for in-app updates

## Compatibility and File Safety

The app is designed to preserve old content while moving files toward the current format.

Current safeguards include:

- one-time migration support
- every-launch startup normalization
- settings schema version tracking
- preservation of unknown settings fields where possible
- backup copies before normalization rewrites

This improves both forward and limited backward compatibility, but it is still best-effort. Extremely old builds may still need a clean reinstall.

## Requirements

- Windows 10 or Windows 11
- OBS Studio for the browser source use case
- WebView2 runtime for embedded preview features

The published release build is self-contained, so users do not need to install .NET separately.

## Build From Source

From the project folder:

```powershell
dotnet build SpotifyNowPlayingApp.csproj -c Debug
```

Release publish:

```powershell
dotnet publish SpotifyNowPlayingApp.csproj -c Release -r win-x64
```

## Release Process

A release helper and checklist are included in the repo:

- [RELEASE_PROCESS.md](RELEASE_PROCESS.md)
- [release.ps1](release.ps1)

Typical release flow:

```powershell
.\release.ps1 -Version X.Y.Z -ReleaseNotes "Describe what changed here."
dotnet publish SpotifyNowPlayingApp.csproj -c Release -r win-x64
& "C:\Program Files\GitHub CLI\gh.exe" release create vX.Y.Z "bin\Release\net8.0-windows10.0.19041.0\win-x64\publish\MediaNowPlayingApp.exe" --repo fittercleric60/MediaNowPlaying --title "MediaNowPlayingApp X.Y.Z" --notes "Describe what changed here."
```

## Current Project Direction

This app is now being treated as a free utility and portfolio project rather than a licensed paid app.

The public-facing license UI has been removed, while the app remains focused on:

- accessibility
- easy setup
- safe updates
- compatibility over time

## Donations

If someone wants to support development, the app includes a donation link to:

```text
https://paypal.me/FitterclericStreams
```

## Known Limitations

- Media tracking still depends primarily on Windows media session behavior, which can be inconsistent across apps
- Very old builds may require manual reinstall instead of in-app update
- Updating in place works best from normal user-writable folders, not protected install locations like `Program Files`
- Backward compatibility is improved, but not guaranteed across every possible historical build

## Repo Notes

The repo still uses the historical project filename:

```text
SpotifyNowPlayingApp.csproj
```

but the built app identity and output are:

```text
MediaNowPlayingApp.exe
```
