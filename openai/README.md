# dMatrix Decision Capture — OpenAI (ChatGPT and Codex)

Set up dMatrix decision capture in ChatGPT. You need a free dMatrix account: create one at
[dmatrix.com](https://dmatrix.com).

Setup has two parts, and you need both:

1. **The connection** — dMatrix's tools, added once on chatgpt.com as a custom MCP server.
2. **The Skill** — the decide Skill, which teaches ChatGPT when to offer a capture and how to
   draw out options, criteria and scores.

With only the Skill, ChatGPT can talk a decision through but cannot create or save anything in
dMatrix. With only the connection, ChatGPT has the tools but does not know when to offer them.

---

## 1. Set up dMatrix on chatgpt.com

Do this once, on the ChatGPT website. It covers the website, the desktop app and Codex signed in
with ChatGPT.

1. Open `chatgpt.com/plugins`. Click **Add**, then **Add custom MCP server**.
2. Name: `dMatrix`. Server URL: `https://mcp.dmatrix.com/mcp`. Authentication: **OAuth**.
   Optional icon: [`assets/dmatrix-icon-chatgpt.png`](../assets/dmatrix-icon-chatgpt.png).
3. Tick **I understand and want to continue**, then click **Create as a plugin**.
4. Click **Continue to dMatrix**, then **Allow Access** on dMatrix's page.
5. Download the Skill archive,
   [`decide.zip`](https://github.com/oxford-heavy/dmatrix-extensions/releases/latest/download/decide.zip).
   On the **Skills** tab click **Add**, then **Upload from your computer**, and choose
   `decide.zip`.

## 2. Where it works

One setup covers all three. On the ChatGPT website and in the desktop app, dMatrix shows each step
as a card in the chat — the draft, the matrix, each criterion to score, the analysis. Codex signed
in with ChatGPT has the same tools and acts when you ask it to use dMatrix.

## 3. If "Add custom MCP server" is missing

Your workspace has switched custom MCP servers off. Ask a workspace admin to allow them.

## 4. After a dMatrix release that changes its tools

Open the dMatrix plugin on chatgpt.com and click **Refresh**. Until you do, ChatGPT keeps the tool
list it saved when you created the plugin.

## 5. Codex with an API key

Codex signed in with an API key has no ChatGPT sign-in, so it does not get the plugin from step 1.
Add the server by command instead:

```bash
codex mcp add dmatrix --url https://mcp.dmatrix.com/mcp
```

dMatrix acts when asked there. To have Codex offer it on its own in a project, copy
[`codex/AGENTS.md`](codex/AGENTS.md) into the project's `AGENTS.md`.

> Use this only if dMatrix is not connected on your account. With both, your client loads dMatrix
> twice.

---

## ChatGPT Projects (paste-in)

To keep the behavior inside one Project instead of every chat, put it in the Project's
instructions: open [`paste-in/dmatrix.md`](paste-in/dmatrix.md), copy the **entire** contents, and
paste them into the Project's instructions. A Custom GPT's instructions work the same way. The
connection from step 1 is still needed.

## Update the Skill

On the **Skills** tab, delete `decide`, then upload the new
[`decide.zip`](https://github.com/oxford-heavy/dmatrix-extensions/releases/latest/download/decide.zip)
the same way.

## Remove

1. **The plugin**: open the dMatrix plugin on chatgpt.com, click **…**, then **Delete plugin**,
   and confirm.
2. **The Skill**: delete `decide` on the **Skills** tab.
3. **The approval**: click **Disconnect** for ChatGPT in dMatrix's
   [AI App Setup](https://app.dmatrix.com/ai-app-setup).

---

## Troubleshooting

- **ChatGPT doesn't offer to capture decisions** — confirm the Skill finished scanning and is
  enabled on the **Skills** tab, or, if you used the paste-in, that the instructions were pasted
  in full. Start a new chat and try a clearer decision ("help me choose between A and B on cost
  and speed").
- **ChatGPT can't create or save a matrix** — the connection isn't active. Open the dMatrix plugin
  on chatgpt.com and check it is connected; if it asks you to sign in, connect it again.
- **A dMatrix tool is missing after a release** — click **Refresh** on the dMatrix plugin (step 4).
- **The Skill upload says "Needs Review" or "Blocked"** — ChatGPT scans every uploaded Skill.
  Open the **Skills** tab to review and approve it; if it stays blocked, use the Project paste-in
  instead.
- **ChatGPT asks before each change to a matrix** — that's expected: it confirms the first write
  in each conversation.
