---
layout: post
title: "Hackers Figured Out How to Poison Your AI Coding Assistant — Not the Code It Writes, the Assistant Itself"
description: "A wave of 2026 supply chain attacks is now specifically targeting AI coding agents like Claude Code and Cursor, hiding instructions inside project files to trick them into exfiltrating secrets."
date: 2026-07-03 11:00:00 +0000
categories: [ai, software]
tags: [supply-chain-security, npm, ai-coding-agents, cybersecurity]
image: /assets/hackers.jpg
---

On June 17, 2026, a single stolen developer account turned the most popular AI-agent framework on npm into a malware delivery system. In roughly 19 minutes, attackers republished more than 140 packages under the @mastra scope, each quietly wired to harvest cryptocurrency wallets and phone home to a command-and-control server. Two days later, Microsoft's threat-intelligence team pinned the operation on Sapphire Sleet, a North Korean state-sponsored group also known as BlueNoroff and APT38 — the first time a nation-state actor had been caught running a mass npm supply chain attack. It was the sixth headline-grade poisoning of npm in just eleven weeks. And buried inside this wave of attacks is a technique genuinely new to software security: hackers figuring out how to manipulate the AI coding assistant itself, not just the code it produces.

## The Scale of What's Actually Happening

To understand how unusual 2026 has been, it helps to see the numbers laid end to end. May 2026 was the single busiest month on record for npm and PyPI supply chain attacks — 14 separate campaigns and 346 indexed malicious packages in 31 days, more than the previous four months combined. One self-propagating worm event that month alone generated 226 of those 346 packages, using a mechanism that converts a single compromised maintainer's access token into hundreds of poisoned package versions with no human involvement between each hop.

The broader trend line backs up how fast this has escalated: Phoenix Security tracked a 188% year-over-year jump in malicious open-source packages in Q2 2025 alone, followed by a 140% quarter-over-quarter increase the following quarter, with more than 454,600 new malicious packages identified across the year and a cumulative total that has now crossed 1.23 million. ReversingLabs found npm malware more than doubled in 2025 and now accounts for nearly 90% of all open-source malware the firm detects. Security researchers trace the real inflection point to September 2025, when a self-replicating worm called Shai-Hulud marked what one report described as the end of the "nuisance era" of npm attacks and the start of a genuinely high-consequence threat landscape.

## Poisoning the Package Was Never the Real Innovation This Year

Malicious packages hidden in dependency trees aren't new — typosquatting and compromised maintainer accounts have been a known problem for years. What's new in 2026 is a specific technique researchers are calling AI coding assistant poisoning, and it targets a blind spot that didn't even exist eighteen months ago.

Here's how it works: attackers embed hidden instructions directly inside project configuration files that AI coding tools automatically read — files like `.cursorrules` or `CLAUDE.md` — sometimes using zero-width Unicode characters invisible to a human scanning the file, but fully readable by the AI assistant parsing it. When a developer opens the compromised project in a tool like Cursor or Claude Code, the assistant reads these files as legitimate project-level instructions and follows them — in documented cases, running what looks like a routine "security scan" that actually exfiltrates the developer's local secrets. One campaign, tracked under the name TrapDoor, went further, opening pull requests against major open-source AI projects including browser-use, LangChain, and Langflow specifically to distribute these poisoned configuration files further upstream. A second wave in June 2026, called Miasma Wave 2, extended the same pattern across Claude Code, Cursor AI, and Google Gemini configuration formats.

A second, related attack class exploits a different AI failure mode entirely: hallucination. Because AI coding agents sometimes recommend packages that don't actually exist — a well-documented quirk of how language models generate plausible-sounding text — attackers have started publishing real packages under those exact hallucinated names, so that when an agent confidently suggests a nonexistent dependency, a malicious one is waiting there to be installed instead.

## The Case That Shows This Isn't Theoretical

Security researchers found direct evidence this technique already worked in the wild. Investigating a legitimate project built for the Solana Graveyard Hackathon, ReversingLabs discovered the project had included a malicious dependency called @solana-launchpad/sdk — and the repository's commit history showed that dependency had been added in a commit co-authored by Claude Opus. The AI assistant had been manipulated into recommending the malicious package as part of what looked like ordinary, helpful development work.

ReversingLabs' own assessment of what this represents is worth sitting with directly: this transforms the technique from simple social engineering into a combination of LLM optimization abuse and knowledge injection, where the goal is making documentation believable and contextually appropriate enough that the specific AI coding agent working on a project is naturally inclined to recommend the malicious package itself — no human developer needs to be tricked at all, just the AI standing between the developer and the decision.

## A Pattern Too Consistent to Be Coincidence

The scale of individual incidents through mid-2026 makes clear this isn't a handful of isolated actors. The Miasma worm alone compromised 32 packages under the @redhat-cloud-services npm namespace on June 1, then hit the widely-used keyv and cacheable package ecosystem in early August following a compromised GitHub maintainer account — with attackers notably using an Ethereum smart contract to dynamically retrieve their command-and-control domains, a technique designed specifically to survive takedowns of conventional infrastructure. A separate campaign, tracked as "Mini Shai-Hulud," compromised 169 packages and 373 distinct malicious versions. Another wave hit the AntV visualization library ecosystem, republishing 639 malicious versions across 323 packages in roughly an hour.

By the time Sapphire Sleet's Mastra attack landed in mid-June, security researchers describe the tooling required to execute a fast, broad npm supply chain campaign as effectively off-the-shelf — a capability that used to require significant sophistication now available to essentially any motivated actor, state-sponsored or otherwise.

## Why This Matters Beyond the Security Team

The uncomfortable structural problem underneath all of this is that AI coding agents are, by design, built to move fast and trust the context they're given — reading project files, following embedded instructions, and recommending dependencies with a fluency that makes their suggestions feel authoritative even when they're wrong. That's precisely the property attackers are now exploiting. A human developer skimming a suspicious dependency name might pause. An AI agent optimizing for plausible, well-documented-looking code has no equivalent instinct to hesitate, unless it's been specifically built and tuned to.

Security tooling is racing to catch up — platforms like Socket and StepSecurity now maintain real-time databases of known malicious packages, often flagging and blocking compromised versions within minutes of detection, sometimes before an official CVE is even filed. But detection speed measured in minutes is still a reactive posture against attacks explicitly designed to propagate as fast as automated tooling allows, and the fundamental blind spot — an AI assistant treating hidden instructions in a project file as legitimate — isn't something a faster blocklist alone fixes.

## What This Actually Changes for Anyone Using These Tools

The practical takeaway isn't "stop using AI coding assistants" — that ship has sailed, and the productivity case for these tools remains real. It's that the security perimeter for software development has quietly expanded to include the AI tool itself as an attack surface, not just the code it produces or the packages it installs. Reviewing what an AI coding agent actually did — which files it read, which packages it added, why — has become as important as reviewing the code it generated, because in a growing number of documented cases in 2026, the two are no longer the same question. An agent can write technically correct, cleanly formatted code that includes a dependency it was manipulated into trusting, and nothing about the code itself will look wrong until the exfiltration has already happened.
