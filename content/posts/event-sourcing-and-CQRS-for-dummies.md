---
date: '2025-05-27T18:30:00+02:00'
draft: false
description: "Speaker Kim Van Renterghem appeared in a public event at Howest, which was organized by Ryan Quivy and myself."
title: 'Event Sourcing and CQRS for Dummies'

# weight: 1
# aliases: ["/first"]
tags: ["tech", "PR event"]
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

As part of my university curriculum, I organized a public relations event at Howest featuring Kim Van Renterghem, a specialist I had the pleasure of meeting during my internship at ZF. The event, titled "Event Sourcing & CQRS for Dummies," provided an in-depth exploration of these advanced software design patterns. 

Here's a detailed recap of the key insights shared during the session.

![Kim Van Renterghem in front of the audience](/images/pr-event.png)

## Traditional Systems and Their Limitations

Kim began by discussing traditional CRUD (Create, Read, Update, Delete) systems, which are predominantly relational. He also spoke about using Git, where viewing history and bug-fixing in production can often lead to handling incorrect data. However, he explained that audits in such systems used at scale are crucial, but these systems often fail to explain why or how changes are made, making audit trails and logs unreliable.

## Logs as the Source of Truth

The concept of using logs as the sole source of truth was introduced as a more reliable method. In event sourcing, logs are immutable; any adjustment requires a cancel or revert action followed by a corrective action. Events are structured JSON data objects that form a data stream with a definitive end. Event sourcing embeds metadata within the stream, fragmenting data into events that are replayable and validated before storage.

## Event Storming: Determining the Domain

Event Storming is a workshop-based method to determine the domain by exploring events through post-its and identifying the aggregate or root object. This process involves creating a state-machine flow that includes both happy paths and edge cases. The steps are:

1. **Command**: With or without an actor.
2. **Aggregate**: The root object.
3. **Domain Event**: Leads to a read model or policy concern.

This continuous process requires consistent naming and public records in code, ensuring clarity and maintainability.

## Event Sourcing in Detail

Event sourcing assigns a command to each event, making it easy to test and ideal for environments requiring rigorous data integrity, such as hospitals and banks. It excels in debugging production issues, optimizing report generation, and building modular systems. However, it may not be suitable for projects needing low abstraction or for teams lacking discipline.

## Command Query Responsibility Segregation (CQRS)

CQRS segregates the responsibilities of commands and queries. Events arrive in a database, and simple getters handle queries. An event bus manages the flow of commands becoming events in event sourcing, leading to projections of data changes. CQRS is beneficial for scaling systems separately and managing transactions efficiently.

## CQRS Demo

The demo illustrated CQRS, which is often used within DDD. It showed how state changes are managed through base aggregates and event types. Validation is achieved through composition, avoiding complex if-statements. The flow involves:

1. A `get` command.
2. A command execution.
3. A `SaveAsync` operation.

Events are immutable and logged in the database, reflecting state changes, whereas commands can be altered without changing the state.

## Questions and Answers

The session concluded with an insightful Q&A:

- The **Visitor Pattern** he showed was primarily used to avoid conditional statements, though not crucial to the demo.
- **Sharding** involves saving states with endpoints and continuing from previous states.
- Each **Entity** has its own handlers.
- There are pre-built **Frameworks** for this flow, which can act as mediators, but are not always useful. Kim preferred creating everything yourself from the get-go, using event storming.
- There is an important **Cost Trade-off** to be made when fully implementing Event Handling & CQRS. More storage may be required, but normalization is avoided, making it ideal for large business with many evolutions in its future. It offers incredibly fast reads and is eventually correct, though not immediately.

## Conclusion

The event provided a comprehensive overview of event sourcing and CQRS, highlighting their benefits and potential challenges. These patterns offer robust solutions for managing complex data systems, ensuring data integrity, and enhancing system scalability. As a Software Engineering student, understanding these concepts were great for understanding the development of efficient, reliable software systems at a larger scale than what I have usually come into contact with.

## Review

This was my first time organising a PR-event, and planning it did not go off without a hitch. The first date for which a public speaker had originally been booked, had to be cancelled due to an administrative mistake. Luckily, finding a second speaker for another date proved not as hard as I had feared.

We also provided a QR-code, which led to a feedback form. It wasn't filled in a lot, but that was to be expected by an event with less than 30 people. All reviewers rated the event highly, and showed interest in learning even more about the subject. I consider it a win! 

Lastly, I'd also like to thank both the speaker, Kim Van Renterghem, and Ryan Quivy, who helped organise the event. They did an amazing job, and I couldn't have done it without them!

> Find links to all of the speaker's socials here:
> 
> - [Kim Van Renterghem (@kimvanrenterghem) on Speaker Deck](https://speakerdeck.com/kimvanrenterghem)
> - [kimvanrenterghemnew.github.io/Pages/](https://kimvanrenterghemnew.github.io/Pages/)
> - [kimVanRenterghemNew · GitHub](https://github.com/kimVanRenterghemNew/)
> - [Kim Van Renterghem's Speaker Profile @ Sessionize](https://github.com/kimVanRenterghemNew/)