---
name: artifact-update-checker
description: Use ALWAYS before any edit, fix or republish of an existing artifact - first fetch the current published version, then apply changes on top of it.
---

# Artifact update checker - always edit the latest version

Artifacts can be updated from any chat, not only the one they were created in, and by several people at once. The local copy from earlier in this chat (or the version you remember) may be outdated. Publishing from an outdated copy silently overwrites other people's changes. Rule: **never publish from a file you did not fetch in this step.** The user should not have to remind you.

## Procedure (every time, even for a tiny change)

1. **Find the artifact URL** - from the conversation, a link from the user, or `Artifact` with `action: "list"`. If you still can't find it, ask.

2. **Fetch the current version right before editing** - `Artifact` with `action: "read"` and `url`. Do this even if you published the artifact in this chat a few minutes ago, and again before each further edit if time has passed or other work happened in between.
   - The result says whether the user has "writer" access and names the saved file with the full page. **That file is the only base for your edits.**
   - If the user is not a writer, do not publish over someone else's artifact; say so and offer a separate copy.
   - For multi-file artifacts, also fetch the files you will change (`action: "read"` with `path`/`paths`; list them with `action: "list"`, `scope: "files"`).

3. **Compare with your older copy (if you have one)** - `diff` the earlier local version against the freshly fetched one. If they differ, tell the user in one sentence what changed in the meantime, and keep those changes.

4. **Apply your changes to the fetched version.**
   - Small changes: publish with the fetched file as `file_path` + `url` + `edits` (old_str/new_str copied exactly from the fetched version).
   - Bigger changes: `Edit` the fetched file, then publish with `url` and the same `file_path` in the same response.
   - Never rewrite the page from memory or from an old local copy.

5. **Publish conflict** - if the publish is refused because a newer version exists, the response contains the live version: take it, re-apply your changes and publish again. Never use `force: true` unless the user explicitly asked to discard that specific version.

6. **Data is not in the HTML** - if the artifact uses a shared database (`db` capability), read and change records via `ArtifactData`, not by writing them into the page code. When editing code, don't remove or break the logic that loads the data.

7. **Artifacts made from types** (Docs, Sheets, Slides, Tasks...) - read and edit them with their own tools / data files; load the current state first there too, never a version from memory.

8. **After publishing** - one sentence: what changed, and whether you preserved changes that others made in the meantime.

## Avoid

- Publishing without a `read` in this step just because "I published it myself".
- Editing a scratchpad file from earlier in the chat.
- Asking the user whether to fetch the latest version - always fetch it yourself.
