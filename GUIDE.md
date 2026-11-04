# Editing Guide — Garrulus Website

A plain-language map of this website: **what lives where, and which file to open to change
something.** No prior Ruby, Docker, or web experience needed.

If you haven't set up the local preview yet, do that first — see the **Getting Started**
section of [`README.md`](README.md). Keep the preview server running (`localhost:4000`)
while you edit; it refreshes your browser every time you save.

---

## 1. The 30-second mental model

This site is built by **Jekyll**. Jekyll's job is simple: it takes your text files, drops
them into page templates, and produces the finished HTML website in a folder called
`_site/`. You **never edit `_site/` by hand** — it is generated, and gets overwritten every
time you save. You edit the *source* files described below, and Jekyll rebuilds the rest.

Two file types you'll touch:

- **`.md` (Markdown)** — for text-heavy pages and news posts. Markdown is a simple way to
  write formatted text: `## Heading`, `**bold**`, `[link](https://...)`, `![](image.jpg)`.
- **`.html`** — for pages with a more designed layout (the homepage, team, publications).

Most content files start with a block fenced by `---` lines at the very top. That block is
called **front matter** and it sets options for the page (its title, which layout to use,
etc.). Everything *below* the second `---` is the actual page content.

```
---
layout: article        <- front matter (settings)
title: Kontakt
---
## Kontakt             <- page content starts here
Text goes here...
```

---

## 2. Where do I change...? (quick reference)

| I want to change...                    | Open this                                             |
| -------------------------------------- | ----------------------------------------------------- |
| The **homepage** (intro, sections)     | `index.html`                                          |
| The **"About the Project"** page text  | `about.md`                                            |
| The **Team** members                   | `team.html`                                           |
| The **Publications** list              | `Publications.html`                                   |
| The **Contact** page                   | `contact.md`                                          |
| A **news / blog post** (add or edit)   | `_posts/` (see §4)                                    |
| A **photo / logo / image**             | `assets/images/`                                      |
| The **top navigation menu**            | `_data/navigation.yml`                                |
| Site **title, language, settings**     | `_config.yml`                                         |
| The **color theme**                    | `_config.yml` → `text_skin:` (see §6)                 |
| **Colors / fonts / spacing** (deep)    | `_sass/` (advanced — see §6)                          |
| Page **structure / templates**         | `_layouts/` and `_includes/` (advanced — see §5)      |

Everything you'll normally touch is in the **top level of the repo** (the content pages)
plus **`_posts/`**, **`_data/`**, and **`assets/images/`**. The rest is machinery.

---

## 3. Content — the pages (edit these most often)

These files sit in the top level of the repo. Each is one page of the site.

- **`index.html`** — the **homepage**. Its front matter defines the big cover image and a
  list of `sections` (the intro blocks with headings, text, and buttons). Below that, it
  automatically lists the latest **news posts** from `_posts/`.
- **`about.md`** — the **"Über das Projekt" / About** page. Plain Markdown; just edit the
  text below the front matter.
- **`team.html`** — the **Team** page. Every person is an entry in the front matter under
  `data: sections: children:`. To add someone, copy an existing block and change the name,
  role (`excerpt`), photo (`image: src:`), and profile link (`actions:`). See §7 for a
  worked example.
- **`Publications.html`** — the **Publications** page. This is a hand-written HTML table.
  To add a paper, copy an existing `<tr>...</tr>` row and edit the title, authors, and
  link.
- **`contact.md`** — the **Contact** page. Plain Markdown (address, email).

> **Which language?** The site is German (`lang: "de"` in `_config.yml`). Just write your
> text in German; you don't need to deal with the other-language entries you may see in
> some front matter — those come from the theme and can be left alone.

---

## 4. News posts (the blog)

News items live in the **`_posts/`** folder. Each post is one Markdown file, and the
**filename must follow the pattern**:

```
YYYY-MM-DD-Some-Title.md      e.g.  2024-03-13-Drohnenprojekt-Finale-Phase.md
```

The date in the filename sets the post's date and ordering. To **add a news post**, copy an
existing file, rename it with today's date, and edit the top and body:

```markdown
---
title: "Your headline here"
tags:  Garrulus Portrait
cover: /assets/images/your-photo.webp
---

![Alt text](/assets/images/your-photo.webp)
Your article text in Markdown...
```

