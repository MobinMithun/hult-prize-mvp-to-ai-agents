# 🧱 Chapter 2: Choose Your Stack

> *"Your first product won't be perfect. Make it anyway."*

The tools you choose determine how fast you can ship — not how good your
product eventually becomes. This chapter covers every tool shown in the
session, with up-to-date pricing, honest comparisons, and prompts to
get started immediately.

---

## The Decision Framework

Before picking a tool, answer two questions:

1. **Can I write code?** → If yes, VS Code + Copilot. If no, Lovable or Bolt.
2. **Do I need a full product or just a prototype?** → Full product needs
   a backend (Supabase). A prototype just needs a live URL to share.

---

## 🤖 AI Prototyping Tools (shown in the session)

These are tools that turn a plain English description into a working,
deployable app — no traditional coding required.

AI prototyping tools like Lovable, Bolt, Replit, and v0 are
fundamentally changing how we go from idea to interface, skipping multiple
layers of traditional workflows. With a solid prompt, each of them can
generate results that would have once taken a small team of designers and
developers weeks to produce.

---

### 🩷 Lovable
**Best for: Non-technical founders, UI-heavy MVPs, full-stack without yak-shaving**

If you want one tool that lets you build anything from a throwaway
prototype to an internal tool or small production-ready app without staring
at code all day, choose Lovable. v0 is the second-best fit.

Lovable generates production-ready full-stack code, commits directly
to GitHub, and deploys via Lovable Cloud. Teams can create private projects,
connect custom domains, and remove branding on paid tiers.

**Pricing (2026):**
| Plan | Price | What you get |
|------|-------|-------------|
| Free | $0/mo | 5 messages/day, unlimited public projects |
| Pro | $25/mo | 100 credits/mo, private projects, custom domains |
| Teams | $30/mo | 20 seats, centralized billing |

**Strengths:**
- Click-to-select any element in the preview and chat about it directly
- Native Supabase integration for auth + database
- Built-in Knowledge Base: define your stack, conventions, design rules
- Commits directly to GitHub — you own the code
- `lovable.dev` deployment out of the box

**Weaknesses:**
- Requires you to connect Supabase yourself (can confuse beginners)
- Lovable generates beautiful React code but then asks you to "connect
  Supabase" — for a non-technical user this can mean 3 days trying to
  debug why form submissions aren't saving
- Less suited for complex custom backends or non-React frameworks

