# tangent (codename tangent discoveries)

I'm software engineer with 5+ years of experience specializing in ruby on rails, api development, saas products and microservices architecture. proven ability to deliver clean, maintainable, scalable code in collaborative and fast-paced environments. skilled in optimizing subscription platforms, integrating apis, improving product performance with strong ownership and pragmatic approach.

I'm also very active in mastodon and bluesky as @jaggiesweekly and @vulgofoobar respectevely.

now, I want to try a new project: TIL bot. this needs to be divided into multiple sub-projects here.

## 1. ai based bot organizer

I need a `@mcp.prompt` named `/create-tangent-discoveries <MY_FILE>` where I can mention an obsidian note file and from that the bot read its content then it create new separated concise files for each tangent discovery found on that note file.

in my learning routine I'm used to use obsidian and create `.md` files to take notes on my new learnings (for reference let's call this "learning note") and within note that the tangent discoveries (for reference let's call this "tangent discovery notes"). every time I take note on some tangent discovery they have the following structure:

```
see <TANGENT_DISCOVERY_NAME>
[[<FOO_TAG>]] [[<ANOTHER_TAG]]
<FIRST_NOTE_LINE>
<SECOND_NOTE_LINE>
...
```

for example:

```
see what's the code to create an mcp server w mcp sdk?
[[dev]] [[ai]]
from mcp.server.fastmcp import FastMCP
**mcp** = FastMCP("DocumentMCP", log_leve="ERROR")
```

from that, later I create separate files for each one of those tangent discoveries. the new tangent discovery note would have <TODAY_DATETIME>, a `#child` status, tags, <TANGENT_DISOCOVERY_NAME> and the <N_NOTE_LINES> contents as the following structure:

```
<TODAY_DATETIME>

status: #child

tags: [[<FOO_TAG>]] [[<ANOTHER_TAG>]]

# <TANGENT_DISCOVERY_NAME>

<FIRST_NOTE_LINE>

<SECOND_NOTE_LINE>




# references
```

for example:

```
2026-09-06 17:07

status: #child 

tags: [[dev]] [[ai]]

# what's mcp and what it stands for?

stands for **model context protocol**

open source

connect ai w **external systems**

act on **user behalf**




# references

- [[introduction to model context protocol]]
- [[why does mcp matters?]]
```

### important!

when extracting the contents of the learning note to separated tangent discovery notes is important to:

- keep their format like **bold**, *italic*, ~~strikethrough~~, `code`, ```code snippet```, etc..
- remove tags and note lines and only leave the hyperlink reference from learning note.

for example, this:

```
see what's the code to create an mcp server w mcp sdk?
[[dev]] [[ai]]
from mcp.server.fastmcp import FastMCP
**mcp** = FastMCP("DocumentMCP", log_leve="ERROR"
```

results in:

```
see [[what's the code to create an mcp server w mcp sdk?]]
```

## 2. ai based micro blog posts generator

I need a `@mcp.prompt` named `/blog-post-generator <MY_FILE>` where I can mention an obsidian tangent discovery note file and from that the bot read its content then it create 3 separated and concise TIL micro blog posts. one for mastodon, one for bluesky and one for linkedin format.

### 2.1 hashtags

for a blog post, read the content and include the most suitable tags. consider those in characters count as the tags also counts as characters. tags include (but not limited to):

`#ai`, `#mcp`, `#devlife`, `#learninginpubli`, `#fedhire`, `#database`, `#performance`, `#ruby`, `#softwareengineer`, `#git`, `#linux`, `#privacy`, `#memorymanagement` and `#softwarearchitecture`

for each social media format consider the following rules:

### 2.3 mastodon/bluesky/linkedin

- text should be downcase, except "TIL" word
- each <N_NOTE_LINE> should be written one after another separated by `;`
- commas are only used to separate ideas within the same <N_NOTE_LINE>
- I'm looking for my new gig, so before insert the hashtags, include the finish line `additionally, I'm still available for hire. let's talk!`

### 2.4 mastodon

- character count: 500 chars max.
- tone: informal

### 2.4 bluesky

- character count: 300 chars max.
- tone: informal

### 2.4 linkedin

- tone: formal
- starts with: "✨ TIL"

### examples

given the following tangent discovery note:

```
2026-09-06 17:30

status: #child 

tags: [[dev]] [[ai]]

# what problem mcp solves?

save dev **write**, **test** n **maintain time**

**enhance ai capabilities**




# references

- [[introduction to model context protocol]]
- [[what's mcp server?]]
```

this would generate those three micro blog posts for mastodon, bluesky and linkedin respectively:

```
TIL: what problem mcp solves?

save dev write, test and maintain time; enhance ai capabilities

I'm still available for hire. let's talk!

#ai #devlife #fedhire
```

---

```
TIL: what problem mcp solves?

save dev write, test and maintain time; enhance ai capabilities

I'm still available for hire. let's talk!

#ai #devlife #fedhire
```

---

```
✨ TIL: what problem mcp solves?

save dev write, test and maintain time; enhance ai capabilities

I'm still available for hire. let's talk!

#ai #devlife #fediHire #ruby #rails #rubyonrails #rorjobs #rordeveloper #railsdevs #rubyjobs
```

## outbox export references

for reference, I’ve exported my outbox data from mastodon and bluesky. you can look at it and see what my "TIL" writing style looks like.

## tech stack

for the `@mcp.prompt` I prefer built that using ruby.

for future projects (quiz generator website and a progress artifact) I prefer to use ruby on rails 8 and I need you to use proper rails defaults and built-in features, such as (but not limited to):

- proper config/initializers instead of copying and pasting repeated stuff everywhere
- proper before/after in controller, etc to avoid repetition. take care of setup/teardown operations
- proper use of partials, turbo streams, hotwire/stimulus where necessary
- every feature must have proper test coverage to avoid accidental bugs in the future - the tests should also help drive development and make it easier to find bugs in the implementation that you might have missed
- use ruby-llm to integrate with AIs (more on that later)
- make tasks semantically sound
- use rails naming conventions (controllers, routes, models, etc)
- use rails asset pipeline conventions
- not entirely necessary, but maybe use rails built-in scaffolds to generate the initial skeleton for resources (use restful whenever possible)
- run rubocop, brakeman, simplecov to keep track of small problems in coding

## future projects

keep track of those, but for now they’re only for future implementation.

* quiz generator website from those TIL contents.
* a progress artifact. a live page showing “what I’ve learned this month” that could also serve as an endpoint so I can request a list of three TILs and update on my github profile.
