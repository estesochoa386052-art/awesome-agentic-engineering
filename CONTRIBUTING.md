# Contributing to Awesome Agentic Engineering

Thanks for your interest in contributing! This document explains how to add resources and maintain the list.

## How to Add a Resource

### 1. Update README.md

Add your resource to the appropriate category in `README.md` using this format:

```markdown
- [Resource Name](https://url.com) - One-line description ending with a period.
```

**Guidelines:**
- Place entries alphabetically within each category, or group logically when ordering matters.
- Descriptions should be concise (one sentence), start with a capital letter, and end with a period.
- Links should point to the primary source (GitHub repo, official site, or paper).
- Avoid marketing language — keep descriptions factual and specific.

### 2. Update the Website

The website at `docs/index.html` has its own structured HTML sections. Add a matching entry to the appropriate section using the existing markup patterns. Look at any `resource-item` block for the format:

```html
<a class="resource-item" href="https://url.com" target="_blank">
  <div>
    <div class="res-title">Resource Title</div>
    <div class="res-meta">
      <span>Company</span><span>Year</span>
      <span class="res-tag">Category</span>
    </div>
  </div>
  <span class="res-arrow">&rarr;</span>
</a>
```

### 3. Submit a Pull Request

- Fork the repo
- Create a branch: `git checkout -b add-resource-name`
- Commit your changes: `git commit -m "Add Resource Name to Category"`
- Push and open a PR

## Quality Standards

Before submitting, make sure the resource:

- **Is relevant** to agentic engineering (AI agents, coding agents, LLM tooling, evaluation, etc.)
- **Is actively maintained** (for tools/frameworks) or **is a recognized work** (for papers/blogs)
- **Is not a duplicate** of an existing entry
- **Has a working URL**
- **Is not purely promotional** — we curate based on technical merit

## Categories

| Category | What belongs here |
|---|---|
| Company Deployments | First-party accounts of production agent deployments with metrics |
| Agent Frameworks & Harnesses | Frameworks and tools for building/orchestrating AI coding agents |
| Engineering Blogs | First-party engineering posts describing production systems |
| Papers & Research | Academic papers, technical reports, data analyses |
| Talks & Podcasts | Conference talks, interviews, podcast episodes |
| Tools & Repos | Open-source tools, SDKs, standards, and products |
| Guides & Tutorials | Analysis pieces, playbooks, learning roadmaps |

### Proposing a New Category

If your resource doesn't fit any existing category, open an issue first to discuss adding a new one. New categories should have at least 3 initial items.

## Maintenance

If you find a broken link or outdated resource, please open an issue or submit a PR to fix it.
