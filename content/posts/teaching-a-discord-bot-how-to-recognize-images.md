---
title: "Teaching a Discord bot how to recognize images"
date: 2020-06-12
draft: false
categories: [ General ]
tags: [ bot, tensorflow, ai, discord ]
---

Do you want to have fun? Build bots for Discord!

## What Discord is

Discord is a VoIP application used mainly by gaming communities. I didn't use it at all before meeting [Eddie](https://twitter.com/eddiejaoude). He built a [bot](https://github.com/EddieJaoudeCommunity/EddieBot) for [its own Discord server](https://discord.gg/WT3HkxR) and it's great. While I'm writing this, he's probably integrating Firebase in it to add some perstistence.

Anyway, since I wanted to help him with his bot, I needed to practice so I created my first Discord server and my first bot.

## What a bot is

Think of a bot as a software, programmed with special libraries, which is able to manage the interaction with the user autonomously, providing intelligent answers.

You can build a bot which can solve math equations, for example. It only needs the equation as parameter and some internal rules to recognize brackets and numbers.

## Long time no see, Python

The idea of an image classificator came to me chatting with my friend [Nizar](https://www.linkedin.com/in/nizarbs/). He's a Data Science postgraduate student in Italy.

To do that, I needed to re-write the old bot in Python so that we could use some Python libraries like [keras](https://keras.io/) and [tensorflow](https://www.tensorflow.org/).

It was a challenge for me. I hadn't written a line of Python since my first year in college many years ago. I found out it's like when you learn biking: you do it once forever.

So Nizar wrote the module we named *brain* and I wrote the bot itself which contains the creation of commands the user can invoke.

The idea was: when the user loads an image as attachment with the command *!analyze*, the bot has to use the module *brain* to obtain predictions and has to show them as an embed message.

## The outcome after a couple of hours

Say hi to *rossanodroid-py*!

![Demo](https://dev-to-uploads.s3.amazonaws.com/i/o7z3dvl34wiwcqe7ycjl.gif)

This project is open source and the code is available at https://github.com/rossanodan/rossanodroid-py. Do not hesitate to create an issue if you find a bug or if you have an idea to improve *rossanodroid-py*.

## Join my server to have a try

At the moment the bot runs locally but we're doing our best to deploy it as soon as possible. Join us to discuss about it and to help us improving it.

My Discord server is open to everyone. [Join us!](https://discord.gg/mwTFEJr).

## Resources

[discord.py](https://discordpy.readthedocs.io/en/latest/)
[Tensorflow](https://www.tensorflow.org/)
[keras](https://keras.io/)
[Discord Developers](https://discord.com/developers/applications)
