# FinancePilot AI — file-by-file corrections

## 1. `finpilot/orchestrator.py` — corrected
- Chat handler accepts the documented JSON `PortfolioInput`.
- Also accepts one-stock shorthand: `TCS.NS,30,3000` (ticker, shares, average buy price).
- Plain ticker shorthand such as `TCS,30,3000` is normalized to `TCS.NS`.
- Invalid shorthand receives a helpful parse error instead of an opaque failure.
- Python syntax checked.

## 2. `finpilot/schemas.py` — no changes
The existing `PortfolioInput`, `HoldingItem`, and enums define the contract used by the orchestrator. The corrected handler builds a payload compatible with these schemas.

## 3. `finpilot/screener.py` — no changes
This file is downstream of the ASI:One reachability problem. It must be running and its actual agent address must be configured in `finpilot/.env` for screening to continue.

## 4. `finpilot/researcher.py` — no changes
This file is downstream of the ASI:One reachability problem. It must be running and its actual agent address must be configured in `finpilot/.env` for research to continue.

## 5. `finpilot/trigger.py` — no changes
This is a direct trigger path, not the ASI:One chat payload parser.

## 6. `.env` — do not replace
Keep your own existing seed and agent addresses. Set `ORCHESTRATOR_PORT=8001`, `SCREENER_AGENT_ADDRESS` to the real screener address, and `RESEARCHER_AGENT_ADDRESS` to the real researcher address. Never use placeholder addresses.

## Important
This code correction fixes the input format mismatch, not Agentverse registration or mailbox availability. For the screenshot's `unreachable` message, run the orchestrator, verify the mailbox is connected, and confirm ASI:One targets the exact current agent address.
