---
title: "Who Contributes to Chrome"
date: 2026-09-27T10:00:00+02:00
categories: ["License"]
---
Chrome is built on Chromium, an open source project under the permissive BSD license. Google writes the large majority of its code. The rest comes from companies like Microsoft, Igalia, Intel, Samsung, Opera and a long tail of individuals.

Many browsers ship on top of it: Edge, Brave, Opera, Vivaldi. They take everything Google publishes and add their own layer. The BSD license lets them keep that layer closed. So the flow is mostly one-way: public work flows into private products, private work rarely flows back.

Why does it still work? Because private forks are expensive. Every Chromium release, each fork has to merge upstream changes into its own patches. The bigger the patch set, the higher the cost. That is why Microsoft upstreams much of its work instead of keeping it: sharing is cheaper than maintaining. The market, not the license, enforces part of the reciprocity.

But only part. A fork gets every public improvement plus its own secret ones. If the secret part is small, merge costs win and it gets shared. If the secret part is the core of the product, the fork can stay ahead forever. For a browser, the engine is shared and the differentiation sits on top, so it works. For a search service, the ranking is the product, so a closed fork can win on quality. That is the gap AGPL closes and GPLv2 leaves open for services.

If you are the open alternative to closed SaaS, a closed fork of you is not really your competitor. It becomes just another closed SaaS, the thing your customers are choosing to avoid. They pick you because they can read the code, self-host it, and not depend on one vendor.

In the age of AI this matters more. Code gets cheap to write, so keeping it secret protects less. AI makes more decisions for people, so being able to inspect it matters more. What lasts is trust, community and speed, and openness helps with all three.
