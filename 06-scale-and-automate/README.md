# ⚡ Chapter 6: Scale & Automate

> *"If you fail, then fail fast."* — Md. Ahsanul Mobin

Scaling is not hiring more people to do the same work faster.
Scaling is replacing repetitive human work with automated systems
that run 24 hours a day without you. This chapter covers the two
automation pillars shown in the session — Telegram bot automation
and no-code workflow tools — plus the AI agent frameworks that
represent the next frontier.

---

## The Automation Mindset

Before picking tools, ask one question about every task your team
does repeatedly:

> **"Does this require human judgment, or just execution?"**

If the answer is execution — automate it. The session shows exactly
this in action: GitHub pushes automatically notify the team on
Telegram, Notion task updates ping the relevant people instantly,
and daily reports arrive at 9 AM without anyone doing anything.

Every hour your team spends on notifications, status updates, data
entry, and report generation is an hour not spent building, selling,
or talking to users.

---

## 🤖 Part 1: Telegram Bot Automation

The session slide shows three real automation examples in production:

1. **GitHub → Telegram**: Every `git push` to any branch sends a
   message to the team's Telegram channel — repo name, branch,
   commit hash, and commit message
2. **Notion → Telegram**: Task updates from the Notion project
   tracker fire into a team channel with full task details,
   delivery date, status, priority, and a "View in Notion" link
3. **BotFather**: The official Telegram tool for creating bots,
   shown as the starting point for all of this

### Why Telegram bots for Bangladesh startups

- Telegram is free, has no per-message cost, and no API rate
  limits for bots under normal usage
- Your whole team is already on Telegram — zero adoption friction
- No app store approval needed — bots are just API calls
- Works on all platforms (iOS, Android, web, desktop)
- Group channels can have unlimited members
- Supports rich formatting: bold, code blocks, inline buttons,
  file attachments, and inline keyboards

### Creating your first bot — step by step

**Step 1: Create the bot via BotFather**

1. Open Telegram → search `@BotFather`
2. Send `/newbot`
3. Enter a display name (e.g. `Somadhan Tracker`)
4. Enter a username — must end in `bot`
   (e.g. `somadhan_tracker_bot`)
5. BotFather replies with your token:
   `123456789:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`
6. **Never commit this token to Git.** Add it to `.env` immediately.

**Step 2: Get your chat ID**

Every Telegram chat, group, or channel has a numeric ID.
You need this to send messages to a specific place.
```bash
# Replace YOUR_TOKEN with your actual token:
curl https://api.telegram.org/botYOUR_TOKEN/getUpdates
```

1. Add the bot to your group/channel first
2. Send any message in the group
3. Run the curl command above
4. Look for `"chat":{"id": -123456789}` in the response
5. That negative number is your group chat ID

**Step 3: Send your first message — the simplest possible bot**

No library needed. Just an HTTP request:
```python
import requests
import os

BOT_TOKEN = os.environ["TELEGRAM_BOT_TOKEN"]
CHAT_ID    = os.environ["TELEGRAM_CHAT_ID"]   # the negative group ID

def send(text: str, parse_mode: str = "HTML") -> bool:
    url = f"https://api.telegram.org/bot{BOT_TOKEN}/sendMessage"
    payload = {
        "chat_id":    CHAT_ID,
        "text":       text,
        "parse_mode": parse_mode,          # HTML or Markdown
    }
    r = requests.post(url, json=payload, timeout=10)
    return r.status_code == 200

# Call it anywhere:
send("🚀 Deployment complete — <b>v1.4.2</b> is live")
```

```javascript
// JavaScript / Node.js version
const BOT_TOKEN = process.env.TELEGRAM_BOT_TOKEN;
const CHAT_ID   = process.env.TELEGRAM_CHAT_ID;

async function send(text) {
  const url = `https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`;
  await fetch(url, {
    method:  "POST",
    headers: { "Content-Type": "application/json" },
    body:    JSON.stringify({
      chat_id:    CHAT_ID,
      text,
      parse_mode: "HTML",
    }),
  });
}

await send("✅ New user signed up — <b>Rahim Uddin</b> from Rajshahi");
```

### HTML formatting in Telegram messages

