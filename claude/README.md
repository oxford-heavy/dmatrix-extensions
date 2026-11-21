# dMatrix Decision Capture — Claude

Set up dMatrix decision capture in Claude. You need a free dMatrix account: create one at
[dmatrix.com](https://dmatrix.com).

Setup has two parts, and you need both:

1. **The connection** — dMatrix's tools, added once to your Claude account as a custom
   connector. It covers claude.ai, the desktop app's Chat and Code tabs, and Claude Code signed
   in with your Claude account.
2. **The plugin** — the decide Skill, which teaches Claude when to offer a capture and how to
   draw out options, criteria and scores. The plugin carries only the Skill; it adds no
   connection of its own.

With only the plugin, Claude can talk a decision through but cannot create or save anything in
dMatrix. With only the connection, Claude has the tools but does not know when to offer them.

In claude.ai and the desktop app, dMatrix shows each step as a card in the chat — the draft, the
matrix, each criterion to score, the analysis. Claude Code gets the same steps as text.

---

## 1. Connect dMatrix to your Claude account

Do this once.

1. Open **Customize › Connectors**.
2. Click **+**, then **Add custom connector**.
3. Name: `dMatrix`. URL: `https://mcp.dmatrix.com/mcp`. Click **Continue**.
4. Leave Authentication on **Sign in now** and the client on **Use Claude's published
   identity**. Click **Add**.
5. On dMatrix's page, click **Allow Access**.
6. Open **dMatrix** in the connector list. Under **Tool permissions**, set **Interactive tools**
   to **Always allow**.

## 2. Add the plugin

1. Open **Customize › Plugins**.
2. Click **+ Add**, then **Add marketplace**, then **Add from a repository**.
3. Paste `https://github.com/oxford-heavy/dmatrix-extensions` in the **URL** box and pick
   **Use "https://github.com/oxford-heavy/dmatrix-extensions"**. Leave **Sync automatically**
   on.
4. Click **Add** on **dMatrix Decision Capture**.

The marketplace is `oxford-heavy/dmatrix-extensions`; it holds one plugin, `dmatrix`.

## 3. Check it

Start a new conversation and ask Claude to help you choose between two options. It offers to
capture the decision in dMatrix.

## 4. If you cannot add a connector

- **Free plan**: Claude allows one custom connector. Remove another connector first, or
  upgrade.
- **Team and Enterprise**: an Owner adds the connector for the organization. Each member then
  connects it under **Customize › Connectors**.

## 5. Claude Code with an API key

Claude Code signed in with an API key has no Claude account, so it has no account connector.
Add the plugin and the server by command instead:

```bash
claude plugin marketplace add oxford-heavy/dmatrix-extensions
```

```bash
claude plugin install dmatrix@dmatrix-extensions
```

```bash
claude mcp add --transport http dmatrix https://mcp.dmatrix.com/mcp
```

Then, in Claude Code, run `/mcp`, choose `dmatrix`, and pick **Authenticate** to sign in to
dMatrix.

> Use this only if dMatrix is not connected on your account. With both, your client loads dMatrix
> twice.

---

## Update

Open **Customize › Plugins**, click **+ Add**, then **Manage marketplaces**. Click **…** next to
**dmatrix-extensions**, then **Check for updates**. With **Sync automatically** on, updates also
arrive by themselves when the repository changes.

Claude Code with an API key:

```bash
claude plugin marketplace update dmatrix-extensions
```

```bash
claude plugin update dmatrix@dmatrix-extensions
```

## Remove

1. **The plugin**: open **Customize › Plugins**, click **+ Add**, then **Manage marketplaces**.
   Click **…** next to **dmatrix-extensions**, then **Remove**, and confirm. This also removes
   dMatrix Decision Capture.
2. **The connector**: removing the plugin does not remove it. Open **Customize › Connectors**,
   click **dMatrix**, click **…** next to **Disconnect**, then **Remove**, and confirm.
3. **The approval**: click **Disconnect** for Claude in dMatrix's
   [AI App Setup](https://app.dmatrix.com/ai-app-setup). Without this, adding the connector
   again reuses the old approval and skips dMatrix's page.

---

## Troubleshooting

- **Claude doesn't offer to capture decisions** — check the plugin is added under
  **Customize › Plugins**. In Claude Code, a newly added plugin loads after `/reload-plugins`
  or in a new session. Try a clearer decision ("help me choose between A and B on cost and
  speed").
- **Claude won't create or save a matrix, or says the dMatrix tools aren't reachable** — the
  connection is missing. **Customize › Connectors** should list **dMatrix** at
  `https://mcp.dmatrix.com/mcp`, connected. If it says it needs you to sign in, reconnect it
  there.
- **Claude asks before every card** — set **Interactive tools** to **Always allow** under the
  connector's **Tool permissions** (step 6 of the connection).
- **Can't add the marketplace, or the dMatrix plugin is missing (Team and Enterprise)** —
  plugins must be enabled for the organization by an Owner first. Ask your admin.
- **"This plugin uses a source type your Claude Code version does not support"** — update
  Claude Code to the latest version, then add the marketplace again.
