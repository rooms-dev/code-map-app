# Code Map

Code Map is the desktop app of [Code Contractor](https://code-contractor.ai). It maps pull requests and whole repositories on your computer, with the Claude Code you already use.

This repository only holds the app's releases. To use the app you need a Code Contractor account in an organization that has Code Maps turned on; the app asks you to sign in with it.

## Download

Get the latest version from the [Releases](https://github.com/rooms-dev/code-map-app/releases/latest) page, or from **Code Map App** in the Code Contractor Dashboard.

| Platform | File |
|---|---|
| macOS (Apple silicon) | [code-map-mac-arm64.zip](https://github.com/rooms-dev/code-map-app/releases/latest/download/code-map-mac-arm64.zip) |
| macOS (Intel) | [code-map-mac-x64.zip](https://github.com/rooms-dev/code-map-app/releases/latest/download/code-map-mac-x64.zip) |
| Windows (x64) | [code-map-windows-x64-setup.exe](https://github.com/rooms-dev/code-map-app/releases/latest/download/code-map-windows-x64-setup.exe) |
| Linux (x64) | [code-map-linux-x64.AppImage](https://github.com/rooms-dev/code-map-app/releases/latest/download/code-map-linux-x64.AppImage) |

Each release lists the files' SHA-256 in `SHA256SUMS`.

## Opening the app

The app is not signed yet.

- **macOS**: unzip, move `code-map.app` to Applications, and clear the quarantine flag once: `xattr -dr com.apple.quarantine /Applications/code-map.app`. Or open it, then choose **Open Anyway** under System Settings → Privacy & Security.
- **Windows**: if “Windows protected your PC” appears, choose **More info**, then **Run anyway**.
- **Linux**: `chmod +x code-map-linux-x64.AppImage && ./code-map-linux-x64.AppImage`. It needs FUSE 2 (on Ubuntu, `libfuse2t64`).

Install and sign in to [Claude Code](https://claude.com/claude-code) before you start.