Telegram supports a subset of HTML for bot messages. Use it to
make alerts readable at a glance:
```html
<!-- Bold -->
<b>New deployment</b>

<!-- Code (monospace) -->
<code>commit: 4d18daa</code>

<!-- Preformatted block -->
<pre>Branch: main
Author: mobinmithun
Message: fix login crash</pre>

<!-- Link -->
<a href="https://github.com/org/repo/commit/abc123">View commit</a>

<!-- Combined: the real-world pattern used in the session -->
🔔 <b>GitHub Update</b>
Repo: <code>somadhan-legal/mobile-app</code>
Branch: <code>dev</code>
Author: prattoy29
Commit: <code>4d18daa</code> — button fixation
<a href="https://github.com/somadhan-legal/mobile-app">View in GitHub</a>
```

### Replicating the Notion → Telegram flow shown in the session

The session shows task updates arriving in Telegram with this format:
```text
📋 Task Updated
Delivery Date: None → 2026-03-14
Changed at: 06 Mar 2026, 01:34 AM
Edited by: Mobin Mithun

Project: Product Roadmap
Deliverable Status: 🔴🔴🔴
Status: Not started
Priority: ⚠️ Top Ten
Department: Technology
Function: Technology (Data)
Lead: Mobin Mithun

[View in Notion →]
```

This is built with **Make.com** (no code, 15 minutes to set up):

1. Make.com → New scenario
2. Trigger: **Notion** → Watch Database Items (your tasks DB)
3. Action: **Telegram** → Send Message
4. Map Notion fields to the message template above
5. Set the interval to every 15 minutes (free tier) or every
   1 minute (paid)

Alternatively with **n8n** (more powerful, free self-hosted):

1. Trigger: Notion → On Database Item Updated
2. Node: Set → format the message string
3. Node: Telegram → Send Message

### The GitHub → Telegram bot shown in the session (Python)

This is the exact pattern used in the `pack-n-trace` project — a
Python script running as a webhook that fires on every GitHub push:
```python
# github_telegram_bot.py
import os, hmac, hashlib
from flask import Flask, request, abort
import requests

app = Flask(__name__)

BOT_TOKEN       = os.environ["TELEGRAM_BOT_TOKEN"]
CHAT_ID         = os.environ["TELEGRAM_CHAT_ID"]
GITHUB_SECRET   = os.environ["GITHUB_WEBHOOK_SECRET"].encode()

def verify_signature(payload: bytes, signature: str) -> bool:
    expected = "sha256=" + hmac.new(
        GITHUB_SECRET, payload, hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(expected, signature)

def send(text: str):
    requests.post(
        f"https://api.telegram.org/bot{BOT_TOKEN}/sendMessage",
        json={"chat_id": CHAT_ID, "text": text, "parse_mode": "HTML"},
        timeout=10,
    )

@app.route("/webhook/github", methods=["POST"])
def github_webhook():
    sig = request.headers.get("X-Hub-Signature-256", "")
    if not verify_signature(request.data, sig):
        abort(403)

    data   = request.json
    repo   = data["repository"]["name"]
    branch = data["ref"].replace("refs/heads/", "")
    pusher = data["pusher"]["name"]

    for commit in data.get("commits", []):
        short_sha = commit["id"][:7]
        message   = commit["message"].split("\n")[0]   # first line only
        url       = commit["url"]
        send(
            f"📦 <b>GitHub Update</b>\n"
            f"Repo: <code>{repo}</code>\n"
            f"Branch: <code>{branch}</code>\n"
            f"Author: {pusher}\n"
            f"<code>{short_sha}</code> — {message}\n"
            f'<a href="{url}">View in GitHub</a>'
        )
    return "ok", 200

if __name__ == "__main__":
    app.run(port=5000)
```

**Deploy this to Railway or Render (free tier), then in GitHub:**

1. Repo → Settings → Webhooks → Add webhook
2. Payload URL: `https://your-app.railway.app/webhook/github`
3. Content type: `application/json`
4. Secret: your `GITHUB_WEBHOOK_SECRET` value
5. Events: select "Pushes"
6. Done — every push triggers a Telegram message within 2 seconds

