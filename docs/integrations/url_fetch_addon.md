# URL-Fetch Bootstrap (Optional Add-on)

> **What this is**: a one-line instruction that, when pasted into any LLM's Custom Instructions / system-prompt slot, makes the LLM fetch the latest `PERSONA.md` from your GitHub repo on every new conversation.
>
> **Why it's optional**: it only works on LLMs with an active web/fetch tool, and it spends tokens on every conversation. Use it when you value live freshness over paste simplicity.

## The one-liner

Replace `{user}` with your GitHub username:

```
On every new conversation, before responding to the first user message, fetch https://raw.githubusercontent.com/{user}/Mypersona/master/PERSONA.md and follow the directives it contains. Pay special attention to the COMPACT section between <!-- COMPACT START --> and <!-- COMPACT END --> markers. If the fetch fails, ask the user to paste PERSONA.md manually.
```

Paste into:
- ChatGPT Custom Instructions field 2 ("How you should respond")
- Claude Projects Custom Instructions
- Gemini Gems system prompt
- Any other LLM with a persistent system-instruction slot

## Where this works well

- **Claude (web + Projects)**: native web fetch is reliable.
- **Gemini**: search integration handles this cleanly.
- **ChatGPT (Plus, browsing tool on)**: works when browsing is enabled.

## Where this fails

- ChatGPT free tier without browsing.
- Offline / air-gapped sessions.
- GitHub rate limits if invoked from a shared IP at high frequency.

## Trade-offs vs. paste

| | Paste (Strategy 1) | URL fetch (this) |
|---|---|---|
| Setup effort | Higher (copy + paste once per tool) | Lower (one line) |
| Always-latest | No — manual sync | Yes |
| Token cost / conversation | Free (loaded as instructions) | Spent on fetch each turn |
| Reliability | High | Depends on web tool + network |
| Works on free tier | Yes | Only if browsing is available |

## Hybrid recommendation

Paste the **COMPACT section as a fallback** AND add the URL-fetch one-liner. If fetch succeeds, the LLM gets fresh content; if it fails, it still has the pasted persona to operate from. Belt and suspenders.