**🔗 Links:**
- [lovable.dev](https://lovable.dev)
- [Lovable docs](https://docs.lovable.dev)
- [Lovable + Supabase integration guide](https://docs.lovable.dev/integrations/supabase)
- [Lovable YouTube tutorials](https://www.youtube.com/@Lovable-dev)

**🚀 Starter prompt for Hult Prize teams:**
```text
Build a web app for [your startup name]. It should have:
- A landing page with a hero section, problem statement, and waitlist signup
- An admin dashboard showing signups with name, email, and date
- A Supabase backend with auth
- Clean, modern UI using Tailwind and shadcn

The product is [one sentence description]. Target users are [describe them].
```

---

### ⬛ v0 by Vercel
**Best for: React UI components, frontend-first, Next.js projects**

v0 is an AI-powered prompt-to-UI tool designed by Vercel. It generates
clean, ready-to-use React + Tailwind components from natural language prompts.
You can copy the code, tweak it, and export it to your local dev environment.

v0 is the best vibe coding tool if you're someone who can actually code.
It tries to strike a very different balance between ease of use and
customization, leaning heavily toward the latter. It also has the smoothest,
fastest, and most accessible publishing and deployment flow of any of these
tools — unsurprising given it's from the Vercel team.

**Pricing (2026):**
| Plan | Price | What you get |
|------|-------|-------------|
| Free | $0/mo | $5 in credits every month |
| Pro | $20/mo | $20 in credits, faster generation |
| Team | $30/user/mo | Collaboration, SOC2, audit logs |

**Strengths:**
- Best-in-class component output quality
- One-click Vercel deployment
- Planning mode — tell it to plan before building
- Supports full-stack (backend routes + Supabase)
- Fast iteration on existing codebases

**Weaknesses:**
- Tightly coupled to Vercel/Next.js ecosystem
- v0 generates shadcn/ui components rather than full applications —
  better used to compose components into apps than to generate apps
  from scratch
- Credit system can feel limiting for heavy users

**🔗 Links:**
- [v0.dev](https://v0.dev)
- [v0 documentation](https://vercel.com/docs/v0)
- [v0 prompt guide](https://v0.dev/faq)

**🚀 Starter prompt:**
```text
Create a dashboard for a [legal tech / agri-fintech / logistics] startup.
Include:
- Sidebar navigation with icons
- Stats cards (total users, active sessions, revenue)
- A line chart showing growth over 30 days
- A data table with sortable columns
Use shadcn/ui and Tailwind. Dark mode compatible.
```

---

### ⚡ Bolt.new
**Best for: Rapid prototyping, full-stack MVPs, sharing fast**

Bolt is strong for prototyping because it bundles more of the launch
plumbing into the experience. Use it when you want to build a prototype
for a scheduling app, booking flow, or niche community site and share
it quickly.

Bolt supports full GitHub sync and React Native via Expo, letting you
build native apps and web apps from the same codebase — useful if your
end goal is publishing to the App Store or Google Play.

**Pricing (2026):**
| Plan | Price | What you get |
|------|-------|-------------|
| Free | $0/mo | Limited tokens/month, public deployment |
| Pro | $20/mo | More tokens, private projects, custom domains |

**Strengths:**
- Built-in Supabase backend (zero configuration)
- Full GitHub two-way sync
- Supports React Native (Expo) for mobile apps
- Netlify deployment built in
- Strong for non-React frameworks (Angular, Vue)

**Weaknesses:**
- Bolt.new users report frustrations with its token-based system;
  simple fixes can consume a significant number of tokens
- UX can feel rougher than Lovable for first-time builders
- Generates more bugs that require manual debugging sessions

**🔗 Links:**
- [bolt.new](https://bolt.new)
- [Bolt documentation](https://docs.bolt.new)
- [Bolt GitHub integration guide](https://docs.bolt.new/github)

---

### 🔁 Replit
**Best for: Learning to code while building, cloud IDE, collaboration**

Replit was the most feature-rich, well thought-out, and powerful of the
major vibe coding tools. If you'd personify the Replit Agent, it feels like
that zany engineer friend who chaotically works all night, zigging and
zagging, but somehow the final product is actually amazing.

Replit stands out with a user base of 40 million app creators and robust
live collaboration features. It supports real-time collaboration and
one-click deployments, and it's especially useful for students and teams
with varying technical backgrounds.

**Pricing (2026):**
| Plan | Price | What you get |
|------|-------|-------------|
| Free | $0/mo | Basic compute, public apps |
| Core | $25/mo | More compute, private projects, custom domains |
| Teams | Custom | Shared workspace, admin controls |

**Strengths:**
- Zero local setup — build entirely in browser
- Supports 50+ languages
- Best for learning: you see the code as it's generated
- Full-stack with built-in database and auth
- GitHub import/export for existing codebases
- React Native (Expo) support for mobile

**🔗 Links:**
- [replit.com](https://replit.com)
- [Replit Agent docs](https://docs.replit.com/replit-ai/replit-agent)
- [Replit for Education](https://replit.com/site/teams-for-education)

---

### 🤖 Manus (now part of Meta)
**Best for: Autonomous multi-step tasks, research, agentic workflows**

This one is different from the others — Manus is not a code generator.
It's an **autonomous AI agent** that executes tasks on your behalf.

Manus AI is an autonomous AI agent that plans and completes multi-step
tasks with minimal prompting. Unlike a chatbot, it runs an agent loop —
analyze, pick tools, execute in a Linux sandbox, refine, and return
structured results.

In December 2025, Meta announced that it would acquire Manus. Meta said
it would continue to operate and sell the Manus service and integrate its
technology into products including Meta AI. Manus said it would continue
offering subscriptions through its own app and website.

**What Manus can do for startup founders:**
- Deep market research → structured report, automatically
- Competitor analysis across 20+ sources → synthesized output
- Building a prototype website from a single description
- Sorting resumes, analyzing data, drafting outreach campaigns
- Running scheduled reports and sending them to your inbox

Manus AI works well for simple, repetitive digital tasks that don't
require advanced customization. It's easy to set up, runs quietly in the
background, and handles focused workflows like research, reporting, or
data collection without much oversight.

**Pricing:** $39–$200/month (credit-based). Access via manus.im.

**🔗 Links:**
- [manus.im](https://manus.im)
- [MIT Technology Review: Manus review](https://www.technologyreview.com/2025/03/11/1113133/manus-ai-review/)
- [What is Manus AI — full guide](https://www.singlegrain.com/digital-marketing/manus-ai-the-ultimate-guide-to-understanding-and-using-it/)

---

### 🆓 Google AI Studio *(shown in session as "Free")*
**Best for: Prototyping AI features, free Gemini API access, experimentation**

Google AI Studio is the best free way to access frontier AI models in
2026. Where else can you test Gemini 3 Pro (the same model that costs
$19.99/month elsewhere), generate images, create videos, and export
working code to your applications — all without entering a credit card?

Google AI Studio is provided as a free interface with no monthly fee,
no seat-based pricing, and no standalone billing model. Users can access
AI Studio with a standard Google account and begin prompting Gemini models
immediately.

**What you get for free (2026):**
| Model | Requests/day | Tokens/min |
|-------|-------------|------------|
| Gemini 2.5 Pro | 100 req/day | 250,000 |
| Gemini 2.5 Flash | 250 req/day | 250,000 |
| Google AI Studio UI | Free in all regions | No hard limit |

**Important caveat:** Google uses your prompts to train their models on the
free tier. For prototyping and experimentation, this trade-off is
acceptable. For anything sensitive, you'll need to enable billing.

**What to use it for as a startup:**
- Test your AI feature idea before paying for API access
- Generate working React + Tailwind code from a prompt (Vibe Code feature)
- Prototype chatbots, search features, classification systems
- Export to your codebase once validated

**🔗 Links:**
- [aistudio.google.com](https://aistudio.google.com)
- [Gemini API pricing](https://ai.google.dev/gemini-api/docs/pricing)
- [Google AI Studio 2026 guide](https://www.shipai.dev/blog/google-ai-studio-2026-guide)
- [Free tier rate limits explained](https://blog.laozhang.ai/en/posts/gemini-api-free-tier)

---

## 🛠️ Full Comparison Table

| Tool | Technical skill needed | Backend | Free tier | Best use case |
|------|----------------------|---------|-----------|---------------|
| **Lovable** | None | Supabase (manual) | 5 msg/day | Full MVP, non-technical founder |
| **v0** | Some (React) | Supabase | $5 credits/mo | UI components, Next.js apps |
| **Bolt.new** | Low | Built-in | Limited tokens | Quick prototype, mobile-ready |
| **Replit** | Low-Medium | Built-in | Free tier | Learning + building, collaboration |
| **Manus** | None (agentic) | N/A | No | Research, autonomous task execution |
| **Google AI Studio** | None to medium | N/A | **Completely free** | AI feature prototyping |
| **VS Code + Copilot** | High | You choose | Copilot Free (limited) | Production-grade development |

---

## 💻 VS Code + GitHub Copilot (shown in session)

The developer's choice — maximum control, maximum power.

### VS Code
Free, open-source code editor from Microsoft. The most popular editor
in the world. Install it, add extensions, and it becomes a full IDE.

- 🔗 [code.visualstudio.com](https://code.visualstudio.com/)
- 🔗 [VS Code docs](https://code.visualstudio.com/docs)

**Must-have extensions for startup development:**
| Extension | What it does |
|-----------|-------------|
| GitHub Copilot | AI code completion + chat |
| Prettier | Auto-format your code |
| ESLint | Catch JS/TS bugs before they ship |
| Tailwind CSS IntelliSense | Autocomplete Tailwind classes |
| GitLens | See who wrote every line and why |
| Thunder Client | Test APIs without leaving VS Code |
| Error Lens | Show errors inline as you type |

### GitHub Copilot — Free Tiers

GitHub Copilot brings AI agents to Visual Studio Code. Describe what you
want to build, and an agent plans the approach, writes the code, and verifies
the result across your entire project. It can run locally, in the background,
or in the cloud.

**Copilot Free (no credit card):**
GitHub Copilot Free provides 2,000 completions and 50 chat requests
(including Copilot Edits) per month. No trial. No credit card required.
Just your GitHub account.

**Copilot Pro for students (completely free):**
Verified students get Copilot Pro completely free through GitHub Education.
You get unlimited code completion with no hard usage cap for everyday coding,
plus Copilot Chat as a programming assistant. The benefit is tied to your
student status and regularly re-evaluated.

**How to get it free as a student:**
1. Go to [education.github.com/pack](https://education.github.com/pack)
2. Apply with your university email + student ID
3. Once verified, go to GitHub → Settings → Copilot → Enable
4. Install the GitHub Copilot extension in VS Code
5. Done — full Copilot Pro, free

Verified students also get one free voucher code for either the
GitHub Foundations or Copilot Certification exam. Current coupons expire
June 30, 2026.

**🔗 Copilot links:**
- [GitHub Copilot plans](https://github.com/features/copilot/plans)
- [GitHub Student Developer Pack](https://education.github.com/pack)
- [Set up Copilot in VS Code](https://code.visualstudio.com/docs/copilot/setup)
- [Copilot getting started tutorial](https://code.visualstudio.com/docs/copilot/getting-started)
- [Copilot cheat sheet](https://code.visualstudio.com/docs/copilot/reference)

**🚀 Key Copilot commands to know:**
```text
Ctrl+I (Cmd+I on Mac)    -> Open inline chat, describe what you want
Ctrl+Alt+I               -> Open Copilot Chat panel
Tab                      -> Accept a suggestion
Esc                      -> Dismiss a suggestion
/explain                 -> Explain selected code
/fix                     -> Fix a bug in selected code
/tests                   -> Generate unit tests
/doc                     -> Generate documentation
```

---

## 🎨 UI/UX Design Inspiration (shown in session)

Before you build, you need to know what good looks like.

| Platform | What it's for | Link |
|----------|--------------|------|
| **Behance** | Portfolio-quality design work, case studies | [behance.net](https://behance.net) |
| **Awwwards** | Award-winning websites, cutting-edge web design | [awwwards.com](https://awwwards.com) |
| **Dribbble** | UI shots, product design, micro-interactions | [dribbble.com](https://dribbble.com) |
| **Pinterest** | Mood boards, color palettes, visual references | [pinterest.com](https://pinterest.com) |
| **Mobbin** | Real app UI screenshots — iOS + Android | [mobbin.com](https://mobbin.com) |
| **Figma Community** | Free design files, UI kits, templates | [figma.com/community](https://figma.com/community) |
| **Landingfolio** | Landing page inspiration + templates | [landingfolio.com](https://www.landingfolio.com) |
| **SaaS Pages** | Real SaaS product landing pages | [saaspages.xyz](https://saaspages.xyz) |
| **UIverse** | Open-source UI components (copy free) | [uiverse.io](https://uiverse.io) |
| **Checklist Design** | Best practices for UI patterns | [checklist.design](https://www.checklist.design) |

### How to use these effectively
1. **Before you prompt:** Search Mobbin for apps similar to yours and
   screenshot 5–10 screens you like.
2. **Paste in your prompt:** Upload the screenshots to Lovable/Bolt/v0
   and say "build something with this vibe."
3. **After you build:** Check Awwwards for polish inspiration.
4. **For your landing page:** Study SaaS Pages and Landingfolio —
   the best landing pages all follow similar structural patterns.

---

## 🖊️ Pencil.dev → Figma Workflow (shown in session)

The fastest wireframe-to-design pipeline for non-designers.

**Step 1 — Wireframe in Pencil.dev**
- Free and open-source
- Drag-and-drop UI elements (buttons, forms, inputs, navbars)
- Sketch all your screens in 30–60 minutes
- 🔗 [pencil.evolus.vn](https://pencil.evolus.vn/)

**Step 2 — Export to Figma**
- The Pencil → Figma plugin converts your sketches to editable frames
- Outputs: auto-layout, editable layers, SVG icons, styles
- You keep: the exact structure and placement of every element

**Step 3 — Polish in Figma**
- Apply your brand colors, typography, and spacing
- Share with your team for feedback
- Hand off to developers with exact measurements

**Alternative workflow (faster, AI-powered):**
- Describe your app to **Lovable** or **v0**
- Generate a live prototype in minutes
- Screenshot the result
- Import screenshot into Figma for manual polish
- This skips wireframing entirely for simple apps

---

## 📚 Learning Resources

### Courses (free)
| Resource | What you'll learn | Link |
|----------|------------------|------|
| freeCodeCamp | HTML, CSS, JavaScript, React from zero | [freecodecamp.org](https://freecodecamp.org) |
| The Odin Project | Full-stack web development, project-based | [theodinproject.com](https://www.theodinproject.com) |
| CS50 (Harvard, free) | Programming fundamentals, Python, web | [cs50.harvard.edu](https://cs50.harvard.edu) |
| Scrimba | Interactive coding in the browser | [scrimba.com](https://scrimba.com) |
| Fireship on YouTube | Fast, visual explanations of every web tech | [youtube.com/@Fireship](https://www.youtube.com/@Fireship) |

### Understand the stack used by these tools
All four major AI prototyping tools (Lovable, v0, Bolt, Replit) default
to the same technology stack:
```text
Frontend:  React + Tailwind CSS + shadcn/ui
Backend:   Supabase (PostgreSQL + Auth + Storage)
Hosting:   Vercel or Netlify
Language:  TypeScript
```

Learning these five things will let you understand, edit, and debug
everything these tools produce.

| Technology | Best free resource |
|-----------|-------------------|
| **React** | [react.dev/learn](https://react.dev/learn) (official, free) |
| **Tailwind CSS** | [tailwindcss.com/docs](https://tailwindcss.com/docs) |
| **shadcn/ui** | [ui.shadcn.com](https://ui.shadcn.com) |
| **Supabase** | [supabase.com/docs/guides/getting-started](https://supabase.com/docs/guides/getting-started) |
| **TypeScript** | [typescriptlang.org/docs](https://www.typescriptlang.org/docs/) |

---

## 🧪 Which tool should YOUR team use right now?

If you're a **Hult Prize team** with non-technical members and a deadline:
```text
Day 1–2:   Lovable -> Get a working prototype live with Supabase
Day 3–4:   Show it to 5 real users, collect feedback
Day 5–7:   Iterate in Lovable or export to VS Code for custom changes
Week 2+:   If you need to go deeper, move to VS Code + Copilot
```

If you're a **technical founder** already comfortable with code:
```text
Start:     VS Code + GitHub Copilot (Pro if you're a student — it's free)
Database:  Supabase
Deploy:    Vercel
AI APIs:   Google AI Studio to prototype, then pay-as-you-go Gemini API
```

---

## 💬 Discussion

Questions from this chapter? **[Ask in Discussions →](https://github.com/MobinMithun/hult-prize-mvp-to-ai-agents/discussions)**

Common questions:
- *"Lovable broke after 10 prompts — what do I do?"*
- *"How do I export from Lovable and edit the code myself?"*
- *"Is Google AI Studio really free? What's the catch?"*
- *"Which tools work best for mobile app development?"*
