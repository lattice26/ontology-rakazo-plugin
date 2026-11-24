# ontology-data-agent for Rakazo

A Rakazo plugin for asking an e-commerce data agent about real shop data.

| Part | What it does |
|---|---|
| `skills/ecommerce-data` | When to hand a question to the data agent and how to write it |
| `skills/ecommerce-data-results` | How to read its data sheet (gaps, outcomes) and answer the user |
| `skills/ecommerce-report-page` | Turn results into a page (metrics, trend charts, rankings) and keep it current with a routine |
| `commands/` | `/shop-diagnosis`, `/daily-report`, `/product-ranking`, `/creator-performance` |

1. Install: **Integrations → + → From GitHub**, paste this repository's URL, **Preview**, then **Add skills**.
2. Add the server yourself: **Integrations → + → MCP server**, enter the server URL you were given, and put
   your personal access token under **Advanced → Access token**. Then choose **Use in this bot**.