- `title` — the headline shown on the site.
- `cover` — the thumbnail image (put the file in `assets/images/` first).
- The body is normal Markdown. New posts appear on the homepage automatically.

---

## 5. Layout — the page templates (advanced, rarely touched)

"Layout" means the **skeleton** each page is poured into — where the header, footer, and
sidebar go. You usually **don't** need to touch these; they come from the theme.

- **`_layouts/`** — the page skeletons. When a page's front matter says `layout: home`,
  Jekyll wraps it in `_layouts/home.html`. Others: `landing` (used by the team page),
  `article` / `articles` (text pages), `page`, `base`.
- **`_includes/`** — smaller reusable pieces that the layouts pull in (the navigation bar,
  the footer, article cards, the sidebar, etc.). For example the header/menu bar is
  assembled from files in `_includes/`.

Change these only when you need to alter the **structure** of pages themselves (e.g. move
the menu, change the footer). For everyday content, stay in §3 and §4.

---

## 6. Design — colors, fonts, spacing

Two levels, from easy to advanced:

**Easy — switch the built-in color theme.** In `_config.yml`, find:

```yaml
text_skin: default   # "default", "dark", "forest", "ocean", "chocolate", "orange"
```

Change `default` to one of the listed names and save. Each corresponds to a file in
`_sass/skins/` (e.g. `_forest.scss`).

**Advanced — tweak the actual styles.** The site's styling lives in **`_sass/`** (files
written in SCSS, an extension of CSS). The entry point is `assets/css/main.scss`, which
pulls in everything under `_sass/`. Useful spots:

- `_sass/skins/` — the color palettes (one file per theme above).
- `_sass/common/_variables.scss` — shared values like base font sizes and spacing.
- `_sass/components/`, `_sass/layout/` — styling for specific pieces and page regions.

Editing SCSS is real front-end work; go slowly and use the live preview to check each
change. You'll see Dart Sass deprecation warnings in the terminal when it rebuilds — those
are pre-existing and harmless.

---

## 7. Worked example: add a team member

1. Put the person's photo in `assets/images/` (e.g. `assets/images/jane.jpeg`).
2. Open `team.html`. Find an existing person block under `children:` — it looks like:

   ```yaml
   - title: M.Sc. Ahmad Drak
     excerpt: Wissenschaftlicher Mitarbeiter
     image:
       src: /assets/images/logo/drak.jpeg
       style: "max-width: 50%"
     actions:
       - text: Profil
         url: https://www.h-brs.de/de/inf/ahmad-drak
   ```

3. Copy the whole block, paste it right below, and edit the values:
   - `title:` — the person's name and title.
   - `excerpt:` — their role.
   - `image: src:` — path to the photo you added (`/assets/images/jane.jpeg`).
   - `actions: url:` — link to their profile (or delete the `actions:` block if none).
4. Save. Check `localhost:4000/team.html` — the new card appears.

> **Indentation matters** in these `.yml`-style blocks. Keep the spacing exactly like the
> surrounding entries (spaces, not tabs). If the page breaks after an edit, an indentation
> slip is the usual cause.

---

## 8. Folders you can ignore

These exist but are **not** part of editing the site's content:

- **`_site/`** — the generated output. Never edit; it's rebuilt automatically.
- **`vendor/`, `.bundle/`, `.jekyll-cache/`** — local build machinery (not committed).
- **`docs/`** — the original theme's *own* documentation website. Not our content.
- **`test/`, `tools/`, `docker/`, `Dockerfile.dev`, `package.json`, `.travis.yml`** —
  developer tooling inherited from the theme; not needed for content edits.

---

## 9. Publishing your changes

When your edits look right in the local preview:

```sh
git add <the files you changed>
git commit -m "Describe what you changed"
git push
```

Pushing to the **`master`** branch triggers GitHub Pages to rebuild and publish the live
site at <https://garrulus-project.github.io> (usually within a minute or two). If you're
working on a separate branch, open a pull request into `master` when ready.

> **Tip:** Don't commit generated or local-only folders. `_site/`, `vendor/`, `.bundle/`,
> and similar are already excluded, so a normal `git add` of your content files is safe.
