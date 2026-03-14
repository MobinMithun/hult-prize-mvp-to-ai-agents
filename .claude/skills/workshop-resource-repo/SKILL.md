---
name: workshop-resource-repo
description: Create or update a GitHub-ready workshop resources repository from VS Code. Use when asked to scaffold a workshop repo, organize workshop assets, write a main README plus chapter READMEs, add slide or poster links, and prepare the repo for commit and GitHub push.
---

# Workshop Resource Repo

Use this skill when building a workshop materials repository like this one:
- one root `README.md` with workshop intro, poster, slides, speaker info, and chapter links
- multiple chapter folders with their own `README.md`
- local assets such as posters, slide PDFs, and cover images
- GitHub-friendly links and discussion links
- a repo that is easy to edit from VS Code and publish to GitHub

## Default repo structure

Create this structure unless the user asks for a different layout:

```text
repo-name/
├── README.md
├── 01-topic-name/
│   └── README.md
├── 02-topic-name/
│   └── README.md
├── 03-topic-name/
│   └── README.md
├── 04-topic-name/
│   └── README.md
├── 05-topic-name/
│   └── README.md
├── 06-topic-name/
│   └── README.md
└── resources/
    ├── poster.png|jpg
    ├── slides.pdf
    └── slide-cover.jpg
```

Use `resources/` for uploaded workshop assets by default.

## Workflow

1. Inspect the current repo first.
2. Create any missing folders and Markdown files.
3. Put workshop assets in `resources/` unless the user explicitly wants another folder.
4. Update the root `README.md` with:
   - workshop title
   - short intro paragraph
   - centered poster image if provided
   - slide download link
   - slide view link if provided
   - chapter table
   - discussion link
   - speaker details
5. Create or expand chapter READMEs from user-provided notes.
6. Prefer absolute GitHub Discussions URLs over fragile relative paths.
7. When linking local assets in Markdown:
   - use URL-encoded spaces
   - use HTML `<img>` if centering is needed on GitHub
8. Verify file paths after editing so README links point to real files.
9. If asked, stage and commit with a clear workshop-focused commit message.

## Root README pattern

Keep the root README structured like this:

```markdown
# Workshop Title
**Short subtitle**

> Short quote or one-line framing

---

<p align="center">
  <img src="resources/poster-file.png" alt="Workshop poster" width="700">
</p>

Short workshop intro paragraph.

## Session Details
- **Resource Person:** Name
- **Role:** Title
- **Date:** Date
- **Time:** Time
- **Platform:** Platform

---

## Slides
[Download the session slides →](./resources/slides.pdf)

[View the slides online →](https://...)

<p align="center">
  <img src="resources/slide-cover.jpg" alt="Slide cover poster" width="700">
</p>

---

## Workshop Chapters
| # | Chapter | What You'll Learn |
|---|---------|-------------------|
```

## Chapter README pattern

Use this structure unless the user provides fuller content:

```markdown
# Chapter Title

> Short quote

Short intro.

---

## Section 1

## Section 2

## Resources

## Discussion
Questions from this chapter?
**[Ask in Discussions →](https://github.com/OWNER/REPO/discussions)**
```

## Naming rules

- Prefer numbered chapter folders like `01-plan-and-architect`
- Use lowercase kebab-case for folder names
- Keep asset filenames stable once linked from README
- If the user supplies files with spaces in names, link them with URL-encoded spaces rather than renaming unless asked

## GitHub publishing checklist

When the repo is ready, provide or run:

```bash
git init
git add .
git commit -m "docs: add workshop resource repository"
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

If `origin` already exists, do not overwrite it unless the user asks.

## Quality bar

Before finishing:
- confirm every linked local file exists
- confirm poster images render with the right path
- confirm discussion links use the correct repo URL
- confirm chapter links point to real folders
- avoid placeholder usernames, filenames, or broken relative links in the final state
