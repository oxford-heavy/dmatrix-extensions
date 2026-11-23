# dMatrix Decision Capture — Claude

Set up dMatrix decision capture in Claude. You need a free dMatrix account: create one at
[dmatrix.com](https://dmatrix.com).

Setup has two parts, and you need both:

1. **The plugin** — the decide Skill, which teaches Claude when to offer a capture and how to
   draw out options, criteria and scores. It comes from the dMatrix marketplace and carries only
   the Skill; it adds no connection of its own.
2. **The connection** — dMatrix's tools, added once to your Claude account as a custom
   connector. It covers claude.ai, the Claude desktop app, Cowork and Claude Code signed in with
   your Claude account.

With only the plugin, Claude can talk a decision through but cannot create or save anything in
dMatrix. With only the connection, Claude has the tools but does not know when to offer them.

In claude.ai and the desktop app, dMatrix shows each step as a card in the chat — the draft, the
matrix, each criterion to score, the analysis. Claude Code gets the same steps as text.

---

## 1. Add the marketplace

1. Open [Plugins](https://claude.ai/plugins) on claude.ai.
2. Click **Add**, choose **Add marketplace**, then **Add from a repository**.
3. Click the **Select a repository** box, paste `https://github.com/oxford-heavy/dmatrix-extensions`
   into the search box that opens, then choose
   **Use "https://github.com/oxford-heavy/dmatrix-extensions"** under it.
4. Leave **Sync automatically** on and click **Sync**. After a few seconds, Claude lists
   **dMatrix Decision Capture**.

The marketplace is `oxford-heavy/dmatrix-extensions`; it holds one plugin, `dmatrix`.

## 2. Add the plugin

In the list Claude shows after syncing, point at **dMatrix Decision Capture** and click its **+**.
It installs straight away and opens the plugin's page.

## 3. Connect your account

Do this once.

1. Back on **Plugins**, click **Add**, then **Add custom connector**.
2. Type `dMatrix` as the **Name** and paste `https://mcp.dmatrix.com/mcp` into
   **MCP server URL**. Click **Continue**.
3. Leave **Sign in now** and **Use Claude's published identity** as they are, scroll down and
   click **Add**.
4. A dMatrix page opens. Click **Allow Access**, and Claude brings you back with
   **Connected to dMatrix**.
5. Open **dMatrix** on **Plugins** and choose **Permissions**. Next to **Interactive tools**,
   change **Needs approval** to **Always allow**, so dMatrix shows its cards without asking.

Then start a new conversation and ask Claude to help you choose between two options. It offers to
capture the decision in dMatrix.

## 4. If you cannot add a custom connector

- **Free plan**: Claude allows one custom connector. Remove another first, or upgrade.
- **Team and Enterprise**: an Owner adds dMatrix for everyone. Each member then connects it from
  **Plugins**.

## 5. Claude Code with an API key

Claude Code signed in with an API key has no Claude account, so it gets nothing from your
account's plugin or connector. Run this in Terminal; it adds the marketplace, the plugin and the
server:

```bash
claude plugin marketplace add oxford-heavy/dmatrix-extensions && claude plugin install dmatrix@dmatrix-extensions && claude mcp add --transport http dmatrix https://mcp.dmatrix.com/mcp
```

Then, in Claude Code, run `/mcp`, choose `dmatrix`, and pick **Authenticate** to sign in to
dMatrix.

> Use this only if dMatrix is not connected on your account. With both, your client loads dMatrix
> twice.

---

## Update

On **Plugins**, click **Add**, then **Manage marketplaces**. Next to **dmatrix-extensions**, click
**…**, then **Check for updates**. With **Sync automatically** on, updates also arrive by
themselves when the repository changes.

Claude Code with an API key:

```bash
claude plugin marketplace update dmatrix-extensions
```

```bash
claude plugin update dmatrix@dmatrix-extensions
```

## Remove

1. **The marketplace**: on **Plugins**, click **Add**, then **Manage marketplaces**. Next to
   **dmatrix-extensions**, click **…** and choose **Remove**. Claude says it also uninstalls
   dMatrix Decision Capture: click **Remove**, then **Done**.
2. **The connector**: removing the marketplace leaves it. On **Plugins**, click **dMatrix**, then
   **…** at the top right. Choose **Remove**, then **Delete** to confirm.
3. **The approval**: click **Disconnect** for Claude in dMatrix's
   [AI App Setup](https://app.dmatrix.com/ai-app-setup). Without this, adding the connector
   again reuses the old approval and skips dMatrix's page.

---

## Troubleshooting

- **Claude doesn't offer to capture decisions** — check **Plugins** lists
  **dMatrix Decision Capture**. In Claude Code, a newly added plugin loads after
  `/reload-plugins` or in a new session. Try a clearer decision ("help me choose between A and B
  on cost and speed").
- **Claude won't create or save a matrix, or says the dMatrix tools aren't reachable** — the
  connection is missing. **Plugins** should list the **dMatrix** connector at
  `https://mcp.dmatrix.com/mcp`, connected. If it says it needs you to sign in, reconnect it
  there.
- **Claude asks before every card** — set **Interactive tools** to **Always allow** on the
  connector's **Permissions** (step 5 of the connection).
- **Can't add the marketplace, or the dMatrix plugin is missing (Team and Enterprise)** —
  plugins must be enabled for the organization by an Owner first. Ask your admin.
- **"This plugin uses a source type your Claude Code version does not support"** — update
  Claude Code to the latest version, then add the marketplace again.
