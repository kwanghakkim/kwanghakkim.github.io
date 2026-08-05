# CLAUDE.md — kwanghakkim.github.io

Personal academic site of Kwang Hak Kim (PhD candidate, Mechanical Engineering, UC San Diego).
Jekyll site on a beautiful-jekyll fork, deployed by GitHub Pages.

## Ground rules

- **Default branch is `master`** (not main). Deploys via GitHub Pages **legacy branch build**:
  pushing to master deploys in ~1–2 min. There is no CI workflow — it was deleted deliberately.
- **No blog, no comments, no tags, no search, no RSS.** That machinery (posts, feed.xml,
  tags.html, staticman, search corpus, paginate) was deliberately removed — do not reintroduce.
  Inactive theme includes (e.g. `_includes/*comment*.html`) are kept intentionally because
  deleting them risks breaking include chains; leave them alone and never activate them.
- `theme: null` in `_config.yml` must stay: if the key is absent, the github-pages gem silently
  injects jekyll-theme-primer and its assets into the build.

## Content conventions

- **News** lives in `_data/news.yml` — single source of truth, newest first, new items added
  at the top. One-line add: `- { date: "Aug 2026", text: "Your update here." }`
  (optional `link:` makes the text clickable). File order IS display order; nothing is
  date-parsed. Homepage shows the first 4; `/news` shows all, grouped by the trailing year
  token of `date`.
- **Publications** (`publications.md`) is synced from the user's CV (LaTeX, kept outside this
  repo). **The CV is the source of truth for paper status and venues** — only change entries
  when the user provides an updated CV or explicit instructions. Structure: Journal Articles /
  Conference Papers / Manuscripts in Review.
- **Publication ordering**: most recent first within each section, by **actual event/
  publication date, not the year string** (e.g. CDC 2026 = December, ACC 2026 = July,
  AIAA SciTech 2026 = January — so CDC 2026 outranks ACC 2026 despite the same year).
  Manuscripts in review order by arXiv submission date (from the arXiv abs page); entries
  with no arXiv link keep their current relative position. **When dates tie, first-author
  (Kim) papers go first.**
- **CV PDF**: `assets/Kwang_Hak_Kim_CV_website.pdf`, linked from the hero and the navbar.
- **Homepage** (`index.html`): hero (name + role only — advisors/lab belong in the bio, not
  the header), orange NOW card for current position, bio, News (top 4), Talks/Teaching/
  Service/Awards 2×2 grid, personal line at the end.

## Design — Direction 1 "Margins of Safety"

Flight-test document restyle of beautiful-jekyll (CSS + config only — layouts/includes were
not modified for styling and shouldn't be).

- Tokens: paper `#FBFBF9` · ink `#101828` · flight-orange `#E8490F` · hatch `#98A2B3` ·
  panel `#EEF0ED`. **Orange is the only accent** and appears at rest in exactly one place
  (the NOW card); everywhere else only on hover/focus. Keep that restraint.
- Type: IBM Plex Sans (display) / IBM Plex Serif (body) / IBM Plex Mono (dates, labels, nav).
  Loaded via `@import` in main.css; theme fonts rethemed through `--body-font`/`--header-font`.
- Signature element: the **barrier rule** — dividers drawn as a safe-set boundary (ink line
  with diagonal hatching on one side). Classes: `.rule-barrier`, and `main hr` gets the same
  treatment (this is how Publications' `<hr>`s are styled without touching content).
- All custom CSS lives in `assets/css/main.css` (loaded last via `site-css`). `_config.yml`
  is the source of truth for anything theme-native (colors, navbar links, avatar).
- Accessibility floor: visible keyboard focus (2px orange outline), `prefers-reduced-motion`
  respected, responsive down to 375px. Verify at 375px before shipping layout changes.

## Local preview

- `.claude/launch.json` has a `jekyll` config → use the preview tooling to start it;
  serves http://localhost:4000 with LiveReload.
- Manual equivalent: `/opt/homebrew/opt/ruby/bin/bundle exec jekyll serve --livereload`
  (Homebrew Ruby 3.3; gems installed project-locally in `vendor/bundle`).
- `_config.yml` is **not** watched — restart the server after config changes.
- `Gemfile` pins the `github-pages` gem to mirror production; `Gemfile.lock` is committed
  on purpose.
