---
schemaId: urn:gala:schema:content-frontmatter:2.0.0
schemaVersion: 2.0.0
id: 01a1690e-c558-72af-b26f-5c1418161731
kind: article
title: 'LangChain101: Question A 300 Page Book (w/ OpenAI + Pinecone)'
description: Ask questions of a whole book and get answers drawn from its text, using LangChain, OpenAI and a Pinecone vector store in the cloud.
language: en-US
authors:
- 01a16913-c7a6-7f2b-9511-f82391d2f8cf
tags:
- langchain
- openai
- pinecone
- embeddings
- tutorial
status: published
createdAt: '2023-02-27T12:00:00.000Z'
publishedAt: '2023-02-27T12:00:00.000Z'
slug: langchain101-question-a-300-page-book-openai-pinecone
hero:
  path: assets/content-langchain101-question-a-300-page-book-openai-pinecone-hero.jpg
  alt: 'Thumbnail of the video "LangChain101: Question A 300 Page Book (w/ OpenAI + Pinecone)"'
  role: informative
redirects: []
extensions: {}
---
*Adapted from the video [LangChain101: Question A 300 Page Book (w/ OpenAI + Pinecone)](https://www.youtube.com/watch?v=h0DHDp1FbmQ)*

> **TL;DR:** I walk through asking questions of a long PDF, The Field Guide to Data Science, and getting answers taken directly from the source. LangChain loads the PDF and splits it into 228 documents of up to a thousand characters. OpenAI turns each into an embedding of 1536 numbers, and Pinecone stores them in the cloud. A question becomes an embedding, Pinecone returns the five most similar documents, and a question-answering chain has OpenAI answer in natural language from them.

In this tutorial we are going to query a book. That means asking questions to a 300 page book and getting answers back that come directly from the source and are contextually relevant.

We will use OpenAI and LangChain. The really cool part is that we will use a vector store that lives in the cloud. Up until now I have shown you embeddings stored locally, but this time we will use Pinecone, an external vector store that LangChain supports natively.

## The book

*[Watch from 0:40](https://www.youtube.com/watch?v=h0DHDp1FbmQ&t=40s)*

The book is the Field Guide to Data Science. It was made back in 2015, when data science was still a relatively new and cool term, and it has a lot of dense, really good information. I checked the last page and it is 123 pages, so let's say ballpark around there.

I will load the book into LangChain using the unstructured integration they have to read the text in the PDF, then ingest it and do a bunch of things with it.

## The diagram, without code

*[Watch from 1:23](https://www.youtube.com/watch?v=h0DHDp1FbmQ&t=83s)*

As always I want to start with the diagram, because I think it is easier to understand before the code. The flow goes like this:

1. **Split.** We ingest the PDF, and LangChain helps us split it into a bunch of documents. Think of documents as pieces or chunks of text. They can be small chunks, big chunks, whatever you like.
2. **Embed.** We use OpenAI's embedding engine to change these documents into embeddings. An embedding is literally a list of numbers, a big fat vector. The OpenAI engine we use has about 1500 numbers to represent the semantic meaning of each document, which means not what the words say per se, but what the document means.
3. **Store.** We store the embeddings on Pinecone instead of in a local database on your computer. That makes them easy to retrieve later, they persist across sessions, and you can make the database available to other people to query too, so you get a kind of shared memory of the book.
4. **Ask.** We ask a simple question like "what is a data scientist". The question gets turned into an embedding using OpenAI's engine.
5. **Retrieve.** Pinecone says: based on the embedding you just gave me, here are the two documents most important to answering that question. Technically, they are the two documents most similar to the question you asked. In the diagram, that is embedding one and embedding three.
6. **Answer.** LangChain takes those documents and uses OpenAI to answer the question for us.

## Loading the PDF and splitting it

*[Watch from 3:25](https://www.youtube.com/watch?v=h0DHDp1FbmQ&t=205s)*

In the code, I first import some document loaders: the unstructured PDF loader, plus the online PDF loader just to show you how that can be done. I also import the recursive text splitter, which splits up my documents.

I create the loader with the unstructured PDF loader. I am calling a local file, and I have commented out how to do it from online, but because this is a large book I use the local one to speed things up. Calling load takes quite some time, so I paused the video and jumped ahead.

Once loaded, I check the length of the data to see what LangChain actually loaded. There is only one document, with about 176 000 characters. That is way too much to put into a prompt with OpenAI, so the first thing to do is break it into a bunch of small documents instead of one huge one.

I use the recursive text splitter with the chunk size set to a thousand. You can play around with this to see what works best for you. Chunk overlap is zero, since I don't need any. I pass in the data we loaded, and we go from 1 document to 228.

The first one starts with the title, the Field Guide to Data Science, second edition, and there is some funky formatting. I don't think it will be an issue for me, but if you are doing this in a professional setting it might be a different story.

## Embedding the documents and setting up Pinecone

*[Watch from 5:32](https://www.youtube.com/watch?v=h0DHDp1FbmQ&t=332s)*

Now we create embeddings of those 228 documents and get them ready for semantic search. From the vector stores I import Pinecone (I used Chroma beforehand while messing around, but we use Pinecone today). I also import the OpenAI embeddings, the model that changes our documents into vectors. Make sure your API keys are set up and ready in your environment.

I stage my embeddings by calling the OpenAI embeddings class and passing my OpenAI key. Then I initialize Pinecone: you pass your API key, the environment your Pinecone instance is in, and your index name. I called mine langchain one, but I want to show you how to create one, because it takes only a couple of clicks.

When creating the index, I name it langchain two. With OpenAI embeddings I know there are 1536 dimensions, so that is the dimension setting. For the metric I pick cosine for now, and you can play around to see if another suits your use case better. For the pod type I go with faster queries, and I am on the free tier anyway. I create the index, take the name, and pass it in as my index name.

Then I get the embeddings and pass them to Pinecone, a couple of stages in a one-liner. I take the texts from all my documents, pass in the embeddings engine I made with OpenAI, and pass the index name. Running it takes all those texts, creates embeddings of them and passes them up to Pinecone, the external data source.

In the Pinecone metrics there was no data at first because the upload had not finished, but then the vector count started to populate. We end up with as many vectors as we had documents: 228 documents, 228 vectors.

## Asking the book a question

*[Watch from 8:35](https://www.youtube.com/watch?v=h0DHDp1FbmQ&t=515s)*

Now we ask questions to the book. My question is "what are the examples of good data science teams". I call similarity search on the document store (the doc search we were querying before), passing in the query. You don't have to include metadata, but I did to show it.

It goes up to Pinecone and asks which documents are similar to the query. It passed back five documents, because by default similarity search returns five. These are the documents from the PDF that Pinecone says have the highest cosine similarity with our question.

## Getting a natural-language answer

*[Watch from 9:17](https://www.youtube.com/watch?v=h0DHDp1FbmQ&t=557s)*

That is cool, but I want the question answered in natural language, so I won't do anything with those raw documents directly. Instead I import OpenAI and the question answering chain from LangChain, and get my OpenAI ready. I use the stuff chain type, which takes all those documents, puts them into the prompt, and then answers the question.

I set the query to "what are good examples of data science teams", just like above. Then the magical part is chain run: I input the relevant docs we got before and the query. The natural response from OpenAI is that good data science teams are multi-disciplinary teams of computer scientists and so on.

## Trying more questions

*[Watch from 10:18](https://www.youtube.com/watch?v=h0DHDp1FbmQ&t=618s)*

What if I ask something nuanced to the book itself? A good one is "what is the Advise stage of data maturity". If I asked OpenAI this directly it might not know what I am talking about, but because I am querying straight from the book, it answers correctly. I tried the collect stage too, and it answered that the collect stage is focused on collecting internal documents or external data sets.

So what we just did is ask a question to the book itself, which is very cool. You can do this across many fields. You could load up more books, but keep in mind that the more data you use, the more expensive it will be. You could use your internal documents, or build a chatbot that can reference external embeddings or other documents for specific questions.

Let me know if you have any questions, and please subscribe and thumbs up the video if you want more.

*[Watch the full video on YouTube](https://www.youtube.com/watch?v=h0DHDp1FbmQ)*
