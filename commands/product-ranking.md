---
description: Rank a shop's products by sales with real data and chart it. Use when the user runs /product-ranking.
---

Rank products for the shop and period in $ARGUMENTS (defaults: the user's main shop, last 30 days).

1. Ask the data agent: "<shop> top products by GMV over <period>, with units sold, orders and each
   product's share of the shop's GMV."
2. Answer per the `ecommerce-data-results` skill: how concentrated sales are, what leads, what stalled.
3. When the ranking has more than five rows or the user wants it kept, build a page with `Bars` and a
   `Table` per the `ecommerce-report-page` skill.
4. Offer: the top product's daily trend, or why a product dropped.
