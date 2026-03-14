# 🧠 Chapter 4: Add Memory with MCP

> You're re-explaining yourself to AI in every conversation. There's a fix.

---

## Model Context Protocol (MCP)
MCP is an open protocol by Anthropic that lets AI models (like Claude) talk to external tools, databases, and design files — giving them persistent context.

**MCP Host** (Claude / Claude Code) → **MCP Servers** (Notion, Figma, etc.) → **Your Data**

- 🔗 [MCP Official Docs](https://modelcontextprotocol.io)
- 🔗 [Anthropic MCP Announcement](https://www.anthropic.com/news/model-context-protocol)

### MCP Servers shown in the slides
| Server | What it connects |
|--------|-----------------|
| **Miro MCP** | Reads/writes your Miro boards |
| **Notion MCP** | Reads/writes your Notion databases |
| **Figma MCP** | Reads your Figma design files |

### How to set up MCP in Claude Desktop
```json
// claude_desktop_config.json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-notion"],
      "env": { "NOTION_API_KEY": "your_key" }
    }
  }
}
```

---

## Claude Skills
A **skill** is a folder containing a `SKILL.md` file. Claude reads it before tasks to get persistent procedural knowledge — like giving your AI a manual.

- 🔗 [The Complete Guide to Building Skills for Claude (Anthropic)](https://www.anthropic.com/research/building-effective-agents)
- 🔗 [Agent Skills Directory (skills.sh)](https://skills.sh)

### Install a skill via CLI
```bash
npx skills add vercel-labs/agent-skills
npx skills find "notion"
npx skills update
```

---

## 📖 Resources
- [MCP GitHub Repository](https://github.com/modelcontextprotocol)
- [Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code)
- [Awesome MCP Servers List](https://github.com/punkpeye/awesome-mcp-servers)
