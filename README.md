# Code Map

Code Map is the desktop app of [Code Contractor](https://code-contractor.ai). It maps pull requests and whole repositories on your computer, with the Claude Code you already use.

This repository holds the app's releases and the Claude Code plugin `/code-map`. To use either you need a Code Contractor account in an organization on Code Contractor (as a member who can view validations); both ask you to sign in with it. The AI work runs on your computer with your own Claude Code sign-in, so Code Contractor only stores the maps you share.

- [Desktop app](#desktop-app): build maps of projects, pull requests and features, and read them on your computer.
- [Claude Code plugin](#claude-code-plugin-code-map): build the map of a pull request from Claude Code and share it with your team on the web.

## What you need

| Command | What it is for |
|---|---|
| [Claude Code](https://claude.com/claude-code) (`claude`) | Writes the summaries, review notes and explainers. Start it once and sign in. |
| [GitHub CLI](https://cli.github.com) (`gh`) | Reads pull requests and private repositories. Run `gh auth login`. |
| `git` | Reads the code. |
| [Node.js](https://nodejs.org) 22 or later | The plugin only. |

## Desktop app

### Download

Get the latest version from the [Releases](https://github.com/rooms-dev/code-map-app/releases/latest) page, or from **Code Map App** in the Code Contractor Dashboard.

| Platform | File |
|---|---|
| macOS (Apple silicon) | [code-map-mac-arm64.zip](https://github.com/rooms-dev/code-map-app/releases/latest/download/code-map-mac-arm64.zip) |
| macOS (Intel) | [code-map-mac-x64.zip](https://github.com/rooms-dev/code-map-app/releases/latest/download/code-map-mac-x64.zip) |
| Windows (x64) | [code-map-windows-x64-setup.exe](https://github.com/rooms-dev/code-map-app/releases/latest/download/code-map-windows-x64-setup.exe) |
| Linux (x64) | [code-map-linux-x64.AppImage](https://github.com/rooms-dev/code-map-app/releases/latest/download/code-map-linux-x64.AppImage) |

Each release lists the files' SHA-256 in `SHA256SUMS`. The app updates itself when a new version comes out.

### Opening the app

The app is not signed yet.

- **macOS**: unzip, move `code-map.app` to Applications, and clear the quarantine flag once: `xattr -dr com.apple.quarantine /Applications/code-map.app`. Or open it, then choose **Open Anyway** under System Settings → Privacy & Security.
- **Windows**: if “Windows protected your PC” appears, choose **More info**, then **Run anyway**.
- **Linux**: `chmod +x code-map-linux-x64.AppImage && ./code-map-linux-x64.AppImage --no-sandbox`. It needs FUSE 2 (on Ubuntu, `libfuse2t64`). `--no-sandbox` is needed on Ubuntu 23.10 and later, which block the app's sandbox.

When the app starts, choose **Sign in with Code Contractor**. The Dashboard opens in your browser; pick your organization and choose **Sign in**.

### Using the app

Maps are kept per project. Choose **Add project** and pick where the code is:

- **GitHub repository**: `owner/name` or its URL.
- **Local folder**: a clone on this computer, or a folder in it (the map then covers only that folder).
- **WSL** / **SSH host**: a clone in WSL or on a Linux machine you reach with SSH. Only `git` is needed there.

In a project you can build:

- **Whole project**: the map of the whole repository, built when you add the project. **Sync** rebuilds it from the latest commit.
- **Pull request**: pick an open pull request, or type its number or URL. The map opens on an explainer page (why it changes, before and after, the flow, what a reviewer should judge).
- **Find a feature**: ask in words, e.g. “Where are webhooks verified?”. Claude Code finds the files and the map covers just those.
- **Open pull requests**: all open pull requests on one map, so you see which ones touch the same code.

Building a map takes a few minutes. On a map:

- Scroll or pinch to zoom, drag to pan. Click to select, click again to zoom in. `Esc` zooms out one level, `0` shows everything.
- **Ask** (⌘K / Ctrl+K) answers questions about the code. Click lines in the code reader to ask about them.
- **Share with team** (pull request maps) puts the map on the Code Contractor Dashboard and links it from the pull request. Your team can read it, ask questions and leave **Comments** there.
- **Open in editor** opens the file you are reading (local projects).

### Reading maps from Claude Code

In the app's Settings, choose **Connect to Claude Code**. Claude Code can then read your maps (`list_maps`, `get_map`, `get_function`, …), move the app to what it is talking about, read what you selected in the app (“what does this do?”), and build a map of a feature for you.

## Claude Code plugin (`/code-map`)

Build the map of a pull request from Claude Code, without opening the app, and share it so your team reads it on the web.

### Install

In Claude Code:

```
/plugin marketplace add rooms-dev/code-map-app
/plugin install code-map@code-contractor
```

To get a new version: `/plugin marketplace update code-contractor` (or turn on auto-update for the marketplace under `/plugin` → Marketplaces).

### Usage

Run these in a clone of the repository, so a pull request number refers to it:

```
/code-map 1234                                   # map pull request #1234 and share it
/code-map https://github.com/owner/name/pull/1234
/code-map 1234 --ai codex                        # write the notes with Codex instead of Claude Code
/code-map 1234 --lang English                    # language of the notes (default: the language you write in)
/code-map open-prs                               # one map of all open pull requests, shared under the repository
/code-map status | login | logout                # check, sign in, or sign out
```

- The first time, `/code-map` signs you in: a browser tab opens where you pick your organization on Code Contractor.
- Building takes a few minutes and runs in the background. When it ends, Claude Code tells you the URL of the map on the Dashboard; a comment with the link is added to the pull request from your GitHub account.
- Sharing the same pull request again updates that comment.
