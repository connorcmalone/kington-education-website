# Website source files (local only — gitignored)

This folder holds the **original source files** for the website's assets — the
raw Gemini video outputs, original logo files, screenshots used as references,
etc. These are not deployed and not tracked in git (per `.gitignore`).

Why keep them here?

- `assets/img/` and `assets/video/` are the **production** files served by
  the live site.
- If you ever need to re-edit, re-encode, or replace an asset, the original
  high-quality source is here next to the project, not buried in Downloads
  or Desktop.

If you replace a production asset and want to keep the new original, drop
it in this folder. If you delete from here, the website still works (the
production copy in `assets/` is what matters).
