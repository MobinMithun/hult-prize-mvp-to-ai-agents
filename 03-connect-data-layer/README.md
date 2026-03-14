# 🗄️ Chapter 3: Connect Your Data Layer

> *"Your first product won't be perfect. Make it anyway."*

This chapter covers the three pillars of your data and deployment
infrastructure — shown directly in the session through real screenshots
of the WeGro/Somadhan stack. By the end of this, you'll have your code
versioned, your database live, and your product deployed to the internet.

---

## The Three Pillars

| Pillar | Tool | What it does |
|--------|------|-------------|
| **Version Control** | GitHub | Store, version, and collaborate on your code |
| **Backend** | Supabase | Database, auth, storage, realtime, edge functions |
| **Deployment** | Vercel / Netlify | Host your frontend live in seconds from GitHub |

---

## 🐙 Pillar 1: GitHub — Host Your Source Code

The session slide shows the `pack-n-trace` repository hosted on GitHub,
built with Lovable, connected to Vercel for deployment, and with a
Telegram bot integrated for notifications. Every serious project starts
here.

### Why GitHub, not just saving files locally

Git is a version control system that saves every change you make
to your project as a history point — so if you break something,
you can go back to the last working version. GitHub is the cloud
platform where those histories live, adding collaboration, pull
requests, and CI/CD triggers on top.

Without it: one teammate overwrites another's work. With it:
everyone works on separate branches, reviews each other's code,
and merges cleanly.

### Setting up Git for the first time
```bash
# 1. Install Git: https://git-scm.com/downloads
# 2. Configure your identity (do this once)
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
git config --global init.defaultBranch main
```

### The core daily workflow (90% of what you'll ever use)

The cycle you will repeat dozens of times a day is:
Modify -> Stage -> Commit.
```bash
git init                          # Start tracking a folder as a repo
git add .                         # Stage ALL changes for the next commit
git add filename.js               # Stage ONE specific file
git commit -m "feat: add login"   # Save a snapshot with a message
git status                        # See what's changed and what's staged
git log --oneline                 # See your commit history (compact)
git diff                          # See exactly what changed line by line
```

### Connecting to GitHub and pushing
```bash
# Create a new repo on github.com first, then:
git remote add origin https://github.com/USERNAME/REPO-NAME.git
git branch -M main
git push -u origin main           # First push — sets upstream

# Every push after that:
git push
```

### Branching — how teams work without stepping on each other

Branches are for a purpose, not a person. One person may have
several branches, and one branch may have several people collaborate
on it. You can create branches from other branches, tags, or any
commit.
```bash
git checkout -b feature/login     # Create and switch to a new branch
git checkout main                 # Switch back to main
git merge feature/login           # Merge your feature into main
git branch -d feature/login       # Delete branch after merge

# Modern syntax (Git 2.23+):
git switch -c feature/login       # Create + switch
git switch main                   # Switch to existing branch
```

### Recommended branch strategy for Hult Prize teams
```text
main          <- always live, always deployable
dev           <- integration branch (merge features here first)
feature/xyz   <- one branch per feature, created from dev
```

**Rule:** Never commit directly to `main`. Always branch -> build ->
merge via Pull Request. This lets teammates review before anything
goes live.

### Writing good commit messages

Use conventional commit formats:
`type(scope): description` — tools parse `feat` for minor version
bumps, `fix` for patches, and `BREAKING CHANGE` for majors.
Common mistake: vague messages like "updates" — be specific.
```bash
feat: add OTP verification screen
fix: resolve login crash on empty email
docs: update README with setup instructions
refactor: simplify farmer credit scoring logic
chore: upgrade dependencies to latest versions
```

### Essential GitHub features to use

| Feature | What it does | Why it matters |
|---------|-------------|----------------|
| **Pull Requests** | Propose changes for review before merge | Catch bugs before they hit production |
| **Issues** | Track bugs, features, tasks | Your team's task board |
| **Actions** | Automate tests and deploys on every push | CI/CD for free |
| **Discussions** | Forum-style conversation in the repo | Great for async Q&A (like this repo!) |
| **Releases** | Tag specific versions of your product | Mark milestones, v1.0, v2.0 etc. |

### GitHub Desktop (no terminal needed)

If your team isn't comfortable with the command line, GitHub Desktop
is a free GUI app that handles all the above with drag-and-drop.