### Building a scheduled daily report bot

This pattern sends a summary every morning at 9 AM — useful for
daily standups, revenue updates, or system health checks:
```python
# daily_report.py  — run with: python daily_report.py
import os, schedule, time, requests
from datetime import datetime
import pytz  # pip install pytz

BOT_TOKEN = os.environ["TELEGRAM_BOT_TOKEN"]
CHAT_ID   = os.environ["TELEGRAM_CHAT_ID"]
DHAKA     = pytz.timezone("Asia/Dhaka")

def fetch_metrics():
    # Replace with your actual Supabase or DB queries
    return {
        "new_signups":   42,
        "active_users": 318,
        "revenue_bdt":  "৳ 184,500",
    }

def send_daily_report():
    m   = fetch_metrics()
    now = datetime.now(DHAKA).strftime("%d %b %Y, %I:%M %p")
    text = (
        f"📊 <b>Daily Report — {now}</b>\n"
        f"━━━━━━━━━━━━━━\n"
        f"New signups:  <b>{m['new_signups']}</b>\n"
        f"Active users: <b>{m['active_users']}</b>\n"
        f"Revenue:      <b>{m['revenue_bdt']}</b>\n"
        f"━━━━━━━━━━━━━━"
    )
    requests.post(
        f"https://api.telegram.org/bot{BOT_TOKEN}/sendMessage",
        json={"chat_id": CHAT_ID, "text": text, "parse_mode": "HTML"},
        timeout=10,
    )

schedule.every().day.at("09:00").do(send_daily_report)

while True:
    schedule.run_pending()
    time.sleep(60)
```

### Building a full interactive bot (python-telegram-bot v21)

The python-telegram-bot library version 21.11, released January
2026, provides full support for Telegram Bot API 8.3 and requires
Python 3.9 or higher. For production deployments, webhooks are
the superior choice — they eliminate server polling overhead and
deliver messages instantly.

Use webhooks for production deployments, e-commerce bots requiring
instant order processing, customer support bots, real-time
notification systems, and any bot with more than 100 daily active
users. Use polling only for local development, bots with fewer
than 10 users, or testing environments without HTTPS.
```bash
pip install "python-telegram-bot[all]"
```

```python
# full_bot.py — polling mode (local dev)
import os
from telegram import Update
from telegram.ext import (
    ApplicationBuilder, CommandHandler,
    MessageHandler, ContextTypes, filters
)

TOKEN = os.environ["TELEGRAM_BOT_TOKEN"]

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    name = update.effective_user.first_name
    await update.message.reply_text(
        f"👋 Hello {name}!\n\n"
        "Commands:\n"
        "/stats — view today's metrics\n"
        "/report — trigger a manual report\n"
        "/help — show this message"
    )

async def stats(update: Update, context: ContextTypes.DEFAULT_TYPE):
    # Fetch from your Supabase DB here
    await update.message.reply_text(
        "📊 <b>Today's Stats</b>\n"
        "New users: <b>12</b>\n"
        "Revenue: <b>৳ 24,500</b>",
        parse_mode="HTML"
    )

async def echo(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        f"You said: {update.message.text}"
    )

def main():
    app = ApplicationBuilder().token(TOKEN).build()
    app.add_handler(CommandHandler("start",  start))
    app.add_handler(CommandHandler("stats",  stats))
    app.add_handler(
        MessageHandler(filters.TEXT & ~filters.COMMAND, echo)
    )
    app.run_polling()

if __name__ == "__main__":
    main()
```

### 🔗 All Telegram bot links

