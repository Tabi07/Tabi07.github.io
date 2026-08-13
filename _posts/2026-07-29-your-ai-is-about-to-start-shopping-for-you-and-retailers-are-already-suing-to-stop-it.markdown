---
layout: post

title: "Amazon vs. Perplexity: The Lawsuit That Will Decide Who Controls Your AI's Shopping Cart"

description: "Agentic commerce is changing online shopping as AI agents begin to browse, compare, and buy on your behalf — and retailers are racing to respond."

date: 2026-07-29 00:00:00 +0000

categories: [ai, commerce]

tags: [agentic-commerce, ai-agents, payments, ecommerce]

image: /assets/ai-shopping.png
---

"AI agent" used to mean a chatbot that answered questions. It increasingly means something that can actually spend your money — plan a purchase, compare options, authorize payment, and complete the order, without you clicking through a single product page. That shift has quietly triggered a genuine fight over who controls the internet's checkout button, and it's playing out on three fronts at once: a standards war nobody outside fintech is watching, a live federal lawsuit, and a much older question — trust — that no protocol can solve on its own.

### What Agentic Commerce Actually Looks Like Right Now

This isn't a future scenario. Consumer versions are already live: Perplexity's Comet browser shops and buys directly, Amazon's Rufus assistant navigates external sites and completes purchases through a "Buy for Me" feature, and Google's AI Mode lets you check out from retailers like Etsy and Wayfair without leaving the search interface. On the enterprise side, tools tied to Microsoft Copilot and Salesforce Agentforce are already reordering office supplies, renewing SaaS subscriptions, and paying invoices on companies' behalf. Boston Consulting Group projects agent-led shopping could represent over a quarter of all e-commerce spending within a few years — the kind of number that explains why every major payments company is racing to claim a piece of it.

### Front One: The Standards War

For an AI agent to shop across different retailers, everyone needs to agree on a shared language for how agents discover products, authenticate themselves, move money, and confirm an order happened. Right now, nobody agrees, and one tracker has described the resulting scramble as the most contested standards war in payments history.

The current field: Google and Shopify's **Universal Commerce Protocol (UCP)**, backed by Etsy, Wayfair, Target, and Walmart. OpenAI and Stripe's **Agentic Commerce Protocol (ACP)**, built for checkout inside ChatGPT. Google's separate **AP2**, developed with PayPal for payment authorization specifically. Stripe and Tempo's **Machine Payments Protocol (MPP)**, launched in March with over 100 partners on day one, including Visa, Mastercard, Anthropic, and OpenAI. Coinbase's crypto-native **x402**, now under neutral Linux Foundation governance with 40 member organizations. And underneath most of it, **MCP** — Anthropic's original protocol for connecting AI to tools and data, also now under the Linux Foundation, which one industry tracker calls upstream of every commerce protocol currently in active use.

Visa and Mastercard aren't picking a side so much as hedging every side at once, building "Know Your Agent" frameworks — registration, cryptographic signatures, network tokens — designed to distinguish legitimate agents from malicious bots regardless of which protocol wins. Visa has gone further, offering merchants one integration that accepts agent-initiated payments across nearly every competing protocol simultaneously. The mess itself is the actual story here: fragmentation across competing standards is currently the single biggest risk merchants face, since it determines who can even afford to be findable by an agent at all.

### Front Two: The Lawsuit That Matters More Than Any Protocol

While standards bodies argue over specs, the fight that will actually shape this industry has been playing out in a federal courtroom in San Francisco. In November 2025, Amazon sued Perplexity, accusing its Comet browser of accessing customer accounts on Amazon's site without authorization and disguising that automated activity to look like ordinary human browsing. In March, a federal judge sided with Amazon, granting a preliminary injunction and finding Amazon likely to succeed on claims that Perplexity violated the federal Computer Fraud and Abuse Act. Perplexity appealed within a day, framing the fight as one over "people's right to choose their own AI." The Ninth Circuit granted a temporary stay while it considers the case — as of this writing, still unresolved.

Strip away the legal language and the actual question is almost philosophical: if you authorize an AI agent to act as you, does the platform get to decide it doesn't recognize that authorization? Amazon's position, in effect: not without a partnership agreement. Perplexity's position: a user's consent should be enough. Neither side is obviously wrong, which is exactly why this case is likely to set the template every other retailer follows. Tellingly, Amazon's own CEO has publicly acknowledged agentic commerce "has a chance to be really good for e-commerce" — while his company simultaneously sues the one doing it without Amazon's blessing. The objection was never to agents shopping. It's to agents Amazon doesn't control doing it on Amazon's turf.

### Front Three: Trust, Which No Protocol Can Fix

Even OpenAI, the company most aggressively pushing in-chat commerce, backed off its most ambitious move. After launching "Instant Checkout" inside ChatGPT, it deprecated the buy-in-chat model by April 2026, shifting to a "discover in chat, transact on the merchant's own site" approach specifically so brands could retain customer relationships, login data, and loyalty engagement. Even the company building the agent decided full disintermediation was a step too far.

There's a second, quieter anxiety layered on top: as agents become the thing doing the "browsing," being visible to them starts to matter as much as ranking in a Google search. One analysis frames it bluntly — "being findable" increasingly overlaps with "being executable." Retailers whose product data isn't structured cleanly enough for an agent to parse risk becoming invisible to an entire emerging commerce channel, regardless of how good their actual storefront is.

But the plainest obstacle sits above all of this. Surveyed merchants and consumers don't rank technical integration or protocol choice as the top barrier to agentic commerce — they rank trust. Juniper Research found trust the number-one barrier to deployment, ahead of every technical concern. That tracks: handing software your card details and letting it act autonomously is a fundamentally different level of delegation than letting it draft an email.

### What This Actually Adds Up To

Agentic commerce isn't really a technology story — the underlying capability, agents that plan, compare, and execute, is mostly already solved. It's a trust-and-control story wearing a technology costume, and those problems resolve far more slowly and unevenly than shipping a new API ever does.

The Amazon-Perplexity case makes that plain. Nobody in that dispute is arguing agents shouldn't shop — Amazon's own CEO said as much. The fight is entirely over who sits in the middle of that transaction, and on whose terms. Code doesn't answer that question. Standards, meanwhile, tend to converge eventually regardless of how messy the current field looks — they almost always do. Trust and legal precedent converge far more slowly, one court ruling and one burned customer at a time.

The next twelve months probably won't look like a clean technical rollout. They'll likely look like what's already happening: a handful of retailers partnering openly (Etsy, Wayfair, Target), a handful litigating instead (Amazon), and a long, messy middle of businesses waiting to see which approach actually protects them before committing either way. The practical lesson for anyone building in this space isn't "pick the winning protocol." It's that the businesses treating agent access as a trust relationship to be negotiated — not a technical integration to be shipped — are the ones still standing once this actually shakes out.
