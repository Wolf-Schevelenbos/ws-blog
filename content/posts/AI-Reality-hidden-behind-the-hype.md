---
date: '2024-12-10T12:32:29+01:00'
draft: true
description: "This is a post about Wim Delvaux's reality check on AI"
title: 'AI - the Reality Hidden Behind the Hype'

# weight: 1
# aliases: ["/first"]
tags: ["tech", "passive event"]
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

Wim Delvaux is a civil engineer and lecturer at HOGENT University of Applied Sciences and Arts. He recently gave an engaging talk to us IT students about his skepticism regarding the modern AI hype. While he made it clear that he’s a fan of AI’s recent developments, he also thinks there’s way too much BS floating around about it.

## Intelligence

He argued that to understand _artificial_ intelligence, we first need to understand _intelligence_ itself. According to Wim Delvaux, we can split up intelligence in these aspects:

- Processing observations
  - For example: seeing, feeling...
- Learning
  - This covers both remembering and generalising.
  - For instance, if you learn that red metal means something is hot and that touching hot things hurts, you’ll probably avoid touching red metal in the future.
- Reasoning
  - This involves making inferences and conclusions.
  - It can be deductive (based on logic or math) or inductive (based on probabilities).
- Problem solving
  - This applies to both specific or general problems.
- Use of language
  - Speech-to-text is intelligence, as it needs to cross-reference what it hears to what it knows of the language.
  - Text-to-speech is not intelligence, as it simply adds sounds to letters and words it stored in a database.

## AI & Computers

In computers, intelligence is simulated in one of two ways: either it is bottom-up, or it is top-down.

| bottom-up                                        | top-down                               |
| ------------------------------------------------ | -------------------------------------- |
| a.k.a connectionistic                            | /                                      |
| mimics biology                                   | uses pre-defined rules                 |
| fails and re-tries till succesful                | applies math and logic                 |
| needs a lot of data to achieve general knowledge | needs rules within one specific domain |
| low-energy consumption (after training)          | computationally heavy                  |
| always gives a result                            | can tell the user, "I don't know"      |

### Neural networks

Neural networks are a bottom-up approach to AI.

They use regression to make predictions, which is why they need so much data. They’re designed to recognize patterns but can (and do) fail. Since their outputs are based on predictions, they can’t tell you when they’re lacking enough data to provide a proper answer.

![linear regression graph](/images/linear-regression.png)

Wim Delvaux explained the concept with a simplified example: neural networks use nodes to perform simple operations on input data. These nodes are connected by edges, which have a numeric value called a weight (indicating the importance of the operation). The process is repeated multiple times in layers.

![graphical representation of a neural network](/images/neural-network.png)

The network essentially trains itself by randomly assigning weights and gradually improving results. It’s all about statistical likelihood based on past data. Once trained, running the program doesn’t take many resources.

### Knowledge banks

Knowledge banks, on the other hand, are a top-down approach.

They use something called an inference engine. It is, basically, a heap of rules to follow. Since these rules are applied at runtime, knowledge banks are much more computationally intensive than neural networks.

He mentioned IDP, a project from KU Leuven that represents data transformations using mathematical operations. SQL is also, in essence, a knowledge bank.

Google’s knowledge graph was another example he brought up. He didn’t dive too deeply into it, but knowing it uses a top-down AI approach makes sense to me.

## AI & Society

Wim compared the rise of AI to the invention of the calculator and the internet. He even called it the "fourth phase of humanity."

Here are those four phases, according to him:

1. The Spoken Word, which let us transfer knowledge.
2. The Written Word, which let us store knowledge.
3. The Internet, which lets us access knowledge quickly.
4. AI, which lets us summarize knowledge efficiently.

While AI has potential, there are plenty of dangers related to it with our early fourth-phase society according to him:

- Jumping the gun: Mistaking 80% correct output for the whole truth.
- Overhyping it: Forcing it into machines it doesn’t belong in.
- Being blinded by it: Focusing only on its positives while ignoring drawbacks.
- Laziness: Letting go of common sense.
- Abuse: Deliberately misrepresenting AI to manipulate others.

He also highlighted the European Union’s efforts to create laws around AI. While he acknowledged their good intentions, he called these efforts “futile.”

## Software development

In software development, Wim made an intriguing prediction: AI could create a new layer in coding. The progression would look something like this:

microcode → machine code → assembler → lower programming languages → higher programming languages → object-oriented coding → AI prompting

## Closing remarks

Personally, I agree with most of his points about AI being overhyped. That said, hype can have very real consequences, especially for people who struggle to separate facts from misinformation.

As for software development, I think AI will indeed add a new layer—but not necessarily through “prompting.” It seems more likely that pseudocode (used in universities to explain algorithms without worrying about syntax) will become even more abstract and integral.

Anyway, those were my two cents. I know it was a long one. Hope you enjoyed reading! Bye, guys.
