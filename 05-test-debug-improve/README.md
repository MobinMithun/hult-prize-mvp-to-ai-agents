# 🧪 Chapter 5: Test, Debug & Improve

> *"If you are not embarrassed by the first version of your product,
> you are not shipping fast enough."* — Hussain Elius, Co-founder, Pathao

Shipping is not the finish line — it's the starting gun. This chapter
covers everything shown in the session for understanding what users
actually do in your product (analytics), understanding *why* they do
it (user feedback), and acting on that signal fast.

---

## The Core Loop

Every successful product team runs the same four-step cycle:
```text
Ship → Measure (what happened?) → Learn (why did it happen?)
→ Improve → Ship again
```

Most Hult Prize teams skip straight from "Ship" to "Improve" — which
means they're guessing. Analytics and user interviews are what make
the loop real.

---

## 📊 Part 1: Integrating Analytics

The session slide shows five tools: PostHog, Google Analytics,
Mixpanel, Microsoft Clarity, and Amplitude. Here is everything
you need to know about all of them — and exactly which one to
install today.

---

### 🦔 PostHog — Recommended for Hult Prize Teams

**What it is:** An open-source, all-in-one product analytics platform.
The session lists it first for good reason — it is the best free
option for engineering-led startup teams by a wide margin.

PostHog offers the most generous free tier of any analytics tool:
1 million events, 5,000 session replays, 1 million feature flag
requests, and 1,500 survey responses per month — all completely
free with no credit card required.

PostHog is an all-in-one platform — it replaces multiple tools
by combining analytics, session replay, feature flags, A/B testing,
error tracking, LLM analytics, and surveys in a single dashboard.
Its pricing is 100% transparent, usage-based, with a generous free
tier on all products.

**What's included on the free tier:**

| Feature | Free limit |
|---------|-----------|
| Product analytics (funnels, retention, cohorts) | 1M events/mo |
| Session recordings | 5,000/mo |
| Feature flags | 1M requests/mo |
| A/B testing | Included |
| Surveys | 1,500 responses/mo |
| Error tracking | Included |
| LLM analytics | Included |
| SQL query access | Included |

**Startup bonus:**
Startups can apply for PostHog for Startups to receive $50,000
in additional free credits. The usage-based pricing means you only
pay for what you use as you scale, rather than committing to
seat-based or MTU contracts upfront.

**Installing PostHog in your app:**
```bash
# React / Next.js
npm install posthog-js

# Initialize in your app (e.g. _app.tsx or layout.tsx):
```

```javascript
import posthog from 'posthog-js'

posthog.init('YOUR_PROJECT_API_KEY', {
  api_host: 'https://app.posthog.com',
  person_profiles: 'identified_only'
})
```

**Track a custom event:**
```javascript
// When a user does something meaningful
posthog.capture('farmer_loan_applied', {
  district: 'Rajshahi',
  crop_type: 'Rice',
  loan_amount: 50000
})

// Identify a user (links events to a person)
posthog.identify('user-123', {
  email: 'farmer@example.com',
  name: 'Rahim Uddin'
})
```

**The 5 questions PostHog answers for you:**
1. Where are users dropping off in my onboarding funnel?
2. Which features do users actually use vs. ignore?
3. What does a user do right before they churn?
4. Which version of my landing page converts better? (A/B test)
5. Where exactly are users getting stuck? (session replay)

