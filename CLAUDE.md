# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static Jekyll site (GitHub Pages) for the "Is Robotics Underinvesting in Its Own Foundations?" IROS 2026 special forum. No app code, no build scripts, no tests — content and styling only. Deployed automatically via GitHub Pages when pushed to `main`. Sibling site: `IEEE-RAS-Robot-Control/ocrc_p2_ifac26` (same theme family, different palette).

## Commands

No package.json / Gemfile is committed (`.gitignore` excludes `Gemfile`, `Gemfile.lock`, `.bundle/`, `vendor/`). To preview locally:

```
gem install bundler jekyll
bundle init && bundle add jekyll github-pages
bundle exec jekyll serve
```

No lint or test suite. Verify by checking HTML/Liquid renders and content structure stays intact.

## Architecture

- **`_config.yaml`** — site title/description and theme (`jekyll-theme-cayman`, remote gem).
- **`index.md`** — entire page content (single-page site). Front matter (`title`, `display_title`, `description`, `date`, `venue`) feeds `_layouts/default.html`. Sections: About, Program, Speakers, What We Ask of Speakers, Organizers, Further Reading.
- **`_layouts/default.html`** — wraps `index.md`. Renders header from front matter, TC logo, event-meta badges (date/venue), footer.
- **Styling**: `assets/css/style.scss` imports the Cayman theme and overrides `.page-header` gradient + heading color (purple/amber palette). `_sass/jekyll-theme-cayman.scss` is a local shadow of the remote theme's SCSS (needed only to inject `@import "workshop"` into the chain — do not diverge it further from upstream cayman). `_sass/_workshop.scss` holds all custom component styles: event-meta badges, program `.agenda` table (session-colored rows), `.speaker-grid`/`.speaker-chip` (name+affiliation, no photo), `.profile-grid`/`.profile-card` (organizers, with photo).
- Speakers have no bios/photos in the source brief, so they render as plain chips; organizers reuse existing photos from the sibling `ocrc_p2_ifac26` repo (same people).
- Editing schedule: update the `.agenda` block in `index.md` directly (rows use `s1`/`s2`/`s3`/`break`/`plain` modifier classes).
