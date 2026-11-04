## Getting Started with the Garrulus Page

This is the website for the Garrulus research project. It is built with
[Jekyll](https://jekyllrb.com/), a tool that turns simple text files into a website. To
preview your changes before publishing them, you run a small web server on your own
computer that shows the site at `http://localhost:4000/`.

**You do not need to know Ruby, Docker, or web development to edit this site.** Follow the
steps below once to set up your computer, then see **[`GUIDE.md`](GUIDE.md)** for where the
content lives and how to change it.

> **New here? Read [`GUIDE.md`](GUIDE.md) first.** It is a plain-language tour of the repo:
> what each folder is for, and exactly which file to open to change the text, photos, team
> members, news posts, menu, and colors.

### One-time setup

The site needs a specific version of Ruby (**3.2**) to preview locally. The easiest way to
get it — without touching your system's own Ruby — is a tool called
[**mise**](https://mise.jdx.dev/) that installs the right version automatically.

1. **Install mise** (once per computer). On Linux/macOS, open a terminal and run:

   ```sh
   curl https://mise.run | sh
   ```

   Then close and reopen your terminal. (See the [mise install docs](https://mise.jdx.dev/getting-started.html)
   for Windows or other options.)

2. **Get the code** and enter the folder:

   ```sh
   git clone https://github.com/garrulus-project/garrulus-project.github.io.git
   cd garrulus-project.github.io
   ```

3. **Install the right Ruby and the site's dependencies.** The repo already pins Ruby 3.2
   (via the `.ruby-version` file), so mise knows what to fetch:

   ```sh
   mise install ruby@3.2                     # installs Ruby 3.2
   mise exec ruby@3.2 -- bundle install      # installs the site's building blocks
   ```

### Previewing the site (every time you work on it)

From the project folder, start the local server:

```sh
mise exec ruby@3.2 -- bundle exec jekyll serve --livereload
```

Now open **http://localhost:4000/** in your browser. Leave this running while you work:
every time you save a `.md` or `.html` file, the site rebuilds and your browser refreshes
automatically. Press `Ctrl+C` in the terminal to stop it.

You will see a wall of yellow `DEPRECATION WARNING` messages about Dart Sass and `/`
division when it starts — **this is normal, ignore them.** They come from the theme, not
from anything you did.

### Why Ruby 3.2 specifically?

The `.ruby-version` file pins Ruby 3.2 on purpose. The site depends on a few components
(`google-protobuf`, `sass-embedded`) whose ready-made packages are only published for Ruby
older than 3.3. On newer Ruby (3.3/3.4) they try to build from scratch and fail — most
visibly on Arch Linux, whose Ruby breaks the build at the linking step. Using mise as
above sidesteps this entirely; you never touch your system Ruby.

If you tried an install before this note and it failed, delete the leftovers with
`rm -rf vendor` and run `mise exec ruby@3.2 -- bundle install` again.

### A note on Docker

There are `Dockerfile.dev` and `docker/` files in the repo, but they are **leftovers from
the original theme (they use an ancient Ruby 2.7) and are not used** for this site. Stick
with mise above. If you specifically want a container, a plain
`docker run --rm -it -v "$PWD":/srv -w /srv -p 4000:4000 ruby:3.2 bash -c "bundle install && bundle exec jekyll serve --host 0.0.0.0"`
works, but it is not the recommended path.

### Where does the live site come from?

The public site at <https://garrulus-project.github.io> is built and published
automatically by **GitHub Pages** whenever changes land on the `master` branch. GitHub uses
its own copy of Jekyll and **ignores the `Gemfile`/`Gemfile.lock`** in this repo — so the
local setup above is only for *previewing*. It has no effect on what visitors see; only
pushing to `master` does.

---

# Documentation for [TeXt Theme](https://github.com/kitian616/jekyll-TeXt-theme)

[![license](https://img.shields.io/github/license/kitian616/jekyll-TeXt-theme.svg)](https://github.com/kitian616/jekyll-TeXt-theme/blob/master/LICENSE)
[![Gem Version](https://img.shields.io/gem/v/jekyll-text-theme.svg)](https://github.com/kitian616/jekyll-TeXt-theme/releases)
[![Travis](https://img.shields.io/travis/kitian616/jekyll-TeXt-theme.svg)](https://travis-ci.org/kitian616/jekyll-TeXt-theme)
[![Tip Me via PayPal](https://img.shields.io/badge/PayPal-tip%20me-1462ab.svg?logo=paypal)](https://www.paypal.me/kitian616)
[![Tip Me via Bitcoin](https://img.shields.io/badge/Bitcoin-tip%20me-f7931a.svg?logo=bitcoin)](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/3Fkufxcw2xd8HnaRJBNK4ccdtkUDyyNu4V.jpg)

![TeXt Theme](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/TeXt-home.jpg)

![TeXt Theme Details](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/TeXt-layouts.png)

TeXt is a super customizable Jekyll theme for personal site, team site, blog, project, documentation, etc. Similar to iOS 11 style, it has large and prominent titles, round buttons and cards.

**[Change Log](https://github.com/kitian616/jekyll-TeXt-theme/blob/master/CHANGELOG.md)** | **[中文](https://github.com/kitian616/jekyll-TeXt-theme/blob/master/README-zh.md)**

## Features

- Responsive
- Semantic HTML
- Skins
- Highlight Theme
- Internationalization
- Search
- Table of contents
- Authors
- Additional styles (alert, tag, image, icon, button, grid, etc)
- Extensions (audios, videos, slides, demos)
- Markdown enhancements ([MathJax](https://www.mathjax.org/), [mermaid](https://mermaidjs.github.io/), [chartjs](http://www.chartjs.org/))
- Sharing ([AddToAny](https://www.addtoany.com/), [AddThis](https://www.addthis.com/))
- Comments ([Disqus](https://disqus.com/), [Gitalk](https://gitalk.github.io/), [Valine](https://valine.js.org/en/))
- Pageview ([LeanCloud](https://leancloud.cn/))
- Analytics ([Google Analytics](https://analytics.google.com/analytics/web/))
- RSS ([jekyll-feed](https://github.com/jekyll/jekyll-feed))

## Skins

TeXt has 6 built-in skins, you can also set up your own skin.

| `default` | `dark` | `forest` |
| --- |  --- | --- |
| ![Default](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/skins_default.jpg) | ![Dark](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/skins_dark.jpg) | ![Forest](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/skins_forest.jpg) |

| `ocean` | `chocolate` | `orange` |
| --- |  --- | --- |
| ![Ocean](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/skins_ocean.jpg) | ![Chocolate](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/skins_chocolate.jpg) | ![Orange](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/skins_orange.jpg) |

### Highlight Theme

TeXt use [Tomorrow](https://github.com/chriskempson/tomorrow-theme) as the highlight theme.

| `tomorrow` | `tomorrow-night` | `tomorrow-night-eighties` | `tomorrow-night-blue` | `tomorrow-night-bright` |
| --- |  --- | --- | --- |  --- |
| ![Tomorrow](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/highlight_tomorrow.png) | ![Tomorrow Night](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/highlight_tomorrow-night.png) | ![Tomorrow Night Eighties](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/highlight_tomorrow-night-eighties.png) | ![Tomorrow Night Blue](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/highlight_tomorrow-night-blue.png) | ![Tomorrow Night Bright](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/screenshots/highlight_tomorrow-night-bright.png) |

## Documentation

### Start

- [Quick Start](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/quick-start)
- [Update from 1.x to 2.x](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/update-from-1-to-2)

### Customization

- [Configuration](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/configuration)
- [Navigation](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/navigation)
- [Layouts](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/layouts)
- [Logo and Favicon](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/logo-and-favicon)
- [Authors](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/authors)
- [Internationalization](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/i18n)

### Content

- [Writing Posts](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/writing-posts)
- [Additional styles](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/additional-styles)
- [Extensions](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/extensions)
- [Markdown Enhancements](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/markdown-enhancements)

## Demo Pages

| Name | Description |
| --- | --- |
| [Home](https://kitian616.github.io/jekyll-TeXt-theme/test/) | Home page |
| [Archive](https://kitian616.github.io/jekyll-TeXt-theme/archive.html) | Archive page |
| [Layout Examples](https://kitian616.github.io/jekyll-TeXt-theme/samples.html) | Examples for different layouts |

## License

TeXt Theme is [MIT licensed](https://github.com/kitian616/jekyll-TeXt-theme/blob/master/LICENSE).
