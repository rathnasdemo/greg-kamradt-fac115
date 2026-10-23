---
schemaId: urn:gala:schema:content-frontmatter:2.0.0
schemaVersion: 2.0.0
id: 01a1690e-c3fd-78e0-bdd3-40452f06bb15
kind: article
title: The LangChain Cookbook - Beginner Guide To 7 Essential Concepts
description: 'A walkthrough of the LangChain basics with a working code sample for each: schema, models, prompts, indexes, memory, chains and agents.'
language: en-US
authors:
- 01a16913-c7a6-7f2b-9511-f82391d2f8cf
tags:
- langchain
- openai
- agents
- embeddings
- tutorial
status: published
createdAt: '2023-03-29T12:00:00.000Z'
publishedAt: '2023-03-29T12:00:00.000Z'
slug: the-langchain-cookbook-beginner-guide-to-7-essential-concepts
hero:
  path: assets/content-the-langchain-cookbook-beginner-guide-to-7-essential-concepts-hero.jpg
  alt: Thumbnail of the video "The LangChain Cookbook - Beginner Guide To 7 Essential Concepts"
  role: informative
redirects: []
extensions: {}
---
*Adapted from the video [The LangChain Cookbook - Beginner Guide To 7 Essential Concepts](https://www.youtube.com/watch?v=2xxziIWmaSA)*

> **TL;DR:** This is a tour of the LangChain basics, based on LangChain's new conceptual docs and my companion cookbook. LangChain makes working with language models easier through integration, bringing in your own data, and agency, letting the model decide the next action. I go through schema, models, prompts, indexes, memory, chains and agents, each with working code. The point is a broad overview of the nuts and bolts so you can get building quickly. Use cases come in part two.

Have you ever wondered what LangChain was? Or maybe you have heard about it and played around with a few sections, but you are not sure where to look next. In this video we cover all of the LangChain basics, with the goal of getting you building and having fun as quickly as possible. My name is Greg, and I have been having a ton of fun building apps in LangChain. I share most of my work on Twitter, so links are in the description if you want to follow along.

This video is based on the new conceptual docs from LangChain. The Python and JavaScript docs are the technical ones. The conceptual docs take all the technical pieces and abstract them up into more theoretical, qualitative aspects, which I think is extremely helpful. To understand it better I created a companion for this video, the LangChain Cookbook. Links are in the description, and I put a lot of timestamps there too. There is a fair amount of content in this one, so you can watch it all the way through or, if you want to skip to a certain section, jump to that timestamp. I recommend following along with the GitHub repository.

## What we will cover

*[Watch from 1:01](https://www.youtube.com/watch?v=2xxziIWmaSA&t=61s)*

The conceptual docs also have a whole section on use cases, which is where you put these pieces into practice. That will be part two of this video, because it would be too long for today.

Today we run through schema, models, prompts, indexes, memory, chains and agents, with a working code sample for each. My goal with the cookbook is a dense document with a ton of links so you can self-serve. If you want to follow along, I encourage you to get it on your computer.

## What LangChain is and why I like it

*[Watch from 2:21](https://www.youtube.com/watch?v=2xxziIWmaSA&t=141s)*

The goal of the cookbook is an introductory understanding of the components of LangChain, explained in an explain-like-I'm-five way, with examples and code snippets.

LangChain is a framework for developing applications powered by language models. OpenAI just came out with plugins, but there is a whole lot of other things you can do with language models, and LangChain helps abstract a ton of that so you can work with it more easily, intermix different pieces and customize how you need to. It makes the complicated parts of building with AI models easier in two main ways:

- **Integration.** You can bring external data, such as your files, other applications and API data, to your language models.
- **Agency.** It allows your language models to interact with their environment via decision making. You use the language model to help decide which action to take next, which is useful when the path is not clear or may be unknown.

There are four big reasons I like LangChain:

- **Components.** It makes it easy to swap out the abstractions and components needed to work with language models like ChatGPT or anything on Hugging Face.
- **Customizable chains.** There is a ton of out-of-the-box support for using and customizing chains, which means combining a series of actions together.
- **Speed.** Almost every day I update to the latest branch, so the speed is awesome.
- **Community.** There are meetups, a Discord channel and events like webinars throughout the week, which are really awesome learning resources.

To summarize why we need it: language models can be pretty straightforward, text in and text out, but once you start developing applications there are a ton of friction points, and LangChain helps with them.

The cookbook will not cover every aspect of LangChain and is not a replacement for the documentation online. It is a broad overview of the capabilities, with my interpretation and voice-over, and I hope it gets you to building and making an impact as quickly as possible. I am super curious to see what you build, so please let me know.

## Schema: text, chat messages and documents

*[Watch from 5:09](https://www.youtube.com/watch?v=2xxziIWmaSA&t=309s)*

First I import my OpenAI API key. The first component is the schema.

**Text.** What is really cool about these language models is that text is the new programming language. Not verbatim, but we use a lot more English to tell language models what to do. "What day comes after Friday" is something I might tell a model, and it responds in natural language.

**Chat messages.** These are similar to text but come in different types:

- **System** messages are helpful background context that tells the AI what to do, like "your helpful teacher assistant bot".
- **Human** messages represent the user, literally the user input.
- **AI** messages show what the AI responded with. The AI may or may not actually have responded with it, but you can tell it that it did, so it has additional context on how to answer.

I import the chat OpenAI model and my three message types, and create my chat model. The system message says "you are a nice AI bot that helps a user figure out what to eat in a short sentence", and the human message says "I like tomatoes, what should I eat". An AI message comes back suggesting a tomato salad with fresh basil and mozzarella.

You can also pass more chat history. In the second example the system message says to help the user figure out where to travel to in one short sentence, and I say I like the beaches. I tell it that it responded "you should go to Nice, France", though it did not actually say that, and then ask what else I should do there. I never said where I went, so it has to infer it from the history, and it does pick up that I am in Nice. If you are making a chatbot, you can see how you would append the messages going back and forth with the user.

**Documents.** A document represents a piece of text along with associated metadata. Metadata is just a fancy word for things about that document. The text is held in a field called page content, and the metadata is a dictionary of key-value pairs. Mine has a document ID (a random integer, though it could be whatever you want), a document source (the LangChain papers) and a create time (a timestamp, in whatever format you want). This is extremely helpful when you are building a large repository of information and want to filter. Instead of asking LangChain to look at all the documents in your database, you can filter by certain metadata. Running it gives me a document object with the metadata on it.

## Models: language, chat and text embedding

*[Watch from 8:53](https://www.youtube.com/watch?v=2xxziIWmaSA&t=533s)*

Models are the ways of interacting with different model types.

- **Language model.** Text goes in and text comes out. I import OpenAI, make my model, pass in a regular string, "what day comes after Friday", and Saturday comes out.
- **Chat model.** I import the chat OpenAI model and my messages again, and set temperature to one, which just means more creativity and more exaggeration. The system message says "you are an unhelpful AI bot that makes jokes at whatever the user says", and the user says they would like to go to New York and asks how. The reply suggests trying walking, but not unless you have a lot of time on your hands, or flapping your arms really hard to see if it can fly there. It followed the system message, and it was not very helpful because I told it not to be.
- **Text embedding model.** This one matters because we do a lot of similarity searches and comparing of texts when working with language models. OpenAI has an embeddings model, and there are a lot of embedding models out there. I use OpenAI because it feels like a standard and is very simple right now. I define the text "hi, it's time for the beach" and embed it. That converts the string into a vector, a one-dimensional array, meaning a list of numbers, that is a semantic representation of the text: the meaning of the text is embedded in those numbers, which makes it easy to compare against other texts. The embedding length is 1536, so 1536 different numbers represent the meaning of my text. I am glad the computer deals with them and I don't. I only show the first five, so there are 1531 other numbers out there.

## Prompts, templates and example selectors

*[Watch from 11:58](https://www.youtube.com/watch?v=2xxziIWmaSA&t=718s)*

A prompt is the text you send to your language model. So far my prompts have been simple. Here I use DaVinci as my model and write a more instructional prompt in triple quotes, which I just find easier to use. It says today is Monday and tomorrow is Wednesday, and asks what is wrong with the statement. The model replies that the statement is incorrect: tomorrow is Tuesday, not Wednesday.

**Prompt templates.** Most of the time you will generate prompts dynamically, so they are not static strings you type out, but have placeholders filled based on the scenario. I create a template that says "I really want to travel to" followed by a location in curly brackets, then "what should I do there, respond in one short sentence". The prompt template takes location as its input variable, matching the name in the template. Formatting the prompt with Rome inserts it where it says location, and the model answers in one short sentence.

**Example selectors.** When constructing prompts you often do in-context learning: you show the language model what you want it to do, commonly through examples, such as how to answer a customer service request or a nuanced question. If you had ten thousand different examples, you would not want to throw all of them into your prompt. They may not fit and they may not be relevant. So you select which ones to include.

The star of the show is the semantic similarity example selector. It is a long name for functionality that selects similar examples. My examples name a noun and the place it is usually found: a pirate on a ship, a pilot on a plane, a driver in a car, a tree in the ground, a bird in a nest. I pass the selector the list of examples and my embedding engine, because we match examples on their semantic meaning, not on similar strings. I set k to two so I get two examples back.

Then I build a few-shot prompt template, meaning it contains a few examples. It takes the example selector and the example prompt, plus strings before and after, with a prefix "give the location that an item is usually found in" and a suffix holding the input and output. With the noun student, it finds the driver and pilot examples as most similar. With flower, it gives the tree and bird examples. I stick with student, pass that prompt into the language model, and get back classroom.

## Output parsers

*[Watch from 17:31](https://www.youtube.com/watch?v=2xxziIWmaSA&t=1051s)*

Sometimes you need structured output, such as a JSON object coming back from the language model, because it is a heck of a lot easier to deal with on the other side. There are two big concepts:

- **Format instructions.** This is the prompt template that tells your language model how to respond, and LangChain provides conventions to generate it automatically.
- **The parser.** The language model can only return a string, so if you want a JSON object you need a tool that parses the string and extracts the JSON.

I define a response schema with two fields: a bad string, which is a poorly formatted user input, and a good string, which is a formatted response. I create an output parser that reads the response schema, and ask it for its format instructions. That is a piece of text to insert into the prompt, saying the output should be a markdown code snippet in the following schema, with my two fields. LangChain did that formatting for me.

Then I create a prompt template with placeholders for the format instructions and the user input, and a final line to signal that I am done giving instructions and want a response. The user input I use is "welcome to California" with an exclamation point. The model returns a string that looks like gobbledygook, but after I parse it I get a nice typed object back, a dictionary.

## Indexes: document loaders, text splitters, retrievers and vector stores

*[Watch from 20:36](https://www.youtube.com/watch?v=2xxziIWmaSA&t=1236s)*

Indexes structure documents in a way that language models have a better time working with.

**Document loaders.** These are very similar to the OpenAI plugins that were just released, but LangChain supports a lot of really cool data sources that are not yet supported in the plugin world. I use a Hacker News data loader and pass it a simple URL. It found 76 comments in that post, and I print a sample, which shows different comments you can then work with in your language model.

**Text splitters.** Your document, such as a book or an essay, will often be too long for your language model, so you split it into chunks. If you want a single answer out of a book, it would not behoove you to put the entire book into the prompt. One reason is that it is too long. The other is that the signal-to-noise ratio is too low for the model to do its job effectively. It is a lot better to put in a few pieces of text, and to get those you split or chunk the document.

The one I use most often is the recursive character text splitter, and there are many types depending on your use case. I pull in a Paul Graham essay, which starts as one big long document, and set the chunk size to 150. Chunk overlap means the chunks overlap a little bit, and I encourage you to play with these variables. Normally I would not use 150. I would probably use a thousand or two thousand, but 150 is for demonstration. After splitting, one document becomes 606, and they are super small.

**Retrievers.** Retrievers are easy ways to combine your documents with your language models. The most widely supported is the vector store retriever, because we do so much similarity search within embeddings. I load a Paul Graham essay, split it, create embeddings of all the little chunks, store the vectors in a document store, and set that store as the retriever so it knows to go get things. I ask it for the relevant documents for "what types of things did the author want to build".

In the background it takes the string, converts it to a vector, compares that against the vector store, and finds the similar documents. Of all the documents, it found the two most similar to what I was looking for, one saying he wanted to build things that would last.

**Vector stores.** The way I think about it, a vector store is a table with rows of your embeddings and the associated metadata. Two main players in the space are Pinecone and Weaviate, and OpenAI's retriever documentation lists a whole bunch of others you may like. With a chunk size of a thousand I get 78 documents out of the essay, and I create embeddings for them. The embedding list has 78 embeddings, because there is one vector for each document. Each is a numerical representation of the semantic meaning of the document. The vector store stores your embeddings and makes them easily searchable, like a database.

## Memory

*[Watch from 26:26](https://www.youtube.com/watch?v=2xxziIWmaSA&t=1586s)*

Memory is how you help your language models remember things. The most common use case is chat history: if you are making a chatbot, you can give it the history of the messages you have had, which makes it a whole lot better at helping your user.

I import chat message history and the chat OpenAI model, create my chat model, and create a history. To it I add an AI message, "hi", and a user message, "what is the capital of France". The history messages come out in the right order. I pass the history to the language model, and it responds that the capital of France is Paris, as an AI message. I add that response content to my history, and print the messages again to see it appended to the end of my chat history. LangChain also makes it extremely simple to save this chat history so you can load it later.

## Chains

*[Watch from 28:10](https://www.youtube.com/watch?v=2xxziIWmaSA&t=1690s)*

Chains combine different language model calls and actions automatically. Say you have one input, and you want to use the output of that call as the input to another call, and then another. That is where the chain in LangChain comes from. I cover two of many. There are some complicated ones, so check the documentation to see whether another covers your use case better.

**Simple sequential chain.** You tell it to do X, then Y, then Z. I like this because it breaks up the task. Language models can get distracted, and if you ask for too many things in a row they can get confused and start to hallucinate, which is not good for anybody. Splitting also lets me check the output of each step and make sure my thinking is sound. The two prompts share the same variable names, so the wiring would have worked either way, but I renamed the second one to the user's meal to make it clearer.

I use two prompt templates. The first says your job is to come up with a classic dish from the area the user suggests, and I make it into a location chain. The second says, given a meal, give a short and simple recipe to make that dish at home, and I make it into a meal chain. I create the simple sequential chain with the location chain and then the meal chain. Order matters, so be careful. I set verbose to true so it prints what it is doing, which makes debugging easier. I run it with Rome as the single input. It runs Rome against the first template, gets a classic dish, then gives a recipe for it. Two runs, one go, no complicated code.

**Summarization chain.** I use this one quite often. If you have a long piece of text, like an article, a tweet thread or a Hacker News post, you chunk it up, summarize each chunk, and then get a final summary. I load the summarize chain, use a Paul Graham essay, and split it with a chunk size of 700. The chain type I use is the one where you get small summaries of the individual sections and then a summary of the small summaries. I have a whole video on the different chain types if you are curious.

When I run it, LangChain asks the language model to summarize the first piece, then the second, since we only had two chunks, and then asks for a final concise summary of the summaries. All the back and forth to get there is built into that one line, which is one of the powers of LangChain.

## Agents

*[Watch from 32:41](https://www.youtube.com/watch?v=2xxziIWmaSA&t=1961s)*

Agents are one of the most complicated concepts in LangChain, which is why I leave them for last. I thought the official docs described them well: some applications will not require just a predetermined chain of calls to language models and other tools, but potentially an unknown chain that depends on the user input. What we did above was a predetermined chain. An unknown chain, emphasis mine, means we are not sure which route to take, but we want the language model to tell us which route it thinks it should take. In these chains there is an agent with access to a suite of tools, and depending on the user input the agent decides which, if any, of these tools to call.

For example, say you have two databases on completely different topics and the user asks about trees. An agent can decide which database to go to.

The vocabulary:

- **Agent.** The language model that drives the decision making.
- **Tool.** A capability of the agent, similar to the OpenAI plugins that just came out. It could be the ability to search Google, to look at your email, whatever it may be.
- **Toolkit.** A collection of tools. An agent has a toolkit.

In the example I load tools, initialize the agent and create my language model. I inserted a SerpAPI key, an easy way to search Google, and I load only that one tool. You could load all the tools in the world, but it gets difficult for the agent to know which to use when, so only use the ones you know you will need. I pass in the toolkit and the language model, and choose the agent type. There are different types for different tasks, and I encourage you to check the documentation. I set verbose to true so we can see it thinking, and return the intermediate steps, which just means we get more granularity into what it is actually doing.

My query is "what was the first album of the band that Natalie Bergman is a part of". I asked this because I have not uploaded any documents, so there is no information pre-loaded, and it is a complicated question with multiple steps. That makes it a perfect question for an agent.

It reasons that it should find out what band she is a part of, and uses the search tool I gave it. Its observation is that she is an American singer-songwriter and one half of the duo Wild Belle. Then it decides to search for the debut album of Wild Belle, and observes that it is Isles. It now knows the final answer: Isles is the debut album of Wild Belle, the band Natalie Bergman is a part of.

That is a multi-step question, and the agent knew what it needed to find out without me telling it the chain. The chain could have been a lot longer if it needed more steps, and it figured that out dynamically along the way. Printing the intermediate steps shows more about how it searched. I confirmed it: Wild Belle is a brother and sister duo with Natalie Bergman. I would play their song if it would not give me copyright trouble, but a link to my favorite song of theirs is in the description.

## Wrapping up

*[Watch from 37:27](https://www.youtube.com/watch?v=2xxziIWmaSA&t=2247s)*

That was a very broad overview of the tactical nuts and bolts of LangChain. Congratulations on making it to the end. If you have questions, let me know. Subscribe to check out part two, when we go through actual use cases for these nuts and bolts. I share a lot of tools on Twitter, so follow me there, and leave comments to tell me what you think of the video.

*[Watch the full video on YouTube](https://www.youtube.com/watch?v=2xxziIWmaSA)*
