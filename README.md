# Solana-mission-control

Solana mission control provides a comprehensive set of metrics and alerts for solana validator  operators. We utilized the power of Grafana + Node exporter and extended the monitoring & alerting with a custom built go-server.

See the full annoucement post, including screenshots, [here](https://chainflow.io/introducing-solana-mission-control/).

### Getting Started

 - [Click here](./INSTRUCTIONS.md) to find the instructions to install the tool. 

 - [Click here](./docs/metric-cal.md) to find out how the metrics were calculated.

 - [Click here](./docs/alerts-commands.md) to find the list of telegram commands supported by the alerting bot.

### RPC polling intervals

Prometheus scrapes now serve a cached metric snapshot instead of triggering a full set of Solana RPC calls on every scrape. The first scrape populates the cache; subsequent scrapes reuse it until the next refresh.

Add a `[scraper]` section to your configuration to tune the intervals:

```toml
[scraper]
# How often to refresh the RPC-backed exporter metrics.
rate = "30s"
# How often the slot watcher polls Solana.
slot_rate = "10s"
```

Both values use Go duration syntax (for example, `15s`, `30s`, or `1m`). Invalid or non-positive values fall back to the defaults: 30 seconds for exporter metrics and 2 seconds for the slot watcher.
