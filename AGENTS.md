## Project Summary

This project creates a mod to the video game Stardew Valley. This mod allows Robin, an NPC, to become a romance and marriage candidate. It changes game dialog, festivals, maps, events, schedules, and characters to achieve this goal.

Currently, all of this is done using Content Patcher. You are an expert Stardew Valley mod developer using Content Patcher.

## Documantation

Use the official author guide and documentation as the primary source of truth. This documentation takes precedence over the other documentation linked below:
<https://github.com/Pathoschild/StardewMods/tree/develop/ContentPatcher/docs/author-guide>

Here are guides from the official wiki that relate to modding with Content Patcher. Refer to these as needed to accomplish your tasks:

- Basic concepts: <https://wiki.stardewvalley.net/Modding:Content_Patcher>
- Modding Dialogue: <https://wiki.stardewvalley.net/Modding:Dialogue>
- Modding Event Data: <https://wiki.stardewvalley.net/Modding:Event_data>
- Modding Maps: <https://wiki.stardewvalley.net/Modding:Maps>
- Modding NPC Data: <https://wiki.stardewvalley.net/Modding:NPC_data>

## Rules

- Prefer tokens and conditions over hardcoding (e.g. `{{season}}`, `HasMod`).
- Patch minimally:
  - Use `EditImage` with `FromArea` where it makes sense
  - Use `EditData` for targeted changes
  - Avoid full asset replacements
- Use `EditData` for game data (dialogue, schedules, shops, events).
- Design for compatibility:
  - Avoid conflicts with other mods
  - Guard patches with `When`
- Support config (assume Generic Mod Config Menu).
- Keep assets organized, optimized, and stylistically consistent.
- Add `LogName` where helpful for debugging.
- Produce valid, minimal, well-structured JSON (`content.json`). Tolerate comments.
- Comment only when it adds value.
- All text must support translation: i18n/default.json

## Output

- Output only the requested mod files.

## Important Note

I have ADHD; please make your responses ADHD-friendly. Specifically, put the "bottom line" up front. Make good use of headings, bullets and similar techniques to make your responses easily scannable and digestible. Avoid "walls" of text; lean towards summaries and let me ask for further details if I need them. I need my tasks broken down to basic actions. Propose strategies, processes, approaches, systems, and tasks that will be congruent with my neurodivergent brain.

## Task: Release Zip

When asked to create a release zip (or "package the mod"), follow this checklist exactly.

### Bottom line

Build the zip with `git archive`, never with Finder's "Compress". `git archive` produces a clean, cross-platform zip (Mac, Windows, Android) with no `__MACOSX/` folders, no `._*` AppleDouble files, no `.DS_Store`, and no extended attributes — the junk Finder adds is what breaks extractors on other platforms.

### What goes in

- `manifest.json`
- `content.json`
- `config.json` — shipped so users without GMCM still get a valid config; before releasing, confirm it matches the `ConfigSchema` defaults in `content.json` (so personal settings don't ship)
- `LICENSE`
- `i18n/**`
- `assets/**`
- Everything inside a single top-level folder: `[CP] Dateable Robin/` (extract-ready for `Mods/`)

### What stays out

- `.git/`, `.gitignore` — excluded via pathspec (`.git` is never tracked anyway)
- Dev files that ARE git-tracked and MUST be excluded explicitly: `AGENTS.md`, `plan.md`, `.prettierrc`, `.vscode/`
- `.idea/`, `.opencode/`, `.continue/`
- Any `.DS_Store`, `._*`, `__MACOSX` — auto-excluded because none are git-tracked

### Steps

1. **Check the tree is clean.** `git archive` ships committed state (HEAD), not the working tree. If there are uncommitted changes to files that belong in the zip, commit them first (ask before committing).
2. **Create the zip** (version is read from `manifest.json` automatically):

   ```sh
   cd "/Users/brianbosch/Library/Application Support/Steam/steamapps/common/Stardew Valley/Contents/MacOS/Mods/[CP] Dateable Robin"
   VERSION=$(python3 -c "import json;print(json.load(open('manifest.json'))['Version'])")
   git archive --format=zip \
     -o "$HOME/Downloads/Dateable-Robin-${VERSION}.zip" \
     --prefix="[CP] Dateable Robin/" \
     HEAD -- . \
     ':(exclude).gitignore' \
     ':(exclude)AGENTS.md' \
     ':(exclude)plan.md' \
     ':(exclude).prettierrc' \
     ':(exclude).vscode'
   ```

3. **Verify:**
   - `unzip -l` the output: only `manifest.json`, `content.json`, `config.json`, `LICENSE`, `i18n/`, `assets/` under the `[CP] Dateable Robin/` prefix; zero `.DS_Store` / `__MACOSX` / `.git` entries.
   - Extract to a temp dir (e.g. `/var/folders/r4/2p_dctb95l97c247fjhzl_tr0000gn/T/opencode`), confirm the structure, and JSON-validate `manifest.json` + `content.json` + `config.json`.
   - Report final zip size and entry count.

### Naming

- File: `Dateable-Robin-<version>.zip` in `~/Downloads` — version from `manifest.json`, brackets dropped from the filename to avoid extractor quirks on other platforms.
- Folder inside the zip: `[CP] Dateable Robin/` (the standard Stardew mod folder convention; square brackets are safe inside the zip).

### Notes

- If the version in the output filename already exists, that usually means a re-release — ask before overwriting.
- If new non-runtime files are ever added to the repo root (e.g. notes, docs, dev scripts), either gitignore them or add an explicit `:(exclude)` to the command above.

## Open Brain

Open Brain is the persistent memory system for this project.

### Searching Open Brain

When searching Open Brain during work on this repository:

- Treat cp-dateable-robin as the primary project context.
- Include `cp-dateable-robin` and/or `[CP] Dateable Robin` in Open Brain searches when practical.
- Prefer memories that clearly relate to this project.
- Do not treat memories from other projects as applicable merely because they contain similar technical terms.
- If search results contain memories from another project, ignore them unless they are clearly relevant.

At the beginning of a substantial new coding session, search Open Brain for relevant memories about cp-dateable-robin before making architectural decisions.

### Capturing memories

When an important reusable discovery, architectural decision, constraint, bug, or unresolved issue is discovered, capture it in Open Brain.

Include the project identifier in the captured thought:

"cp-dateable-robin — [decision/discovery/constraint/etc.] ..."

Do NOT capture routine coding activity, temporary debugging information, or source code.

### Project state

Git is the source of truth for code.

[[plan.md]]is the source of truth for the current implementation plan.

Open Brain is the source of truth for history, discoveries, constraints, and reasoning that may be useful in future sessions.
