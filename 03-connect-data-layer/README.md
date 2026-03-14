# 🗄️ Chapter 3: Connect Your Data Layer

---

## Version Control — GitHub
Host your source code, collaborate with your team, and trigger deployments.
- 🔗 [github.com](https://github.com)
- Free for public and private repos
- **[GitHub Student Developer Pack](https://education.github.com/pack)** — tons of free tools for students

### Git basics cheat sheet
```bash
git init                    # Start a new repo
git add .                   # Stage all changes
git commit -m "first commit" # Commit
git remote add origin <url> # Connect to GitHub
git push -u origin main     # Push to GitHub
```

---

## Backend — Supabase
Open-source Firebase alternative. Gives you a Postgres database, Auth, Storage, and Edge Functions — all from a dashboard.
- 🔗 [supabase.com](https://supabase.com)
- Free tier: 500MB DB, 1GB storage, 2 projects
- The **Schema Visualizer** (shown in the slides) lets you see all your tables and relationships visually

### What Supabase gives you
- ✅ PostgreSQL database
- ✅ Auth (email, Google, GitHub, phone OTP)
- ✅ Row Level Security (RLS)
- ✅ Storage buckets
- ✅ Realtime subscriptions
- ✅ Edge Functions (serverless)

---

## Deployment — Vercel & Netlify
Deploy your frontend in seconds by connecting your GitHub repo.

| Platform | Best For | Free Tier |
|----------|----------|-----------|
| [Vercel](https://vercel.com) | Next.js, React apps | Generous free tier |
| [Netlify](https://netlify.com) | Static sites, JAMstack | Free tier |

---

## 📖 Resources
- [Supabase Docs](https://supabase.com/docs)
- [Supabase + Lovable Integration Guide](https://docs.lovable.dev/integrations/supabase)
- [Git & GitHub Crash Course (freeCodeCamp)](https://www.youtube.com/watch?v=RGOj5yH7evk)
- [Vercel Deployment Guide](https://vercel.com/docs/deployments/overview)
