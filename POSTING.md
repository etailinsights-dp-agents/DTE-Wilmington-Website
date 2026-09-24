# Publishing a Resources post

The site builds with Jekyll on GitHub Pages. A post is one markdown file. Merge it to main and the
site rebuilds itself in about a minute: the post page, the /resources/ index, sitemap.xml,
feed.xml, and llms.txt all update automatically. Nothing else needs editing.

## Add a post

1. Create a file in `_posts/` named `YYYY-MM-DD-short-slug.md` (the date must not be in the future,
   or Jekyll will silently skip it; the slug becomes the URL under /resources/).
2. Start it with this front matter, then write the post in normal markdown below it:

```
---
layout: post
title: "Question-shaped title readers actually type"
description: "One-sentence summary, 140-160 characters. Shows in Google and on the index."
author: "Katy, Lead Trainer"
---
```

3. Open a PR to main. After merge, confirm the post at
   https://dogtrainingelitewilmington.com/resources/ (build status is visible in the repo's
   Actions tab if anything fails).

## Content rules

- Title is the question; the first paragraph gives the direct answer. AI assistants and Google
  both extract from pages built this way.
- Name the towns naturally: Wilmington, Leland, Hampstead, Wrightsville Beach, Carolina Beach.
- One verbatim Google review quote per post is encouraged (blockquote, attribute by name).
- NO em dashes anywhere. Sentence case headings. 500 to 900 words.
- NO pricing, offer, or guarantee specifics until Darren confirms them in writing. No medical or
  legal claims beyond the ADA basics already established in the service dog post.
- Byline stays "Katy, Lead Trainer" unless Darren says otherwise.

## Topic bank (grounded in our FAQ and reviews)

- Puppy training: what to start the first week you bring the puppy home
- Rescue dogs: helping a rescue settle in (Karen Foland's Archer story is the anchor quote)
- Crate training without the crying
- Dog training for families with young kids
- What "positive reinforcement training" actually means
- Preparing your dog for beach season in Wrightsville and Carolina Beach

## Clara: weekly publishing run

Standing instruction from Darren: one post per week. Open the PR by Monday, Darren approves,
merge Tuesday. No post merges without Darren's explicit approval on the PR. Follow this section
top to bottom every run; the Add-a-post steps and Content rules above apply in full.

### 1. Pick the topic

- Take the TOP unused item from the Topic bank above. Never reuse a slug or re-cover a topic:
  check `_posts/` first.
- When you take the last item, add three new ones to the bank in the same PR. A valid topic is a
  question a Wilmington dog owner would type into Google or ask an AI assistant, answerable
  without any unverified business fact (no pricing, offers, guarantees, staff claims).

### 2. Draft

- One new file in `_posts/`, date = planned merge date, never a future date relative to merge day
  (Jekyll skips future-dated posts with no error; the failure is invisible).
- Every claim about Dog Training Elite Wilmington must trace to the live site, the review set
  already on /typ, or something Darren has stated. Anything you cannot source: leave it out and
  list it under "Needs Darren" in the PR description instead.
- Review quotes: verbatim from the /typ carousel set only, one per post, attributed by name.

### 3. Verify before opening the PR (all must pass)

- Filename matches `^[0-9]{4}-[0-9]{2}-[0-9]{2}-[a-z0-9-]+\.md$` and the slug is unused
- Front matter has layout, title, description (140-160 characters), author
- grep returns NOTHING for: em dash, en dash, the ellipsis character, and `\$[0-9]`
- grep finds ALL of: Wilmington, Leland, Hampstead, Wrightsville Beach, Carolina Beach
- Exactly one "Google review" attribution
- If Ruby/Jekyll is available on your droplet, `bundle exec jekyll build` must succeed. If not,
  the Pages build after merge is the test; then the post-merge checks are mandatory.

### 4. PR protocol

- Changed paths: the ONE new `_posts/` file, plus POSTING.md only when refilling the topic bank.
  Nothing else, ever, in a weekly post PR. index.html, typ.html, `_layouts/`, `_config.yml`,
  robots.txt, llms.txt, CNAME, README.md, images/, videos/ are all out of bounds here.
- PR body: post title, final URL, the topic-bank line consumed, and a "Needs Darren" list (or
  "none").
- Merge only after Darren's explicit approval.

### 5. Verify after merge (non-negotiable, in order)

1. Repo Actions tab: build green.
2. `https://dogtrainingelitewilmington.com/resources/<slug>/` renders.
3. /resources/ index lists the new post.
4. /sitemap.xml AND /llms.txt both contain the new URL. Both are auto-generated; if either is
   missing it, the build did not actually run: stop and report.
5. Home page and /typ spot-check: unchanged.

Report the five results to Darren with the PR link.

### If a build breaks

Commit a `.nojekyll` file to the repo root: the site instantly reverts to serving raw files
(the blog goes dark, home and /typ stay up). Then report to Darren and the external dev. Do not
debug by editing layouts or config on your own.

### Escalation

- Pricing, offers, guarantee wording, staff facts, credentials: Darren decides, always.
- Layout, CSS, config, or structural changes a post seems to need: the external dev's lane;
  flag it in the PR, do not make them.
- Two consecutive build failures: stop the cadence and escalate to the external dev.

## Do not touch

CNAME, README.md, index.html, typ.html, the videos/ and images/ directories. This blog is
additive. The instant off-switch, if a Pages build ever breaks the site, is committing a
`.nojekyll` file to the repo root: Jekyll processing stops and the site serves raw files again.
