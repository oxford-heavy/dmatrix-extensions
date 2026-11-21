# dMatrix Decision Capture — Google (Antigravity CLI)

Set up dMatrix decision capture in Antigravity CLI (`agy`). You need a free dMatrix account: create
one at [dmatrix.com](https://dmatrix.com).

Antigravity has no account connection, so it gets one bundle that carries both parts: the decide
Skill, which teaches it when to offer a capture, and its own connection to dMatrix. Antigravity
works in text.

The bundle at [`antigravity/dmatrix/`](antigravity/dmatrix):

```
antigravity/dmatrix/
├── plugin.json                          # plugin marker
├── mcp_config.json                      # dMatrix MCP server (serverUrl)
└── skills/decide/SKILL.md               # decision-capture behavior
```

> **Why not the Gemini app or Gemini CLI?** The consumer Gemini app (and Gems) can hold
> instructions but **can't connect to dMatrix**, so nothing you discuss could be saved there.
> Gemini CLI stopped serving free and individual-paid tiers on **June 18, 2026** (Gemini Code
> Assist Standard and Enterprise licenses keep working — see
> [Gemini CLI](#still-on-gemini-cli-enterprise) below).

## Before you start

You need the `agy` command and `git` on your PATH.

## Install

macOS and Linux:

```bash
git clone --depth 1 https://github.com/oxford-heavy/dmatrix-extensions.git ~/.dmatrix-extensions
```

```bash
agy plugin install ~/.dmatrix-extensions/google/antigravity/dmatrix
```

Windows (PowerShell):

```powershell
git clone --depth 1 https://github.com/oxford-heavy/dmatrix-extensions.git "$HOME\.dmatrix-extensions"
```

```powershell
agy plugin install "$HOME\.dmatrix-extensions\google\antigravity\dmatrix"
```

Keep the folder: updates come from it. Restart `agy`; inside a session, `/skills` lists `decide`
and `/mcp` lists `dmatrix`. The first time dMatrix connects, approve access on dMatrix's page.

## Update

```bash
git -C ~/.dmatrix-extensions pull
```

Then run the install command again.

## Remove

```bash
agy plugin uninstall dmatrix
```

Delete the `~/.dmatrix-extensions` folder, then click **Disconnect** for Antigravity in dMatrix's
[AI App Setup](https://app.dmatrix.com/ai-app-setup).

---

## Manual setup

If you'd rather not install the bundle as a plugin, set up the two parts by hand:

1. **Behavior:** copy the skill into the CLI's global skills directory, e.g.
   `~/.gemini/antigravity-cli/skills/decide/SKILL.md` (or `.agents/skills/` inside a workspace,
   to scope it to one project).
2. **Tools:** add the dMatrix server to `~/.gemini/config/mcp_config.json` (global) or
   `.agents/mcp_config.json` (workspace):
   ```json
   {
     "mcpServers": {
       "dmatrix": { "serverUrl": "https://mcp.dmatrix.com/mcp" }
     }
   }
   ```
   The key must be `serverUrl` — Antigravity does not support the legacy `url` / `httpUrl`
   keys, and a misconfigured entry fails **silently** at startup.

Restart `agy` and confirm with `/skills` and `/mcp` inside a session.

## Still on Gemini CLI? (enterprise)

If you're on an enterprise Code Assist license and staying on **Gemini CLI**, the keys differ —
Gemini CLI uses `httpUrl` (not `serverUrl`) for a streamable-HTTP server, and reads instructions
from `GEMINI.md`:

1. **Behavior:** put the decision-capture instructions in `~/.gemini/GEMINI.md` (global) or a
   project-root `GEMINI.md`.
2. **Tools:** add the server to `~/.gemini/settings.json`:
   ```json
   {
     "mcpServers": {
       "dmatrix": { "httpUrl": "https://mcp.dmatrix.com/mcp" }
     }
   }
   ```
   Restart `gemini` and confirm with `/mcp`.

## Troubleshooting

- **`/skills` doesn't list decide** — `agy plugin list` should show `dmatrix`; if not, run the
  install command again. For the manual route, confirm `SKILL.md` sits at
  `~/.gemini/antigravity-cli/skills/decide/SKILL.md` or in `.agents/skills/` in the workspace,
  then restart `agy`.
- **`/mcp` doesn't list dmatrix** — confirm the MCP config uses `serverUrl` (not `httpUrl` or
  `url`, which fail silently) and lives at `~/.gemini/config/mcp_config.json` or
  `.agents/mcp_config.json`, then restart `agy`. On Gemini CLI it's the reverse: use `httpUrl`
  in `~/.gemini/settings.json`.
- **Tools fail to authenticate** — sign in to your dMatrix account when `agy` asks; the server
  `https://mcp.dmatrix.com/mcp` requires one.
