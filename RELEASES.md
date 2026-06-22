# Releases

## v0.7.0

A "Now tray" that keeps the current line under the video — even when the
transcript is scrolled away.

### Added

- **Now tray** — a frosted caption bar pinned below the player showing the
  current line as the video plays: timestamp · original · Chinese. It is driven
  by the follow view, so it keeps tracking playback even when you've scrolled
  the transcript elsewhere.
- **Replay current sentence** — a one-tap button on the tray jumps back to the
  start of the current line and plays it again.
- **Toggle in Settings → Now tray** — on by default; turn it off for a bare
  player.

### Install

This release supports [BRAT](https://github.com/TfTHacker/obsidian42-brat). Add
`https://github.com/leoyang1984/obsidian-lumen-youtube-public` as a beta plugin,
or download `main.js`, `manifest.json`, and `styles.css` from the release and
place them in `<your-vault>/.obsidian/plugins/lumen-youtube/`.

## v0.6.0

Transcript controls stay put, plus a status bar and an optional retro skin.

### Fixed

- **Pinned controls no longer disappear** — the mode toggle and note-capture bar
  stay visible while the transcript scrolls during playback and when the pane is
  resized. The view is now split into a fixed control area and a single
  scrolling transcript, so the controls can't be dragged off the top.

### Added

- **Bottom status bar** — shows the current mode, follow state, playback time,
  and line position, pinned below the transcript.
- **Pill-style mode toggle** — original / Chinese / bilingual rendered as
  rounded segmented buttons.
- **Optional "Retro terminal" skin** (Settings → transcript skin) — a
  skeuomorphic look applied to both the transcript view and the settings tab.
  The default skin remains theme-aware and is unchanged.

### Install

This release supports [BRAT](https://github.com/TfTHacker/obsidian42-brat). Add
`https://github.com/leoyang1984/obsidian-lumen-youtube-public` as a beta plugin,
or download `main.js`, `manifest.json`, and `styles.css` from the release and
place them in `<your-vault>/.obsidian/plugins/lumen-youtube/`.

## v0.5.0

Player and note-capture polish.

### Changed

- **Note capture moved up** — the timestamped-note input now sits directly
  below the player header, above the transcript, so it stays visible at any
  pane height (previously it was pinned to the bottom and could fall out of
  view in a stacked layout).
- **Player fills its pane** — the video now resizes with the pane on both width
  and height instead of staying a fixed height; the embedded player letterboxes
  so any pane shape looks right.

### Install

This release supports [BRAT](https://github.com/TfTHacker/obsidian42-brat). Add
`https://github.com/leoyang1984/obsidian-lumen-youtube-public` as a beta plugin,
or download `main.js`, `manifest.json`, and `styles.css` from the release and
place them in `<your-vault>/.obsidian/plugins/lumen-youtube/`.

## v0.4.0

In-Obsidian player with a synced transcript, plus timestamped notes.

### Added

- **Open player with synced transcript** (desktop) — resolves the clipping's
  video, opens the player and transcript side by side, and starts syncing. If the
  clipping has no transcript yet, it auto-fetches (and translates, only when
  translation is configured) first.
- **Line-level follow** — the current line highlights, past lines dim, and the
  list autoscrolls to keep it centered. **Click any line to seek** the video.
- **Original / Chinese / bilingual** display toggle in the player header;
  bilingual shows both languages per line and is the default when a CN file
  exists.
- **Smart autoscroll** — scrolling the transcript manually pauses follow; a
  "↓ 回到当前" button (or clicking a line) re-engages.
- **Timestamped notes** — a capture bar (or the **Add note at current time**
  command) freezes the current playback time, pauses the video, and appends a
  clickable `- [MM:SS](…) note` line to the clipping's `## Notes` section.
- **Player settings** — default mode, autoscroll on/off, highlight style
  (filled / side bar / accent text), and layout (side by side / stacked).

### Notes

- The player is **desktop only**; the command is hidden on mobile. Transcript
  fetching and translation remain cross-platform.
- Videos that disallow embedding open in your browser instead.

### Install

This release supports [BRAT](https://github.com/TfTHacker/obsidian42-brat). Add
`https://github.com/leoyang1984/obsidian-lumen-youtube-public` as a beta plugin,
or download `main.js`, `manifest.json`, and `styles.css` from the release and
place them in `<your-vault>/.obsidian/plugins/lumen-youtube/`.

## v0.3.0

Usability hardening.

### Added

- **Caption language picker** when several tracks could match the preferred
  language (otherwise the best track is chosen automatically; manual captions are
  preferred over auto-generated).
- **Smart existing-file handling** — a file for the same `videoId` is recognized
  even if the clipping's title (and desired filename) changed, so renaming never
  leaves an orphan. Originals and CN files are tracked independently and reused,
  not clobbered, unless overwrite is on.
- **Graded errors** — "no captions" vs "YouTube blocked unauthenticated access"
  vs other errors give distinct, actionable notices.
- **Auto-generated marker** — the chosen track's kind (manual / auto-generated)
  is recorded in frontmatter and the `## Lumen YouTube` section.
- **Settings validation** — the translation section warns inline when enabled but
  the API key or model is missing.

## v0.2.0

Optional translation.

### Added

- **Chinese translation** into a sibling `… CN.md` file via any OpenAI-compatible
  provider (OpenAI / OpenRouter / DeepSeek / Kimi / Custom). Base URLs prefilled
  but editable; model name free-form.
- Translation is **off by default** and runs only when the API key *and* model
  are set — no silent API calls or costs. Every timestamp line is preserved.
- Chunked translation (default 120 lines/request); a chunk failure aborts
  cleanly, keeps the original transcript, and never writes a partial CN file.

## v0.1.0

Initial public plugin release.

### Added

- Identifies a YouTube URL in the active note (frontmatter `source` / `url` /
  `link`, then a body scan; supports `watch`, `youtu.be`, `shorts`, `live`,
  `embed`, and URLs inside Markdown image/link syntax).
- Fetches existing captions via YouTube's InnerTube player API through Obsidian's
  `requestUrl`.
- Writes an original-transcript Markdown file to the output folder
  (`{title} - {videoId}.md`) with clickable per-line timestamps.
- Writes status and links back into the source note (frontmatter +
  `## Lumen YouTube` section); re-running is idempotent.
- Reports `no_caption` / `missing_url` / `error` cleanly.
- Lightweight UI localization following the Obsidian language.

### Known Notes

- The plugin reads captions that already exist on YouTube; it does not transcribe
  audio. Some videos expose no caption tracks without a logged-in session.
- This repository does not publish source code.
