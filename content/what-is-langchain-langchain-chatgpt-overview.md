---
schemaId: urn:gala:schema:content-frontmatter:2.0.0
schemaVersion: 2.0.0
id: 01a1690e-c4bc-7e39-ac28-9ca39c23223b
kind: article
title: What Is LangChain? - LangChain + ChatGPT Overview
description: LangChain connects AI models to your own information and tools. Here is the problem it solves and why I think learning it is a good bet.
language: en-US
authors:
- 01a16913-c7a6-7f2b-9511-f82391d2f8cf
tags:
- langchain
- chatgpt
- tutorial
status: published
createdAt: '2023-02-13T12:00:00.000Z'
publishedAt: '2023-02-13T12:00:00.000Z'
slug: what-is-langchain-langchain-chatgpt-overview
hero:
  path: assets/content-what-is-langchain-langchain-chatgpt-overview-hero.jpg
  alt: Thumbnail of the video "What Is LangChain? - LangChain + ChatGPT Overview"
  role: informative
redirects: []
extensions: {}
---
*Adapted from the video [What Is LangChain? - LangChain + ChatGPT Overview](https://www.youtube.com/watch?v=_v_fgW2SkkQ)*

> **TL;DR:** This is the kickoff for my LangChain tutorial series. ChatGPT cannot tell you what LangChain is, because it was not trained on recent data, and it cannot answer questions about your own documents, because it has no access to them. LangChain connects AI models to outside sources and lets you chain commands together. I think learning it is a bet that OpenAI will stay at the bottom API layer and leave integrations to the community. The series runs through the documentation with real-world code.

Welcome to a tutorial series on LangChain. In this introduction I want to cover our goals for the series, what LangChain is, and why I think it is a crucial investment to put energy into learning it and how you can use it.

## How the series will work

*[Watch from 0:20](https://www.youtube.com/watch?v=_v_fgW2SkkQ&t=20s)*

We are going to run through the documentation they have provided, and I will speak over it and provide some real-world code samples. I will extend them a little bit so you can see functionality you may find applicable in your business or your personal life.

The series will mostly be short tutorial videos, though I may go crazy and do some three-hour videos. We will see.

## The problem: ChatGPT does not know about LangChain or about you

*[Watch from 0:40](https://www.youtube.com/watch?v=_v_fgW2SkkQ&t=40s)*

Before I explain what LangChain is, I want to set up the problem. I asked ChatGPT what LangChain is, and it said it was not familiar with the term.

The reason is that LangChain is a more recent library. I think Harrison, one of its creators, said he went full time on it three weeks ago, so around January of 23. ChatGPT has not been trained on data more recent than, I think, 2021. OpenAI will get there eventually, but they have not yet. That is problem number one.

Problem number two: how many Google Docs did I write last year? I asked ChatGPT, and it said that as an AI model it does not have access to my personal information. That makes complete sense, because I have not linked my Google Drive to it and it has no understanding of who I am.

## Where LangChain comes in

*[Watch from 2:22](https://www.youtube.com/watch?v=_v_fgW2SkkQ&t=142s)*

Picture me as the person accessing the OpenAI models. I did it through my browser, but you could also do it through their API, and there are plenty of tutorials on that. Either way, the model is not connected to my outside information.

LangChain connects the AI models you want to use, whether that is OpenAI or something on Hugging Face, to outside sources. All of a sudden you can chain commands together, which is the chain in LangChain. You can ask OpenAI what the weather is today, and the language models work out the series of questions they need to ask to get the information you want.

The applications are almost endless, and they are building more integrations every day. If you follow them on Twitter or read their GitHub changelog, you can see some really cool things they are putting out.

## Why I think it is a good bet

*[Watch from 3:43](https://www.youtube.com/watch?v=_v_fgW2SkkQ&t=223s)*

By choosing to learn this, you are betting that OpenAI and Hugging Face are not going to build direct integrations to the tools you use every day. In my opinion, OpenAI wants to remain on the API at the very bottom layer, an API for certain machine learning models. They do not want to build direct integrations into Google, Notion or Wolfram Alpha. They want the community to do that.

So by learning LangChain you are taking the bet that there will be a separation into different abstraction layers, and that this is the piece that connects them. Is LangChain going to be the library that wins it all and becomes ubiquitous? Who knows, I don't. But I guarantee that by learning the functionality in this library, whichever one does come along, you will find it extremely valuable.

## What the series will cover

*[Watch from 4:44](https://www.youtube.com/watch?v=_v_fgW2SkkQ&t=284s)*

We will run through their documentation and I will explain what you can do with it. They have a lot of modules and use cases:

- **Agents** that can do things on your behalf
- **Chatbots**
- **Generation**
- **Question answering**
- **Summarization**
- **Evaluation**, and more

As more documentation comes out we will do more videos. Subscribe to the channel to see when they come out, or sign up at data independent.com, which this channel is associated with, to get updated by email when new videos are posted.

## My emphasis as an instructor

*[Watch from 5:45](https://www.youtube.com/watch?v=_v_fgW2SkkQ&t=345s)*

My emphasis is always on real-world applications. I don't really care about theory, and I am not a hardcore machine learning and stats person who will show you academic papers. I care about having you make an impact in the B2B environment or in your personal life, because I believe these tools can leverage the impact we have, so that one person or a small team can do a lot more good in the world.

I am very excited to learn this alongside you. Let's have some fun.

*[Watch the full video on YouTube](https://www.youtube.com/watch?v=_v_fgW2SkkQ)*
