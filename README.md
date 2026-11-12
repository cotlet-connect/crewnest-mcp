# CrewNest MCP server for ChatGPT and Claude

Connect CrewNest to ChatGPT, Claude and other AI agents through Cotlet. Work with estimates, job scheduling, crew assignments and receivables in your own signed-in account. CrewNest also offers its own Job Pricing MCP for public price calculations and benchmarks. Cotlet provides an independent connection for work in your signed-in business account and is not affiliated with CrewNest.

## What you can ask

> Show outstanding receivables for the period I select.

> Draft an unsent estimate for the customer property I select using my service, area, rate and tax. Stop before emailing it.

> Schedule the job I select and assign it to a crew member after showing me the details and getting my approval.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Claude

Add `https://cotlet.dev/mcp/v1` as a custom connector in Claude and sign in with Cotlet.dev. Follow the steps in your Cotlet console.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its CrewNest tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers": {"crewnest": {"command": "python3", "args": ["/absolute/path/to/crewnest-mcp/crewnest_agent.py", "serve"], "env": {"COTLET_API_KEY": "your-key"}}}}
```

Or with Docker:

```bash
docker build -t crewnest-mcp .
docker run -i --rm -e COTLET_API_KEY crewnest-mcp
```

Tools: `crewnest_guide`, `crewnest_status`, `crewnest_open`, `crewnest_read`, `crewnest_click`, `crewnest_type`, `crewnest_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Run from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 crewnest_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 crewnest_agent.py status    # is CrewNest ready in your Cotlet.dev account
python3 crewnest_agent.py guide     # CrewNest screens and sign-in link
python3 crewnest_agent.py read      # open CrewNest, read the page, close the browser
python3 crewnest_agent.py tools     # list Cotlet.dev tools
python3 crewnest_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from CrewNest users

**How do I connect CrewNest to ChatGPT or Claude?**

Sign up at cotlet.dev, log in to CrewNest once in its Cloud Browser and add Cotlet to ChatGPT or Claude, following the steps in your console. No API key is needed. ChatGPT and Claude then work in your CrewNest account through Cotlet, in their phone apps too.

**What can ChatGPT do in CrewNest?**

With Cotlet, ChatGPT, Claude and other AI agents handle jobs like these in CrewNest: create estimate draft; schedule job; assign crew member. You ask in plain words, and anything that reaches other people waits for your OK first.

**Is there an official ChatGPT or Claude app for CrewNest?**

Yes. CrewNest publishes its own Job Pricing MCP server for custom connections to ChatGPT and Claude. Its three read-only tools calculate public prices and benchmarks; they do not access your CrewNest business records. No CrewNest listing was found in public ChatGPT apps or Claude connectors directory searches on 11 November 2026. Cotlet is an independent connection for work in your signed-in account.

**Can ChatGPT create estimate in CrewNest?**

ChatGPT creates an unsent CrewNest estimate for an existing customer property using your service, area, rate and tax. Drafting stops before emailing the customer.

**Does CrewNest have an API?**

CrewNest publishes an official, free Job Pricing MCP server with three read-only tools for public price calculations and benchmarks. It needs no sign-in or API key. It does not read your business's jobs, invoices, customers or crew assignments. No public account-management API documentation or self-serve key page was found.

**Is Cotlet affiliated with CrewNest?**

No. Cotlet is independent and not affiliated with CrewNest.

## Find it on

- [CrewNest on Cotlet](https://cotlet.dev/integrations/crewnest-api-mcp-server)
- [All Cotlet packages](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/crewnest-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=crewnest

Request access: https://cotlet.dev/signup?app=crewnest&utm_source=github&utm_medium=readme&utm_campaign=crewnest
