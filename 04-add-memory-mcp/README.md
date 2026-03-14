# 🧠 Chapter 4: Add Memory with MCP

> *"You're re-explaining yourself to AI in every conversation.
> There's a fix."*

This chapter covers the two most important concepts for making AI
agents genuinely useful in your startup workflow — Model Context
Protocol (MCP) and Claude Skills. Together they solve the same
root problem: AI has no memory, and you keep paying the tax of
re-explaining everything from scratch.

---

## The Core Problem MCP Solves

Before MCP, every AI tool needed its own custom connector to every
data source. Claude needed a custom GitHub plugin. ChatGPT needed a
different GitHub plugin. Cursor needed yet another one. Three AI
clients × five tools = 15 custom integrations to maintain. Anthropic
called this the **N×M problem**.

MCP was announced by Anthropic in November 2024 as an open standard
for connecting AI assistants to data systems such as content
repositories, business tools, and development environments — replacing
fragmented integrations with a single protocol.

You can think of MCP for AI applications as serving the same purpose
as a USB-C port serves for hardware — a universal connector that
works across every tool and every AI client.

**The shift:** Build one MCP server for GitHub → it works in Claude,
ChatGPT, Cursor, VS Code Copilot, and Gemini CLI. No duplicate work.

---

## 🔌 What is MCP — Deep Explanation

### The three components

The LLM is contained within the MCP Host — an AI application or
environment such as an AI-powered IDE or conversational AI. The MCP
Client, located within the host, translates the LLM's requests for
the MCP and converts the MCP's replies for the LLM. The MCP Server
is the external service that provides context, data, or capabilities
to the LLM — connecting to external systems like databases and web
services and translating their responses into a format the LLM can
understand.

In plain terms:
- **MCP Host** = the AI app you're using (Claude Desktop, Cursor,
  VS Code)
- **MCP Client** = the built-in connector inside that app that speaks
  the protocol
- **MCP Server** = a small program that wraps a tool (Notion, GitHub,
  Figma, your database) and makes it readable by any MCP client

### What MCP servers expose

The protocol defines three primitives: **Tools** — actions an AI
can invoke like running a search, creating a file, or deploying code;
**Resources** — data sources the AI can read such as files, database
records, and API responses; and **Prompts** — reusable templates the
server can expose to the client.

### How a real interaction works

The LLM understands it cannot access a database or send emails on
its own. It uses the MCP client to search for available tools, where
it finds relevant tools registered on MCP servers. It generates a
structured request to use these tools. The MCP client sends this
request to the appropriate MCP server. The server receives the
request, translates it into a secure operation, retrieves the data,
and sends back a structured response. The LLM provides a final
response equipped with the real data.

### The current state of MCP (March 2026)

In one year, MCP became one of the fastest-growing open-source
projects in AI: over 97 million monthly SDK downloads, 10,000 active
servers, and first-class client support across Claude, ChatGPT,
Cursor, Gemini, Microsoft Copilot, Visual Studio Code, and many
more.

In December 2025, Anthropic donated MCP to the Agentic AI Foundation
(AAIF), a directed fund under the Linux Foundation, co-founded by
Anthropic, Block and OpenAI. AWS, Google, Microsoft, Cloudflare, and
Bloomberg joined as supporting members — cementing MCP as
infrastructure-level governance, not a single company's product.

MCP's current spec release came out in November 2025. It now runs in
production at companies large and small, powers agent workflows, and
is shaped by a growing community through Working Groups, Spec
Enhancement Proposals (SEPs), and a formal governance process.

### Is MCP only for Claude?

No. MCP is a vendor-neutral open standard. Following its
announcement, OpenAI, Google DeepMind, Microsoft, and hundreds of
developer tools adopted it. Any MCP-compatible client — Claude,
ChatGPT Desktop, Cursor, GitHub Copilot, Gemini, VS Code — can
connect to any MCP server. That interoperability is the point.

---

## 🛠️ Setting Up MCP — Step by Step

