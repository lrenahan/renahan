---
title: "Last Orders at the Language Model"
description: "How LLMs actually work — not the marketing version. Grab a stool, we're explaining one of the most significant technologies of the past decade using beer."
date: 2025-05-15
series: "beer-drinkers-guide"
readtime: "~8 min read"
tags: ["llm", "ai", "machine-learning", "explainer"]
youtube_id: "SUdRmuj3XVc"
youtube_url: "https://www.youtube.com/watch?v=SUdRmuj3XVc"
---

Ever wondered how a Large Language Model actually works? Not the marketing version — the real version. Grab a stool. We're going to explain one of the most significant technologies of the past decade using beer. Obviously.

When you type a prompt into an AI — something like "Write me a poem about ordering a beer" — you're walking up to a bar and placing an order. You tell the bartender what you want. The bartender nods. And behind the scenes, the brewery kicks into action.

## Before Any Beer Gets Poured: The Ingredients

Before a brewery can make anything, it needs ingredients. Malt, hops, yeast, water — each one contributes something to the final product. Without them, there's nothing to brew with.

For a Large Language Model, the ingredients are text. Enormous, almost incomprehensible quantities of it: books, articles, websites, conversations, code, academic papers, forum threads. The model doesn't memorise every sentence it encounters — that would be like a brewer trying to remember every individual hop pellet. Instead, it learns patterns. Which words tend to appear near which other words. How sentences are structured. What ideas are connected. Just like a brewer learns which hops create which flavours, the model learns which linguistic combinations create which meanings.

> *An LLM doesn't know facts the way a textbook does. It knows patterns the way an expert brewer knows flavour — through exposure, repetition, and a lot of refinement.*

## Crushing the Grain: Tokenisation

In the first stage of brewing, the grain gets crushed. This isn't about destruction — it's about preparation. Crushing exposes more surface area, making it easier for the water to extract the sugars needed for fermentation.

In an LLM, the equivalent step is called **tokenisation**. Before the model can process any text, it chops it into small pieces called tokens. A token might be a whole word, a part of a word, a punctuation mark, or even a single character. The sentence "Write me a poem about ordering a beer" might become something like: `[Write] [me] [a] [poem] [about] [order] [ing] [a] [beer]`.

Just like crushed grain is easier to brew with than whole barley, tokens make text easier for the model to work with. They're the raw material everything else is built from.

> *Tokenisation is why LLMs occasionally stumble on unusual words or names — if a word gets split in an unexpected way, the model is working with unfamiliar grain.*

## The Flavour Profile: Embeddings

Once the grain is crushed, a brewer doesn't just see "grain" — they see a specific set of characteristics. This malt is nutty. That one's roasty. This one will give the beer a rich amber colour. Each ingredient has a flavour profile that describes what it brings to the mix.

In an LLM, each token gets turned into an **embedding** — a kind of numerical flavour profile. Rather than storing a token as just a word, the model represents it as a long list of numbers that encode its meaning and its relationships to other words. The model learns that "poem" sits close to "creative", "verse" and "lyric" in this numerical space. That "order" relates to bars, restaurants, and queues. That "IPA" is what people ask for when they want to look knowledgeable.

These embeddings are crucial because they let the model understand not just what a word is, but what it means in context — and how it relates to everything else in the sentence.

> *Two words can look completely different but have very similar embeddings if they mean similar things. "Pub" and "bar" end up very close together in embedding space. "Pub" and "parliament" — perhaps closer than you'd hope.*

## Paying Attention: The Transformer's Attention Mechanism

A good brewer doesn't treat every ingredient equally. Some hops dominate the aroma. Some malts define the body. Knowing which ingredients matter most — and how they interact — is what separates a great brew from a mediocre one.

In an LLM, this is handled by something called the **attention mechanism**, which sits at the heart of the transformer architecture that underpins most modern AI models. When processing a prompt, the model looks at all the tokens simultaneously and calculates which ones are most relevant to each other. In the sentence "Write me a poem about ordering a beer", the word "poem" needs to pay a lot of attention to "creative" and "write" — and rather less attention to "a".

It's the bartender paying close attention to your actual drink order, rather than the extended personal backstory you felt the need to share first.

> *Attention is what lets LLMs handle long, complex sentences without losing track of what's connected to what. It's the mechanism that makes context possible — and it's genuinely one of the most elegant ideas in modern computer science.*

## The Mash Tun: Training and Parameters

Now the real brewing begins. The mash tun is where the crushed grain and hot water combine, allowing enzymes to convert starches into sugars. Everything interacts. Flavours develop. The character of the beer starts to emerge.

In an LLM, **training** is where everything comes together. The model processes billions of tokens, adjusting millions — sometimes hundreds of billions — of internal values called **parameters**. These aren't facts stored in a database. They're more like the precise settings on a vast mixing desk: each one slightly influencing how the model interprets language, how it weighs relationships between words, and how it generates responses.

During training, the model makes predictions ("what word comes next?"), compares them to the actual answer, and adjusts its parameters to do slightly better next time. This happens billions of times across the training dataset. It's not memorising. It's learning relationships:

- which words tend to follow which others
- how sentences are structured across different styles and topics
- what ideas connect, contradict, or qualify each other
- and that "hold my beer" rarely ends well for anyone involved

