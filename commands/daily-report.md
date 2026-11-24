---
description: A daily business report for a shop as a page, optionally kept up to date every morning. Use when the user runs /daily-report.
---

Make a daily report for the shop in $ARGUMENTS (if none, the user's main shop from memory).

1. Ask the data agent: "<shop> yesterday: GMV, orders, visitors and conversion, compared with the day
   before and the same day last week, plus the top 5 products by GMV."
2. Answer in a few lines (what moved and why it matters), per the `ecommerce-data-results` skill.
3. Build a dashboard page per the `ecommerce-report-page` skill.
4. Offer to keep it current: a routine every morning (the user's time) that asks the same question and
   updates this page, posting one line and the link.
