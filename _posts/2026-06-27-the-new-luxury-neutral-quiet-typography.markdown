---
layout: post
title: "Your AI Has a Million-Token Context Window. It Can't Actually Use Most of It."
description: "New research shows every major AI model degrades as input length grows, even well before hitting its advertised context limit — a problem researchers call context rot."
date: 2026-06-27 16:00:00 +0000
categories: [ai, software]
tags: [context-rot, llm-research, ai-agents, context-engineering]
image: /assets/window.png
---

**The claim:** Modern AI models advertise context windows of 200,000, even 1 million tokens — enough to hold entire codebases or books in a single conversation. **The reality:** researchers at Chroma tested 18 frontier models systematically and found something the marketing pages don't mention: every single one gets measurably worse as the input grows, often long before it comes close to that advertised limit. Not some models. Not most. All of them. Here's what's actually happening, in plain terms.

#### Wait — isn't a bigger context window supposed to make AI *better*, not worse?

That's the intuitive assumption, and it's wrong in a specific, measurable way. A controlled study cited in recent research on the topic found reasoning accuracy falling from 0.92 to 0.68 as inputs grew from a few hundred tokens to just three thousand — a meaningful drop at a token count nowhere near any model's actual limit. A separate benchmark found ten of twelve tested models dropping below half their short-context performance by just 32,000 tokens, in models advertising context windows many times that size. The industry has a name for this now: **context rot**, formally described by Chroma's 2025 research as the systematic degradation of output quality as input length increases, independent of whether the content is even relevant.

#### Is this the same thing as "lost in the middle"?

Related, but not identical — and conflating the two has muddied a lot of coverage of this topic. Researchers now separate two distinct failure modes. **Positional degradation** ("lost in the middle") is the effect first documented back in a 2023 paper: accuracy depends heavily on *where* in the input the relevant information sits, following a U-shape — strong at the very start and end of a document, 20 to 30 points weaker for anything buried in the middle. **Length degradation** (context rot proper) is a separate phenomenon: accuracy declines simply as input grows *longer*, even when the relevant evidence is fixed in a favorable position the whole time. A model can have the right information sitting right where it should — and still perform worse just because there's more text around it.

#### Why would more text hurt a model that's specifically built to handle long documents?

One of the more counterintuitive findings in this research cuts against a natural assumption: coherent, well-organized input actually degrades a model's attention *more* than shuffled, disorganized input does. Researchers describe this as a signal-to-noise problem rather than a capability problem — the models are generally smart enough to solve the underlying task if their context stayed clean, but real context doesn't stay clean. As an AI agent works through a task, it accumulates search results, file reads, backtracking, and corrections, and all of that noise directly degrades the quality of every output that follows, even when the actual answer the agent needs was there from the start.

#### Does this actually matter outside a research paper, or is it mostly theoretical?

It matters enough that one analysis attributes nearly 65% of enterprise AI failures in 2025 to context drift or memory loss during multi-step reasoning — making this a leading practical cause of AI systems failing in production, not a lab curiosity. For coding agents specifically, researchers have identified a concrete, almost eerie threshold: agent success rate drops measurably after roughly 35 minutes of continuous work, and the relationship isn't linear — doubling the task duration roughly quadruples the failure rate. The explanation traces directly back to context accumulation: by the 35-minute mark, a typical coding agent has read 15–30 files and run multiple searches, accumulating somewhere between 80,000 and 150,000 tokens of context. Even inside a 200,000-token window nowhere near full, the signal-to-noise ratio has already degraded enough for reasoning quality to measurably drop. Worse, this compounds on itself: a less accurate agent makes more mistakes, mistakes require corrections, and corrections mean reading more files and running more searches — adding yet more noise to an already degraded context, in a loop that gets harder to escape the longer it runs.

#### So the "200K token" or "1M token" number on a model's spec sheet is basically fiction?

Not fiction, exactly, but importantly not the number to plan around. One analysis of the gap between advertised and effective context length put it starkly: models typically become unreliable 30–40% before their claimed limit — meaning a model advertised at 200,000 tokens may become genuinely unreliable around 130,000 tokens of real, working content. Performance drops are also often sudden rather than gradual, showing up as sharp cliffs rather than a smooth decline you could anticipate and plan for. Roughly two-thirds of tested models in one benchmark failed to reliably find a single simple sentence in a document just 2,000 tokens long — a task far below what any of these models' advertised limits would suggest should be trivial.

#### Okay, so is the fix just "stuff less into the context"?

That's the instinct, and it's only half right. Pure retrieval-based approaches (pulling in only the specific relevant snippet rather than dumping in everything) avoid context rot but miss a different capability: genuine reasoning across an entire document that requires holding the whole thing in view at once. The 2026 architectural default emerging from this research is a hybrid: retrieve a focused 50,000–200,000 relevant tokens first, then reason over that curated set at length, rather than either extreme. Researchers frame the real design question as no longer "which approach wins" but "which pattern fits this specific data shape, latency budget, and freshness requirement" — architecture-level thinking rather than chasing a bigger context-window number on a spec sheet.

Concrete techniques are already showing measurable results. Anthropic's own Claude Code uses native auto-compaction that, in documented sessions, reduced 132,000 tokens of accumulated message history down to roughly 2,300 tokens — a 98% reduction — specifically to keep working context clean during long agent sessions. Newer research frameworks go further, letting an agent "fold" a completed sub-task into a brief summary rather than keeping every intermediate step in view, and benchmarked results show these approaches outperforming standard long-context handling at every tested length between 32,000 tokens and 1 million.

#### Is this a permanent limitation of how these models work, or something that gets fixed?

The researchers behind the most rigorous mechanistic study of this problem are explicit that it isn't a law of nature — their findings describe the dominant transformer architecture as deployed through early 2026 specifically, and note that a genuinely different architectural approach to attention or position encoding could weaken or eliminate the effect entirely. They frame that possibility in an unusual way for a research paper: as "the desirable kind of obsolescence" — meaning the researchers documenting this limitation are actively hoping their own findings get outdated by better architecture, rather than defending them as a permanent ceiling.

#### What's the actual takeaway if you're building on top of these models today?

Stop treating the advertised context window as a budget to spend freely. Treat it as a resource that degrades in quality well before it runs out numerically, and architect around that reality rather than around the number printed on a pricing page. For anyone running long AI coding sessions specifically, the 35-minute, compounding-failure pattern is worth knowing by name, because the practical fix isn't "wait for a bigger context window" — it's actively managing what stays in that window as a session runs, the same way a good engineer manages memory in any other system that degrades under uncontrolled growth.
