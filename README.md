# Lumen YouTube

Lumen YouTube is an Obsidian plugin that turns YouTube clippings into clean
transcript Markdown — original text plus an optional Chinese translation — and,
since v0.4, plays the video inside Obsidian with the transcript following along.

It identifies the YouTube URL in a clipping note, fetches the video's existing
captions, and writes a tidy, timestamped transcript into your vault for
[Lumen](https://github.com/leoyang1984) (or any other workflow) to digest.

## What It Does

- **Find the video automatically** — reads the YouTube URL from a note's
  frontmatter (`source` / `url` / `link`) or body. Supports `watch`, `youtu.be`,
  `shorts`, `live`, and `embed` links, including ones inside Markdown syntax.
- **Fetch existing captions** via YouTube's InnerTube player API — no Whisper, no
  audio download, no video download. Manual captions are preferred over
  auto-generated ones, and a picker appears when several tracks could match.
- **Write a clean transcript** to your output folder as `{title} - {videoId}.md`,
  with clickable per-line timestamps under a stable `## Transcript` heading.
- **Optional Chinese translation** into a sibling `… CN.md` file via any
  OpenAI-compatible provider (**OpenAI / OpenRouter / DeepSeek / Kimi / Custom**).
  Off by default; runs only when an API key **and** model are set, so there are
  no silent API calls or costs. Every timestamp line is preserved.
- **Link back to the clipping** — writes status frontmatter
  (`transcript_status`, `transcript_file`, `transcript_cn_file`, …) and a
  `## Lumen YouTube` section into the source note. Re-running is idempotent.
- **Play inside Obsidian** (desktop, v0.4) — open the clipping's video next to
  its transcript, with the current line highlighting and autoscrolling in sync.
  Click any line to seek; toggle original / Chinese / bilingual display.
- **Timestamped notes** — freeze the current playback time and append a clickable
  `- [MM:SS](…) note` line to the clipping's `## Notes` section.
- **Localized UI** — English or Chinese, following Obsidian's configured language.

## What It Is Not

Lumen YouTube does **not** summarize, download video or audio, transcribe with
Whisper, or talk to the Lumen plugin directly. It produces text assets from
captions that already exist on YouTube; the player is a read/review surface
streamed live from YouTube.

```text
Web Clipper note → Lumen YouTube → Transcript Markdown (+ optional CN) → Lumen Summary
                                 ↘ Player + synced transcript (v0.4, desktop)
```

## Installation

Lumen YouTube is not yet in the Obsidian community plugin store.

### Via BRAT (recommended)

[BRAT](https://github.com/TfTHacker/obsidian42-brat) installs the plugin and
keeps it auto-updated from this repository.

1. Install **BRAT** from Community Plugins and enable it.
2. Run the command **BRAT: Add a beta plugin for testing**.
3. Paste this repository URL:

   ```text
   https://github.com/leoyang1984/obsidian-lumen-youtube-public
   ```

4. BRAT downloads the latest release into your vault.
5. Enable **Lumen YouTube** in Community Plugins, then open its settings.

### Manual install

1. Download `main.js`, `manifest.json`, and `styles.css` from the
   [latest release](https://github.com/leoyang1984/obsidian-lumen-youtube-public/releases/latest).
2. Put all three files in `<your-vault>/.obsidian/plugins/lumen-youtube/`.
3. Reload Obsidian and enable **Lumen YouTube** in Community Plugins.

## Usage

1. Open a clipping note that contains a YouTube URL.
2. Click the ribbon icon **Process YouTube transcript**, or run a command:
   - **Lumen YouTube: Process current note** — fetch (and translate, if enabled).
   - **Lumen YouTube: Fetch transcript only** — never translates.
   - **Lumen YouTube: Translate current transcript** — translate an already-open
     transcript file into a CN file.
   - **Lumen YouTube: Open player with synced transcript** — desktop only.
   - **Lumen YouTube: Add note at current time** — desktop only.

Optional translation is configured in settings: pick a provider, paste an API
key, and set a model name. Base URLs are prefilled but editable.

## Output Format

A transcript file with clickable, per-line timestamps:

```md
---
source: "https://www.youtube.com/watch?v=VIDEOID"
video_id: VIDEOID
caption_kind: manual
generator: Lumen YouTube
---

# Video title

## Transcript

- [00:00](https://www.youtube.com/watch?v=VIDEOID&t=0s) First line of dialogue
- [00:04](https://www.youtube.com/watch?v=VIDEOID&t=4s) Second line of dialogue
```

With translation enabled, a sibling `… CN.md` file mirrors the timestamps under
a `## 中文翻译` heading so the player can switch languages line-for-line.

## Known Limitation

YouTube has been tightening unauthenticated caption access. Most public videos
work, but some (often newer or auth-gated ones) expose **no caption tracks**
without a logged-in session — for those the plugin correctly reports
`no_caption`. This is a YouTube-side constraint, not a bug in the fetch logic.

The in-Obsidian player is **desktop only** (the YouTube embed and custom views
are impractical on mobile); transcript fetching and translation stay
cross-platform. Videos that disallow embedding open in your browser instead.

## Source Code

This public repository is used for plugin distribution and release notes only.
The compiled `main.js` is published here for installation; the TypeScript source
is not published.

## Credits

The InnerTube caption-fetching strategy is adapted from
[ljantzen/obsidian-youtube-transcript](https://github.com/ljantzen/obsidian-youtube-transcript)
(MIT).

## License

Lumen YouTube is available for **non-commercial use only**. See
[LICENSE.md](LICENSE.md).

Commercial use, resale, SaaS hosting, paid-client use, marketplace
redistribution, and commercial bundling require prior written permission.
