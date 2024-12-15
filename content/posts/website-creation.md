---
date: '2024-12-13T18:17:54+01:00'
draft: false
description: "In this blog post I go over how I created the website you're now reading from."
title: 'Website Creation'

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

## Original blog

This isn't my first try at making a blog. In fact, my previous version is still floating around online [here](https://wolfschevelenbos.be/). It’s totally empty because, well, I gave up on it.

![image of original blog](/images/original-website.png#center)

Here’s the thing: that blog just wasn’t me. It was a WordPress site hosted on some Belgian provider called Combell. Honestly, not a fan. It’s fine if you’re sticking to basic CMS stuff like WordPress, Joomla, or Drupal, but anything beyond that? Good luck. The documentation is... not great. The only reason I used it in the first place was because Howest, the university I go to, gave us a free domain. So I gave it a shot and quickly decided it wasn’t worth the hassle.

Also, I’m a big fan of open-source projects, and this setup just didn’t cut it.

## Hugo framework

> Hugo is an open-source static site generator designed for building fast, lightweight websites, particularly blogs or documentation. It is written in Go (Golang) and is known for its speed and flexibility.

I got the idea to use Hugo from two YouTube videos (linked below) and a quick explainer video. My workflow ended up being a mix of what I saw in those videos and some stuff I found in Hugo’s documentation.

- [I started a blog.....in 2024 (why you should too)](https://www.youtube.com/watch?v=dnE7c0ELEH8&t=1681s)
- [Getting Started With Hugo | FREE COURSE](https://www.youtube.com/watch?v=hjD9jTi_DQ4&t=2475s)
- [Hugo in 100 Seconds](https://www.youtube.com/watch?v=0RKpf3rK57I)

Designing a whole website through Vue or React seemed like overkill for this simple website. Hugo generates static HTML from Markdown files, which makes it super easy to create and publish stuff without needing a back-end. That’s much more my speed, though I had to figure some things out along the way.

For starters, Hugo was completely new to me. If you’re interested, the [Hugo Documentation](https://gohugo.io/documentation/) has all the nitty-gritty details. I’ll keep it short here for those who don’t need a step-by-step guide.

It comes down to installing prerequisites like Git, Go and Dart Sass. After that, I made sure my path variables were set so I could use those prerequisites from a powershell CLI (as I am working on Windows while at the university, sadly 🥲) and installed Hugo through `choco install hugo-extended`.

![path variables](/images/path-variables.png#center)

The commands to use Hugo are pretty straight-forward. To get started: `hugo new site <my-website> --format yaml` sets up a new project using `.yaml` instead of the default `.toml` (because I’m less familiar with `.toml`).

Hugo has a ton of _themes_ that can be found online to make your Markdown files look nice. I installed one such theme, [PaperMod](https://themes.gohugo.io/themes/hugo-papermod/), as a submodule. Doing it that way allows me to easily update to a later version if and when it comes out. It does require that I mirror its file structure if I want to overwrite some of the layout elements or pages. Luckily, it is mostly just fine as-is to me. I'm not a UI/UX fanatic, less front-end work is why I picked it after all.

```powershell
>> git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
>> git submodule update --init --recursive
```

For the posts, I set up an empty archetype file with some default metadata. The posts convert the filename to their title for instance, and always show the time they were created at. I can easily create new posts using `hugo new posts/<post-title>.md -k post`.

Other pages like the [About page](/about/) I added manually.

## Deployment

Once the site was up and running, it was time to figure out how to deploy it. I synced the project to a GitHub repository and set up a pipeline using [Netlify](https://app.netlify.com/). It gives me 100 GB of bandwidth for free, which is way more than this blog will ever need.

I hooked up a webhook, so now the site redeploys automatically whenever I push changes to the main branch on GitHub.

![deployment process](/images/deployment-process.png)

If I ever decide I want a more custom URL, I could get it from Netlify too at a pretty fair price. I tried to set it up so the Combell address I got for my previous blog would refer to this one, but Combell clearly didn't intend for me to change DNS A-records and such, and the documentation was more than a little dated.

## Making new posts

Now that everything’s set up, making a new post is a breeze. I just create a Markdown file, run `hugo server` to preview it locally, and then use `hugo` to build the HTML. After that, I commit the changes and push them to GitHub, and Netlify handles the deployment automatically.

Setting up this blog was a fun little project, and I look forward to expanding it further while sharing my journey with you.
