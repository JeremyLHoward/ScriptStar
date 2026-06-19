# Changelog

All notable changes to ScriptStar are documented in this file.

## [1.2.1] — 2026-06-19

### Fixed
- Fixed the **Install New Script** dialog on Windows. The file-type filter previously showed raw function source instead of script types and listed no files; it now offers a **Script Files** filter (`.jsx`, `.js`, `.jsxbin`, `.txt`, `.vbs`, `.scpt`) plus an **All Files** option.

-------

## [1.2.0] — 2026-06-18

### Added
- **Windows support.** ScriptStar now runs on Windows in addition to macOS.
- Added support for running **VBScript (`.vbs`)** scripts on Windows. VBScript files can now be installed and run alongside JavaScript and AppleScript files.

### Changed
- Script execution is now platform-aware: AppleScript (`.scpt`/`.applescript`) runs on macOS only and VBScript (`.vbs`) runs on Windows only. Opening a script on the wrong platform now shows a clear message instead of failing silently.
- Folder deletion now uses a cross-platform recursive delete that behaves identically on macOS and Windows, falling back to the operating system's own removal only for locked or unusual files.
- The **Reveal in Finder** context-menu item now reads **Reveal in Explorer** on Windows.
- Stale-install detection now scans the correct Adobe CEP extension folders on Windows (`%APPDATA%` and the Common Files location) in addition to the macOS locations.

### Fixed
- Fixed a Windows-only bug that prevented the panel from finishing startup (it would hit the boot timeout). Windows file paths weren't being encoded correctly when passed back from InDesign, which stopped the script list from loading. Paths are now encoded properly on both platforms.

-------

## [1.1.0] — 2026-05-11

### Updated
- Renamed the **All Scripts** tab to **User Scripts** to better distinguish user-installed scripts from InDesign’s built-in **App Scripts**.
- Moved **Show/Hide File Icons** from the flyout menu to the preferences dialog.
- Moved **Show/Hide File Extensions** from the flyout menu to the preferences dialog.

### Added
- Added an optional **App Scripts** tab for browsing InDesign application scripts. This tab can be enabled or disabled in the preferences dialog.
- Added a preferences dialog with the following options:
  - **Hide File Extensions**
  - **Hide File Icons**
  - **Show Application Scripts**
  - **Exclude Archived Scripts From Search**
- Added support for excluding archived scripts from search results. When **Exclude Archived Scripts From Search** is enabled, any file inside a folder named **Archive** is omitted from search results in both the **User Scripts** and **App Scripts** tabs.
- Added tooltips for truncated file and folder names so the full name can be viewed in the UI.

### Fixed
- Fixed a row-height rendering issue that caused script and folder rows to “jiggle” by a pixel while resizing the panel.
- Fixed file icons shrinking in search results when long `filename — folder/path` labels were displayed. Icons now retain their full size regardless of label length.

-------

## [1.0.2] — 2026-04-30

### Fixed
- ScriptStar now refuses to start if the install state is broken (most often when stale copies of the extension exist alongside a new install) instead of risking a crash. When this happens, the panel shows a clear error screen with diagnostics and a "Reload Panel" button rather than silently failing or taking InDesign down with it.
- The panel now detects multiple ScriptStar installations on the same machine and surfaces a warning banner explaining how to clean them up.
- Added a 10-second boot watchdog. If ScriptStar can’t finish loading in that window, the panel shows a timeout error rather than leaving the user staring at the loading screen indefinitely.
- Hardened the host-script (`host.jsx`) load step. If the file is missing, unreadable, or doesn’t define the expected functions after evaluation, the panel surfaces a clear error rather than letting the failure cascade.

-------

## [1.0.1] — 2026-04-29

### Added
- Drag-and-drop reordering of scripts in the **Favorites** tab. The order is persisted across sessions.
- Flyout menu option to **show/hide file extensions** for scripts.
- Flyout menu option to **show/hide file icons** for scripts.
- **Keyboard shortcuts** are now displayed alongside scripts that have them assigned.

### Updated
- Read All Script Labels (triggered from the flyout menu) now respects user interface color settings so that headers in the displayed table are readable in all cases.

### Fixed
- Fixed a bug that crashed InDesign when the extension was installed for all users.
