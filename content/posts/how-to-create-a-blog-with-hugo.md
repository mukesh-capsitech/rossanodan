---
title: "How to create a blog with Hugo"
subtitle: ""
date: 2020-05-06T08:49:32+01:00
draft: false
description: "Hello"
tags: []
categories: [ General ]
featuredImage: ""
featuredImagePreview: ""
---

This is yet another attempt to create a blog and probably the last. Thanks for the hint, [Lucas](https://twitter.com/_StaticVoid)!

### What is Hugo

Hugo is an open-source framework for building static websites. It's perfect for simple websites that don't require dynamicity (interaction client - server). 

### Pros

It's easy to setup. Once Hugo is installed ( take a look here to do so https://gohugo.io/getting-started/quick-start/#step-1-install-hugo ), open a terminal and run

```bash
hugo new site <name_of_the_website>
cd <name_of_the_website>
npm install
hugo serve
```

It starts Hugo website on http://localhost:1313/ (by default).

Installing a theme is easy too. Following these steps https://hugoloveit.com/theme-documentation-basics/#22-install-the-theme is a matter of minutes, for real!

Once done, the theme can be customized! Open `config.toml` file with a text editor: there there are all the settings, from the website name to the structure of the pages.

That said, it's clear Hugo allows you to focus only on the content.. Creating content! That's the function of a blog, right?

### Cons

Hugo is not for who likes enjoying the creation of a blog from scratch. It allows to do a lot of things and it has tons of settings but there's no code to write but Markdown (or HTML) for posts.