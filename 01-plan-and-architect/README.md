# 📐 Chapter 1: Plan & Architect

> *"Keep it simple, or no one cares."*

Before writing a single line of code, the best founders spend time mapping
out what they're actually building. This chapter covers the tools and
techniques shown in the session — from brainstorming to process flows to
product roadmaps.

---

## The 4-Phase Planning Flow

| Phase | What it is | Key output |
|-------|-----------|------------|
| **Ideate** | Brainstorm the problem + solution space | Sticky notes, mind maps |
| **Map process** | Document every step and decision in the workflow | Swimlane / flowchart diagram |
| **Roadmap** | Prioritize features across modules and surfaces | Notion database / Gantt |
| **Design** | Translate roadmap into UI wireframes | Figma / Pencil.dev screens |

---

## 🧩 Tool 1: FigJam (Process Mapping & Brainstorming)

**What it is:** FigJam is Figma's collaborative online whiteboard. It's shown
in the session as the tool for building the **Digital Loan Flow** diagram —
a swimlane flowchart covering every step from phone OTP to loan disbursement.

**Why startups love it:**
- Over 300 templates available — flowcharts, customer journey maps,
  roadmaps, timelines, retrospectives, and more.
- Multiple stakeholders and team members can work on a FigJam board
  simultaneously without any lag, which makes it ideal for
  cross-functional planning.
- FigJam AI lets you use a simple prompt to create meeting templates,
  visualize timelines, and sort stickies into themes — all in seconds.

**Free tier:** Included with all Figma seats. 3 shared boards on the free plan.

