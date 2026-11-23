# dMatrix Decision Capture — OpenAI (ChatGPT and Codex)

Set up dMatrix decision capture in ChatGPT. You need a free dMatrix account: create one at
[dmatrix.com](https://dmatrix.com).

Setup has two parts, both on chatgpt.com, and you need both:

1. **The Skill** — the decide Skill, which teaches ChatGPT when to offer a capture and how to
   draw out options, criteria and scores.
2. **The connection** — dMatrix's tools, added once as a custom MCP server. One connection
   covers chatgpt.com, the desktop app and Codex signed in with ChatGPT.

With only the Skill, ChatGPT can talk a decision through but cannot create or save anything in
dMatrix. With only the connection, ChatGPT has the tools but does not know when to offer them.

---

## 1. Add the decision skill

1. Download
   [`decide.zip`](https://github.com/oxford-heavy/dmatrix-extensions/releases/latest/download/decide.zip).
2. In ChatGPT, open **Skills**, click **Add**, then **Upload from your computer**. Drop
   `decide.zip` in the box, or click it and choose the file.
3. ChatGPT lists it as **dMatrix Decision Capture**.

## 2. Connect dMatrix

Do this once, on the ChatGPT website.

1. Open [chatgpt.com/plugins](https://chatgpt.com/plugins). Click **Add** at the top right, then
   **Add custom MCP server**.
2. Type `dMatrix` as the **Name**. Leave **Connection** on **Server URL** and paste
   `https://mcp.dmatrix.com/mcp` into the box under it. Leave **Authentication** on **OAuth**.
   Optional icon: [`assets/dmatrix-icon-chatgpt.png`](../assets/dmatrix-icon-chatgpt.png).
3. Tick **I understand and want to continue**, then click **Create as a plugin**.
4. Click **Continue to dMatrix**, then **Allow Access** on dMatrix's page. ChatGPT brings you back
   to **Plugins**, with dMatrix under **Installed**.

One connection covers chatgpt.com, the desktop app and Codex. On the ChatGPT website and in the
desktop app, dMatrix shows each step as a card in the chat — the draft, the matrix, each criterion
to score, the analysis. Codex signed in with ChatGPT has the same tools and acts when you ask it to
use dMatrix.

If **Add custom MCP server** is missing, your workspace has switched custom servers off. Ask a
workspace admin to allow them.

## 3. Codex with an API key

Codex signed in with an API key has no ChatGPT sign-in, so it does not get the connection from
step 2. Run this in Terminal; it opens dMatrix's sign-in page:

```bash
codex mcp add dmatrix --url https://mcp.dmatrix.com/mcp
```

dMatrix acts when asked there. To have Codex offer it on its own in a project, copy
[`codex/AGENTS.md`](codex/AGENTS.md) into the project's `AGENTS.md`.

> Use this only if dMatrix is not connected on your account. With both, your client loads dMatrix
> twice.

To keep the behavior inside one ChatGPT Project instead of every chat, put it in the Project's
instructions: open [`paste-in/dmatrix.md`](paste-in/dmatrix.md), copy the **entire** contents,
and paste them into the Project's instructions. A Custom GPT's instructions work the same way. The
connection from step 2 is still needed.

---

## Update

On chatgpt.com, open **Skills**, click **…** on **dMatrix Decision Capture** and choose
**Delete**, then upload the latest `decide.zip` with **Add › Upload from your computer**. If you
pasted dMatrix's instructions into a project, paste the latest ones.

After a dMatrix release that changes its tools, open the dMatrix plugin on chatgpt.com and click
**Refresh**. Until you do, ChatGPT keeps the tool list it saved when you created the plugin.

## Remove

1. **The Skill**: in ChatGPT, open **Skills**, click **…** on **dMatrix Decision Capture**,
   choose **Delete**, then confirm.
2. **The plugin**: on `chatgpt.com/plugins`, click **dMatrix** under **Installed**, then **…**
   next to **Settings**. Choose **Delete plugin**, then **Delete plugin** again to confirm.
3. **The approval**: click **Disconnect** for ChatGPT in dMatrix's
   [AI App Setup](https://app.dmatrix.com/ai-app-setup).

---

## Troubleshooting

- **ChatGPT doesn't offer to capture decisions** — confirm the Skill finished scanning and is
  enabled under **Skills**, or, if you used the paste-in, that the instructions were pasted in
  full. Start a new chat and try a clearer decision ("help me choose between A and B on cost and
  speed").
- **ChatGPT can't create or save a matrix** — the connection isn't active. Open the dMatrix plugin
  on chatgpt.com and check it is connected; if it asks you to sign in, connect it again.
- **A dMatrix tool is missing after a release** — click **Refresh** on the dMatrix plugin (see
  Update).
- **The Skill upload says "Needs Review" or "Blocked"** — ChatGPT scans every uploaded Skill.
  Open **Skills** to review and approve it; if it stays blocked, use the Project paste-in
  instead.
- **ChatGPT asks before each change to a matrix** — that's expected: it confirms the first write
  in each conversation.
