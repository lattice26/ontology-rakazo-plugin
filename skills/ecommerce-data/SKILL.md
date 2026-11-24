---
name: ecommerce-data
description: Answer questions about the user's e-commerce business with real data — store sales, GMV, orders, traffic, conversion, products, creators and affiliates, videos, ads, refunds, settlements and market trends on TikTok Shop, Shopify or Amazon. Use whenever the answer depends on numbers from these sources.
---

1. Call `ask_ontology_agent` with the user's question in their own words. Keep relative dates
   ("yesterday", "last 7 days") exactly as said; the data agent resolves them in the shop's time zone.
   If this chat already has a `conversation_id` from an earlier call, pass it so the agent keeps
   the context.
2. Call `wait_ontology_agent` with the returned `turn_id` right away. It blocks until the answer is
   ready; if it says the turn is still running, call it again with the same `turn_id`. The progress card
   under the first call already shows the user each step live, so do not narrate the steps yourself.
3. Answer from what it returns. Keep every figure, currency and date range exactly; you may
   summarise, compare or add advice, but never change or invent numbers.
4. If the data agent needs the user to decide, the user usually gets a question card while
   `wait_ontology_agent` runs, and the wait continues by itself after they answer: do not ask again.
   Only when the wait returns `needs_user` ask the user yourself, then call `reply_ontology_agent`
   with the same `conversation_id` and their answer, and wait again.
5. If it cannot answer (unavailable or failed), tell the user why in plain words and offer its
   suggestions. Do not fill the gap with estimates.
6. If the user changes their mind while it runs, call `cancel_ontology_agent`.
7. For a recurring report ("every morning send me yesterday's GMV"), make a routine whose prompt is the
   question in the user's words with its relative dates, so each run asks the data agent afresh.
