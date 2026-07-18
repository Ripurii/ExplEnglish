# ExplEnglish

The source for [explenglish.com](https://explenglish.com) (currently live at [ripurii.github.io/ExplEnglish](https://ripurii.github.io/ExplEnglish/)) — a Jekyll site hosted on GitHub Pages. Push to `master` and it deploys automatically in 1-2 minutes.

## Adding a new lesson

Create a file in `_posts/` named `YYYY-MM-DD-your-slug.md` (the date can be today, or whenever the lesson was actually written — it drives sorting on the Latest page and the default relative-time display).

```yaml
---
layout: post
title: "Adjective Order Practice"
level: A2                     # A1, A2, B1, B2, C1, or C2 — required for the filter pills
tags: [grammar]                # see "Tags" below — controls badge color + which page(s) it appears on
duration: 20 min
date: 2026-08-01
---

Regular Markdown content goes here. This becomes the lesson body if you
don't set an `intro` field below.
```

That's the minimum. It'll immediately show up on `/library` (alphabetical) and on whichever tag pages match (e.g. `/grammar`), grouped under the right level header.

### Tags

Each tag both colors the badge and decides which page(s) the lesson appears on. Use one of these exact values: `reading`, `listening`, `speaking`, `writing`, `vocabulary`, `grammar`, `literature`, `novels`, `short-stories`, `poetry`, `literary-devices`, `author-studies`, `themed-series`, `book-series`, `culture`, `cross-curricular`, `tools`, `digital-tools`, `games`. A lesson can have more than one tag (e.g. `[grammar, writing]`), and it'll show up on every matching page. `tools`, `digital-tools`, and `games` are A-Z (not level-based) pages — everything else groups by level. Tag badges always display in the canonical order defined in `_data/tag_order.yml`, regardless of the order you list them in front matter.

### Richer lesson pages (optional)

The lesson layout supports extra front matter for a fuller page — banner image color (auto-picked from your first tag), learning objectives, a side image, video exercises, and an episode picker for multi-part series:

```yaml
---
layout: post
title: "Our Planet: Episode 1"
level: B1
tags: [listening]
duration: 45 min
date: 2026-08-01
lesson_number: 1
tagline: "What will I learn?"
intro: "This lesson series uses clips from the documentary Our Planet..."
image: /assets/lessons/our-planet/lesson-1.jpg
learning_goals:
  - You recognize and understand spoken English in different accents and speeds.
  - You expand your vocabulary around nature, climate, and biodiversity.
exercises:
  - title: "Who is David Attenborough?"
    video_url: https://www.youtube.com/embed/VIDEO_ID
episodes:
  - label: "Episode 1"
    url: /our-planet-episode-1
  - label: "Episode 2"
    url: /our-planet-episode-2
---
```

Every field above is optional — leave any of them out and that section just doesn't render. `episodes` entries can also be plain strings (`- "Episode 1"`) if you don't want them clickable yet.

Answer inputs on the exercise boxes are currently just styled placeholders (no submit logic wired up yet — see "Student answer submission" below).

## Lesson series (multiple episodes/parts)

There's no special "series" machinery — each episode is just its own post in `_posts/`. To link them together:
1. Give each one the same `tags` (so they group together) and its own `lesson_number`.
2. Use the `episodes` field (see above) with real `url`s pointing at each episode's page so readers can jump between them.
3. Put shared materials in one folder — see below.

## Downloadable materials (worksheets, PDFs, images, posters)

Yes — put these directly in this repo, under `assets/lessons/<slug>/`, one folder per lesson or per series. Example:

```
assets/lessons/our-planet/
  lesson-1.jpg
  episode-1-worksheet.pdf
  episode-2-worksheet.pdf
```

Then reference them with a site-root-relative path in your post: `/assets/lessons/our-planet/episode-1-worksheet.pdf`. Any file type works (PDF, images, docx, etc.) — Jekyll just copies them through untouched. Keep individual files well under GitHub's 100MB hard limit (in practice, worksheets/posters/images are tiny — this only matters for video, see below).

There's a placeholder example folder at `assets/lessons/example-lesson-slug/` — delete it once you've added your first real one.

## Video

**Don't put video files in this repo.** Git handles large binaries badly (every version ever committed stays in the repo's history forever, even after deleting the file, so it only ever grows), and GitHub hard-blocks anything over 100MB anyway.

Instead: upload the video to **YouTube** (set it to "Unlisted" if you don't want it publicly searchable — it'll still be viewable/embeddable by anyone with the link) or Vimeo, then just give me the video's URL and I'll wire it into the lesson's `exercises[].video_url` field. That matches how your Webnode lessons already worked (embedded YouTube trailer).

If you already have YouTube/Vimeo links for existing material, just paste them in chat and I'll add them.

## Student answer submission (not built yet)

You mentioned wanting students to save answers and have them emailed to you or the student. You're right that this doesn't need a custom backend — GitHub Pages only serves static files, so the usual approach is a form that posts to a third-party form-to-email service instead of your own server:

- **[Formspree](https://formspree.io)** — simplest option. Point a plain HTML `<form>` at it, it emails the submission to you. Free tier is 50 submissions/month.
- **[EmailJS](https://www.emailjs.com)** — sends email straight from the browser via JS, no page reload needed. More setup, but more control (e.g. templating, sending a copy to the student too).

Emailing a copy back to the *student* (not just to you) usually needs either EmailJS's templating or a paid Formspree plan, since the free tier only emails the form owner by default. Happy to wire this up whenever you're ready — just let me know which pages need it.

## Local preview

Local `jekyll serve` isn't fully set up in this environment yet (Ruby's installed, but the native build toolchain for gem compilation wasn't finished). In the meantime, changes are verified by pushing and checking the live GitHub Pages build, or via a temporary local static preview during development sessions.

## Site structure (for reference)

- `_posts/` — every lesson, one file each
- `_layouts/post.html` — the lesson detail page template
- `_includes/level-listing.html` / `abc-listing.html` — shared templates behind Grammar/Vocabulary/Library/Tools/etc.
- `assets/lessons/` — downloadable materials and images, one folder per lesson/series
- `public/css/hyde.css` — all site styling (colors, fonts, layout)
- Root `.html` files (`grammar.html`, `library.html`, `reading.html`, etc.) — one per nav page, each just front matter + an include call
