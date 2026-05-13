# Gemini Integration — Gems + Drive Sync

Gemini Gems is the only consumer LLM with **automatic live sync** via Google Drive. This makes it uniquely well-suited for Mypersona's compounding-memory model — wiki edits propagate without manual re-upload.

## Path — Gem with Drive sync

### Steps

1. Mirror your Mypersona repo into a Google Drive folder. Two options:
   - **Drive Desktop** (recommended): install Google Drive desktop sync, then place a clone of Mypersona inside the Drive-synced directory. Drive picks it up automatically.
   - **Manual upload**: zip the repo and upload to a Drive folder. Re-upload on changes (loses the auto-sync advantage).
2. gemini.google.com → Gems → New Gem.
3. **System prompt**: paste the entire content of `PERSONA.md`.
4. **Context / Drive integration**: in the Gem's knowledge/context configuration, reference the Drive folder where Mypersona lives. Gemini will index it.
5. Activate the Gem. The persona is now backed by live Drive sync.

## Update procedure

Edit files locally → Drive Desktop syncs automatically → next Gem invocation sees the new content. No manual step.

## Limitations

- **Read-only from Gemini's side**. Gem can reference files but cannot write back to Drive directly during conversation (as of 2026). Write-back remains manual or via Claude Code on the local clone.
- Drive sync is **eventually consistent**, not instant. Allow a few seconds after local edit before invoking the Gem.
- 1M context window is helpful but practical loading is still selective — Gemini chooses what to read.

## Recommendation

Use Gemini Gems for **read-heavy** persona scenarios — when you want the persona to consult its memory often, but writing back to the repo happens elsewhere (Claude Code session, manual editing). The auto-sync makes this the lowest-friction "always current" path among consumer LLMs.
