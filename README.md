# cowork24 for Claude

Find, compare and book workspaces on [cowork24.ch](https://www.cowork24.ch) from Claude:
coworking desks, private offices and meeting rooms in Swiss cities, plus airport lounges in
Switzerland and at international airports. Prices and availability are live. Payment always
happens on cowork24.ch, never in the chat.

## Install

In Claude Code:

```bash
claude plugin marketplace add matthias-wortmann/cowork24-claude-plugin
```

```bash
claude plugin install cowork24@cowork24
```

In Claude Cowork or claude.ai, add the plugin from the directory, or upload the `.plugin` file
from the latest release.

## What it does

| Skill | Use it for |
| --- | --- |
| `find-workspace` | "Find me a coworking space in Zürich under CHF 40 a day" |
| `book-space` | "Is this meeting room free next Wednesday 9 to 12, and what does it cost?" |
| `plan-team-day` | "Workshop for 8 people in Bern on 3 December, compare three rooms" |
| `manage-bookings` | "What have I booked on cowork24?" and cancelling an open request |

## Connectors

| Connector | Endpoint | Sign-in | Tools |
| --- | --- | --- | --- |
| `cowork24` | `https://mcp.cowork24.ch/mcp/app` | none | `search_spaces`, `get_space_details`, `check_availability`, `get_price_quote`, `prepare_booking` |
| `cowork24-account` | `https://mcp.cowork24.ch/mcp` | cowork24 account (OAuth) | the five above plus `list_my_bookings`, `cancel_booking` |

Searching, pricing and preparing a booking need no account. `cowork24-account` is optional
and only needed to see or cancel your own bookings.

## Data and payment

- The `cowork24` connector is anonymous. It receives search parameters (place, dates, seats,
  budget, listing) and returns public listing content.
- `prepare_booking` creates no reservation and takes no payment. After you confirm, it
  returns a link to the checkout on cowork24.ch, where you sign in and pay.
- `cowork24-account` acts as you on cowork24.ch after you sign in. It can list your bookings
  and cancel a request that the host has not accepted yet, each time only after you confirm.
- Privacy policy: https://www.cowork24.ch/privacy-policy
- Terms: https://www.cowork24.ch/terms-of-service

## Support

support@cowork24.ch

## License

MIT. cowork24 is a service of Pinnacle Interactive GmbH.
