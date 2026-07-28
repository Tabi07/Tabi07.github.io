---
layout: post
title: "Your Website Is About to Talk to AI Agents — Whether You've Prepared or Not (WebMCP Explained)"
date: 2026-07-28 00:00:00 +0000
categories: [ai, agents]
tags: [webmcp, mcp, ai-agents, web-standards]
image: /assets/webmcp.png
---

For the last year, every conversation about AI agents has focused on the agent’s side — better models, longer context windows, smarter orchestration. Almost no one’s been talking about the other half of that relationship: the websites the agents actually have to use. That’s changing quietly, and the protocol behind it — WebMCP — is worth understanding now, even though almost nobody has shipped it yet.

## The Problem WebMCP Is Trying to Fix

Right now, when an AI agent wants to do something on your site — search your catalog, check availability, fill out a form — it has exactly two options: parse the raw HTML and guess which button does what, or take a screenshot and click on pixel coordinates. Both approaches are slow, both are fragile, and both break the moment you ship a redesign. If you’ve ever watched an agent try to navigate a modern JavaScript-heavy site, you already know how clumsy this looks.

WebMCP proposes a third option: let the page tell the agent what it can do, directly. A site registers a set of typed functions in JavaScript — a name, a plain-language description, and a schema for the inputs — and the browser exposes those functions to whatever agent is driving the session. The agent calls them like an API. Your existing frontend code does the actual work.

A simplified example of what that looks like in practice:

```javascript
await document.modelContext.registerTool({
  name: "search-products",
  description: "Search the product catalogue and return matching items",
  inputSchema: {
    type: "object",
    properties: { query: { type: "string" }, maxResults: { type: "number" } },
    required: ["query"]
  },
  execute: async ({ query, maxResults = 10 }) => {
    return { content: [{ type: "text", text: JSON.stringify(await searchCatalogue(query, maxResults)) }] };
  }
});
```

If that name sounds familiar, it should — WebMCP borrows its tool concept directly from the Model Context Protocol (MCP) that Anthropic introduced for connecting AI systems to external tools and data. The difference is where it runs. MCP proper connects an AI application to a server somewhere. WebMCP runs the same idea inside the browser tab itself: the page registers the tools, and the browser handles the handoff to whatever agent is present.

## Who’s Actually Building This

WebMCP has an unusually credible pedigree for something this early. It’s a W3C Community Group draft co-edited by engineers from Microsoft and Google — not a scrappy side project. Its roots trace back to a 2025 open-source prototype called MCP-B, which proved the basic idea worked before Microsoft’s Edge team formally proposed the standard in August 2025, with Google joining shortly after as co-author.

Since then it’s moved fast by browser-standards timelines: a first draft report in February 2026, a public origin trial in Chrome starting at Google I/O in May, and experimental support landing in Edge behind a flag in June. As recently as July 21, the spec itself changed — the API relocated from `navigator.modelContext` to `document.modelContext`, meaning anyone who built against the earlier draft is already dealing with migration debt.

## The Uncomfortable Part: Almost Nobody Is Using It Yet

Here’s where I think most coverage of new web standards gets too breathless, so let me be blunt about where WebMCP actually stands: adoption right now is close to zero. Not “early stage” — actually close to zero. No mainstream AI agent calls these tools yet. Claude, ChatGPT Agent, Perplexity, and Gemini all still read pages the old way, by parsing the DOM or working from screenshots. Google has said Gemini in Chrome will be the first agent to consume WebMCP tools, but that hasn’t shipped as of this writing.

What does exist is a set of big-name pilot participants — Expedia, Booking.com, Shopify, Etsy, Instacart, Target, and others signed up for Chrome’s origin trial — which signals real interest from companies with agent-driven traffic to protect. But signing up for a trial isn’t the same as deploying tools in production, and none of those companies has confirmed they’ve actually done the latter yet.

There’s also a small but telling pattern: a cottage industry of “WebMCP checker” tools has sprung up faster than actual WebMCP implementations. When the tools that measure adoption of a standard outnumber the sites that have adopted it, that tells you something about which phase you’re in.

## Why This Matters Even Before It’s Widely Used

I’d normally be skeptical of covering a standard with essentially no real-world usage. But there are two reasons this one is worth paying attention to now rather than in twelve months:

**Chrome’s DevTools already grade you on it.** Since May, Lighthouse — the audit tool baked into Chrome that most SEO and dev teams already run — has shipped an “agentic-browsing” category with WebMCP-specific checks. Right now those checks mostly return “Not Applicable” because most sites haven’t implemented anything. But the moment that changes to an active warning, it lands on a lot of sprint backlogs at once. Getting ahead of that costs very little today.

**The security model deserves attention before the traffic does.** A WebMCP tool executes inside the page using the current user’s session. That’s what makes it genuinely useful — an agent can act as the logged-in user — and it’s also what makes it a real attack surface. If an agent gets manipulated by content it reads elsewhere (a classic prompt-injection scenario), it can call your legitimate tools with real session credentials. The practical mitigation is the same discipline good API design has always required: expose the narrowest tools possible, require explicit confirmation for anything that spends money or changes account data, and log every call. Treat a WebMCP tool the way you’d treat any public-facing endpoint, because that’s exactly what it is.

## My Take

What strikes me most about WebMCP isn’t the technology itself — registering typed functions for an AI to call is a pretty modest idea once you see it. It’s the timing problem underneath it. This is a classic two-sided standard: it only becomes valuable once both browsers expose it and agents actually call it, and right now only one side of that equation has moved. Google happens to control both halves — Chrome and Gemini — which is probably the only reason this doesn’t stall out the way several browser proposals before it have.

If I were running a site with meaningful agent traffic already — travel, e-commerce, anything with a lead form that converts — I’d treat the current quiet period as a genuine advantage rather than a reason to wait. Ship one or two tools where structure clearly beats scraping (site search and a lead form are the obvious starting points), keep the schemas simple, and put a human-confirmation step on anything with real-world consequences. For most other sites, the smarter move for the next several months is lower down the stack: making sure your content is actually readable and well-structured for the agents that are already crawling you today, before worrying about exposing interactive tools to agents that mostly don’t exist yet.

Standards like this tend to arrive in exactly this order — quietly, with almost no users, right up until one company flips a default and the adoption curve becomes a wall. WebMCP is sitting in that quiet window right now. Whether you build for it or just watch it, it’s worth knowing it’s there.
