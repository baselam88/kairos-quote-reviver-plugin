# Stale Quote Reviver — plugin for Grok Bot, Cursor, and MCP hosts

**What it does.** Sent quotes die in inboxes — owners rarely follow
up systematically. Give your agent the details of a quote that's
gone quiet and it builds a drafted 3-touch follow-up sequence: a
check-in today, a value note in 3 days, and a polite choice-close
("keep it open or close the file?") 7 days after that. Report what
happens after each touch and the sequence advances — or closes
gracefully when the customer answers, wins, or declines.

Every message is a draft. Nothing is ever sent for you; you review
and send each touch yourself.

**Why it matters.** Systematic follow-up is benchmarked to recover
an ESTIMATED 10–15% of quotes that would otherwise go stale — for a
contractor sending 20 quotes a month at a $1,500 average, that's an
ESTIMATED ~$4,500/mo in won work. These are estimates from public
sales-follow-up benchmarks, not promises: your results depend on
your quotes and your customers.

**Tools**

| Tool | Label | What it does |
|---|---|---|
| `kairos_quote_reviver_plan` | Write | Opens a follow-up sequence for one stale quote and returns the drafted 3-touch cadence |
| `kairos_quote_reviver_next` | Write | Records the outcome of a touch (no reply / interested / declined / won) and advances or closes the sequence |

**Configure variables.** None. The endpoint is public and
rate-limited; no key, no sign-in, and no credentials of yours are
ever requested or stored.

**Privacy.** The server stores nothing. Your quote details travel
between calls inside a signed token your own agent carries, and are
used only to draft the sequence. Nothing is sent anywhere on your
behalf.

## Test locally

The package points at the hosted endpoint in `mcp.json`. To exercise
the tools from any MCP client, add the server from `mcp.json` and
ask your agent to "revive a stale quote".

Cursor IDE local load:

```bash
ln -s /path/to/kairos-quote-reviver ~/.cursor/plugins/local/kairos-quote-reviver
```

Then reload the window and confirm the `kairos-quote-reviver` skill
and MCP server load.

## Submit

- Grok Bot / Cursor marketplace: https://x.ai/bot/marketplace/submit-a-plugin
- License: MIT (see LICENSE) — the plugin package is open; the
  follow-up service itself is hosted by KAIROS AI Systems.

Built by KAIROS AI Systems — https://kairosasi.com
