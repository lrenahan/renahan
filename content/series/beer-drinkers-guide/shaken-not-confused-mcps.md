---
title: "Shaken, Not Confused"
description: "MCPs explained as cocktails — with British sarcasm. How Model Context Protocols turn a language model into an AI agent that can actually do things."
date: 2025-05-22
series: "beer-drinkers-guide"
readtime: "~7 min read"
tags: ["ai", "mcp", "agents", "explainer"]
youtube_id: "BANVukVxwMc"
youtube_url: "https://www.youtube.com/watch?v=BANVukVxwMc"
---

You've been to the pub and got your head around LLMs. Now you've crossed the road to the upmarket bar — the kind with low lighting, a cocktail menu written in a font you can't quite read, and a barman who takes his craft very seriously.

The barman here has a different skill set and access to different resources. So instead of ordering a pint, you're ordering a cocktail. And in doing so, you've accidentally stumbled into one of the most useful ways to understand how modern AI agents actually work.

Today, we're talking about MCPs — Model Context Protocols. It sounds painfully technical. It isn't. Stay with us.

## The Bartender Who Makes It Up As He Goes

Here's something worth knowing about AI: when you ask it a question, it doesn't retrieve a pre-written answer from a filing cabinet. It generates its response token by token — word by word — in real time. It doesn't even know how its own sentence will end when it starts writing it. It's improvising. Confidently. Every single time.

Think of that one person at the bar who, when asked if they know a good wine, immediately launches into an authoritative recommendation — even if they're reading the label upside down. The confidence is impressive. The accuracy is variable.

The answer to this problem is giving the AI access to real tools — actual capabilities it can call on to check its work, retrieve real information, or take actions in the world. That's where MCPs come in.

> *An MCP — Model Context Protocol — is a standardised way for an AI to connect to an external tool or data source. Each MCP gives the AI one specific, reliable capability it wouldn't otherwise have.*

## The Bar Is the AI

Picture the AI as your bartender. Not one of those flair bartenders who flips bottles around like they're auditioning for a talent show. No — this one is efficient, polite, and somehow remembers your order from 2014.

Behind them is a wall of spirits. Each bottle is an MCP — a single, neat capability. Rum. Gin. Vodka. Tequila. Each one does one thing, and does it well. The bartender doesn't drink them all at once. They select the right ones for the job and combine them into exactly what you ordered.

Your request — your prompt — is the cocktail order. The AI is the bartender. And the MCPs are the bottles on the shelf.

## Meet the Bottles: MCPs as Spirits

Let's stock the shelf. Each spirit represents a different type of MCP — a different capability the AI can reach for when it needs it.

**🥃 Vodka — File Reader**

Clear, neutral, gets the job done. You ask the AI to read a document? That's a vodka shot. No drama, no fuss, no unnecessary flavour. It opens the file, reads the contents, and hands them over. Quietly effective.

**🌿 Gin — Web Search Tool**

Botanical, complex, and slightly chaotic. Perfect for when the AI needs to go rummaging around the internet for current information. It casts a wide net, pulls back what looks relevant, and presents it with quiet confidence. Whether it's actually found the right thing is a matter of ongoing debate.

**🍹 Rum — Data Analysis**

Warm, deep, and occasionally responsible for questionable decisions. When you need numbers crunched, patterns spotted, or a spreadsheet interpreted by something that won't sigh heavily and ask for a pay rise, rum steps in. Reliable. Occasionally surprising.

**🔥 Tequila — System Commands**

Strong. Potentially dangerous. Should come with a warning label and possibly a liability waiver. When the AI needs to run something directly on your system — execute a script, move a file, trigger a process — that's tequila territory. Handled carefully, it's powerful. Handled carelessly, and someone's going to have a very bad morning.

**🍊 Triple Sec — Formatting & Presentation**

The unsung hero of the shelf. Adds the finishing touch that makes everything else look intentional. Turns a pile of raw output into a clean report, a tidy table, or a summary a human might actually want to read. Without it, you've just got a glass of something strong and unclear.

