# How to connect StreamElements to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your StreamElements account.** StreamElements has an AI chatbot variable, `$(ai)`, but it runs inside your stream chat, not as an app in ChatGPT or Claude. Cotlet.dev connects your own signed-in StreamElements account to any AI agent, so you can ask in plain words and the AI lists and edits your chat commands for you.

## What you can ask

> List all my StreamElements chat commands with their cooldown and user level, sorted by name.

> Change the !discord command to reply "Join the crew: discord.gg/pixelpals" and set the cooldown to 30 seconds.

> Update !schedule to say I stream Monday, Wednesday and Friday at 7 pm CET.

> Which of my commands are disabled? Turn !giveaway and !merch back on.

> Rename !socials to !links and add my new TikTok handle @pixelpals to the reply.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

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

This repo is a real MCP server. It speaks MCP over stdio, lists its StreamElements tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"streamelements":{"command":"uvx","args":["streamelements-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t streamelements-mcp .
docker run -i --rm -e COTLET_API_KEY streamelements-mcp
```

Tools: `streamelements_guide`, `streamelements_status`, `streamelements_open`, `streamelements_read`, `streamelements_click`, `streamelements_type`, `streamelements_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install streamelements-mcp        # or run it once: uvx streamelements-mcp connect
streamelements-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 streamelements_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 streamelements_agent.py status    # is StreamElements ready in your Cotlet.dev account
python3 streamelements_agent.py guide     # StreamElements screens and sign-in link
python3 streamelements_agent.py read      # open StreamElements, read the page, close the browser
python3 streamelements_agent.py tools     # list Cotlet.dev tools
python3 streamelements_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from StreamElements users

**Is there StreamElements API documentation I need to use first?**

You don't need to work with any StreamElements API. Cotlet.dev works in your own signed-in StreamElements account, so your AI agent can list and edit chat commands without code, tokens or API setup.

**How do I connect StreamElements to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to StreamElements once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no StreamElements API key.

**Is there a way to use Claude with StreamElements?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own StreamElements account.

**Is there a StreamElements MCP server?**

Cotlet.dev is a hosted MCP server that works in StreamElements for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

**Does StreamElements have a ChatGPT chatbot built in?**

StreamElements has an AI chatbot variable, `$(ai)` (alias `$(chatgpt)`), that answers viewers inside your stream chat. To have ChatGPT or Claude manage your StreamElements commands for you, connect them with Cotlet.dev.

## Find it on

- [StreamElements on Cotlet.dev](https://cotlet.dev/integrations/streamelements-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=streamelements&utm_content=find)
- [PyPI package streamelements-mcp](https://pypi.org/project/streamelements-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-streamelements-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/streamelements-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=streamelements

Start free: https://cotlet.dev/signup?app=streamelements&utm_source=github&utm_medium=readme&utm_campaign=streamelements
