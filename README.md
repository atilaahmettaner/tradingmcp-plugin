# TradingMCP

Cursor plugin that connects agents to [TradingMCP](https://tradingmcp.ai), a hosted remote [Model Context Protocol](https://modelcontextprotocol.io/) server for market data and analysis.

Ask for a market brief, scan for movers, run technical analysis from the weekly chart down to 15 minutes, backtest a strategy or chart a symbol, across crypto, US and international stocks, FX and futures. Prices and indicators are fetched when you ask.

## Install

1. In Cursor, open **Settings → Plugins**, search for **TradingMCP** and click **Install**. In Grok Bot, open **Plugins** and add it.
2. When asked to connect, sign in to TradingMCP with the email you subscribed with and choose **Allow**.

Or, in a Grok Bot chat, send `Add a custom MCP server called TradingMCP at https://mcp.tradingmcp.ai/mcp` and sign in on the connect card it shows.

## MCP

```json
{
  "mcpServers": {
    "tradingmcp": {
      "type": "http",
      "url": "https://mcp.tradingmcp.ai/mcp"
    }
  }
}
```

Auth is OAuth with PKCE and dynamic client registration; leave any OAuth client ID and secret blank. Access refreshes on its own.

## Before you connect

You need a TradingMCP plan: Pro is $9 a month (2,500 tool calls per rolling 30 days), Pro+ is $29 a month (10,000). Every plan has a 14-day money-back guarantee. Only tool calls count; connecting and listing the tools are free. If you sign in with an email that has no plan, the connection works and tool calls explain how to choose one.

## What agents can do

| Category | Tools |
| --- | --- |
| Market overview and news | `market_snapshot`, `markets_dashboard`, `bitcoin_market_pulse`, `futures_market_overview`, `futures_category_snapshot`, `financial_news`, `market_sentiment` |
| Screeners | `top_gainers`, `top_losers`, `stock_screener`, `rating_filter`, `bollinger_scan`, `smart_volume_scanner`, `volume_breakout_scanner`, `consecutive_candles_scan`, `futures_top_movers`, `stock_options_unusual_activity` |
| Analysis | `coin_analysis`, `combined_analysis`, `multi_timeframe_analysis`, `multi_agent_analysis`, `smart_money_analysis`, `advanced_candle_pattern`, `volume_confirmation_analysis` |
| Backtesting | `backtest_strategy`, `compare_strategies`, `walk_forward_backtest_strategy`, `backtest_chart` |
| Prices and charts | `stock_prices`, `yahoo_price`, `price_chart`, `stock_extended_hours`, `stock_options_chain` |
| Watchlist | `my_watchlist`, `watchlist_add`, `watchlist_remove`, `futures_watchlist` |
| Egyptian Exchange (EGX) | `egx_market_overview`, `egx_index_analysis`, `egx_sector_scan`, `egx_sector_scanner`, `egx_stock_screener`, `egx_smart_money_scanner`, `egx_trade_plan`, `egx_fibonacci_retracement` |

The hosted server is the source of truth for tool names and schemas.

Some questions to start with:

- "Give me today's market brief."
- "Multi-timeframe analysis of BTCUSDT on KuCoin."
- "Walk-forward test the EMA cross strategy on SPY. Does it hold up out of sample?"
- "Add ETHUSDT to my watchlist, then show me how my watchlist is doing."

## Notes

- Every tool reads market data except `watchlist_add` and `watchlist_remove`, which change your own TradingMCP watchlist. No tool connects to a brokerage or exchange account, places orders or moves money.
- `markets_dashboard`, `price_chart` and `backtest_chart` open interactive views in apps that support MCP Apps; elsewhere, including Grok Bot, they answer in text.
- Crypto is live. Stocks, FX and futures can be delayed by their exchanges.
- Tool calls run as the TradingMCP account that authorizes the connection and count toward that account's plan.
- Nothing here is financial advice.

## Docs

- Setup and usage: https://tradingmcp.ai/docs
- Privacy policy: https://tradingmcp.ai/legal/privacy
- Terms: https://tradingmcp.ai/legal/terms
- Support: hello@cryptosieve.com
- Server URL: https://mcp.tradingmcp.ai/mcp