- 🔗 [desktop.github.com](https://desktop.github.com/)

### 🔗 All GitHub links

| Resource | Link |
|----------|------|
| GitHub homepage | [github.com](https://github.com) |
| GitHub Student Developer Pack | [education.github.com/pack](https://education.github.com/pack) |
| GitHub Desktop | [desktop.github.com](https://desktop.github.com) |
| GitHub Docs | [docs.github.com](https://docs.github.com) |
| GitHub Git Guides | [github.com/git-guides](https://github.com/git-guides) |
| Interactive Git learning | [learngitbranching.js.org](https://learngitbranching.js.org/) |
| Git simple guide (no deep stuff) | [rogerdudler.github.io/git-guide](https://rogerdudler.github.io/git-guide/) |
| The Odin Project — Git Basics | [theodinproject.com/lessons/foundations-git-basics](https://www.theodinproject.com/lessons/foundations-git-basics) |
| freeCodeCamp Git & GitHub (YouTube) | [youtube.com/watch?v=RGOj5yH7evk](https://www.youtube.com/watch?v=RGOj5yH7evk) |

### .gitignore — what to never commit

Create a `.gitignore` file in your project root and add:
```text
# Environment variables — NEVER commit these
.env
.env.local
.env.production

# Dependencies — reinstall with npm install
node_modules/

# Build output
dist/
.next/
build/

# OS files
.DS_Store
Thumbs.db
```

Generate one automatically at: [gitignore.io](https://www.toptal.com/developers/gitignore)

---

## ⚡ Pillar 2: Supabase — Connect Your Backend

The session shows a Supabase **Schema Visualizer** for the WeGro
project — tables for `profiles`, `user_roles`, `stock_transactions`,
and `products` all visually linked. This is your entire backend,
database, and auth system in one dashboard.

### What Supabase actually is

Supabase is an open-source Firebase alternative built on PostgreSQL.
It gives you a production-grade relational database plus a full suite
of backend services — all managed, all in a dashboard, with no server
to configure.

### Everything Supabase gives you in one package

| Service | What it does |
|---------|-------------|
| **PostgreSQL** | Full SQL database with relationships, indexes, triggers |
| **Auth** | Email/password, magic link, Google, GitHub, phone OTP, SSO |
| **Storage** | S3-compatible file buckets with access policies |
| **Realtime** | Subscribe to database changes live (websockets) |
| **Edge Functions** | Serverless TypeScript/Deno functions at the edge |
| **Schema Visualizer** | Visual map of all your tables and relationships |
| **Row Level Security** | Database-level access control per user |

### Pricing in 2026

Supabase pricing in 2026 starts at $0 on the Free plan — with
500 MB database storage, 50,000 monthly active users, and unlimited
API requests. The Pro plan starts at $25/month per project.

| Plan | Price | Database | MAUs | Storage | Projects |
|------|-------|----------|------|---------|----------|
| **Free** | $0/mo | 500 MB | 50,000 | 1 GB | 2 |
| **Pro** | $25/mo | 8 GB | 100,000 | 100 GB | Unlimited |
| **Team** | $599/mo | Pro limits | Pro limits | Pro limits | Unlimited |
| **Enterprise** | Custom | Custom | Custom | Custom | Custom |

**The most important free tier limit to know:**
Free tier projects that receive no API requests for one week are
paused automatically. Your data is retained, but the project goes
offline until you manually resume it. For anything user-facing,
this is a dealbreaker.

**What this means for you:** Use the free tier for building and
testing. The moment you show your product to real users, upgrade
to Pro ($25/mo). The Pro plan at $25 per month is where most
SaaS products should start — it removes the critical limitations
and adds usage-based scaling so your costs grow with your revenue.

**Hidden cost to know:**
The bandwidth limit is the silent killer. 2 GB sounds like a lot
until you realize every API call transfers data. A typical SaaS
page load might pull 50–100 KB from Supabase. Run the math:
500 daily active users, 20 API calls each, averaging 50 KB per
call — that's 500 MB per day. Your 2 GB allowance is gone
in four days.

### Setting up Supabase from zero
```bash
# 1. Go to supabase.com → New Project
# 2. Copy your project URL and anon key from Settings > API
# 3. Install the JS client in your project:
npm install @supabase/supabase-js

# 4. Create a supabase client file:
```

```javascript
// lib/supabase.js
import { createClient } from '@supabase/supabase-js'

const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL
const supabaseKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY

export const supabase = createClient(supabaseUrl, supabaseKey)
```

```bash
# 5. Add to your .env.local file (never commit this!):
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

### Core Supabase operations
```javascript
// READ — fetch all rows from a table
const { data, error } = await supabase
  .from('products')
  .select('*')

// READ — with filter
const { data } = await supabase
  .from('products')
  .select('name, price')
  .eq('status', 'active')

// INSERT — add a new row
const { data, error } = await supabase
  .from('farmers')
  .insert({ name: 'Rahim', district: 'Rajshahi', crop: 'Rice' })

// UPDATE — modify existing rows
const { data } = await supabase
  .from('products')
  .update({ quantity: 15 })
  .eq('id', 'product-uuid-here')

// DELETE — remove a row
const { error } = await supabase
  .from('orders')
  .delete()
  .eq('id', 'order-uuid-here')

// REALTIME — subscribe to changes live
const channel = supabase
  .channel('orders')
  .on('postgres_changes',
    { event: 'INSERT', schema: 'public', table: 'orders' },
    (payload) => console.log('New order:', payload.new)
  )
  .subscribe()
```

### Auth with Supabase
```javascript
// Sign up
const { data, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password123'
})

// Sign in
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'password123'
})

// Google OAuth (one line)
await supabase.auth.signInWithOAuth({ provider: 'google' })

// Get current user
const { data: { user } } = await supabase.auth.getUser()

// Sign out
await supabase.auth.signOut()
```

### Row Level Security (RLS) — the most important Supabase concept

RLS means your database enforces access rules at the database level —
not just in your app code. Even if someone finds your API key, they
can only see their own data.
```sql
-- Enable RLS on a table
ALTER TABLE orders ENABLE ROW LEVEL SECURITY;

-- Policy: users can only see their own orders
CREATE POLICY "Users see own orders" ON orders
  FOR SELECT USING (auth.uid() = user_id);

-- Policy: users can only insert their own orders
CREATE POLICY "Users insert own orders" ON orders
  FOR INSERT WITH CHECK (auth.uid() = user_id);
```

### What the WeGro schema looked like (from the session slide)
```text
profiles          user_roles
────────          ──────────
id (uuid) ──────► user_id (uuid)
name              role (app_role)
created_at
updated_at

products          stock_transactions
────────          ─────────────────
id (uuid) ◄────── product_id (uuid)
product_code      action (stock_action)
name              qty (int)
price             performed_by (uuid)
quantity_current  note
created_at        created_at
updated_at
```

This is a clean, normalized schema. Notice: no duplicated data,
clear foreign key relationships, timestamps on every table.

### Supabase vs Firebase — why startups choose Supabase

| Factor | Supabase | Firebase |
|--------|----------|---------|
| Database type | PostgreSQL (relational) | NoSQL (document) |
| Query complexity | Full SQL — joins, aggregates | Limited |
| Open source | Yes | No |
| Self-hostable | Yes | No |
| Pricing at 50K users | ~$25–75/mo | Often $100–200+/mo |
| Vendor lock-in | Low | High |

### 🔗 All Supabase links

| Resource | Link |
|----------|------|
| Supabase homepage | [supabase.com](https://supabase.com) |
| Official docs | [supabase.com/docs](https://supabase.com/docs) |
| Getting started guide | [supabase.com/docs/guides/getting-started](https://supabase.com/docs/guides/getting-started) |
| Supabase + Lovable integration | [docs.lovable.dev/integrations/supabase](https://docs.lovable.dev/integrations/supabase) |
| Supabase YouTube channel | [youtube.com/@Supabase](https://www.youtube.com/@Supabase) |
| Supabase Discord | [discord.supabase.com](https://discord.supabase.com) |
| Row Level Security guide | [supabase.com/docs/guides/auth/row-level-security](https://supabase.com/docs/guides/auth/row-level-security) |
| Supabase Schema Visualizer | Available in your dashboard -> Database -> Schema Visualizer |
| 2026 pricing breakdown (detailed) | [uibakery.io/blog/supabase-pricing](https://uibakery.io/blog/supabase-pricing) |
| Supabase vs Firebase full comparison | [supabase.com/alternatives/supabase-vs-firebase](https://supabase.com/alternatives/supabase-vs-firebase) |

---

## 🚀 Pillar 3: Deploy Your Product — Vercel & Netlify

The session slide shows both Vercel and Netlify as the recommended
deployment platforms. Both connect directly to your GitHub repo and
redeploy automatically on every push. Zero server management,
zero configuration.

### How deployment works (the magic part)
```text
You push to GitHub
    ↓
Platform detects the push automatically
    ↓
Runs your build command (npm run build)
    ↓
Deploys to global CDN in ~30 seconds
    ↓
Your app is live at a URL
```

Every branch gets its own **Preview URL** — so you can share
`feature/login.your-project.vercel.app` with a teammate for review
before it ever touches production.

---

### ▲ Vercel

**Best for: Next.js, React, full-stack apps with SSR**

Vercel is generally the stronger choice for full-stack
applications, AI workloads, multi-language runtimes (Node.js,
Python, Go, Ruby), and deep Next.js integration.

**Why the session recommends it:**
- Created by the team who built Next.js — zero-config deployment
- Every Lovable and v0 project deploys to Vercel in one click
- Preview deployments for every branch automatically
- The `pack-n-trace` project shown in the session is hosted on
  Vercel (`pack-n-trace.vercel.app`)

**Pricing (2026):**

| Plan | Price | Bandwidth | Build mins |
|------|-------|-----------|-----------|
| **Hobby (free)** | $0/mo | 100 GB | 6,000/mo |
| **Pro** | $20/member/mo | 1 TB | 24,000/mo |
| **Enterprise** | Custom | Custom | Custom |

**Important:** Unlike Netlify, Vercel doesn't officially allow
commercial use on the free (Hobby) plan. They may block you from
further platform use if they find out you're running a commercial
project without paying. For any revenue-generating product,
use the Pro plan or Netlify.

**Deploying to Vercel — 3 steps:**
1. Go to [vercel.com](https://vercel.com) → New Project
2. Import your GitHub repository
3. Click Deploy — done

From that point, every `git push` to `main` triggers a new
production deployment automatically.

**🔗 Vercel links:**
| Resource | Link |
|----------|------|
| Vercel homepage | [vercel.com](https://vercel.com) |
| Vercel docs | [vercel.com/docs](https://vercel.com/docs) |
| Deploy from GitHub guide | [vercel.com/docs/deployments/git](https://vercel.com/docs/deployments/git) |
| Environment variables | [vercel.com/docs/environment-variables](https://vercel.com/docs/environment-variables) |
| Vercel CLI | [vercel.com/docs/cli](https://vercel.com/docs/cli) |

---

### 🟩 Netlify

**Best for: Any framework, commercial use on free tier, built-in forms**

Netlify takes an open ecosystem approach — it works with any
framework and any workflow, whether you're building with AI tools
like Bolt and Cursor or pushing from Git.

With generous free tiers, instant deployment from anywhere, and
no vendor lock-in, Netlify enables everyone from AI-first builders
to enterprise teams to ship apps on their terms.

**Key difference from Vercel:**
Netlify's free tier allows commercial use. The only restriction
in their ToS is that the content must not break US law — so it's
free to run a commercial product on Netlify. This makes it
the better choice for Hult Prize teams launching their first
revenue-generating MVP on a budget.

**Pricing (2026):**

| Plan | Price | Bandwidth | Build mins |
|------|-------|-----------|-----------|
| **Free** | $0/mo | 100 GB | 300/mo |
| **Pro** | $20/member/mo | 1 TB | 25,000/mo |
| **Business** | $99/mo | Custom | Custom |

**What Netlify has that Vercel doesn't (on free tier):**
- Built-in form handling — 100 form submissions/month free,
  no backend code needed
- Background functions (async tasks up to 15 minutes)
- Scheduled functions (cron jobs)
- Commercial use allowed on free plan
- Split testing (A/B testing) built in

**Deploying to Netlify — 3 steps:**
1. Go to [netlify.com](https://netlify.com) → Add new site
2. Connect to GitHub → select repository
3. Set build command (`npm run build`) and publish directory (`dist` or `.next`) -> Deploy

**🔗 Netlify links:**
| Resource | Link |
|----------|------|
| Netlify homepage | [netlify.com](https://netlify.com) |
| Netlify docs | [docs.netlify.com](https://docs.netlify.com) |
| Deploy from GitHub | [docs.netlify.com/site-deploys/create-deploys](https://docs.netlify.com/site-deploys/create-deploys/) |
| Netlify Forms (free) | [docs.netlify.com/forms/setup](https://docs.netlify.com/forms/setup/) |
| Environment variables | [docs.netlify.com/environment-variables/overview](https://docs.netlify.com/environment-variables/overview/) |

---

### Vercel vs Netlify — which to pick?

| Situation | Recommendation |
|-----------|---------------|
| Using Next.js / v0 output | **Vercel** — zero config, made for it |
| Using Lovable or Bolt output | **Either** — both work, Netlify is safer for commercial |
| Building a commercial product on free tier | **Netlify** |
| Need forms without a backend | **Netlify** |
| Need Python/Ruby serverless functions | **Vercel** |
| Building a static landing page | **Either** |
| Need cron jobs / background tasks | **Netlify** |

There's no one-size-fits-all answer. Vercel is best for Next.js
and dynamic applications, while Netlify is perfect for static
websites and quick deployments. Both offer generous free tiers.

---

## 🔧 Connecting Everything — The Full Environment Setup

Once you have all three pillars running, connect them with environment
variables. These are secret keys that your deployment platform injects
into your app at build time — never hardcoded, never committed to Git.

### Setting environment variables on Vercel

1. Go to your project → Settings → Environment Variables
2. Add each variable for Production / Preview / Development
3. Redeploy — your app now has access to them via `process.env`

### Setting environment variables on Netlify

1. Go to Site settings → Environment variables
2. Add key-value pairs
3. Trigger a new deploy

### The variables you'll always need for a Supabase + Vercel/Netlify stack
```bash
# In your .env.local (local development only, never commit!)
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here

# For server-side operations (never expose to client!)
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key-here
```

Add these same variables to your Vercel or Netlify dashboard for
production. Your app will work the same way both locally and live.

---

## 🧰 Alternative Tools Worth Knowing

### Railway — for full-stack backends

If you need to run a Node.js, Python, or Django server (not just a
frontend), Railway is the simplest option.

- 🔗 [railway.app](https://railway.app)
- Free tier: $5 credit/month
- Supports: Node.js, Python, Go, Ruby, Rust, databases, cron jobs
- One-click database provisioning (PostgreSQL, MySQL, Redis, MongoDB)
- Great for: Python Flask/FastAPI APIs, background workers, bots

### PlanetScale — MySQL alternative to Supabase

- 🔗 [planetscale.com](https://planetscale.com)
- MySQL-compatible, serverless, branch your database like Git

### Firebase — if you specifically need NoSQL

- 🔗 [firebase.google.com](https://firebase.google.com)
- Best for: Real-time apps, mobile-first, Google ecosystem
- Worse than Supabase for: complex queries, relational data, SQL

---

## 📚 Learning Resources

### Courses & Tutorials (all free)
| Resource | Link |
|----------|------|
| Supabase crash course (YouTube) | [youtube.com/watch?v=dU7GwCOgvNY](https://www.youtube.com/watch?v=dU7GwCOgvNY) |
| Git & GitHub full course (freeCodeCamp) | [youtube.com/watch?v=RGOj5yH7evk](https://www.youtube.com/watch?v=RGOj5yH7evk) |
| The Odin Project — Git foundations | [theodinproject.com](https://www.theodinproject.com/paths/foundations) |
| Supabase official tutorials | [supabase.com/docs/guides/tutorials](https://supabase.com/docs/guides/tutorials) |
| Vercel deployment guide | [vercel.com/docs/deployments](https://vercel.com/docs/deployments/overview) |
| Learn Git Branching (interactive) | [learngitbranching.js.org](https://learngitbranching.js.org/) |
| Git simple guide (no jargon) | [rogerdudler.github.io/git-guide](https://rogerdudler.github.io/git-guide/) |

### Cheat Sheets
| Resource | Link |
|----------|------|
| Git cheat sheet (GitHub official) | [education.github.com/git-cheat-sheet](https://education.github.com/git-cheat-sheet-education.pdf) |
| Supabase JavaScript client reference | [supabase.com/docs/reference/javascript](https://supabase.com/docs/reference/javascript/introduction) |
| SQL basics for Supabase | [supabase.com/docs/guides/database/tables](https://supabase.com/docs/guides/database/tables) |

---

## ⚡ Quick-Start Checklist for Hult Prize Teams

Copy this and tick off each step:
```text
[ ] 1. Create a GitHub account (free) — github.com
[ ] 2. Install Git — git-scm.com/downloads
[ ] 3. Install GitHub Desktop (optional GUI) — desktop.github.com
[ ] 4. Create a new repository for your project
[ ] 5. Add a .gitignore (use gitignore.io)
[ ] 6. Create a Supabase project — supabase.com
[ ] 7. Design your database schema in the Supabase Table Editor
[ ] 8. Enable Row Level Security on all tables
[ ] 9. Copy your Supabase URL + anon key to .env.local
[ ] 10. Connect your GitHub repo to Vercel or Netlify
[ ] 11. Add your Supabase env vars to Vercel/Netlify dashboard
[ ] 12. Push to main → confirm your app is live
```

---

## 💬 Discussion

Questions about this chapter? **[Ask in Discussions →](https://github.com/MobinMithun/hult-prize-mvp-to-ai-agents/discussions)**

Common questions:
- *"My Supabase project paused — how do I unpause it?"*
- *"How do I keep my API keys secret when deploying?"*
- *"Can I use Supabase with Bolt/Lovable without any code?"*
- *"Vercel keeps saying commercial use not allowed — what do I do?"*
- *"What's the difference between the anon key and service role key?"*
