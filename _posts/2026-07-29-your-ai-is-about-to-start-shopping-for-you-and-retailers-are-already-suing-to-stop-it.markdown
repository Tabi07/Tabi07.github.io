---
layout: post
title: "Your AI Is About to Start Shopping For You — And Retailers Are Already Suing to Stop It"
date: 2026-07-29 00:00:00 +0000
categories: [ai, commerce]
tags: [agentic-commerce, ai-agents, payments, ecommerce]
image: /assets/ai-shopping.png
---

Somewhere in the last few months, "AI agent" quietly stopped meaning "chatbot that answers questions" and started meaning "thing that can actually spend your money." Not recommend a product. Not summarize reviews. Actually initiate the transaction, authorize the payment, and complete the order — while you're doing something else entirely. This is agentic commerce, and 2026 is turning into the year it stopped being a demo and started being a genuine fight over who controls the internet's checkout button.

## What Agentic Commerce Actually Means

The basic idea is simple enough: you tell an AI agent what you want — "reorder the printer ink we're low on," "find me a weekend bag under $150 with good reviews," "renew whichever SaaS subscriptions are expiring this month" — and the agent takes it from there. It plans the steps, compares options against your stated constraints, authorizes payment within limits you've set, and triggers fulfillment, without you clicking through a single product page.

That last part is the meaningful shift. A recommendation engine still hands control back to you at the moment of purchase. An agent doesn't. It receives a goal in natural language, plans the steps required to satisfy it, queries merchants or marketplaces, evaluates options against your constraints, authorizes a payment within preset limits, and triggers fulfillment — the whole loop, closed, on your behalf.

This isn't a niche experiment anymore. Consumer-facing versions are already live: Perplexity's Comet browser can shop and buy directly, Amazon's Rufus assistant now navigates external sites and completes purchases through a "Buy for Me" feature, and Google's AI Mode lets you check out from retailers like Etsy and Wayfair without ever leaving the search interface. On the enterprise side, tools tied to Microsoft Copilot and Salesforce Agentforce are already reordering office supplies, renewing SaaS subscriptions, and paying invoices on behalf of companies. Analysts at Boston Consulting Group project agent-led shopping could represent over a quarter of all e-commerce spending within the next few years — which is the kind of number that explains why every major payments company is suddenly racing to claim a piece of this.

## The Protocol War Nobody Outside Fintech Is Watching

Here's the part that doesn't make headlines but genuinely matters: for an AI agent to shop across different retailers, everyone needs to agree on a common language for how agents discover products, authenticate themselves, move money, and confirm an order actually happened. Right now, nobody agrees, and the resulting scramble is, by one description, the most contested standards war in payments history.

The current lineup is genuinely crowded. Google and Shopify launched the **Universal Commerce Protocol (UCP)** at NRF in January, backed by Etsy, Wayfair, Target, and Walmart, covering the full journey from product discovery through returns. OpenAI and Stripe built the **Agentic Commerce Protocol (ACP)**, focused on discovery and checkout inside ChatGPT. Google separately runs **AP2 (Agent Payments Protocol)**, developed with PayPal, specifically for the payment-authorization step. Stripe and Tempo shipped the **Machine Payments Protocol (MPP)** in March with over 100 partners on day one, including Visa, Mastercard, Anthropic, and OpenAI. Coinbase built **x402**, a crypto-native rail for agent-to-agent payments, since donated to neutral governance under the Linux Foundation with 40 member organizations backing it. And underneath almost all of it sits **MCP** — the protocol Anthropic originally built for connecting AI to tools and data, since donated to the Linux Foundation's new Agentic AI Foundation, which one industry tracker now describes as upstream of every commerce protocol in active use.

Visa and Mastercard aren't picking a side so much as hedging every side at once. Visa's Intelligent Commerce and Mastercard's Agent Suite are both built around what the industry calls "Know Your Agent" frameworks — registration, cryptographic signatures, and network tokens designed to distinguish legitimate agents from malicious bots, and Visa has gone further, offering merchants one integration that accepts agent-initiated payments across nearly every competing protocol at once, essentially betting that being the neutral middle layer beats picking a winner early.