| Resource | Link |
|----------|------|
| Telegram Bot API official docs | [core.telegram.org/bots/api](https://core.telegram.org/bots/api) |
| BotFather (create bots) | [@BotFather on Telegram](https://t.me/BotFather) |
| python-telegram-bot library | [python-telegram-bot.org](https://python-telegram-bot.org/) |
| python-telegram-bot docs | [docs.python-telegram-bot.org](https://docs.python-telegram-bot.org/) |
| python-telegram-bot GitHub | [github.com/python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) |
| Telegraf (Node.js library) | [telegraf.js.org](https://telegraf.js.org/) |
| Grammy (modern Node.js bot framework) | [grammy.dev](https://grammy.dev/) |
| Webhook setup guide (python-telegram-bot) | [github.com/python-telegram-bot/wiki/Webhooks](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Webhooks) |
| Polling vs webhook explained | [python-telegram-bot wiki](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Webhooks) |
| Bot API 8.3 changelog | [core.telegram.org/bots/api-changelog](https://core.telegram.org/bots/api-changelog) |
| Telegram Bot tutorial (Toptal) | [toptal.com/python/telegram-bot-tutorial-python](https://www.toptal.com/python/telegram-bot-tutorial-python) |
| Deploy to Railway (free tier) | [railway.app](https://railway.app) |

---

## 🔄 Part 2: No-Code Automation — Make, Zapier, n8n

The session slide shows **Make** and **n8n** as the primary no-code
automation tools alongside Zapier and Replit. These platforms sit
between your triggers (GitHub, Notion, Supabase, forms) and your
delivery channels (Telegram, email, Slack, databases) — connecting
everything without custom code.

### The three platforms at a glance

The no-code and low-code automation market has consolidated around
three distinct tiers. Zapier occupies the premium, ease-first tier
with the largest app ecosystem and the most polished user experience.
Make sits in the middle — more powerful than Zapier, more accessible
than code, and considerably cheaper at equivalent volumes. n8n has
grown from a niche developer tool into a serious enterprise
alternative, particularly after raising $55 million in Series B
funding in 2024 and launching a managed cloud service.

The defining shift of 2025–2026 has been AI integration. All three
platforms now offer native connections to OpenAI, Anthropic, and
Google Gemini, plus purpose-built AI agent workflow templates.

---

### 🟣 Make.com (formerly Integromat)
**Best for: Visual thinkers, complex branching logic, startup teams**

Make offers a European-based automation solution that brilliantly
balances accessibility and technical capability. Its intuitive visual
interface enables the creation of sophisticated automation scenarios
while remaining approachable. The platform positions itself
strategically between Zapier's simplicity and n8n's technical power,
providing an attractive compromise for many organizations.

**Why the session recommends it for startup teams:**
- Visual canvas — you can *see* your automation as a diagram
- Operations-based pricing (much cheaper than Zapier at scale)
- 3,000+ app integrations including Notion, GitHub, Supabase,
  Telegram, Slack, WhatsApp
- Handles routers, iterators, error handlers visually
- Free tier is generous enough for real use

**Pricing (2026):**

| Plan | Price | Operations/mo | Active scenarios |
|------|-------|--------------|-----------------|
| **Free** | $0/mo | 1,000 | 2 |
| **Core** | $9/mo | 10,000 | Active |
| **Pro** | $16/mo | 10,000 + extras | Active |
| **Teams** | $29/mo | 10,000 + collab | Unlimited |

Make's free tier with 1,000 operations monthly is perfect for
testing or lightweight automations, though this limit can vanish
quickly with frequent or multi-step workflows.

**Cost reality check:**
A workflow that triggers on a new Shopify order and performs 10
actions runs 20,000 times per month. On Zapier that's 200,000
tasks — costing well over $500/month. On Make, that's 200,000
operations — also requiring a high-tier plan. This shows that
both Zapier and Make become expensive at high volumes for
complex multi-step flows. At that point n8n self-hosted
is the answer.

**🔗 Make links:**
| Resource | Link |
|----------|------|
| Make homepage | [make.com](https://make.com) |
| Make docs | [make.com/en/help](https://www.make.com/en/help) |
| Make Academy (free courses) | [academy.make.com](https://academy.make.com) |
| Make + Notion integration | [make.com/en/integrations/notion](https://www.make.com/en/integrations/notion) |
| Make + Telegram integration | [make.com/en/integrations/telegram](https://www.make.com/en/integrations/telegram) |
| Make + GitHub integration | [make.com/en/integrations/github](https://www.make.com/en/integrations/github) |
| Make YouTube channel | [youtube.com/@Make](https://www.youtube.com/@Make) |
| Make community forum | [community.make.com](https://community.make.com) |

---

### 🟠 n8n
**Best for: Technical teams, self-hosted, AI agent workflows, high volume**

n8n is the only option with true self-hosting and unlimited
executions. Open-source and self-hostable, n8n eliminates
per-execution pricing entirely on self-hosted deployments.

n8n's pricing structure is a game-changer for businesses that
rely on complex automations. A complex workflow with 75 nodes
that runs 5,000 times counts as just 5,000 executions — not
5,000 × 75 operations. This model means n8n can be 1,000 times
more cost-efficient than Zapier or Make at scale.

**Why n8n is the right choice for technical Hult Prize teams:**
- Self-host on Railway, Render, or a $5/mo VPS → runs free
  forever at unlimited volume
- Every node has a Code tab — write real JavaScript or Python
- 70+ AI nodes with LangChain integration for agent workflows
- Inline logs, data replay, node-by-node inspection for debugging
- n8n 2.0, launched December 2025, added enterprise-grade
  security including isolated code execution and granular
  role-based permissions

**Pricing (2026):**

| Option | Price | Executions | Hosting |
|--------|-------|-----------|---------|
| **Self-hosted (Community)** | **$0 forever** | Unlimited | You manage |
| **Starter (cloud)** | $24/mo | 2,500/mo | Managed |
| **Pro (cloud)** | $60/mo | 10,000/mo | Managed |
| **Enterprise** | Custom | Unlimited | Managed |

**Self-host n8n in 2 minutes with Docker:**
```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

Then open `http://localhost:5678` and start building.
For a permanent deployment, use Railway's one-click n8n template.

**The Notion → Telegram workflow in n8n:**
```text
[Notion trigger: Watch Database Items]
        ↓
[Set: format message string]
        ↓
[Telegram: Send Message to group]
```

This takes about 10 minutes to build and runs free forever on
self-hosted n8n — the same flow would cost $9–$29/mo on Make.

**🔗 n8n links:**
| Resource | Link |
|----------|------|
| n8n homepage | [n8n.io](https://n8n.io) |
| n8n docs | [docs.n8n.io](https://docs.n8n.io) |
| n8n community forum | [community.n8n.io](https://community.n8n.io) |
| n8n self-hosting guide | [docs.n8n.io/hosting](https://docs.n8n.io/hosting/) |
| Docker quick-start | [docs.n8n.io/hosting/installation/docker](https://docs.n8n.io/hosting/installation/docker/) |
| Railway n8n template | [railway.app/template/n8n](https://railway.app/template/n8n) |
| n8n + Notion node | [n8n.io/integrations/notion](https://n8n.io/integrations/notion/) |
| n8n + Telegram node | [n8n.io/integrations/telegram](https://n8n.io/integrations/telegram/) |
| n8n AI agent tutorial | [docs.n8n.io/advanced-ai](https://docs.n8n.io/advanced-ai/) |
| n8n YouTube channel | [youtube.com/@n8n-io](https://www.youtube.com/@n8n-io) |

---

### 🟡 Zapier
**Best for: Non-technical teams, widest app catalog, zero setup**

Launched in 2011, Zapier established itself as the benchmark for
no-code automation. Its primary strength lies in accessibility:
the platform was designed to enable users without technical skills
to create effective automations in minutes. Zapier particularly
shines with its massive integration library, supporting over 8,000
different applications and services.

**When to choose Zapier:**
- Your team has zero technical capacity
- You need a niche app that Make and n8n don't support natively
- You want the fastest time-to-first-automation (minutes, not hours)

**Pricing (2026):**

| Plan | Price | Tasks/mo |
|------|-------|----------|
| **Free** | $0/mo | 100 |
| **Starter** | $19.99/mo | 750 |
| **Professional** | $49/mo | 2,000 |
| **Team** | $69/mo | 2,000 + collab |

**The honest warning:**
Zapier's pricing model punishes complexity and volume. A simple
Zap with 1 trigger and 5 actions uses 5 tasks per run. A complex
workflow that runs 20,000 times per month with 10 actions = 200,000
tasks, requiring a very expensive Company plan costing well over
$500/month. Teams scaling beyond a few hundred automations per day
quickly find Zapier unaffordable.

**🔗 Zapier links:**
| Resource | Link |
|----------|------|
| Zapier homepage | [zapier.com](https://zapier.com) |
| Zapier University (free) | [zapier.com/learn](https://zapier.com/learn) |
| Zapier + Telegram | [zapier.com/apps/telegram/integrations](https://zapier.com/apps/telegram/integrations) |
| Zapier + Notion | [zapier.com/apps/notion/integrations](https://zapier.com/apps/notion/integrations) |

---

### Automation tool decision guide

Choose n8n if you want full code control, self-hosting, or are
building AI-powered automation pipelines. Choose Zapier if your
team is non-technical and you need the widest app catalog with
zero setup. Choose Make if you think visually, need complex
branching logic, and want a lower price than Zapier.

| Situation | Tool |
|-----------|------|
| Non-technical team, need it working today | Zapier |
| Visual thinker, moderate complexity, startup budget | **Make** |
| Technical team, high volume, self-hosted | **n8n** |
| Building AI agent workflows | n8n (LangChain nodes) |
| Sensitive data, can't use cloud | n8n self-hosted |
| Need one very specific niche app | Zapier |
| Hult Prize team on zero budget | n8n self-hosted |

---

## 🚀 Part 3: AI Agents at Scale

The session closes with two slides that reframe the entire session:
Mira Murati raised $2B with no product and no deck on the strength
of reputation and vision alone. Alex Wang secured a $14B investment
from Meta for Scale AI's model training data infrastructure.

The lesson: **the market for AI infrastructure and automation is
the largest technology opportunity in history.** Your Hult Prize
MVP is not just a student project — it is a proof of concept for
a category that will define the next decade.

### What AI agents actually are

An AI agent is a system that perceives its environment, reasons
about what to do, and takes actions — repeatedly — until a goal
is accomplished. Unlike a chatbot (one question, one answer), an
agent runs a loop: observe → plan → act → observe → plan → act.

The session shows this concretely: Claude + MCP + Skills is already
an agent system. Claude (the reasoning model) + Supabase MCP (the
data access) + your SKILL.md files (the procedures) = an agent that
can execute multi-step tasks in your startup's context.

### Agent frameworks to explore

| Framework | Best for | Language | Link |
|-----------|----------|----------|------|
| **Claude Code** | Agentic coding, full codebase tasks | Any | [docs.anthropic.com/claude-code](https://docs.anthropic.com/en/docs/claude-code) |
| **LangChain** | Building LLM-powered agents, RAG, chains | Python / JS | [langchain.com](https://python.langchain.com) |
| **CrewAI** | Multi-agent orchestration (agents with roles) | Python | [crewai.io](https://crewai.io) |
| **AutoGen (Microsoft)** | Conversational multi-agent systems | Python | [microsoft.github.io/autogen](https://microsoft.github.io/autogen/) |
| **n8n AI nodes** | Visual agent workflows, no code | Visual | [docs.n8n.io/advanced-ai](https://docs.n8n.io/advanced-ai/) |
| **LlamaIndex** | Data agents, document Q&A, RAG | Python | [llamaindex.ai](https://llamaindex.ai) |

### The simplest possible AI agent (Claude API)
```python
import anthropic
import json

client = anthropic.Anthropic()

# Define a tool the agent can call
tools = [{
    "name": "get_farmer_data",
    "description": "Fetch farmer loan application data from database",
    "input_schema": {
        "type": "object",
        "properties": {
            "farmer_id": {"type": "string",
                          "description": "The farmer's ID"}
        },
        "required": ["farmer_id"]
    }
}]

def run_agent(user_message: str):
    messages = [{"role": "user", "content": user_message}]

    while True:
        response = client.messages.create(
            model="claude-sonnet-4-5",
            max_tokens=1024,
            tools=tools,
            messages=messages,
        )

        # If Claude wants to use a tool, execute it
        if response.stop_reason == "tool_use":
            tool_use = next(
                b for b in response.content
                if b.type == "tool_use"
            )
            # Simulate fetching from DB
            result = {"name": "Rahim", "credit_score": 720,
                      "loan_history": "clean"}

            messages.append({"role": "assistant",
                             "content": response.content})
            messages.append({
                "role": "user",
                "content": [{"type": "tool_result",
                              "tool_use_id": tool_use.id,
                              "content": json.dumps(result)}]
            })
        else:
            # Agent is done — return final answer
            return response.content[0].text

answer = run_agent("What is the credit profile of farmer F-1042?")
print(answer)
```

### 🔗 AI agent learning resources

| Resource | Link |
|----------|------|
| Building effective agents (Anthropic) | [anthropic.com/research/building-effective-agents](https://www.anthropic.com/research/building-effective-agents) |
| LangChain quickstart | [python.langchain.com/docs/get_started/quickstart](https://python.langchain.com/docs/get_started/quickstart) |
| CrewAI docs | [docs.crewai.com](https://docs.crewai.com) |
| Claude Code docs | [docs.anthropic.com/en/docs/claude-code](https://docs.anthropic.com/en/docs/claude-code) |
| Anthropic API quickstart | [docs.anthropic.com/en/api/getting-started](https://docs.anthropic.com/en/api/getting-started) |
| n8n AI agent guide | [docs.n8n.io/advanced-ai/intro-tutorial](https://docs.n8n.io/advanced-ai/intro-tutorial/) |

---

## 📚 Learning Resources

### Books

| Book | Why read it | Link |
|------|-------------|------|
| **The Personal MBA** — Josh Kaufman | Business systems thinking for founders | [personalmba.com](https://personalmba.com) |
| **Zero to One** — Peter Thiel | Building companies that matter | [zerotoonebook.com](http://zerotoonebook.com/) |
| **The Hard Thing About Hard Things** — Ben Horowitz | Real startup war stories | [a16z.com](https://a16z.com/books/the-hard-thing-about-hard-things/) |

### Courses and videos

| Resource | Link |
|----------|------|
| Make.com Academy (free) | [academy.make.com](https://academy.make.com) |
| n8n crash course (YouTube) | [youtube.com/@n8n-io](https://www.youtube.com/@n8n-io) |
| Python Telegram bot tutorial (freeCodeCamp) | [youtube.com/watch?v=vZtm1wuA2yc](https://www.youtube.com/watch?v=vZtm1wuA2yc) |
| LangChain crash course | [youtube.com/@SamWitteveen](https://www.youtube.com/@samwitteveenprogramming8084) |
| Building AI agents (Anthropic YouTube) | [youtube.com/@Anthropic](https://www.youtube.com/@Anthropic) |

---

## ⚡ Quick-Start Checklist for Hult Prize Teams
```text
Telegram bot (30 minutes to first message):
[ ] 1.  Open Telegram → search @BotFather → /newbot
[ ] 2.  Save your bot token in .env file
[ ] 3.  Add bot to your team Telegram group
[ ] 4.  Get your group chat ID via the getUpdates API call
[ ] 5.  Run the simple send() function — confirm a message arrives
[ ] 6.  Add Telegram notifications to your GitHub deploy script
[ ] 7.  Set up a daily report with your core metrics

Automation flows (1 hour to first live flow):
[ ] 8.  Sign up for Make.com (free tier)
[ ] 9.  Connect Notion → Telegram (task update flow)
[ ] 10. Connect GitHub → Telegram (push notification flow)
[ ] 11. Connect Tally form submission → Telegram (new user signup alert)
[ ] 12. If technical: self-host n8n on Railway for free unlimited runs

AI agents (when you're ready to scale further):
[ ] 13. Get an Anthropic API key — console.anthropic.com
[ ] 14. Run the simple agent example above
[ ] 15. Connect Claude to your Supabase MCP server (see Chapter 4)
[ ] 16. Explore LangChain or CrewAI for multi-step agent workflows
```

---

## 💬 Discussion

Questions from this chapter?
**[Ask in Discussions →](https://github.com/MobinMithun/hult-prize-mvp-to-ai-agents/discussions)**

Common questions from past sessions:
- *"How do I stop Telegram from flooding our group with every tiny commit?"*
- *"Is Make free tier enough for a real product launch?"*
- *"n8n Docker keeps crashing — how do I keep it running permanently?"*
- *"What's the cheapest way to run a scheduled Python script 24/7?"*
- *"How do I connect Claude to my own Supabase database as an agent?"*