**🔗 PostHog links:**
| Resource | Link |
|----------|------|
| PostHog homepage | [posthog.com](https://posthog.com) |
| PostHog for Startups ($50K credits) | [posthog.com/startups](https://posthog.com/startups) |
| PostHog docs | [posthog.com/docs](https://posthog.com/docs) |
| Next.js integration guide | [posthog.com/docs/libraries/next-js](https://posthog.com/docs/libraries/next-js) |
| React integration guide | [posthog.com/docs/libraries/react](https://posthog.com/docs/libraries/react) |
| PostHog GitHub (open source) | [github.com/PostHog/posthog](https://github.com/PostHog/posthog) |
| PostHog YouTube | [youtube.com/@PostHog](https://www.youtube.com/@PostHog) |

---

### 🔵 Microsoft Clarity — Completely Free, No Limits

**What it is:** A free behavioral analytics tool from Microsoft that
gives you heatmaps and session recordings with zero limits, zero
cost, and zero upgrade pressure — ever.

Clarity is a free user behavior analytics tool that helps you
understand how users interact with your website through session
replays and heatmaps. It is free forever with no limits on traffic,
no forced upgrades, and no paid tiers.

Unlike most heatmapping tools that charge based on session volume,
Clarity has no traffic limits or forced upgrades — it is forever
free. It is also GDPR and CCPA ready, doesn't use sampling, and is
built on open source.

**What you get for free:**
- Unlimited session recordings (no cap)
- Click heatmaps on every page automatically
- Scroll heatmaps
- AI-powered session summaries (Clarity Copilot)
- Rage click and dead click detection
- Google Analytics 4 integration
- Mobile app SDK (Android, iOS, Flutter, React Native)
- MCP server (connect Clarity to Claude directly)
- Chrome extension for live heatmaps on your site

**Installing Clarity — 3 ways:**
```html
<!-- Option 1: Paste the script tag directly into your HTML <head> -->
<script type="text/javascript">
  (function(c,l,a,r,i,t,y){
    c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
    t=l.createElement(r);t.async=1;t.src="https://www.clarity.ms/tag/"+i;
    y=l.getElementsByTagName(r)[0];y.parentNode.insertBefore(t,y);
  })(window, document, "clarity", "script", "YOUR_PROJECT_ID");
</script>
```

```bash
# Option 2: NPM (React / Next.js)
npm install @microsoft/clarity

# In your app entry point:
```

```javascript
import Clarity from '@microsoft/clarity'
Clarity.init('YOUR_PROJECT_ID')
```

```bash
# Option 3: Google Tag Manager
# Add a Custom HTML tag with the script above — no code deploy needed
```

**Getting your Project ID:**
1. Go to [clarity.microsoft.com](https://clarity.microsoft.com)
2. Sign in with Google, Microsoft, or Facebook (free)
3. Click "Add new project" → enter your site URL
4. Go to Settings → Overview → copy your Project ID
5. Paste it into the script above
6. Data starts appearing within a few hours

**🔗 Clarity links:**
| Resource | Link |
|----------|------|
| Microsoft Clarity homepage | [clarity.microsoft.com](https://clarity.microsoft.com) |
| Clarity docs | [learn.microsoft.com/en-us/clarity](https://learn.microsoft.com/en-us/clarity/) |
| NPM package | [npmjs.com/package/@microsoft/clarity](https://www.npmjs.com/package/@microsoft/clarity) |
| GitHub repo | [github.com/microsoft/clarity](https://github.com/microsoft/clarity) |
| Chrome extension (live heatmaps) | [Chrome Web Store](https://chromewebstore.google.com/detail/microsoft-clarity-live/cjfdbemmaeeohgibnhdhlakiahifjjcf) |
| Clarity MCP server | Available at clarity.microsoft.com |
| Google Analytics integration guide | [learn.microsoft.com/en-us/clarity/google-analytics](https://learn.microsoft.com/en-us/clarity/google-analytics) |

---

### 📈 Google Analytics 4 (GA4) — Best for Marketing Attribution

**What it is:** The industry standard for web analytics. Free,
deeply integrated with Google Ads, Search Console, and Looker Studio.

**Best for:** Understanding where your users come from (SEO, ads,
social, direct) and tracking conversion goals tied to marketing spend.

**Key weakness:** No session recordings or heatmaps. Tells you *what*
happened at a traffic level, not *how* users behave inside your app.

**Free tier:** Up to 10 million events/month free.

**Installing in React/Next.js:**
```bash
npm install @next/third-parties
```

```javascript
// In your layout.tsx (Next.js 14+):
import { GoogleAnalytics } from '@next/third-parties/google'

export default function RootLayout({ children }) {
  return (
    <html>
      <body>{children}</body>
      <GoogleAnalytics gaId="G-YOUR_MEASUREMENT_ID" />
    </html>
  )
}
```

**Best stack:** GA4 (traffic + acquisition) + Clarity (behavior inside
the app) — both free, together they give you the full picture.

**🔗 GA4 links:**
| Resource | Link |
|----------|------|
| GA4 homepage | [analytics.google.com](https://analytics.google.com) |
| GA4 setup guide | [support.google.com/analytics](https://support.google.com/analytics/answer/9304153) |
| GA4 + Next.js guide | [nextjs.org/docs/app/building-your-application/optimizing/third-party-libraries](https://nextjs.org/docs/app/building-your-application/optimizing/third-party-libraries) |
| GA4 YouTube crash course (freeCodeCamp) | [youtube.com/watch?v=mI1Ul4LN870](https://www.youtube.com/watch?v=mI1Ul4LN870) |

---

### 🎯 Mixpanel — Best for Non-Technical Product Teams

**What it is:** A product analytics platform known for its clean UI
and accessibility to non-engineers. Good for marketing and product
managers who want to answer questions without writing SQL.

Mixpanel's free tier supports 100,000 monthly tracked users with
basic event tracking, custom properties, real-time reports, and
90-day data history. Teams can build custom dashboards and analyze
user behavior without immediate upgrade pressure, making it practical
for early-stage companies.

Where Mixpanel makes a difference is in helping teams take ownership
of their metrics. It gives product managers, marketers, and even
non-technical users the freedom to explore data, build custom
dashboards, and track custom events without always bringing in
engineers. The entire team can speak the same data language and
move faster on insights.

**When to choose Mixpanel over PostHog:**
- Your team has non-technical members who need to run their own reports
- You want faster query speeds for complex dashboards
- You need strong customer support and onboarding help
- You're marketing-led (not engineering-led)

**Free tier:** 1M events/mo (credit card required) or 100K MTUs.

**🔗 Mixpanel links:**
| Resource | Link |
|----------|------|
| Mixpanel homepage | [mixpanel.com](https://mixpanel.com) |
| Mixpanel docs | [docs.mixpanel.com](https://docs.mixpanel.com) |
| Mixpanel University (free courses) | [mixpanel.com/university](https://mixpanel.com/university) |
| React SDK | [docs.mixpanel.com/docs/tracking-methods/sdks/react](https://docs.mixpanel.com/docs/tracking-methods/sdks/react) |

---

### 📡 Amplitude — Best for Scale and Enterprise

**What it is:** The most powerful product analytics platform for large
teams. Used by Notion, Shopify, Peloton, and Walmart. More complex
to set up but unmatched for enterprise-grade behavioral analysis.

Amplitude's free starter tier includes up to 10 million monthly
tracked events with core funnel analysis, retention tracking, and
basic behavioral cohorts. Teams can access essential reporting tools
without time limitations.

Amplitude just feels more built for scale. When you're dealing with
complex products, multiple funnels, or countless custom events, it
gives you the structure that PostHog sometimes lacks. Its predictive
insights and statistical significance testing help you see not just
what users did, but why it mattered.

**Honest advice for Hult Prize teams:** Amplitude is overkill at the
MVP stage. Start with PostHog. Come back to Amplitude when you have
a dedicated data analyst and 100K+ MAUs.

**🔗 Amplitude links:**
| Resource | Link |
|----------|------|
| Amplitude homepage | [amplitude.com](https://amplitude.com) |
| Amplitude Academy (free) | [academy.amplitude.com](https://academy.amplitude.com) |
| React SDK | [amplitude.com/docs/sdks/analytics/browser/react](https://amplitude.com/docs/sdks/analytics/browser/react) |

---

### 📊 Analytics Comparison: Which to Use at Each Stage

For most product teams, the recommended stack by stage is: startups
on a Mixpanel free plan or PostHog free tier for basic behavioral
tracking and session watching; growing companies adding Amplitude or
expanding their PostHog usage; large companies combining Amplitude
Enterprise with FullStory for in-depth UX analysis.

| Stage | Recommended stack | Monthly cost |
|-------|-----------------|-------------|
| **Day 1–1K users** | PostHog (free) + Clarity (free) | **$0** |
| **1K–10K users** | PostHog (free) + GA4 (free) | **$0** |
| **10K–100K users** | PostHog paid + GA4 | ~$50–100/mo |
| **100K+ users** | PostHog or Amplitude + GA4 | Custom |

**The recommended free stack for Hult Prize teams:**
```text
PostHog    → user behavior inside the app (funnels, retention)
Clarity    → visual session recordings + heatmaps
GA4        → traffic sources, marketing attribution
```
All three are free, all three install in under 30 minutes, and
together they answer every question your first 10,000 users will
generate.

---

## 🗣️ Part 2: User Feedback — The Mom Test

Analytics tells you *what* users do. It cannot tell you *why*.
For that, you need to talk to them. The session slide features
**The Mom Test** by Rob Fitzpatrick — the most important book a
Hult Prize founder can read before running a customer interview.

### Why most customer interviews are worthless

The problem is painfully simple: humans are hardwired to be nice,
especially to our faces. The moment you mention your idea or your
passion for it, people start telling you what you want to hear
instead of what you need to hear.

The Mom Test is named after a simple truth: if you ask your mom
whether your startup idea is good, she will say yes — because she
loves you. The book teaches you to ask questions that even she
cannot lie to you about.

### The 3 rules of The Mom Test

Rule 1: Talk about their life, not your idea. Rule 2: Ask about
specific past behavior, not hypothetical future opinions. Rule 3:
Talk less and listen more. If you just avoid mentioning your idea,
you automatically start asking better questions.

### Good vs bad questions — the full breakdown

| ❌ Bad question | Why it fails | ✅ Good replacement |
|----------------|-------------|---------------------|
| "Would you use an app like this?" | Hypothetical — people say yes to be polite | "How are you handling this today?" |
| "Do you think this is a good idea?" | Asks for opinion — they'll validate you | "How much time did you spend on this last week?" |
| "Would you pay $10/month for this?" | Hypothetical pricing — means nothing | "How much are you currently paying to solve this?" |
| "How often do you face this problem?" | Asks them to estimate — inaccurate | "When was the last time this happened to you?" |
| "What features would you want?" | Wishlist — not grounded in real need | "Walk me through exactly how you handled it last time." |

Beware three types of bad data that lead founders to chase false
signals and build the wrong product: compliments ("That's amazing!"),
hypothetical fluff ("I would definitely use this"), and wishlists
("It would be great if it also did X").

### The 3 types of bad interview data to ignore

Love bad news. If an assumption is wrong, the sooner you find out
the better. Treat each interview with the mindset of "let me see if
there's anything wrong" rather than "I need to prove I'm right."
When you get a tepid response — a "meh" — don't rush to persuade.
That meh is actually a reliable signal that the person doesn't care
about this problem.

1. **Compliments** — "That's a really cool idea!" → Ignore it. It
   changes nothing.
2. **Hypothetical fluff** — "I would probably use something like
   that." → Ignore it. Talk is free.
3. **Wishlists** — "It would be great if it also had X." → Don't
   build X yet. Check if they've ever tried to solve X before.

Zombie leads are particularly dangerous — customers who keep saying
they're interested but never commit. When you fail to push for
advancement (a paid pilot, a signed letter of intent, an intro to
a decision-maker), you end up in endless polite conversations that
feel productive but lead nowhere.

### The conversation opening script

Use this framing at the start of every customer interview:
```text
"Hi [name], I'm working on [vision — one sentence about the
problem you're solving, not your solution]. I'm not selling
anything today — I'm trying to understand how [your target
customer] currently deals with [the problem].

Could you tell me about the last time you had to [do the
thing your product helps with]?"
```

Then stop talking. Let them tell you their story.

### 20 questions that actually work (Mom Test-approved)

Use these verbatim or adapt them for your specific domain:

**Uncovering the problem:**
1. "Walk me through how you handle [problem area] today."
2. "What's the hardest part of that process?"
3. "How long does it take you to do that from start to finish?"
4. "When was the last time you had to deal with this?"
5. "What did you try before? What happened?"

**Uncovering existing behavior:**
6. "What tools or apps do you currently use for this?"
7. "How much do you currently pay to solve this problem?"
8. "How many times in the past month did this come up?"
9. "Who else in your team / family / organisation has this problem?"
10. "What's your current workaround when things break down?"

**Uncovering willingness to change:**
11. "If you could wave a magic wand and fix one thing about how
    you do this today, what would it be?"
12. "What would have to be true for you to switch away from your
    current solution?"
13. "Have you ever searched for something better? What did you find?"
14. "What would the impact be if this problem went away entirely?"
15. "What would happen if nothing changed for the next 12 months?"

**Validating real commitment (after you've shown something):**
16. "Does this solve the problem you described earlier?"
17. "What would it take for you to start using this tomorrow?"
18. "Can you intro me to two other people who have the same problem?"
19. "Would you be willing to pay for this today, even in early access?"
20. "What would make you stop using this after a month?"

### Running the interview — logistics

Keep to two interviewers maximum — one person asks questions, the
other takes notes. Three or more is overwhelming. Write notes in a
paper notebook during the session. Typing can come across as rude.
Capture exact quotes wherever possible. Transfer notes to a shared
doc immediately after the session.

**Before the interview:**
- Never ask "do you have 30 minutes to talk about my startup idea?"
  Instead: "I'm researching how farmers in Bangladesh manage crop
  financing. Can I ask you 5 questions about your experience?"
- Have only 3 questions prepared. Let the conversation breathe.
- Set a clear end time and stick to it.

**During the interview:**
- Start with past behavior: "Tell me about the last time..."
- When they say something interesting, ask: "Can you tell me
  more about that?"
- When they give a compliment, redirect: "That's helpful — what
  do you currently do about it?"
- Silence is your friend. Don't fill it.

**After the interview:**
- Write up your 3 key learnings within 1 hour while memory is fresh
- Categorize: Confirmed assumption / New insight / Contradicted
  assumption / Follow-up needed
- Share with your whole team — everyone should read real customer
  quotes

**🔗 The Mom Test links:**
| Resource | Link |
|----------|------|
| Official website + free chapter | [momtestbook.com](https://www.momtestbook.com/) |
| Buy the book (Amazon) | [amazon.com — The Mom Test](https://www.amazon.com/Mom-Test-customers-business-everyone/dp/1492180742) |
| Revised & Expanded Edition (2025) | [Simon & Schuster](https://www.simonandschuster.com/books/The-Mom-Test/Rob-Fitzpatrick/9798893312560) |
| Free PDF (original edition) | [manuelohan.com/wp-content/uploads/2017/05/The-Mom-Test-en.pdf](https://manuelohan.com/wp-content/uploads/2017/05/The-Mom-Test-en.pdf) |
| 14-page summary (Readingraphics) | [readingraphics.com/book-summary-the-mom-test](https://readingraphics.com/book-summary-the-mom-test/) |
| Mom Test interview questions guide (Looppanel) | [looppanel.com/blog/customer-interviews](https://www.looppanel.com/blog/customer-interviews) |
| YC: How to talk to users (video) | [youtube.com/watch?v=MT4Ig2uqjTc](https://www.youtube.com/watch?v=MT4Ig2uqjTc) |
| Customer discovery 101 (a16z) | [a16z.com/customer-discovery-101](https://a16z.com/customer-discovery-101/) |

---

## 📋 Part 3: Collecting Structured Feedback

After in-person interviews, you need a scalable way to collect
feedback from your full user base. Here are the tools for that.

### Tools shown in the session

**ManyDial** — shown in the session for OTP-verified user testing
flows. Useful for running surveys with phone-verified respondents
in Bangladesh.
- 🔗 [manydial.com](https://manydial.com)

**OGRO Impact Survey (shown in the session)** — built entirely in
Bengali and English, with role and usage-frequency filters, and
a privacy statement. This is the gold standard for a startup survey
in Bangladesh — it collects structured data and respects users'
time (estimated 5 minutes, shown upfront).

### Free survey tools for your team

| Tool | Free tier | Best for | Link |
|------|-----------|----------|------|
| **Tally.so** | Unlimited responses (free) | Beautiful forms, no branding | [tally.so](https://tally.so) |
| **Google Forms** | Completely free | Quick setup, Google Sheets export | [forms.google.com](https://forms.google.com) |
| **Typeform** | 10 responses/month | Conversational, high completion | [typeform.com](https://typeform.com) |
| **PostHog Surveys** | 1,500 responses/mo free | In-app surveys, tied to analytics | [posthog.com/docs/surveys](https://posthog.com/docs/surveys) |
| **Formspark** | 250 submissions/mo free | Form backend without a form builder | [formspark.io](https://formspark.io) |

### Building a survey that people actually complete

**Rule 1: Tell them upfront how long it takes.** The OGRO survey
does this well — "সার্ভেটি সম্পন্ন করতে প্রায় ৫ মিনিট সময় লাগবে"
(this survey takes approximately 5 minutes). Response rates jump
significantly when people know the time commitment.

**Rule 2: Start with role and context questions.** The OGRO survey
asks for role and usage duration before any opinion questions.
This segments your data automatically — you can filter responses
by farmer vs. field officer, or new user vs. 6-month user.

**Rule 3: Use multiple choice wherever possible.** Open-ended
questions give rich qualitative data but have lower completion
rates. Lead with multiple choice, end with one open-ended
"anything else?" box.

**Rule 4: Tell them what you'll do with the data.** The OGRO
survey states the data is confidential and used only for aggregate
analysis. This increases trust and completion rate.

**Survey template for Hult Prize teams:**
```text
[Survey title: Your Product Name — User Feedback (Month Year)]
[Intro: This survey takes approximately 3 minutes. Your responses
are confidential and will only be used to improve the product.]

Q1. What is your role? (Multiple choice)
→ Farmer / Field Officer / Bank Staff / Admin / Other

Q2. How long have you been using [Product Name]?
→ Less than 1 month / 1–3 months / 3–6 months / 6+ months

Q3. How easy is [Product Name] to use? (1–5 scale)
1 = Very difficult, 5 = Very easy

Q4. Which feature do you use most? (Multiple choice)
→ [List your top 4–5 features]

Q5. What is the ONE thing we should improve? (Open text)

Q6. Would you recommend [Product Name] to a colleague? (1–10)
→ This is your NPS score (9–10 = Promoter, 7–8 = Passive, 0–6 = Detractor)
```

---

## 🐛 Part 4: Debugging Effectively

The session is titled "Test, Debug & Improve" — the debugging part
is as important as the analytics. Here are the tools and habits
that separate fast-moving teams from slow ones.

### Error tracking — know about bugs before your users report them

**Sentry** is the industry standard for error monitoring. It
captures JavaScript errors, performance issues, and backend
exceptions in real time and sends alerts to your Slack or email.
```bash
npm install @sentry/nextjs

# Run the setup wizard:
npx @sentry/wizard@latest -i nextjs
```

- 🔗 [sentry.io](https://sentry.io) — free tier: 5,000 errors/month
- Free for one project, one team member

**PostHog error tracking** is also included in PostHog's free tier
if you're already using it for analytics — no extra install needed.

### Console + network debugging checklist

Before you conclude something is a bug, always check:
```text
[ ] Open browser DevTools → Console tab. Any red errors?
[ ] Open Network tab. Any failed API calls (red rows)?
[ ] Check your Supabase dashboard → API logs. Did the request reach the DB?
[ ] Check your Vercel/Netlify logs. Did the serverless function error?
[ ] Are your environment variables set correctly in the deployment?
```

### AI-assisted debugging

The fastest way to debug in 2026 is to paste the error into Claude
with the surrounding code. Use this prompt structure:
```text
I'm getting this error in my Next.js app using Supabase:

[paste the full error message]

Here is the relevant code:
[paste the function or component]

Here is my Supabase table schema:
[paste the relevant table structure]

What is causing this and how do I fix it?
```

---

## 📚 Learning Resources

### Must-read books for this chapter

| Book | Why read it | Link |
|------|-------------|------|
| **The Mom Test** — Rob Fitzpatrick | The single best book on customer interviews | [momtestbook.com](https://www.momtestbook.com/) |
| **Continuous Discovery Habits** — Teresa Torres | How to run discovery as an ongoing habit, not a one-time project | [producttalk.org](https://www.producttalk.org/2021/05/continuous-discovery-habits/) |
| **Lean Analytics** — Croll & Yoskovitz | Which metrics to track at each startup stage | [leananalyticsbook.com](http://leananalyticsbook.com/) |
| **The Lean Startup** — Eric Ries | Build-Measure-Learn cycle explained in depth | [theleanstartup.com](http://theleanstartup.com/) |

### Free courses and videos

| Resource | Link |
|----------|------|
| YC: How to talk to users (Eric Migicovsky, 20 min) | [youtube.com/watch?v=MT4Ig2uqjTc](https://www.youtube.com/watch?v=MT4Ig2uqjTc) |
| PostHog tutorials (YouTube) | [youtube.com/@PostHog](https://www.youtube.com/@PostHog) |
| Google Analytics GA4 crash course (Analytics Mania) | [youtube.com/@AnalyticsMania](https://www.youtube.com/@AnalyticsMania) |
| How to run user interviews (NN/g) | [youtube.com/@NNgroup](https://www.youtube.com/@NNgroup) |
| Sentry setup tutorial | [youtube.com/watch?v=shzKcE79SsE](https://www.youtube.com/watch?v=shzKcE79SsE) |

---

## ⚡ Quick-Start Checklist for Hult Prize Teams
```text
Analytics setup (do all three — all free):
[ ] 1.  Create PostHog account — posthog.com
[ ] 2.  Install PostHog in your app (npm install posthog-js)
[ ] 3.  Track 3 key custom events (onboarding step, core action, churn point)
[ ] 4.  Create a signup account on Microsoft Clarity — clarity.microsoft.com
[ ] 5.  Add Clarity script tag to your app <head>
[ ] 6.  Connect GA4 — analytics.google.com → add tracking script
[ ] 7.  Connect Clarity to GA4 in Clarity settings (one click)
[ ] 8.  After 48 hours: watch 5 real session recordings in Clarity
[ ] 9.  After 1 week: build a PostHog funnel for your core user flow

User feedback setup:
[ ] 10. Read The Mom Test (free PDF linked above, 118 pages, 2–3 hours)
[ ] 11. Write your 3 core interview questions using the Mom Test rules
[ ] 12. Run 5 customer interviews before your next product sprint
[ ] 13. Create a Tally.so survey with NPS question + one open-ended
[ ] 14. Share survey link with your first 50 users

Error monitoring:
[ ] 15. Install Sentry or enable PostHog error tracking
[ ] 16. Set up Slack or email alerts for new errors
[ ] 17. Fix every error that shows up in the first 48 hours post-launch
```

---

## 💬 Discussion

Questions from this chapter?
**[Ask in Discussions →](https://github.com/MobinMithun/hult-prize-mvp-to-ai-agents/discussions)**

Common questions:
- *"I have zero users yet — how do I set up analytics before launch?"*
- *"Nobody responds to my user interview requests — what do I say?"*
- *"PostHog is showing weird data — how do I filter out my own visits?"*
- *"How do I know which metric matters most at my stage?"*
- *"Someone in the interview said something contradictory — which answer do I trust?"*