### Prerequisites
- [Claude Desktop](https://claude.ai/download) installed (free)
- [Node.js](https://nodejs.org) installed (run `node -v` to check)

### The config file

All MCP servers are configured in a single JSON file:

**Mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows:** `%APPDATA%\Claude\claude_desktop_config.json`
```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "OPENAPI_MCP_HEADERS": "{\"Authorization\": \"Bearer YOUR_NOTION_TOKEN\", \"Notion-Version\": \"2022-06-28\"}"
      }
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "YOUR_GITHUB_TOKEN"
      }
    },
    "supabase": {
      "command": "npx",
      "args": ["-y", "@supabase/mcp-server-supabase@latest",
               "--access-token", "YOUR_SUPABASE_PAT"]
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem",
               "/Users/YOUR_NAME/projects"]
    }
  }
}
```

After editing: **restart Claude Desktop** → look for the 🔨 hammer
icon in the chat input → click it to see all connected tools.

### Getting your API tokens

| Service | Where to get the token |
|---------|----------------------|
| **Notion** | notion.so/my-integrations → New Integration → copy Internal Integration Token |
| **GitHub** | github.com → Settings → Developer Settings → Personal Access Tokens → Fine-grained |
| **Supabase** | supabase.com → Account → Access Tokens |
| **Figma** | figma.com → Settings → Personal Access Tokens |

---

## 📦 The MCP Servers Shown in the Session

The session slide shows **Miro**, **Notion**, and **Figma** as MCP
servers connected to Claude. Here's the full setup for each.

### Notion MCP
The Notion MCP server is one of the best productivity tools for AI
workflows. You can use it with Cursor to fetch the product requirement
document and have it create features accordingly. It stores all the
details from Claude conversations and can fetch any document from
Notion to add as additional context.
```bash
# Official Notion MCP (via Composio for easier OAuth)
npx @composio/mcp@latest setup "https://mcp.composio.dev/notion/YOUR_KEY" --client claude

# Or the official NPX method:
# Add to claude_desktop_config.json (see above)
```

- 🔗 [Official Notion MCP docs](https://developers.notion.com/docs/mcp)
- 🔗 [Composio Notion MCP (easier setup)](https://mcp.composio.dev)
- 🔗 [Tutorial: Integrate Notion with Claude Desktop](https://composio.dev/blog/notion-mcp-server)

**What you can do once connected:**
- "Read my Product Roadmap database and summarize what's overdue"
- "Create a new page in my startup workspace called 'Sprint 3 Plan'"
- "Search my Notion for all pages mentioning Supabase"
- "Update the status of task ID [x] to Done"

### Figma MCP
Figma's official Dev Mode MCP server exposes the live structure of
whatever you have selected in Figma directly to your AI — hierarchy,
auto-layout rules, variants, text styles, spacing tokens, and
component references. Your AI generates code against the real design
rather than guessing from a screenshot.
```bash
# Add to your claude_desktop_config.json:
"figma": {
  "command": "npx",
  "args": ["-y", "figma-developer-mcp", "--figma-api-key=YOUR_KEY"]
}
```

- 🔗 [Figma MCP official docs](https://help.figma.com/hc/en-us/articles/32132100509719)
- 🔗 [GLips/Figma-Context-MCP (community, 80+ tools)](https://github.com/GLips/Figma-Context-MCP)

**What you can do once connected:**
- "Generate React + Tailwind code from this Figma frame URL"
- "What are the exact spacing values in the dashboard design?"
- "List all the color tokens used in the design file"

### Miro MCP
Connect Claude to your Miro boards for reading and writing whiteboard
content, sticky notes, and diagrams.

- 🔗 [Miro MCP on Composio](https://mcp.composio.dev)
- 🔗 [Miro Developer Docs](https://developers.miro.com/docs/miro-apps-overview)

---

## 🗂️ Essential MCP Servers for Startup Teams (2026)

### Productivity & Planning

| Server | What it does | Install |
|--------|-------------|---------|
| **Notion** | Read/write your entire workspace | `npx @notionhq/notion-mcp-server` |
| **Figma** | Access live design files | `npx figma-developer-mcp` |
| **Google Drive** | Read/write docs, sheets, slides | [docs.anthropic.com/mcp](https://docs.anthropic.com) |
| **Google Calendar** | Read/create calendar events | [claude.ai connectors](https://claude.ai) |
| **Slack** | Read messages, send notifications | `npx @modelcontextprotocol/server-slack` |
| **Linear** | Create and update issues | `npx @linear/mcp-server` |

### Development

| Server | What it does | Install |
|--------|-------------|---------|
| **GitHub** | Repos, PRs, issues, code search | `npx @modelcontextprotocol/server-github` |
| **Supabase** | Query and manage your DB | `npx @supabase/mcp-server-supabase` |
| **Filesystem** | Read/write local files | `npx @modelcontextprotocol/server-filesystem` |
| **Postgres** | Direct SQL queries | `npx @modelcontextprotocol/server-postgres` |
| **Context7** | Live docs for any npm package | `npx @upstash/context7-mcp` |

### Research & Web

| Server | What it does | Install |
|--------|-------------|---------|
| **Brave Search** | Web search with private index | API key required |
| **Firecrawl** | Scrape any website → structured data | `npx firecrawl-mcp` |
| **Fetch** | Simple web fetch + HTML to Markdown | `npx @modelcontextprotocol/server-fetch` |

### AI Memory

| Server | What it does | Install |
|--------|-------------|---------|
| **Memory** (official Anthropic) | Persistent knowledge graph across sessions | `npx @modelcontextprotocol/server-memory` |
| **Mem0** | Intelligent memory that learns over time | [mem0.ai](https://mem0.ai) |

### Directories to find more

On January 26, 2026, Anthropic launched MCP Apps — an extension to
the Model Context Protocol that lets MCP servers render interactive
UIs (dashboards, forms, charts) directly inside Claude's chat window.
Launch partners include Amplitude, Asana, Box, Canva, Clay, Figma,
Hex, Monday.com, Slack, and Salesforce.

| Directory | Link |
|-----------|------|
| Awesome MCP Servers (punkpeye, 1000+ servers) | [github.com/punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) |
| MCP Playground (test any server instantly) | [mcpplaygroundonline.com](https://mcpplaygroundonline.com) |
| mcp-awesome.com (1200+ quality-verified) | [mcp-awesome.com](https://mcp-awesome.com) |
| Composio MCP hub (OAuth handled for you) | [mcp.composio.dev](https://mcp.composio.dev) |
| Official Anthropic MCP repo | [github.com/modelcontextprotocol](https://github.com/modelcontextprotocol) |
| MCP market daily rankings | [mcpmarket.com](https://mcpmarket.com) |

---

## 📖 Claude Skills — The Other Half of Memory

MCP gives Claude access to your **tools and data**. Skills give Claude
access to your **procedures and expertise**. Together they make Claude
feel like a team member who has been here for months.

### What a Skill actually is

A skill is a set of instructions, packaged as a simple folder, that
teaches Claude how to handle specific tasks or workflows. Instead of
re-explaining your preferences, processes, and domain expertise in
every conversation, skills let you teach Claude once and benefit every
time.

Every skill needs a `SKILL.md` file with two parts: YAML frontmatter
(between `---` markers) that tells Claude when to use the skill, and
markdown content with instructions Claude follows when the skill is
invoked. The `name` field becomes the `/slash-command`, and the
`description` helps Claude decide when to load it automatically.

### The three levels of content inside a skill

First level (YAML frontmatter): Always loaded in Claude's system
prompt — just enough for Claude to know when each skill should be
used. Second level (SKILL.md body): Loaded when Claude thinks the
skill is relevant — contains the full instructions. Third level
(linked files): Additional files Claude can navigate only as needed.
This progressive disclosure minimizes token usage while maintaining
specialized expertise.

### A minimal working SKILL.md
```markdown
---
name: startup-prd
description: Creates a Product Requirements Document for our startup.
  Use when asked to write a PRD, feature spec, or product brief.
---

# Product Requirements Document Writer

When creating a PRD, always follow this structure:

## Required sections (in order)
1. Problem Statement — what user pain are we solving?
2. Proposed Solution — our specific approach
3. User Stories — written as "As a [user], I want [goal] so that [reason]"
4. Success Metrics — at least 2 measurable KPIs
5. Out of Scope — what we are explicitly NOT building
6. Technical Considerations — DB tables, APIs, third-party services
7. Timeline — rough estimate by week

## Style rules
- Assume the reader is a developer, not a manager
- Be specific: "reduce farmer loan approval time from 7 days to 24 hours"
  not "improve the process"
- Every feature must map to a user story — if it doesn't, cut it
```

### Skill structure for more complex workflows
```text
my-skill/
├── SKILL.md          ← required: YAML frontmatter + instructions
├── references/       ← optional: detailed docs Claude can read on demand
│   └── schema.md
├── scripts/          ← optional: helper scripts Claude can run
│   └── validate.sh
├── examples/         ← optional: sample outputs to match
│   └── sample-prd.md
└── evals/            ← recommended: test queries to verify the skill works
    └── evals.json
```

### Installing skills in Claude Code
```bash
# Skills live in your project's .claude/skills/ directory
mkdir -p .claude/skills/startup-prd
# Create the SKILL.md file there
# Claude Code auto-discovers and loads it

# Install via the community skills CLI:
npx skills add vercel-labs/agent-skills
npx skills find "notion"
npx skills list
npx skills update
```

### Installing skills in Claude Desktop / Claude.ai

1. Zip your skill folder (e.g. `startup-prd.zip`)
2. Go to Claude.ai → Settings → Skills → Upload
3. Claude will load the skill in future conversations

### Anthropic's 17 official open-source skills

Anthropic has open-sourced 17 Agent Skills covering creative design,
document creation, technical development, and enterprise communication.
These skills work across Claude.ai, Claude Code, and the Claude API.

Most skills install via `npx skills add <org>/<repo>`. Official
Anthropic skills use `npx skills add anthropics/claude-code --skill
<name>`.

| Skill | What it does | Install command |
|-------|-------------|----------------|
| **frontend-design** | Production-grade UI that avoids "AI slop" aesthetics | `npx skills add anthropics/claude-code --skill frontend-design` |
| **docx** | Create Word documents with proper formatting | `npx skills add anthropics/claude-code --skill docx` |
| **pptx** | Create PowerPoint presentations | `npx skills add anthropics/claude-code --skill pptx` |
| **xlsx** | Create and edit Excel spreadsheets | `npx skills add anthropics/claude-code --skill xlsx` |
| **pdf** | Generate and manipulate PDFs | `npx skills add anthropics/claude-code --skill pdf` |
| **mcp-builder** | Generate MCP servers from scratch | `npx skills add anthropics/claude-code --skill mcp-builder` |
| **skill-creator** | Create new skills with proper structure | `npx skills add anthropics/claude-code --skill skill-creator` |
| **web-test** | Test web apps using Playwright | `npx skills add anthropics/claude-code --skill web-test` |
| **simplify** | Review code for quality and efficiency | `npx skills add anthropics/claude-code --skill simplify` |

Full list: [github.com/anthropics/skills](https://github.com/anthropics/skills)

### Skills you should build for your startup right now

Here are 5 skill templates directly applicable to Hult Prize teams:

**1. `pitch-deck-reviewer`**
```markdown
---
name: pitch-deck-reviewer
description: Reviews a startup pitch deck slide by slide. Use when
  asked to review, critique, or improve a pitch deck.
---
Review this pitch deck using the Hult Prize judging criteria:
1. Problem clarity — is it specific and quantified?
2. Solution uniqueness — why won't a competitor copy this in 90 days?
3. Market size — is the TAM/SAM/SOM calculated bottom-up?
4. Business model — clear revenue stream with unit economics?
5. Team — does the team have unfair advantage for this problem?
6. Impact — measurable social/environmental outcomes?

For each slide, give: [Score 1-10] [What works] [One specific improvement]
```

**2. `user-interview-guide`**
```markdown
---
name: user-interview-guide
description: Generates user interview questions following The Mom Test
  principles. Use when preparing for customer discovery interviews.
---
Generate interview questions that follow The Mom Test rules:
- Ask about PAST behavior, never hypothetical future behavior
- Ask about their LIFE and PROBLEMS, not our solution
- Never ask leading questions ("Would you use X?")
- Every question must uncover: frequency, severity, workarounds

Produce 8-10 questions for: [the user segment and problem provided]
```

**3. `feature-prioritizer`**
```markdown
---
name: feature-prioritizer
description: Prioritizes a feature backlog using MoSCoW and RICE.
  Use when asked to prioritize features, tasks, or backlog items.
---
For each feature provided, score it on:
- RICE: Reach × Impact × Confidence ÷ Effort (1-10 each)
- MoSCoW: Must / Should / Could / Won't

Output a ranked table with the RICE score, MoSCoW bucket, and a
one-sentence rationale for why it's ranked where it is.
```

---

## 🔗 All MCP & Skills Links

### Official documentation
| Resource | Link |
|----------|------|
| MCP official site | [modelcontextprotocol.io](https://modelcontextprotocol.io) |
| MCP spec (latest Nov 2025) | [modelcontextprotocol.io/specification](https://modelcontextprotocol.io/specification/2025-11-25) |
| Anthropic MCP announcement | [anthropic.com/news/model-context-protocol](https://www.anthropic.com/news/model-context-protocol) |
| MCP GitHub org | [github.com/modelcontextprotocol](https://github.com/modelcontextprotocol) |
| Claude Desktop download | [claude.ai/download](https://claude.ai/download) |
| MCP 2026 roadmap (official) | [blog.modelcontextprotocol.io/posts/2026-mcp-roadmap](http://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/) |
| Anthropic Skills repo (17 official skills) | [github.com/anthropics/skills](https://github.com/anthropics/skills) |
| Skills API quickstart | [platform.claude.com/docs/en/build-with-claude/skills-guide](https://platform.claude.com/docs/en/build-with-claude/skills-guide) |
| Claude Code Skills docs | [code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills) |
| Complete Guide to Building Skills (PDF) | [resources.anthropic.com — official 32-page PDF](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf) |
| Agent Skills open standard | [agentskills.io](https://agentskills.io) |

### Learning resources
| Resource | Link |
|----------|------|
| MCP explained by Google Cloud | [cloud.google.com/discover/what-is-model-context-protocol](https://cloud.google.com/discover/what-is-model-context-protocol) |
| MCP explained by IBM | [ibm.com/think/topics/model-context-protocol](https://www.ibm.com/think/topics/model-context-protocol) |
| MCP deep dive (Descope) | [descope.com/learn/post/mcp](https://www.descope.com/learn/post/mcp) |
| MCP Wikipedia | [en.wikipedia.org/wiki/Model_Context_Protocol](https://en.wikipedia.org/wiki/Model_Context_Protocol) |
| How to create Claude Skills (full guide) | [websearchapi.ai/blog/how-to-create-claude-code-skills](https://websearchapi.ai/blog/how-to-create-claude-code-skills) |
| 10 must-have skills for Claude 2026 | [medium.com/@unicodeveloper](https://medium.com/@unicodeveloper/10-must-have-skills-for-claude-and-any-coding-agent-in-2026-b5451b013051) |
| Best MCP servers 2026 (developer guide) | [firecrawl.dev/blog/best-mcp-servers-for-developers](https://www.firecrawl.dev/blog/best-mcp-servers-for-developers) |
| Top 10 MCP servers (Composio) | [composio.dev/content/10-awesome-mcp-servers](https://composio.dev/content/10-awesome-mcp-servers-to-make-your-life-easier) |

---

## ⚡ Quick-Start Checklist for Hult Prize Teams
```text
MCP Setup:
[ ] 1. Download Claude Desktop — claude.ai/download
[ ] 2. Install Node.js — nodejs.org
[ ] 3. Create claude_desktop_config.json (path above)
[ ] 4. Add Notion MCP + get your Notion integration token
[ ] 5. Add GitHub MCP + get your GitHub PAT
[ ] 6. Add Supabase MCP + get your Supabase access token
[ ] 7. Restart Claude Desktop → verify 🔨 hammer icon appears
[ ] 8. Test: "List all pages in my Notion workspace"

Skills Setup:
[ ] 9.  Install Claude Code — npm install -g @anthropic-ai/claude-code
[ ] 10. Install frontend-design skill
[ ] 11. Install docx and pptx skills (for pitch decks + reports)
[ ] 12. Create a pitch-deck-reviewer skill for your team
[ ] 13. Create a user-interview-guide skill
[ ] 14. Test a skill: /frontend-design "build a landing page for [your startup]"
```

---

## 💬 Discussion

Questions about this chapter?
**[Ask in Discussions →](https://github.com/MobinMithun/hult-prize-mvp-to-ai-agents/discussions)**

Common questions:
- *"How is MCP different from just using the Notion API directly?"*
- *"Can I use MCP with Lovable or Bolt, not just Claude Desktop?"*
- *"How do I make Claude remember something permanently across sessions?"*
- *"What's the difference between a Skill and a System Prompt?"*
- *"My MCP server isn't showing up in Claude — how do I debug it?"*