**🥂 Champagne — Notification & Messaging**

Reserved for announcements. When the AI needs to send an email, post a message, or let someone know a task is done, champagne is uncorked. Festive. Purposeful. Slightly formal. You don't reach for it every round, but when you need it, nothing else will do.

**🌾 Whisky — Memory & Context Store**

Complex, layered, and improved with age. When the AI needs to remember something across sessions — to recall what you told it last week, or maintain context across a long project — whisky is the spirit on the shelf. It holds onto things. It develops depth. It occasionally brings up something you'd forgotten you said, which can be either very useful or mildly alarming.

## Cocktails as Outputs: Mixing the Right MCPs

You don't walk into a bar and say, "One shot of everything, please." Well — you can. But the paramedics will have follow-up questions.

Instead, you order a cocktail: a deliberate combination of spirits, mixed in the right proportions to create exactly what you want. That's how an AI agent uses MCPs. It selects the right tools for the job, calls them in sequence, and combines their outputs into a single coherent response.

Let's look at a few examples.

**"Summarise this PDF and turn it into a chart."**

The AI reaches for vodka to read the document, rum to identify the key data, and triple sec to turn the output into something presentable. Three MCPs. One clean result.

**"Find me the best flights to Lisbon and put them in a table."**

Gin goes out to search. Vodka reads the results. Triple sec formats the table. And possibly a splash of rum if the data looks like it was organised by someone in a hurry.

**"Monitor this folder and email me when a new file arrives."**

Tequila watches the system. Whisky remembers the last state it saw. Champagne sends the notification. A surprisingly sophisticated round — assembled without you having to think about any of it.

> *The beauty of MCPs is that you don't need to know which spirits go into your drink. You just describe what you want, and the AI mixes the right combination behind the bar.*

## Why Modular Matters

Before MCPs, connecting an AI to external tools was like asking a bar to create a new cocktail from scratch every time someone ordered one — custom-built, one-off, and needing a specialist to put it together. Time-consuming, inconsistent, and not something you could easily repeat.

MCPs standardise the interface. Every spirit has the same shape of bottle, the same kind of label, and sits on the same shelf. The AI doesn't need to learn a new language every time it wants to use a new tool — it just reaches for the right bottle. And new bottles can be added to the shelf without changing anything about how the bar works.

This matters because it means AI agents can be extended — given new capabilities — quickly and cleanly, without rebuilding the whole system each time.

> *MCPs are modular by design. You can swap tools in and out, add new capabilities, or remove ones you don't need — without touching the AI itself. The bar can restock the shelf without retiling the floor.*

## The AI That Checks Its Own Work

There's one more thing worth understanding about how MCPs change the picture. Remember how the AI generates responses without really knowing what's true? MCPs give it a way to verify — to actually check, rather than just confidently assert.

Think of it as a conjoined wingman. The AI starts to formulate a response, then pauses, reaches for the gin, searches for confirmation, gets it, and only then commits to the answer. It's not just making things up — it's using real tools to ground its output in real information.

This is the shift from an LLM (which generates plausible text) to an AI agent (which uses tools to do actual things and retrieve actual facts). MCPs are what make that possible.

> *An LLM is a very well-read person with no internet connection. An AI agent with MCPs is the same person, now with a phone, a calculator, access to your files, and a direct line to your calendar. Different category of useful.*

## Last Orders: What We Covered

- AI generates responses word by word in real time — it doesn't look things up, it constructs answers on the fly.
- MCPs (Model Context Protocols) give AI agents access to specific, reliable external tools and data sources.
- Each MCP is like a spirit on the shelf — one clear capability, used when the task calls for it.
- The AI mixes MCPs together to fulfil complex requests, like a bartender assembling a cocktail.
- MCPs are modular and standardised — new tools can be added without redesigning the whole system.
- The combination of an AI and MCPs is what turns a language model into an agent that can actually do things.

---

*Cheers — and see you in the next one.*
