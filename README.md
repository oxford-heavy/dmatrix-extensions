<p align="center">
  <img src="assets/dmatrix-logo.png" alt="dMatrix" width="120" height="120" />
</p>

# dMatrix Extensions

Bring dMatrix **decision capture** to your AI assistant. dMatrix notices when you're weighing
alternatives or trade-offs and offers to capture the decision as a structured, auditable decision
matrix.

You need a free dMatrix account: sign up at [dmatrix.com](https://dmatrix.com).

## How it connects

dMatrix connects once, on your account, wherever your assistant has one. Pick the row that matches
where you work:

| Where you work                                                                           | The connection (once)                                           | The behavior                                                      | Guide                                                  |
| ---------------------------------------------------------------------------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------ |
| Claude: claude.ai, the desktop app's Chat and Code tabs, Claude Code on a Claude account | dMatrix added as a connector on your Claude account, by address | The dMatrix Decision Capture plugin, which carries only the Skill | [claude/README.md](claude/README.md)                   |
| ChatGPT: the website and the desktop app; Codex signed in with ChatGPT                   | dMatrix added on chatgpt.com                                    | The dMatrix Decision Capture plugin, which carries only the Skill | [openai/README.md](openai/README.md)                   |
| A terminal client with no account connection (Claude Code or Codex on an API key)        | One command adds the server                                     | Claude Code: the plugin. Codex: acts when asked                   | [claude](claude/README.md), [openai](openai/README.md) |
| Antigravity CLI                                                                          | Its own bundle, which carries the connection                    | The same bundle                                                   | [google/README.md](google/README.md)                   |

Every connection points at the same address, `https://mcp.dmatrix.com/mcp`. Connect each client
one way only: a client that has dMatrix both on the account and by command loads it twice.

## Two parts, both needed

1. **The connection** — dMatrix's tools, so the assistant can create and save your matrices.
2. **The Skill** — the behavior: when to offer a capture, and how to draw out options, criteria
   and scores.

With only the Skill, the assistant can talk your decision through but can't create or save
anything in dMatrix, so it ends up offering help it can't deliver. With only the connection, it
has the tools but doesn't know when to offer them. Each guide sets up both.

## Cards or text

Claude (claude.ai and the desktop app) and ChatGPT (the website and the desktop app) show each step
as a card in the chat — the draft, the matrix, each criterion to score, the analysis — where you tap
to score, choose an option, or submit a round's scores. Claude Code in a terminal, Codex in a
terminal and Antigravity CLI show the same steps as text.

## What is in this repository

```
.claude-plugin/marketplace.json            # The marketplace; its one plugin is claude/dmatrix
.github/workflows/release.yml              # Publishes dmatrix-chatgpt.zip and its checksum on a tag
.gitignore · LICENSE · README.md           # This repository's own files
assets/                                    # Brand logos and chatgpt.com's icon, used by the guides
claude/README.md                           # Claude guide
claude/dmatrix/                            # The Claude plugin: its manifest and the Skill
google/README.md                           # Google guide
google/antigravity/dmatrix/                # The Antigravity bundle: the Skill and its connection
openai/README.md                           # OpenAI guide
openai/chatgpt/dmatrix/                    # The ChatGPT plugin (dmatrix-chatgpt.zip)
openai/paste-in/dmatrix.md                 # The behavior to paste into a ChatGPT Project
openai/codex/AGENTS.md                     # The same text, as AGENTS.md for terminal Codex
shared/canonical-prompt/source.md          # The canonical behavior every Skill carries
```

## How it is built

Everything here is generated from the dMatrix repository by its renderer
(`packages/canonical-prompt`): the plugins, the bundle and these guides. The canonical
behavior is injected verbatim into each surface and stamped with a content hash (`version_hash`)
so every copy stays provably in sync. Do not edit files here; a change made here is overwritten by
the next render.

## License

Copyright © 2026 Oxford Heavy Industries, LLC. All rights reserved. dMatrix is a product of
Oxford Heavy Industries, LLC.

These extensions are **free to use** with your own dMatrix account. They are not open source:
copying, redistribution, modification, and derivative works are not permitted, and the dMatrix
name, logos, and icons are trademarks that this license does not grant any right to use. See
[LICENSE](LICENSE) for the full terms.

## Support

- Issues: [github.com/oxford-heavy/dmatrix-extensions/issues](https://github.com/oxford-heavy/dmatrix-extensions/issues)
- dMatrix account & app: [dmatrix.com](https://dmatrix.com)
