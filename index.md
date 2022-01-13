---
title: Ruby for Dragons
desc: An unofficial companion to the DragonRuby documentation.
layout: default
published: true
indexed: true
categories: [Wiki]
---

{% include header.html %}

Welcome to the Ruby for Dragons wiki!

If you don't have any programming experience, we suggest you start on the [ABC Tutorial for New Programmers](/Ruby_for_Dragons/abc-tutorial-for-new-programmers).

If you have programming experience, we recommend you start with the [Ruby on Wings](/Ruby_for_Dragons/ruby-on-wings) page. Even if you've used Ruby before, reading this page will help you understand how to use it with DragonRuby.

**The official documentation for DragonRuby is at [http://docs.dragonruby.org](http://docs.dragonruby.org)**  
Join the community discord for more help: [http://discord.dragonruby.org/](http://discord.dragonruby.org/) (It's where most of this information is from).

***

## Contributing
This is a place to document anything developed for the DragonRuby community, that isn’t documented in the sample apps or official documentation. Anything published to this wiki will be considered Public Domain.

Do not submit copyrighted information, files, or documents to this wiki. This includes, but is not limited to:

- DragonRuby Engine binaries, files, documentation or samples.
- Code Samples from other sources, without the express written permission of their author.
- Complete Reproductions of publicly available tutorials, samples or other material (Linking to them is encouraged).

## Contribution Style Guide
- Code should be in DragonRuby style (avoid global variables, etc. See the DragonRuby samples to get a feel for their style).
- Code should pass a basic run of rubocop, excepting method/line length restrictions.
- Code should be easy to read and require few comments, if any.
- New contributions should be added as headers under existing pages, if possible.
- Contributions should be in English.
- Code should not require external assets, like sprites, sound files, or data, unless the sample is demonstrating those features.
- The simplest possible approach should be shown to achieve the desired result. Simplest does not mean most efficient or shortest.

## About the Wiki
The DragonRuby community is amazingly helpful and friendly, and the community discord is full of helpful information, projects, and people. However, we are all programmers, and programmers aren’t always the best at organizing information. Some of us found that the official documentation was opaque and difficult to navigate. We had all created our own repositories, cheat sheets, and libraries to help us find the information that we use the most.

This wiki is a consolidation of the community coming together to organize those cheat sheets and libraries into one, easy to navigate location.

The “Ruby on Wings” page was originally contributed by Kniknoo, and does an excellent job onboarding new Dragonriders. Other contributions are credited above each page/code block.

The wiki is hosted through Github Pages, and therefore uses Jekyll to serve content. There is an unplubilished template page in the root of the github repo. Copy the template to a new file and change published: ` to `true` to publish the page. New pages are automatically indexed in the sitemap. You can view the "compiled" template [here](https://ejectdrive.com/Ruby_for_Dragons/template).
