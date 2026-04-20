# Alanna Burke — Portfolio Site

A modern, bold portfolio and resume site built with React, TypeScript, and Tailwind CSS. Designed with the **Chromatic Confidence** aesthetic — vibrant color blocks, confident typography, and energetic interactions that reflect a bright, community-driven personality.

**Live site:** https://alannaburke.github.io

---

## Table of Contents

1. [Overview](#overview)
2. [Tech Stack](#tech-stack)
3. [Project Structure](#project-structure)
4. [How to Update Content](#how-to-update-content)
5. [Local Development](#local-development)
6. [Building and Deploying](#building-and-deploying)
7. [Adding Images](#adding-images)
8. [Design System Reference](#design-system-reference)

---

## Overview

This is a single-page portfolio site with the following sections:

| Section | Description |
|---|---|
| **Hero** | Name, title, tagline, profile photo, and key stats |
| **About** | Professional summary with illustrated focus-area cards |
| **Resume** | Full work history with company logos, expandable bullet points, education, skills, and volunteer work |
| **Talks** | 3x3 grid of featured talk screenshots plus a filterable archive of all 39+ talks |
| **Publications** | Published articles, blog posts, code standards series, and miscellaneous links |
| **Contact** | "Let's Connect" call-to-action with email and LinkedIn buttons |
| **Footer** | Social links, email, and quick navigation |

A downloadable 2-page PDF resume is also available via a button in the Resume section.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| [React 19](https://react.dev/) | UI framework |
| [TypeScript](https://www.typescriptlang.org/) | Type safety |
| [Tailwind CSS 4](https://tailwindcss.com/) | Utility-first styling |
| [Vite](https://vite.dev/) | Build tool and dev server |
| [Framer Motion](https://www.framer.com/motion/) | Animations |
| [Lucide React](https://lucide.dev/) | Icons |
| [shadcn/ui](https://ui.shadcn.com/) | Pre-built UI components |
| [pnpm](https://pnpm.io/) | Package manager |

---

## Project Structure

The files you will most likely need to edit are highlighted below.

```
client/
├── index.html                  # HTML shell (fonts, meta tags, Open Graph)
├── src/
│   ├── App.tsx                 # Route definitions and theme provider
│   ├── index.css               # Global CSS, design tokens, color palette
│   ├── main.tsx                # React entry point
│   ├── data/
│   │   └── content.ts          # ⭐ ALL SITE CONTENT LIVES HERE
│   ├── components/
│   │   ├── Navigation.tsx      # Top nav bar + "under construction" banner
│   │   ├── HeroSection.tsx     # Hero / intro section
│   │   ├── AboutSection.tsx    # About / focus areas
│   │   ├── ResumeSection.tsx   # Work history, education, skills, volunteer
│   │   ├── TalksSection.tsx    # Featured talks grid + archive
│   │   ├── PublicationsSection.tsx  # Articles, blogs, links
│   │   ├── ContactSection.tsx  # "Let's Connect" CTA
│   │   └── Footer.tsx          # Footer with social links
│   ├── hooks/
│   │   └── useInView.ts        # Scroll-triggered animation hook
│   ├── pages/
│   │   ├── Home.tsx            # Main page (assembles all sections)
│   │   └── NotFound.tsx        # 404 page
│   └── lib/
│       └── utils.ts            # Utility functions
```

---

## How to Update Content

Almost all content is centralized in a single file:

```
client/src/data/content.ts
```

Open this file and you will find clearly labeled sections. Here is what each export controls and how to edit it.

### Site Config (Hero Section)

```ts
export const siteConfig = {
  name: "Alanna Burke",
  title: "Documentation Architect & Developer Advocate",
  tagline: "Building knowledge systems for AI at Meta.",
  description: "Designing documentation that serves humans and machines.",
  email: "aburke626@gmail.com",
  profileImage: "/manus-storage/profile_f458def7.png",
  social: {
    bluesky: "https://bsky.app/profile/alannaburke.bsky.social",
    linkedin: "https://www.linkedin.com/in/alannaburke/",
    github: "https://github.com/AlannaBurke",
  },
};
```

Change your name, title, tagline, email, social links, or profile image path here.

### Work Experience

Each job is an object in the `experience` array. To add a new position, add a new object at the **top** of the array (most recent first):

```ts
{
  company: "Company Name",
  location: "Remote",
  logo: "/manus-storage/company-logo.png",  // optional
  roles: [
    { title: "Your Title", period: "Month Year – Present" },
  ],
  bullets: [
    "Accomplishment or responsibility description.",
  ],
},
```

To add a new role at an existing company, add another entry to that company's `roles` array.

### Education

```ts
export const education = {
  school: "Temple University",
  location: "Philadelphia, PA",
  degree: "Bachelor of Science in Information Science and Technology",
  minor: "Minor in French",
};
```

### Skills

Skills are organized by category. Add or remove items from any category, or add a new category:

```ts
export const skills = {
  "AI & Knowledge Systems": ["LLMO", "RAG Content Design", ...],
  "Documentation & Content": ["Docs-as-Code", "MkDocs", ...],
  // Add a new category:
  "New Category": ["Skill 1", "Skill 2"],
};
```

### Volunteer Work

Add or edit entries in the `volunteerWork` array:

```ts
// Simple entry (no link):
{ org: "Organization Name", role: "Your role description", period: "Year – present" },

// Entry with a single link (org name becomes clickable):
{ org: "Girl Develop It", role: "Chapter Leader", period: "2014 – 2015",
  url: "https://example.com/profile" },

// Entry with multiple article links (shown below the org name):
{ org: "Temple Cats", role: "Founder, Foster Parent", period: "2009 – 2012",
  urls: [
    { label: "Temple News", href: "https://temple-news.com/article" },
    { label: "Around Main Line", href: "https://aroundmainline.com/article" },
  ] },
```

### Talks (Full Archive)

The `talks` array contains every talk. Add new talks at the **top** (most recent first):

```ts
{
  title: "Talk Title",
  event: "Conference Name",
  date: "Month Year",
  year: 2025,
  sessionUrl: "https://...",   // optional
  videoUrl: "https://...",     // optional
},
```

### Featured Talks (3x3 Grid)

The `featuredTalks` array controls the 9 talks shown in the visual grid. Each needs an `image` (a screenshot of your talk slide):

```ts
{
  title: "Talk Title",
  event: "Conference Name",
  date: "Month Year",
  image: "/manus-storage/talk-screenshot.png",
  videoUrl: "https://...",
  description: "Brief description of the talk.",
},
```

To swap a featured talk, replace one of the 9 entries. Keep exactly 9 for the 3x3 grid layout.

### Publications

There are several publication arrays you can edit:

| Export | What it contains |
|---|---|
| `publishedWork` | Major published articles (SD Times, The New Stack) |
| `blogLinks` | Links to blog platforms |
| `amazeeBlogPosts` | amazee.io blog posts |
| `codeStandardsSeries` | Chromatic code standards blog series |
| `miscLinks` | Interviews, awards, and other links |

---

## Local Development

### Prerequisites

You need [Node.js](https://nodejs.org/) (v18 or later) and [pnpm](https://pnpm.io/) installed.

```bash
# Install pnpm if you don't have it
npm install -g pnpm
```

### Getting Started

```bash
# Clone the repo
git clone https://github.com/AlannaBurke/alannaburke.github.io.git
cd alannaburke.github.io

# Install dependencies
pnpm install

# Start the dev server
pnpm dev
```

The site will be available at `http://localhost:3000`. Changes to any file will hot-reload instantly.

### Available Commands

| Command | Description |
|---|---|
| `pnpm dev` | Start the development server with hot reload |
| `pnpm build` | Build the production-ready site to `dist/public/` |
| `pnpm preview` | Preview the production build locally |
| `pnpm check` | Run TypeScript type checking |
| `pnpm format` | Format all files with Prettier |

---

## Building and Deploying

The site is hosted on **GitHub Pages** from the `master` branch of `AlannaBurke/alannaburke.github.io`.

### How It Works

The repo has two sets of files:

1. **Source code** — the `client/`, `server/`, `shared/` directories, `package.json`, etc. These are the editable source files.
2. **Built output** — the `index.html`, `404.html`, `assets/` directory, and `.nojekyll` file at the repo root. GitHub Pages serves these directly.

When you make changes, you need to rebuild and commit both the source changes and the updated build output.

### Step-by-Step Deploy Workflow

```bash
# 1. Make your changes (usually in client/src/data/content.ts)

# 2. Test locally
pnpm dev
# Check everything looks good at http://localhost:3000

# 3. Build the production site
pnpm build

# 4. Copy the built files to the repo root
#    This overwrites the old build output with the new one
cp -r dist/public/index.html .
cp -r dist/public/assets/ .
cp index.html 404.html

# 5. If you added new images during development, make sure they're
#    in assets/images/ (see "Adding Images" section below)

# 6. Commit and push everything
git add -A
git commit -m "Update portfolio content"
git push origin master
```

GitHub Pages will automatically deploy within 2-5 minutes. Visit https://alannaburke.github.io to see the changes.

### Important: Image Paths

During local development, images referenced as `/manus-storage/filename.png` are served by the Vite dev server. For the deployed GitHub Pages site, these images must exist in `assets/images/` at the repo root, and the JS bundle must reference `/assets/images/` instead. The current deployed build already has this handled — all images are in `assets/images/`.

If you add a **new image** during development:

1. Place the image file in `/home/ubuntu/webdev-static-assets/` (or wherever you keep originals)
2. Also copy it to `assets/images/` in the repo root
3. After building, do a find-and-replace in the generated JS file:
   ```bash
   # Replace manus-storage paths with local paths
   sed -i 's|/manus-storage/|/assets/images/|g' assets/index-*.js
   ```

### Important Files for GitHub Pages

Make sure these files exist in your repo root:

| File | Purpose |
|---|---|
| `.nojekyll` | Tells GitHub Pages not to process files with Jekyll |
| `404.html` | SPA fallback — should be a copy of `index.html` |
| `index.html` | The main entry point |
| `assets/` | JS, CSS bundles and `images/` subdirectory |

### GitHub Pages Settings

Your repo Settings > Pages should be configured as:

- **Source:** Deploy from a branch
- **Branch:** `master` / `/ (root)`

### Removing the "Under Construction" Banner

When you're ready to remove the construction banner, edit `client/src/components/Navigation.tsx` and delete or comment out the banner `<div>` at the top of the component's return statement (the gold-background bar with the construction emoji).

---

## Adding Images

### Company Logos

1. Save the logo image (PNG preferred, ideally with a transparent or white background).
2. Place it in `assets/images/` in the repo root for deployment.
3. Add the path to the corresponding company's `logo` field in `content.ts`:
   ```ts
   logo: "/manus-storage/new-company-logo.png",
   ```
4. After building, make sure to run the `sed` replacement command (see deploy workflow above).

### Talk Screenshots

1. Take a screenshot of your talk's title slide (aim for roughly 16:9 aspect ratio).
2. Save it to `assets/images/` in the repo root.
3. Reference it in the `featuredTalks` array:
   ```ts
   image: "/manus-storage/my-new-talk.png",
   ```

### Profile Photo

Replace the `profileImage` value in `siteConfig` with the path to your new photo. The current image has a circular crop baked in — a square or rectangular headshot would also work well with the site's frame design.

### PDF Resume

The downloadable PDF resume is stored as `assets/images/Alanna_Burke_Resume_*.pdf`. To update it, replace the file and update the path in `ResumeSection.tsx` where the download button's `href` is defined.

---

## Design System Reference

The site uses the **Chromatic Confidence** design system. Here are the key design tokens if you want to make style changes.

### Color Palette

| Color | Hex | Usage |
|---|---|---|
| Coral | `#E8553D` | Primary accent, buttons, highlights |
| Teal | `#0EA5A0` | Secondary accent, links, skill pills |
| Gold | `#F5A623` | Tertiary accent, decorative elements, construction banner |
| Navy | `#1a1a2e` | Dark backgrounds (Talks, Footer) |
| Charcoal | `#2d2d3f` | Primary text color |
| Off-white | `#faf9f6` | Light backgrounds |

### Typography

| Element | Font | Weight |
|---|---|---|
| Headings | Space Grotesk | 600–700 |
| Body text | DM Sans | 400–500 |
| Navigation | Space Grotesk | 500 |

Fonts are loaded from Google Fonts in `client/index.html`. The font-family declarations are in `client/src/index.css`.

### Modifying Colors

Global colors are defined as CSS custom properties in `client/src/index.css` under the `:root` selector. Change the OKLCH values there to update the entire site's palette at once. The named color aliases (`--color-coral`, `--color-teal`, etc.) are defined in the `@theme inline` block.

---

## Quick Reference: Common Tasks

| Task | What to edit |
|---|---|
| Add a new job | `content.ts` → `experience` array (add at top) |
| Add a new talk | `content.ts` → `talks` array (add at top) |
| Swap a featured talk | `content.ts` → `featuredTalks` array (replace one of 9) |
| Add a publication | `content.ts` → appropriate publication array |
| Add volunteer work | `content.ts` → `volunteerWork` array |
| Change social links | `content.ts` → `siteConfig.social` |
| Update email | `content.ts` → `siteConfig.email` |
| Change colors | `index.css` → `:root` CSS variables |
| Remove construction banner | `Navigation.tsx` → delete the gold banner div |
| Update PDF resume | Replace file in `assets/images/`, update path in `ResumeSection.tsx` |

---

## Questions?

If you run into issues or want to make changes beyond simple content updates, the component files in `client/src/components/` are well-organized by section and should be straightforward to modify.
