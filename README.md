# AuctionCopilot — a WebMCP collaboration demo

A single-file WebMCP demo where a human sets the goal and an agent does the exploring, comparing, and simulating. The six tools — **list + detail + compare + recommend + simulate** — are not specific to one service: swap the data source and the same pattern applies to real-estate auctions, used equipment, and B2B procurement.

**Live demo:** https://minjun0208.github.io/auction-copilot-webmcp/

> Human sets the goal; the agent explores, compares, and simulates. Six reusable WebMCP tools ("list + detail + compare + recommend + simulate") for any auction/marketplace.

## The six registered WebMCP tools

| Tool | Role |
|------|------|
| `search_listings` | Filter by criteria + refresh the list |
| `get_listing` | Fetch a listing's detail + mark it selected |
| `estimate_value` | Estimate value from year / mileage / condition (read-only) |
| `compare_lots` | Compare multiple listings + update the compare tray |
| `recommend_strategy` | Top 3 + an alternative from budget / purpose / risk |
| `simulate_bid` | Win probability + expected profit by bid amount |

Every tool's `execute` reads and mutates the real page state (DATA / state / DOM) — not mock responses. Return values are wrapped as `{content:[{type:'text',text}]}` (a WebMCP `execute` may return `Promise<any>`, so this isn't required — it's a convenience so agents and inspectors read the text field consistently).

## Try it yourself (Chrome 149+)

1. Open the **live demo** in Google Chrome (version 149 or later). The six WebMCP tools register automatically via a Chrome Origin Trial token — **no flags required**.
2. To inspect the tools, open **DevTools → Application → WebMCP**. You'll see all six tools under *Available Tools*.
3. Run `recommend_strategy` with:
   ```json
   { "budgetManwon": 2000, "purpose": "Family", "riskTolerance": "Low" }
   ```
   Then change `"purpose"` to `"Commute"` and run it again — the recommendation changes completely. The engine actually reasons; it isn't a static list.
4. The on-page **Live trace** panel logs every tool call in real time, tagged `human` or `agent`.

> To see the DevTools WebMCP panel, you may also need to enable `chrome://flags/#devtools-webmcp-support`. The tools themselves work via the Origin Trial token without any flags.

## How it's built

- Self-contained single `index.html`, vanilla JS, **no build step**.
- Tools registered via `document.modelContext.registerTool` (with a `navigator.modelContext` fallback for Chrome 149 / Edge 147).
- `estimate_value` is `readOnlyHint: true`; the state-changing tools are `readOnlyHint: false`.
- Value and deal-score use a transparent, public demo formula.

## The reusable pattern

The six tools are not car-specific: `list + detail + compare + recommend + simulate` is a reusable WebMCP pattern for any auction or marketplace. Replace only the data source and it works for real-estate auctions, used equipment, and B2B procurement.

## Disclaimer

All vehicles, figures, valuations, scores, and probabilities are **illustrative demo values** and are not a basis for real investment or bidding decisions.

## License

MIT