> *The parameters of a large model are the distilled result of processing more text than any human could read in a thousand lifetimes. They're not a knowledge base. They're a finely tuned intuition about language.*

## Into the Kegs: The Trained Model

Once a beer is brewed, it goes into kegs and gets connected to the taps. The hard work is done. The flavours are set. When someone orders a pint, the bar doesn't re-brew the beer from scratch — it just pours from what's already been prepared.

A trained LLM works the same way. Training happens once (or periodically, with updates). After that, the model's parameters are fixed. When you send it a prompt, it doesn't re-learn anything or re-read the internet. It just draws on what it already learned during training and uses that to generate a response.

This is an important point that's often misunderstood: a standard LLM isn't searching for information in real time. It's pouring from a keg that was filled during training. Which is why models have knowledge cutoff dates — the keg was filled at a particular moment, and it doesn't automatically update.

> *When an LLM gets something wrong about recent events, it's not being lazy. The keg was filled before that event happened. It's serving what it has.*

## The Pour: Token Generation

The bartender starts pouring. For an LLM, this is the **generation** step — and it's worth understanding exactly how it works, because it's quite different from how most people imagine it.

The model doesn't compose an entire response and then deliver it. It predicts one token at a time. It looks at your prompt, predicts the most likely next token, adds that token to the context, and then predicts the next one. Then the next. Then the next. Each prediction is informed by everything that came before it — both your original prompt and all the tokens generated so far.

Just like a smooth pour depends on pressure, angle, and the shape of the glass, the quality of the output depends on the model's training, the structure of the prompt, and a setting called **temperature** — which controls how much randomness is introduced into each token selection. Low temperature gives you predictable, conservative responses. High temperature gives you more creative, varied ones. Turn it up too far and the output starts to resemble a closing-time monologue from someone who's had too many.

> *This is why LLMs sometimes trail off, repeat themselves, or take an unexpected turn mid-response. Each token is a fresh prediction. The model is always working from the edge of what's been said so far.*

## Why Every Pint Pours Slightly Differently: Probability

No two pints poured from the same keg are completely identical. The head varies. The pour angle matters. There's inherent variation in the process.

LLMs work on **probability**. At each step, the model assigns a likelihood to every possible next token — and then selects from among the high-probability options, with some controlled randomness built in. This is why if you ask the same question twice, you'll often get subtly different answers. The keg is the same. The pour varies.

It's also why the model genuinely doesn't know how a sentence will end when it starts generating it. It's not retrieving a pre-written answer. It's making a probabilistic decision, one token at a time, all the way to the final full stop. A bit like someone confidently beginning a story at last orders — utterly certain about the opening, considerably less certain about the ending.

> *Probability is a feature, not a bug. It's what allows LLMs to be creative, varied, and contextually appropriate — rather than producing the same mechanical response every time.*

## How Big Is the Glass? Context Windows

Every glass has a limit. You can't pour an infinite amount of beer into a pint glass — at some point, it overflows and the floor gets involved.

LLMs have a **context window**: a limit on how many tokens they can consider at once. Everything inside the window — your prompt, the conversation history, any documents you've shared — is what the model can "see" when generating a response. Everything outside the window is, for the model's purposes, as if it never existed.

Early models had small context windows — a few thousand tokens. Modern models can handle hundreds of thousands. But the principle is the same: the model is always working from a glass of fixed size, and if the conversation gets too long, the oldest parts start to overflow.

> *Context windows explain why very long conversations with an AI can start to feel like it's forgotten what you discussed at the beginning. It hasn't become inattentive. The early parts of the conversation have simply fallen outside the glass.*

## A Seasonal Special: Fine-Tuning

A brewery's core lager might be the same year-round, but a good brewery also produces seasonal specials — takes on the base recipe adapted for a particular occasion, audience, or flavour profile. The brewing knowledge is the same. The output is tailored.

**Fine-tuning** works the same way. Once a base LLM is trained on a vast general dataset, it can be further trained on a smaller, more specific dataset to adapt its behaviour. A customer service chatbot, a coding assistant, a medical information tool — these are often fine-tuned versions of larger base models, trained to follow instructions, maintain a particular tone, or specialise in a particular domain.

Fine-tuning doesn't change the underlying model entirely. It adjusts the pour — the same ingredients, brewed differently, for a specific purpose.

> *When you notice that different AI products feel different even though they're built on the same underlying model, fine-tuning is usually the explanation. Same brewery, different recipe.*

## Last Orders: What We Covered

- LLMs are trained on vast amounts of text — the ingredients of the brewery — learning patterns rather than memorising facts.
- Tokenisation chops text into small pieces, like crushing grain to prepare it for brewing.
- Embeddings give each token a numerical flavour profile, encoding meaning and relationships between words.
- The attention mechanism lets the model focus on what matters most in a prompt — like a bartender ignoring the backstory and focusing on the order.
- Training adjusts billions of parameters across the model — like calibrating a vast mixing desk until the output sounds right.
- The trained model is like a keg: filled once, ready to pour, not re-brewed with every request.
- Generation happens one token at a time, each predicted from what came before — a probabilistic pour, not a pre-written answer.
- Context windows set the limit on how much the model can see at once — a glass with a fixed capacity.
- Fine-tuning adapts a base model for a specific purpose — same brewery, seasonal recipe.

---

*Cheers — and see you in the next one.*
