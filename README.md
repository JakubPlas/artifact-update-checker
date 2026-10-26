# artifact-update-checker

A Claude skill that makes sure Claude always edits the **latest** version of an artifact.

## Why

Claude artifacts can be updated from any chat, not just the one they were created in, and by multiple people. The copy your current chat is working from may already be outdated. Publish from it, and newer changes are silently overwritten.

With this skill, before every artifact update Claude:

1. fetches the latest published version,
2. tells you if anything changed since it last saw it,
3. applies your edits on top of that version,
4. resolves publish conflicts by merging, never by force-overwriting.

## Install

### Claude (web / desktop / Cowork)

1. Download [`artifact-update-checker.zip`](./artifact-update-checker.zip) (or zip the `artifact-update-checker` folder yourself).
2. In Claude, open **Settings → Capabilities → Skills** and click **Upload skill**.
3. Select the zip. Done - the skill triggers automatically whenever you ask Claude to update an artifact.

### Claude Code

Copy the `artifact-update-checker` folder to `~/.claude/skills/` (personal) or `.claude/skills/` in your project.

## License

MIT
