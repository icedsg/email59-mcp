<p align="center"><img src="logo.png" width="96" height="96" alt="email59"></p>

# email59 MCP server

Send transactional email from AI agents: sign up by email code, no domain or DNS setup.

email59's MCP server lets an agent send email on its own. It signs up by asking for a 6-digit code at an address it
can read, then uses the session key for everything else. Mail goes out from a name you choose at email59.com, so
there's no domain to verify before the first send. The free checks (`check_email`, `check_list`) need no sign-in.

This is a **hosted remote server** (Streamable HTTP). There is nothing to install or run: point your MCP client at the
URL below. This repository holds the docs, the logo and the registry entry; the server itself runs at email59.com.

- Endpoint: `https://email59.com/v1/mcp`
- Docs: https://email59.com/docs.html#mcp
- Website: https://email59.com

## Connect

Claude Code:
```bash
claude mcp add --transport http email59 https://email59.com/v1/mcp
```

Claude Desktop, Cursor, Cline, VS Code and other clients that read an `mcpServers` block:
```json
{
  "mcpServers": {
    "email59": {
      "type": "http",
      "url": "https://email59.com/v1/mcp",
      "headers": { "Authorization": "Bearer ${EMAIL59_KEY}" }
    }
  }
}
```

No key yet? Leave the header out, call the `auth` tool with your email, then call it again with the code to get one.

## Tools

| Tool | What it does |
|---|---|
| `auth` | Sign up or sign in by a 6-digit email code; returns a session key. |
| `send_email` | One email to one recipient: codes, receipts, alerts. |
| `send_campaign` | A marketing email to a list; the unsubscribe link is added for you. |
| `check_email` | Free deep check of an address: format, MX, SPF, DMARC, DKIM, MTA-STS, BIMI, disposable and role addresses. No key needed. |
| `check_list` | The same check for a whole mailing list (emails or CSV text). |
| `validate_email` | Quick verdict before sending: ok, invalid, no_mx, disposable, role. |
| `verify_start` / `verify_check` | Send a one-time code to an address and check it (sign-up, sign-in, confirming an email). |
| `block` / `unblock` / `list_blocklist` | Addresses and domains this account never sends to. |
| `add_unsubscribe` | Record an opt-out so campaigns skip that address. |
| `get_account` / `update_account` | Today's allowance and usage; the name, company and brand your email goes out under. |
| `create_api_key` / `list_api_keys` | Long-lived keys, including test keys whose email is stored instead of delivered. |
| `list_test_messages` | Read what was sent with a test key. |
| `get_pricing` / `buy_pack` / `order_status` | What's on offer, and a checkout link for a person to pay. The agent never pays. |

Every tool carries a `title` and `readOnlyHint` / `destructiveHint` / `openWorldHint` annotations.

Worth knowing: email is sent from @email59.com. Every email carries an unsubscribe link and a "system generated"
line, and accounts that send unsolicited mail are closed.

## Check it from a terminal

```bash
curl -s https://email59.com/v1/mcp -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

## Links

- MCP Registry name: `com.email59/email59` (see `server.json`)
- Privacy: https://email59.com/privacy.html · Terms: https://email59.com/terms.html · Contact: support@biz59.net

Made by Biz59 LLC, New York. The docs in this repository are MIT licensed.
