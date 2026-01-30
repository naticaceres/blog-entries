For some time I've needed to publish my blog. There's something in materializing what is on my mind, being able to link it to the original supporting sources and keep it to remember in the future, that is hard to accomplish when there's an external approval to gate the process.

Particularly when that external approval must come with a private first draft, and with exposing oneself to the unknown and the judgement of others.

Most of the time I subconsciously exaggerate how evil the peer review is when judging my work, and this creates an awful analysis paralysis circle of doom. I don't write because I am afraid of the critiques, and I know the first words out there will be rough and misplaced. On the other side I know I will never get better at it unless I finally start jotting down my thoughts and accomplishing my initiatives.

As a result I've ended up with a long list of unpublished articles, bits and pieces, demos and thoughts here and there that never quite made it out to see the light of day. 

A favorite analysis paralysis quote is that of Karl Jung:

> What you resist, not only persists but grows in size.

Even more daunting, the next sentence:

> What you fight you strengthen.

well now I am clearing the path to finally get it done.

and this is step one.

## Building the Blog
The bare bones are react with typescript. In another article I'll link here, I'll expose the principles I follow about the UI architecture and its organization. The fundaments are clean code and hexagonal architecture, and the goals are  creating an easy to follow pattern that I don't hate as I tinker with it to expand its capability and adapt its goals as it grows.

## Basic architecture
The goal is simple:
I need a static website to present my blog, that ideally I want to host in github or another free service. I like github because that's where my repository lives, and it is a straightforward simple tool to use. 
The domain will be my own, and the articles are the interesting part.
I want to be able to write them using a markdown tool such as obsidian, or maybe the github markdown editor (the online editor you use to set up your readme file, as an example).

I like the versatility of being able to open the github website and start taking notes in whatever platform as long as I have internet access. Or using any device to take notes then copy paste and quickly format with markdown.

I also really like the AI current integrations and how seamlessly they wrap around a repository and .md files. Then I can sort of chat with my previous articles and have some LLM help me proofread and fix common grammar mistakes, or tie related thoughts together. Perhaps we can even enrich the experience for the end users eventually.

What I need, then is:

 - one repository with my home website, containing the engine necessary to get the markdown entries and present them as human readable pretty printed content from a source.
 - a home for my blog entries, this will be a secondary repository.

The result will be a Single page application that uses client side rendering to fetch content from a decoupled content repository.
![[Pasted image 20260121104247.png]]

### What about SEO?
Since the content of my blog at this instance is built on runtime, then for SEO my website is a virtually empty website.
In the future I will have to think of a way to run a job (would github actions work for this?) that periodically transforms markdown files from my blog entries repo and push them into my blog website as html files.

## The Setup

### Blog website
I've begun by creating a basic vite react app using the latest vite and react versions.
I've used react router to simplify routing internally and keep it an SPA, and to easily add some sugar like the 404 page and a basic index.

Then I've used [gh-pages](https://www.npmjs.com/package/gh-pages) in this repo to make it fast and easy to deploy my vite react app with github pages. There are a few caveats tho:
 - The output folder must be updated.
 - The assets (images) must all live in the public folder.
 - The baseurl must be updated to match that of the repo name.

### Blog entries 
This is a new repo, it contains my blog entries organized by months and an index.

### Markdown to html engine
I found a couple of existing solutions:
- [showdown](https://www.npmjs.com/package/showdown)
	- highest weekly downloads. will use this one



-------------------
I have architected a **Client-Side Rendered (CSR)** blogging platform using a **Headless** approach.

The application logic is built with **React** and **TypeScript**, bundled using **Vite** for optimized production assets. These artifacts are hosted on **GitHub Pages**.

The content layer is completely **decoupled**; it resides in a separate repository ('blog-entries') acting as a file-based CMS. At **runtime**, the React application asynchronously fetches the raw Markdown content via HTTP requests, parses it using a custom TypeScript-based Markdown-to-HTML engine, and hydrates the view for the user.

This separation allows me to write in Obsidian without touching the codebase, while the frontend app treats the Markdown repository as an external API.