# Melissa's edition of Lemo-Opuscar

A fork of [lemomo-ai/lemo-opuscar](https://github.com/lemomo-ai/lemo-opuscar) (MIT), reviewed and locked on 9 Nov 2026 from upstream commit `143f387`. The full safety review is in Melissa's claude-hq repo: `claude-home/lemo-opuscar-review.md`.

## What is changed from upstream

1. **Locked to this fork.** `plugin/skills/lemo-opuscar/scripts/setup.sh` downloads only from `drmelissapresents/lemo-opuscar`, at the tag named in `PIN`, and never updates itself. No environment setting changes the source. `sh setup.sh update` moves an existing library to `PIN`, and is run only with Melissa's OK.
2. **Packages locked.** `requirements*.txt` hold exact versions for Python 3.12 (resolved with `uv pip compile --universal`); Node packages install with `npm ci` from `package-lock.json`.
3. **Asks before every download or install** (`SKILL.md` step 2).
4. **No online voices.** edge-tts is left out of `requirements-voice.txt`, and `SKILL.md` forbids Microsoft's voices and any other online text-to-speech. Narration is ElevenLabs (Melissa's connector) or her own voice track; Kokoro (offline) is for tests and drafts.
5. **Starts only when named** ("Lemo", "Lemo-Opuscar" or `/lemo-opuscar`), not for any video request.
6. **Removed:** `styles/news-package/demo/tools/gen_image.py` and `gen_plates.sh` (the Codex image helper, which read another app's chat logs).
7. **The project's own rules win** over the library's guides (`SKILL.md`).
8. **The stronger graphics chip on Windows** (tag `melissa-2026-11-09b`, the same day): `core/render/browser.mjs` adds `--force_high_performance_gpu` on Windows, so a computer with built-in Intel graphics plus an NVIDIA card renders on the NVIDIA (measured on the desktop: Iris Xe by default, RTX 2060 with it). `LEMO_GPU=default` turns it off.

Big asset packs (`tools/fetch.sh`: voice model, instruments, HDRIs) still download from upstream's GitHub releases, because forks don't copy releases. Each file is checked against the SHA-256 in this fork's `tools/assets.json`, so a changed file is refused.

## Taking an upstream update (only with Melissa's OK)

1. In a separate clone: `git fetch https://github.com/lemomo-ai/lemo-opuscar.git main`, then review every change the same way as the first review (scripts, downloads, online services, the skill and guides).
2. Show Melissa what's new. With her OK, merge it, keep the changes above, re-lock the requirements, set `PIN` in `setup.sh` and `version` in `plugin.json` to a new tag name (`melissa-YYYY-MM-DD`), commit, tag that commit with the same name, push both.
3. On each computer, with her OK: change the tag in Claude's settings (`extraKnownMarketplaces.lemolab.source.ref`), then `sh setup.sh update`, then `sh setup.sh deps` (and the tiers in use). Record it in claude-hq's `claude-home/BY-HAND.md`.
