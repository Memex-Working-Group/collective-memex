## 0 to 1 Local Personal Knowledge Management Techniques

Let's get you an essential pathway to getting some kind of memex / local personal knowledge management set up.

This will be a practical approach to support you in starting your practice. Setting you up with Authoring, Version Control, and Publishing for human authored knowledge content.

### Authoring

The common approach for human produced content is to author and serialize the content as markdown with yaml front matter.

Predominantly folks use [Obsidian](https://obsidian.md) as their markdown editor, but I also hear [Logseq](https://logseq.com) is used for markdown note taking.

Download obsidian and start creating notes. You'll be able to locate the notes within the designated storage directory in markdown format.

Aside:  For nonhuman produced content and information I do not have a recommendation on serialization. I'll be exploring [DAG-CBOR](https://ipld.io/docs/codecs/known/dag-cbor/) as used with the [AT Protocol](https://atproto.com). [[Paul Mullins|Paul]] is exploring [[Anytype]]'s [anyproto/any-block](https://github.com/anyproto/any-block) protocol which is part of the same toolchain as DAG-CBOR's [[IPLD]] specifications known as [DAG-PB](https://ipld.io/specs/codecs/dag-pb/spec/).

### Syncing and Version Control

The editor tools typically offer syncing and version control management as their profit model, as well as integration with services like iCloud.

Because the data is document based, it is easy to deploy git for version control and manage your content as a git repository.

Aside: there are some folks in the [dweb community](https://getdweb.net) who are exploring the use of [Conflict-free Replicated Data Type (CRDT)](https://crdt.tech).

### Publishing 

Once you have your content you can publish. 
#### 1. Not Publishing 

You don't have to publish if it's not in your use case. 

You can use your personal information as a second brain for local LLM enabled inference or personal reference with a setup up of a local [model context protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro) 

Her is a post I nade on how to set this up with Obsidian and Claude.

2025-08-26

> If anyone wants to come along for the ride I'm planning on starting with obsidian + mcp.
> 
> unsure of model compatibility with MCP, defaulted to Claude.
> 
> Requires:
> - Obsidian
>   - plugin: local rest api https://github.com/coddingtonbear/obsidian-local-rest-api
> - mcp-obsidian https://github.com/MarkusPfundstein/mcp-obsidian
> - claude desktop https://claude.ai/download
> - default UV as python package manager (optionally, switch out)
> 
> My implementation pitfalls:
> the claude desktop app has challenges locating the command to run the server, so best to configure the claude config to call the command from the exact path. eg:
> `"command": "/Users/<USER>/.local/bin/uv",`

#### 2. Publish publicly as a Digital Garden

The prevalent approach for digital gardens publishing is Static Site Generation (SSG). How it works is CI/CD spins up a virtual machine to build a static site artifact and then serve it. This is commonly accomplished with services like Github Actions and Pages, Vercel, or Digital Ocean's App Platform.

I implemented this pattern for [civictech.ca](https://civictech.ca) using Jekyll and importing in the document archive through [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

This is a choose you own adventure.
##### Generators  
- [ruby: Jekyll](https://jekyllrb.com), 
- [go: Hugo](https://gohugo.io), 
- [node js: Astro](https://astro.build)
- [node js: 11ty](https://www.11ty.dev)

and I just found out a Myles I know [made an awesome list of static site generators](https://myles.github.io/awesome-static-generators/).

##### Batteries included libraries
- https://quartz.jzhao.xyz
- … and I'm just going to redirect to Maggie Appleton's list https://github.com/MaggieAppleton/digital-gardeners

#### 3. Publish privately as a Personal Data Store

I wish I could tell you more on the practice of putting into effect a Personal Data Store/Personal Data Server. This is where I'll be doing more discovery effort, predominantly with exploring [AT Protocol](https://atproto.com/guides/self-hosting) or catching up with [ActivityPub](https://activitypub.rocks).

All I can offer at this time is my dead trails. I have been told multiple times not to put my energy into [SOLID](https://solidproject.org). It may be effective to peek at it for the ideas — [Inrupt](https://www.inrupt.com) is the company looking to establish usage, and the [Open Data Institute](https://theodi.org/what-we-do/solid/) has taken over the project.