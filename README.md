# TradeX

TradeX is a forex portfolio management project for researching, monitoring, and
running algorithmic trading strategies. The initial focus includes instruments
such as XAUUSD, subject to the selected broker's symbol definitions and trading
conditions.

> **Status:** Early planning/scaffolding. Features and integrations described
> here are intended direction, not a statement that they are already implemented.

## Project goals

- Display live and historical market data with charts.
- Develop and test versioned trading strategies.
- Support backtesting and paper trading before live deployment.
- Track portfolios, positions, orders, and execution events.
- Apply risk checks before any order reaches a broker.

## Planned architecture

```text
Market-data provider
        │
        ▼
Market-data service ──► event stream ──► strategy runner
                                             │ order intent
                                             ▼
                                      risk checks
                                             │ approved order
                                             ▼
                                        execution
                                             │
                                             ▼
                                           broker

Web dashboard ──► API ──► configuration, portfolio, and monitoring
```

Strategies should emit order intents rather than submit broker orders directly.
The risk and execution components remain separate from strategy code.

## Planned technology

- **Web app:** React and TypeScript
- **Backend API:** Python and FastAPI
- **Persistence:** PostgreSQL
- **Market-data and service messaging:** provider adapters and a message broker
- **Charts and code editor:** a browser charting library and Monaco Editor
- **Local development:** Docker Compose

Specific providers, libraries, and deployment choices are still to be selected.

## Repository layout

```text
apps/web/                 Web dashboard
services/api/             HTTP API and application configuration
services/market-data/     Provider connections and normalized market events
services/strategy-runner/ Isolated strategy execution
services/risk/            Portfolio and order risk checks
services/execution/       Broker orders and reconciliation
packages/contracts/       Shared API and event schemas
strategies/examples/      Example strategies
migrations/               Database migrations
tests/                    Unit and integration tests
infra/                    Local development and deployment configuration
```

This layout is a target structure; folders and services may be introduced
incrementally as the project is implemented.

## Development

The project is under active development and does not yet have a verified
end-to-end setup procedure. Setup and run instructions will be added when the
initial application scaffold and dependencies are in place.

## Safety

Trading involves substantial financial risk. Start with historical testing and
paper trading. Live trading should only be enabled with explicit risk limits,
secure broker credential handling, monitoring, and a way to stop trading.
Backtest results do not guarantee future performance.