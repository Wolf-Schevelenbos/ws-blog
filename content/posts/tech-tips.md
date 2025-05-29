---
date: '2025-04-16T18:50:34+02:00'
draft: false
description: "A collection of small software tips"
title: 'Tech Tips'

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

My dad is an IT veteran. He got his masters more than twenty years ago. While a lot has remained the same, a lot has also changed as well. That includes a lot of big changes, but also some smaller ones. What do university students adjust on their laptops nowadays for ease-of-use? That's what I wanted to answer in this blog post. 

This one's for you dad. 😉

## Note-taking

Fast schematic overviews of any information is key to retaining it over time. This means that I create bulletpoints like so:

```md
- exam
    - explain parts of your typescript project
    - explain a normal folder structure
    - make an endpoint
    - make a use-case
```

There are a number of note-taking apps out there. After a while it really does start to feel like a second brain. However, not all of them are create equally. I look for something customizable, markdown-centric & preferably open-source. Word has fallen out of favor for WYSIWYG (What You See Is What You Get) editors, which have no hidden symbols or styling applied to it outside of simple tags. The following come to mind:

- **Obsidian** is a note-taking app I've seen most students use. It is a beautiful project. However, it is not open source & they do sell your data, which was enough for me to look for alternatives
- **Zettlr** has become my defacto-standard word processor. If you like something simple like using notepad, I really can't recommend it enough. Whereas Obsidian requires a certain amount of customization and extensions to behave like a simple note-taking app, Zettlr is perfect for me by default: it has a spell-checker, linter, and table-of-contents on the side.
- **Joplin** is another open-source alternative I use for its cloud storage. It syncs right onto my phone, which is great for smaller notes or creative ideas I don't want to forget.

## Code editor

AI has boosted the speed at which we write code (and bugs) by a factor ten. A good LLM (Large Language Model) integrated right into your code editor has become a must. Luckily, almost all of them are implementing it currently. However, they're often expensive. Despite receiving them for free or at student-discounts, most of us see the writing on the wall. That's why some of us use **VSCodium**. 

It is the open-source version of VSCode that Microsoft originally claimed it was. It strips said program of all telemitry and adds the free-to-use Windsurf AI. It's really well-maintained and I much prefer it over VSCode.

## Windows OS

Windows 11 has become a pain to use in many aspects for young developers. For one thing: it is bloated with software we never use. Instead of deleting it one-by-one (a futile endeavour), run a **good debloat utility** like [this one from chris titus](https://christitus.com/windows-tool/). You will never have to worry again about OneNote trying to sync docker or VMware files behind your back.

Linux's package managers are sorely missed on Windows. Chocolatey on Windows has proven not to be the one-stop shop for software, and neither is the Microsoft Store. However, Linux can run on Windows. That is where **WSL2** comes in. It allowed me to follow this guide on creating a [terminal word processor](https://viewsourcecode.org/snaptoken/kilo/index.html) in C. Btw: I found this on [Project Based Learning](https://github.com/practical-tutorials/project-based-learning).

Customizing the desktop interface is also not the same as on Linux. **Powertoys** is great program that takes steps in the right direction. It lets me for instance adjust my keyboard and create custom shortcuts.

Lastly, many students don't carry around a portable monitor. Something very similar can be achieved by setting up **touchpad gestures** in Windows to create an navigate through **multiple desktops**. It has been a life-saver for me.

## Web browser

Hopping web browsers is all the rage, but not without cause. Their UX has been improving dramatically recently, while their data safety is slippling. It should have vertical tabs, multiple workspaces, tab grouping, zen mode, an ad blocker and so much more. If you don't know what some of these concepts are, please refrain from using Chrome or Edge any longer. Try out some of these alternatives:

- Vivaldi (which is definitely my personal favorite)
- Zen Browser
- Firefox

These change every month. A quick search or YouTube review can come in handy to be up-to-date with the latest evolutions on browser technlogy.

Got any suggestions? Let me know!