---
name: lemo-opuscar
description: Direct and produce a short film made entirely in code, in one of the styles of the Lemo-Opuscar library (Melissa's locked edition). Use ONLY when the user names Lemo or Lemo-Opuscar (for example "make a Lemo film", "which Lemo styles are there", "change a Lemo style into my own") or types /lemo-opuscar. Do not use it for other requests about videos, films, shorts, promos, explainers or animations, even in a named style; those follow the project's own pipelines. Not for editing, trimming or converting existing video files.
---

# Lemo-Opuscar

The styles, guides and tools live in the Lemo-Opuscar library, from Melissa's fork (github.com/drmelissapresents/lemo-opuscar) at one locked version. This skill hands you over to it.

**The project's own rules come first.** Where the folder's `CLAUDE.md` (Studio's, for example) says something different from the library's guides (approvals, reviews, drafts, spelling, free-space checks, voice), follow the project's rules.

1. **Get the library.** Run `sh "<skill base directory>/scripts/setup.sh"`. On a computer that has the library it only checks it (default `~/lemo-opuscar`) and prints `LIB=<path>` on its last line; it never downloads updates. If the library isn't there yet, it would download it: **ask the user first** (step 2). If it says the library is not on the locked version, tell the user, and run `setup.sh update` only with their OK.
2. **Ask before anything is downloaded or installed.** Before the first download, and before each `setup.sh deps …` tier, `sh tools/fetch.sh …` pack, demo source or package a style needs, tell the user what it is, about how big, and where it comes from (`$LIB/TECHNIQUE.md` §1), and wait for their yes. Only then run it. Report missing system tools (Node, ffmpeg, Python) in your one round of questions; don't install system software yourself. Packages a style needs (its `STYLE.md` lists them) go into the project folder, after the user's OK.
3. **Voice.** Narration uses ElevenLabs by default, through the user's ElevenLabs connector, or a voice track the user supplies. Kokoro (`core/tts/tts.py`, offline) is only for quick tests and drafts. **Never use Microsoft's voices (`core/tts/tts_zh.py`, edge-tts) or any other online text-to-speech** (the Doubao helper in one demo included). The speech check (`core/tts/asr_check.py`) runs offline once its Whisper model is downloaded (ask first, step 2).
4. **Follow the library.** Read `$LIB/AGENTS.md` and do what it says, starting with **Start** (the user's own styles in `~/lemo-my-styles/`, whose README may point to another folder; when they started the skill without writing anything, the language question first, then the ways in): finding the style or making their own, the one round of questions, the treatment, production and delivery. Wherever AGENTS.md says to run `setup.sh deps` or a download, step 2 applies.

What changes in skill mode:

| | |
|---|---|
| Project folder | `<name>/` in the folder the user started from (lowercase letters, digits, hyphens; avoid `#` and `?` in the path), unless the project's rules name another place. Wherever the guides say `films/<name>/`, read this folder |
| Running tools | from `$LIB`, with the project's absolute path: `cd "$LIB" && node core/render/still.mjs "<project>" 1.5 3` |
| Library files in pages | absolute URLs: `/core/lib.js`, `/node_modules/three/…` (the project is served at `/@film/`) |
| Library files in scripts and `build.sh` | `$LIB/…`, with `LIB=<path>` at the top of `build.sh`; never `../..` |
| Demo source | not downloaded. `sh "<skill base directory>/scripts/setup.sh" demo <slug>` (it downloads that style's demo files at the locked version, from Melissa's fork; ask first), only after your `TREATMENT.md` is written, to read its techniques; it is not meant to be rendered. An Edit & Documentary style is the exception: fetch it before the treatment to use the material tools its `STYLE.md` names in `demo/tools/` (`$LIB/AGENTS.md`, "Treatment first") |

Deliver what `$LIB/DIRECTOR.md` §11 lists, in the project folder, and tell the user where it is.