### 🔗 Links
- [FigJam homepage](https://www.figma.com/figjam/)
- [FigJam Getting Started Guide](https://www.figma.com/best-practices/collaborating-in-figjam/)
- [FigJam Template Gallery](https://www.figma.com/community/figjam)
- [FigJam vs Miro vs Mural — 2026 comparison](https://www.gend.co/blog/miro-vs-figjam-vs-mural)

### 🚀 Prompts to try in FigJam AI
```text
Create a swimlane diagram for a [your product] user onboarding flow with
columns for: User, App, Backend, and Third-party services.
```

```text
Map out the decision points for a loan application process in Bangladesh,
showing what happens at each approval or rejection step.
```

### How it was used in the session (WeGro / Digital Loan Flow)
The slide shows a multi-lane process map with:
- **Bank lane**: Phone OTP → NID verification → Loan application → CIB
  check (RPA) → Document signing → Backend check → Disbursement
- **WeGro lane**: Farmer Application → OGRO App → Credit Scoring →
  Project Approval
- Integration between both via **WeGro API**

This exact type of diagram is what you need to build **before** you touch
any code. It becomes your spec sheet.

---

## 🧩 Tool 2: Notion (Product Roadmap)

**What it is:** Notion is an all-in-one workspace combining notes, wikis,
databases, and now autonomous AI agents. The session shows it being used
to build the **Somadhan Legal** product roadmap — a full database tracking
every feature, its module, purpose, surface (Mobile/Backend/Dashboard),
database entities, and app view.

**Why it works for startups:**
- Notion AI can summarize research notes, cluster feedback themes,
  and turn raw input into clear insights far more quickly.
- Notion 3.0, launched in September 2025, introduces autonomous AI
  Agents that fundamentally transform productivity from "AI that suggests"
  to "AI that executes."
- Notion AI streamlines project documentation by generating PRDs,
  user stories, and technical specifications from simple prompts,
  eliminating blank page syndrome.

**Free tier:** Free for individuals. Unlimited pages + blocks. AI is a
paid add-on ($10/member/month).

### 🔗 Links
- [Notion homepage](https://notion.so)
- [Notion AI features](https://www.notion.com/product/ai)
- [Notion for Product Management](https://www.notion.com/use-case/product-management)
- [What's new in Notion 2026](https://www.notion.com/releases)
- [Product Roadmap Templates (free)](https://www.notion.com/templates/category/product-roadmap)
- [7 Best Notion Roadmap Templates 2026](https://www.notionland.co/post/notion-roadmap)

### Free Notion Templates (use directly)
| Template | Use case | Link |
|----------|----------|------|
| Product Roadmap Planner | Agile team roadmap with Kanban + timeline views | [notion.com/templates](https://www.notion.com/templates/notion-product-roadmap) |
| Simple Roadmap | Lightweight for solo founders | [notion.com/templates](https://www.notion.com/templates/roadmap) |
| Product Roadmap 2026 | Updated for current year | [notion.com/templates](https://www.notion.com/templates/notion-product-roadmap) |

### What the Somadhan Legal roadmap contained (from the slide)
Each row had:
- **Item Name** — e.g. Account Overview Screen
- **Module** — e.g. Account & Settings
- **Purpose** — e.g. "Provide centralized access to..."
- **Product Surface** — Mobile App / Backend / Dashboard
- **Database Entities** — the specific DB tables needed
- **App View** — Client App / Admin

This structure is the difference between a startup that ships predictably
and one that always feels chaotic.

### 🚀 Prompts to try in Notion AI
```text
Create a product roadmap table for a [legal tech / agri-fintech /
healthcare] startup with columns: Feature Name, Module, Purpose,
Product Surface (Mobile/Backend/Dashboard), Database Entities,
Priority, and Status.
```

```text
Write a one-paragraph PRD for [feature name] in the context of
[your startup's product]. Include: user problem, proposed solution,
success metrics, and out-of-scope items.
```

```text
I have [X] features backlogged. Help me prioritize them using the
MoSCoW method (Must have, Should have, Could have, Won't have).
```

---

## 🧩 Tool 3: Process Mapping (Concepts & Frameworks)

Process mapping is not a tool — it's a skill. Understanding the different
types of diagrams helps you pick the right one for the right situation.

### Types of Process Maps

| Type | Best for | Example |
|------|----------|---------|
| **Swimlane flowchart** | Multi-team/multi-system workflows | WeGro's Digital Loan Flow |
| **High-level flowchart** | Overview for non-technical stakeholders | User onboarding summary |
| **User journey map** | Mapping emotion + steps of user experience | Customer support flow |
| **SIPOC diagram** | High-level: Suppliers → Inputs → Process → Outputs → Customers | Pre-planning sessions |
| **Value stream map** | Identifying waste and delays in a process | Manufacturing / fulfillment |

A swimlane diagram organizes a process by separating responsibilities
into horizontal or vertical "lanes" — each lane represents a person, role,
or team — making it ideal for clarifying roles in multi-team processes.

### Process Mapping Tools

| Tool | Free tier | Best for | Link |
|------|-----------|----------|------|
| **FigJam** | 3 boards free | Collaborative, visual-first | [figma.com/figjam](https://figma.com/figjam) |
| **draw.io (diagrams.net)** | Completely free | Technical, offline-friendly | [draw.io](https://draw.io) |
| **Lucidchart** | 3 free docs | Complex BPMN diagrams | [lucidchart.com](https://lucidchart.com) |
| **Whimsical** | Limited free | Clean user flows + wireframes | [whimsical.com](https://whimsical.com) |
| **Miro** | 3 free boards | Enterprise workshops | [miro.com](https://miro.com) |
| **Mural** | 30-day trial | Facilitated workshops | [mural.co](https://mural.co) |

### 🔗 Learning resources
- [What is Process Mapping? (Asana, 2026)](https://asana.com/resources/process-mapping)
- [Process Mapping Guide + Symbols (Lucidchart)](https://www.lucidchart.com/pages/tutorial/process-mapping-guide-and-symbols)
- [15 Process Map Examples with Templates](https://www.nutrient.io/blog/process-mapping-examples/)
- [Business Process Mapping Best Practices (Kissflow)](https://kissflow.com/workflow/bpm/business-process-mapping/)

### Steps to map your startup's core process
1. **Identify the process** — pick the most critical workflow (e.g.
   user sign-up, order fulfillment, loan disbursement)
2. **List all actors** — user, backend, third-party APIs, your team
3. **Draw the swimlanes** — one lane per actor
4. **Map every step** — include decision points (diamond shapes),
   success paths, and failure/rejection paths
5. **Validate with your team** — walk through it together; you'll
   always find missing steps
6. **Convert to spec** — the process map becomes your engineering spec

---

## 🧩 Tool 4: Miro (Alternative to FigJam)

**What it is:** Miro is a broader collaborative workspace, stronger than
FigJam for enterprise-scale workshops but with a steeper learning curve.

Miro is the most flexible for cross-functional work and enterprise
scale, with strong governance options and frequent product updates. FigJam
is simplest for teams already in Figma. Mural is facilitation-led, with
enterprise controls built for structured workshops.

**When to choose Miro over FigJam:**
- Your team doesn't use Figma
- You need integrations with Jira, Asana, Slack, Microsoft 365
- You're running large-scale workshops (50+ participants)
- You need GDPR/CCPA-compliant data handling

**Free tier:** 3 editable boards.

### 🔗 Links
- [Miro homepage](https://miro.com)
- [Miro Process Mapping](https://www.mural.co/use-case/process-mapping)
- [300+ Miro Templates](https://miro.com/templates/)

---

## 🧩 Tool 5: Whimsical (Clean Flowcharts Fast)

**What it is:** Whimsical is purpose-built for user flows, wireframes,
and flowcharts. If you need to diagram a user journey quickly, it's faster
than FigJam.

**Why it's good for startups:**
- AI-powered flowchart generation from text descriptions
- Smart connectors with auto-layout
- Built-in wireframing components

**Free tier:** Limited files.

### 🔗 Links
- [Whimsical homepage](https://whimsical.com)
- [Whimsical flowchart templates](https://whimsical.com/templates/flowcharts)

---

## 🧩 Tool 6: Pencil.dev → Figma Workflow

**What it is:** The session slide shows a direct export from **Pencil.dev**
sketches into editable Figma frames. This is the fastest way to go from
rough wireframe to polished design.

**Workflow:**
1. Sketch rough screens in **Pencil.dev** (free, open-source)
2. Export to Figma with auto-layout, editable layers, SVG icons, and styles
3. Polish in Figma before handing off to developers

**Free tier:** Pencil.dev is open-source and free.

### 🔗 Links
- [Pencil.dev (open source wireframing)](https://pencil.evolus.vn/)
- [Pencil to Figma export plugin](https://www.figma.com/community)

---

## 📚 Further Reading & Learning

### Books
| Book | Why read it | Link |
|------|------------|------|
| **The Mom Test** — Rob Fitzpatrick | Validate your plan before you build | [momtestbook.com](https://www.momtestbook.com/) |
| **Inspired** — Marty Cagan | How top product teams work | [svpg.com](https://www.svpg.com/books/inspired-how-to-create-tech-products-customers-love-2nd-edition/) |
| **Running Lean** — Ash Maurya | Lean Canvas + iterating toward product-market fit | [leanstack.com](https://leanstack.com/running-lean-book) |
| **Shape Up** — Ryan Singer (Basecamp) | 6-week cycles, no backlogs | [basecamp.com/shapeup](https://basecamp.com/shapeup) |

### YouTube / Free Courses
| Resource | Link |
|----------|------|
| FigJam crash course (Figma YouTube) | [youtube.com/@Figma](https://www.youtube.com/@Figma) |
| Notion for Product Managers | [youtube.com/c/Notion](https://www.youtube.com/c/Notion) |
| How to run a product discovery sprint | [youtube.com/c/ProductSchool](https://www.youtube.com/c/ProductSchool) |
| User journey mapping tutorial | [NN/g on YouTube](https://www.youtube.com/@NNgroup) |

### Frameworks to know
| Framework | What it does | Learn more |
|-----------|-------------|------------|
| **MoSCoW** | Must / Should / Could / Won't — prioritization | [productplan.com](https://www.productplan.com/glossary/moscow-prioritization/) |
| **SIPOC** | High-level process overview | [asana.com](https://asana.com/resources/sipoc) |
| **Lean Canvas** | One-page business model | [leanstack.com](https://leanstack.com/lean-canvas) |
| **Jobs to be Done** | Understanding user motivations | [jtbd.info](https://jtbd.info/) |
| **Shape Up** | Basecamp's product planning method | [basecamp.com/shapeup](https://basecamp.com/shapeup) |

---

## 🛠️ Recommended Stack for Hult Prize Teams

If you're starting today, here's the exact stack to use (all free):
```text
Brainstorm        →  FigJam (free, 3 boards)
Process map       →  FigJam or draw.io (free)
Product roadmap   →  Notion (free plan)
Wireframes        →  Pencil.dev → Figma (free)
Team workspace    →  Notion (free plan)
```

---

## 💬 Discussion

Have questions about this chapter?
**[Ask in Discussions →](https://github.com/MobinMithun/hult-prize-mvp-to-ai-agents/discussions)**

Common questions from past sessions:
- *"How detailed should my process map be before I start coding?"*
- *"Can I use Notion as both my roadmap AND my project tracker?"*
- *"What's the difference between a user flow and a process map?"*