If this sounds messy, that's because it is — and the mess itself is the actual story. One tracker studying the space put it plainly: fragmentation across competing standards is currently the biggest risk merchants face in agentic commerce, since it determines who can afford to be findable at all.

## The Lawsuit That's Actually Deciding This

While standards bodies argue over specs, a much blunter fight has been playing out in a federal courtroom in San Francisco — and it's the part of this story I think deserves more attention than it's getting.

In November 2025, Amazon sued Perplexity, accusing its Comet browser of accessing customer accounts on Amazon's site to shop and make purchases without Amazon's authorization, and of disguising that automated activity to look like ordinary human browsing. In March, a federal judge sided with Amazon, granting a preliminary injunction and finding Amazon likely to succeed on claims that Perplexity violated the federal Computer Fraud and Abuse Act. Perplexity appealed within a day, calling the fight one over "people's right to choose their own AI," and the Ninth Circuit granted a temporary stay while it considers the case — meaning, as of this writing, the fight is still very much unresolved.

Strip away the legal jargon and the actual question being litigated is almost philosophical: if you authorize an AI agent to act as you, does the platform get to decide it doesn't recognize that authorization? Amazon's answer is essentially "not on our terms, not without a partnership agreement." Perplexity's answer is "the user's consent should be enough." Neither side is obviously wrong, which is exactly why this is the case likely to set the template every other retailer follows. It's telling that Amazon's own CEO has publicly acknowledged agentic commerce "has a chance to be really good for e-commerce," while simultaneously suing the company doing it without Amazon's blessing — the objection isn't to agents shopping, it's to agents Amazon doesn't control doing it on Amazon's turf.

## Why Retailers Are Genuinely Nervous — Not Just Amazon

The deeper anxiety here isn't really about unauthorized scraping. It's about who owns the customer relationship once an AI agent sits between the retailer and the buyer. OpenAI actually walked back its own most aggressive move on this front: after launching "Instant Checkout" inside ChatGPT, it deprecated the buy-in-chat model by April 2026, shifting to a "discover in chat, transact on the merchant's own site" approach specifically so brands could keep customer relationships, login data, and loyalty engagement. Even the company building the agent decided full disintermediation was a step too far, at least for now.

There's a second layer to that anxiety, too. As agents become the thing doing the "browsing," being visible to them starts to matter as much as being visible in a Google search result — one analysis frames it bluntly: "being findable" increasingly overlaps with "being executable." Retailers whose product data isn't structured cleanly enough for an agent to parse risk becoming invisible to an entire emerging channel of commerce, regardless of how good their actual product or storefront is.

And underneath all of it sits the plainest obstacle of all. Surveyed merchants and consumers don't rank technical integration or protocol choice as the top barrier to agentic commerce — they rank trust. Juniper Research's most recent study on the space found trust the number-one barrier to agentic commerce deployment, ahead of every technical concern. That tracks: handing a piece of software your card details and letting it act autonomously is a genuinely different level of delegation than letting it draft an email.

## My Take

What I keep coming back to with agentic commerce is that it's not really a technology story — the technology (agents that plan, compare, and execute) is mostly already solved. It's a trust-and-control story wearing a technology costume, and those are much slower, much messier problems to work out than shipping a new API.

The Amazon-Perplexity case is the clearest evidence of that. Nobody in that dispute is arguing agents shouldn't shop — Amazon's own CEO said as much. The argument is entirely about who gets to sit in the middle of that transaction and on whose terms. That's not a question code can answer, and I don't think the standards war (UCP vs. ACP vs. AP2 vs. whatever comes next) is actually the bottleneck people think it is. Standards converge eventually; they almost always do. Trust and legal precedent converge much more slowly, and unevenly, one court ruling and one burned customer at a time.

If I had to bet, I'd guess the next twelve months look less like a clean technical rollout and more like what we're already seeing: a handful of retailers partnering openly (Etsy, Wayfair, Target), a handful litigating instead (Amazon), and a long messy middle of businesses waiting to see which approach actually protects them before committing either way. For anyone building in this space, the practical lesson isn't "pick the winning protocol" — it's that the businesses treating agent access as a trust relationship to be negotiated, rather than a technical integration to be shipped, are the ones who'll still be standing once this shakes out.
