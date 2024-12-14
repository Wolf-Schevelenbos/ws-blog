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

This isn't my first try at making a blog. In fact, my previous version is still online [here](https://wolfschevelenbos.be/). It is empty, because I abandoned it.

![image of original blog](/ws-blog/assets/images/original-website.png#center)

There is a good reason for that; namely it wasn't _me_ at all. It was a Wordpress website hosted on a Belgian host provider called combell. It is... not the best, if you'd ask me. It is poorly documented how to do anything else with it than host a simple website on it through a CMS other than Wordpress, Joomla or Drupal. However, from Howest, the university I attend, we received a free domain for it. So I tried it out, and didn't like the end result.

However, I love open-source projects. This wasn't it for me.

## Hugo framework

> Hugo is an open-source static site generator designed for building fast, lightweight websites, particularly blogs or documentation. It is written in Go (Golang) and is known for its speed and flexibility.

I got the idea to use Hugo for my blog from 2 YouTube videos which are listed below. My workflow ended up being a blend of these two and info I found in the documentation.

- [video 1]()
- [video 2]()

Designing a whole website through Vue or React seemed like overkill for this simple website. Hugo generates static HTML files from content written in the Markdown format, making it easy to create and deploy websites and posts without relying on a back-end server.

That is much more my speed. However, it did require some figuring out.

For one, it is a new framework to me. The exact setup guide can be found in the [Hugo Documentation](). I'll just briefly cover the process here anyways for those that need less hand-holding than the documentation provides.

It comes down to installing prerequisits like Git, Go and Dart Sass. After that, I double checked the path variables so I can use them from a powershell CLI (as I am working on Windows while at the university, sadly 🥲) and installed Hugo through `choco install hugo-extended`.

![path variables](../../assets/images/path-variables.png#center)

The commands to use Hugo are very straight-forward. `hugo new site ws-blog --format yaml` sets up a new project using `.yaml` instead of the default `.toml` extension, which I am less familiar with.

Hugo has many _themes_ that can be found online, which convert markdown files to HTML with a certain layout. I installed one such theme, [PaperMod](), as a submodule. Doing it that way allows me to easily update to a later version if and when it comes out. It does require that I mirror its file structure if I want to overwrite its layout pages. Luckily, it seems mostly just fine as-is to me. I'm not a UI/UX fanatic, less front-end work is why I picked it after all.

```powershell
>> git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
>> git submodule update --init --recursive
```

For the pages I made an empty archetype with some default meta-data. The posts convert the filename to their title for instance, and always show the time they were created at. I can easily create new posts using `hugo new posts/website-creation.md -k post`.

Other pages like the [About Page]() I added manually.

## Deployment

When the basics of the site were finished, it was time to set up auto-deployment to the web. I synced it to a new github repository, then setup a pipeline with a domain hoster called "Netlify". It gives me 100 GB bandwidth for free, which should be more than enough for this blog in its current state.

## Making new posts

After all is set up, all I have to do now to create a new post is to create a markdown file. I then run `hugo server` to see what it looks like locally as a website & build the html with `hugo`. Finally, I just have to commit the changes and push to my github repository. Auto-deployment takes care of the rest.
