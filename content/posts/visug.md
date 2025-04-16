---
date: '2025-02-27T21:41:54+02:00'
draft: true
description: "A post about joining an event by The Belgian Visual Studio User Group"
title: 'Visug'

# weight: 1
# aliases: ["/first"]
tags: ["tech"]
author: "Wolf Schevelenbos"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: true
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    linkFullImage: true # click image to open it at full size
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## What is VISUG?

I went to a conference of VISUG (the Belgian Visual Studio User Group) in Kortrijk. It was a free event, where the organizer said that they aim to have more talks each year. Their core tenant is that spreading information in this format works and should be encouraged among software developers. The event was hosted by OnCore.

This event consisted of two talks:

- LLMs in .NET
- IConfig & IOptions

The latter was given by Pieter Samyn, my mentor on my current internship at ZF. I'm thankful he mentioned that he was going to give said talk, as otherwise I wouldn't have known the event even existed. It was a rather small event, with some estimated 15-25 people present.

![talk preparation at VISUG](/images/visug.jpeg)

Afterwards, there was also the opportunity to stick around and network. That was quite valuable for me, as I got to meet some higly specialised .NET experts and had some educational conversations.

## LLMs in .NET

> by Wannes Rebry

This talk was about integrating AI, specifically LLMs (Large Language Models), as chatbots in .NET web apps. The speaker started with covering using Semantic Kernel, which is a library that has built-in LLM support, before showing an actual implementation of said knowledge. 

To decide on what LLM you should use in the future, the speaker recommended doing your own research, as the AI landscape shift continuously. He recommended checking out [LLM Stats](https://llm-stats.com).

He first went over the theory behind running ChatGPT, Phi & Deepseek on top of your own database, which would contain the actual information you want the LLMs to use. Through an implementation of semantic search, math can be embedded into certain words as meta-data, which let the LLMs build up vectors to use when providing answers to their users. These vectors can be stored through [Redis](https://redis.io/docs/latest/develop/get-started/vector-database/). To prevent the LLMs from halucinating severly, or from deviating from the topic of your application, or from being abused by users, its outputs are processed by a second LLM instance. This second instance can not be influenced by a user, and will provide a simple alternative phrase to say it can't process the user's request. All this to say: it isn't rocket science.

### Demo

The speaker continued by providing a demo, where he implemented a chatbot for a fitness exercise application. Various detailed sport exercises had been stored in a database. The AIs were to only draw information about fitness from this data, and to ignore unrelated questions. To achieve that, he vectorised & prepped the exercise data. 

Olama is an LLM engine. It lets you run open-source models locally, like DeepSeek, and provides an easy-to-use API connection to proprietary LLMs hosted in the cloud. For the latter, you require tokens which will charge you per invocation. These endpoints also allow dependance injection, which is were the Redis vectorised database comes in. He also set up a crucial layer of middleware, designed to give a prefix to each prompt message. However, the speaker emphasised that users could easily circumvent this trick and for true safety a second instance of an LLM needed to be used, although there wasn't the time to illustrate this in the demo. The speaker used the Phi4 LLM model, which is provided by Microsoft, for the demo.
In large language model use, CAG (Closed-book Augmented Generation) and RAG (Retrieval-Augmented Generation) methods exist:

- CAG is when a model generates answers using only its internal knowledge, with no external data retrieved. Function invocation is not guaranteed here; it allows a language model to call external tools or functions during generation, like a calculator or database query.
- RAG combines the model's generation with external document retrieval, pulling in relevant info during the response process.

For the demo, the speaker successfully create a RAG implentation which supplied the vectorised Redis data to the PHI4 LLM. The result: a chatbot that behaved like a fitness coach.

## IConfig & IOptions

> By Pieter Samyn

This talk was specific to .NET and went over the advantages of combining the `IOptions` pattern with `IConfig` to create a more DRY setup (a.k.a. without repeating yourself) for your project's settings. This talk was fairly technical, but I'll do my best to explain it as simple as I am able to.

`IOptions` and `IConfig` are interfaces in .NET used for accessing app settings:

- `IConfig` reads configuration data directly (like from appsettings.json or environment variables). It is read-only and comes in handy for static deployment configurations. It comes in flavors: overrideable & optional.
- `IOptions<T>` provides a typed way to access configuration by binding it to a class. 

Transistioning from IConfig to IOptions marks a cleaner way to handle configuration in .NET. Managing configuration in .NET has evolved from the basic IConfiguration approach to the more structured and scalable IOptions pattern. While IConfiguration is useful for static values like URIs, secrets, and timeouts, it can get messy as your app grows. It’s read-only, centralized, and can pull from multiple sources (files, environment variables, CLI arguments, manual overrides), but lacks strong structure and validation.

Enter the IOptions pattern: it introduces clarity through separation of concerns and scope-limiting configuration. With IOptions<T>, you can inject strongly-typed settings, validate them (especially with DataAnnotation), and even make them reloadable with IOptionsMonitor<T>. Features like ValidateOnStart allow apps to crash early if settings are invalid, and IValidateOptions supports custom validation logic.

The configuration flow within the dependency injection container also matters: Configure, PostConfigure, and OptionsBuilder calls define behavior and override order. This modular approach reduces errors and boosts testability.

For complex needs, you can create a FinalOptions class that merges everything—ideal for handling feature flags or deeply nested configs. When done right, injecting these options ensures singleton behavior across all layers, giving you consistent, reliable configuration management throughout your application.
