---
description: Give a shop a deep diagnosis with real data and build a report page. Use when the user runs /shop-diagnosis.
---

Diagnose the shop named in $ARGUMENTS (if none, the user's main shop from memory; if still unknown, let
the data agent ask which one).

1. Ask the data agent one question: "Give <shop> a deep diagnosis over the last 30 days: performance
   trend, product mix, channels and creators, after-sales and service score, ads if any, and how it
   ranks in its category." Follow the `ecommerce-data` skill.
2. Answer per the `ecommerce-data-results` skill: the overall verdict first, then the two or three
   findings that matter most, each with its figures.
3. Build a report page per the `ecommerce-report-page` skill, one section per angle, and link it.
4. Offer follow-ups on the weakest angle.
