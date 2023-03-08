---
title: Jekyll Gitbook Theme
permalink: /
---

# Jekyll Gitbook Theme

Make Jelly site have a GitBook look!

### Demo

Live demo on Github Pages: [https://sighingnow.github.io/jekyll-gitbook](https://sighingnow.github.io/jekyll-gitbook)

[![Jekyll Themes](https://img.shields.io/badge/featured%20on-JekyllThemes-red.svg)](https://jekyll-themes.com/jekyll-gitbook/)

### Why Jekyll with GitBook

GitBook is an amazing frontend style to present and organize contents (such as book chapters and blogs) on Web. The typical to deploy GitBook at [Github Pages](https://pages.github.com) is building HTML files locally and then push to Github repository, usually to the `gh-pages` branch. It's quite annoying to repeat such workload and make it hard for people do version control via git for when there are generated HTML files to be staged in and out.

This theme takes style definition out of generated GitBook site and provided the template for Jekyll to rendering markdown documents to HTML, thus the whole site can be deployed to [Github Pages](https://pages.github.com) without generating and uploading HTML bundle every time when there are changes to the original repo.

### How to Get Started

This theme can be used just as other [Jekyll themes](https://pages.github.com) and support [remote theme](https://rubygems.org/gems/jekyll-remote-theme), see [the official guide](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll) as well.

You can introduce this jekyll theme into your own site by either

* [Fork](https://github.com/sighingnow/jekyll-gitbook/fork) this repository and add your markdown posts to the `_posts` folder.
* Use as a remote theme in your [`_config.yml`](https://github.com/sighingnow/jekyll-gitbook/blob/master/\_config.yml)(just like what we do for this site itself),

```yaml
remote_theme: sighingnow/jekyll-gitbook
```

#### Deploy Locally with Jekyll Serve

This theme can be ran locally using Ruby and Gemfiles.

[Testing your GitHub Pages site locally with Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll) - GitHub

### Full-text search

The search functionality in jekyll-gitbook theme is powered by the [gitbook-plugin-search-pro](https://github.com/gitbook-plugins/gitbook-plugin-search-pro) plugin and is enabled by default.

[https://sighingnow.github.io/jekyll-gitbook/?q=generated](https://sighingnow.github.io/jekyll-gitbook/?q=generated)

### Code highlight

The code highlight style is configurable the following entry in `_config.yaml`:

```yaml
syntax_highlighter_style: colorful
```

The default code highlight style is `colorful`, the full supported styles can be found from [the rouge repository](https://github.com/rouge-ruby/rouge/tree/master/lib/rouge/themes). Customized style can be added to [./assets/gitbook/rouge/](../../assets/gitbook/rouge/).

### How to generate TOC

The jekyll-gitbook theme leverages [jekyll-toc](https://github.com/allejo/jekyll-toc) to generate the _Contents_ for the page. The TOC feature is not enabled by default. To use the TOC feature, modify the TOC configuration in `_config.yml`:

```yaml
toc:
    enabled: true
    h_min: 1
    h_max: 3
```

### Google Analytics, etc.

The jekyll-gitboook theme supports embedding the [Google Analytics](https://analytics.google.com/analytics/web/), [CNZZ](https://www.cnzz.com/) and [Application Insights](https://docs.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview) website analytical tools with the following minimal configuration in `_config.yaml`:

```yaml
tracker:
  google_analytics: "<YOUR GOOGLE ANALYTICS KEY, e.g, UA-xxxxxx-x>"
```

Similarly, CNZZ can be added with the following configuration in `_config.yaml`

```yaml
tracker:
  cnzz: "<YOUR CNZZ ANALYTICS KEY, e.g., xxxxxxxx>"
```

Application Insights can be added with the following configuration in `_config.yaml`

```yaml
tracker:
  application_insights: "<YOUR APPLICATION INSIGHTS CONNECTION STRING>"
```

### Extra StyleSheet or Javascript elements

You can add extra CSS or JavaScript references using configuration collections:

* extra\_css: for additional style sheets. If the url does not start by http, the path must be relative to the root of the site, without a starting `/`.
* extra\_header\_js: for additional scripts to be included in the `<head>` tag, after the `extra_css` has been added. If the url does not start by http, the path must be relative to the root of the site, without a starting `/`.
* extra\_footer\_js: for additional scripts to be included at the end of the HTML document, just before the site tracking script. If the url does not start by http, the path must be relative to the root of the site, without a starting `/`.

### Customizing font settings

The fonts can be customized by modifying the `.book.font-family-0` and `.book.font-family-1` entry in [`./assets/gitbook/custom.css`](https://github.com/sighingnow/jekyll-gitbook/blob/master/gitbook/custom.css),

```css
.book.font-family-0 {
    font-family: Georgia, serif;
}
.book.font-family-1 {
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

### Tips, Warnings and Dangers blocks

The jekyll-gitbook theme supports customized kramdown attributes (`{: .block-tip }`, `{: .block-warning }`, `{: .block-danger }`) like that displayed in [the discord.js website](https://discordjs.guide/popular-topics/canvas.html#setting-up-napi-rs-canvas). The marker can be used like

```markdown
> ##### TIP
>
> This guide is last tested with @napi-rs/canvas^0.1.20, so make sure you have
> this or a similar version after installation.
{: .block-tip }
```

Rendered page can be previewed from

[https://sighingnow.github.io/jekyll-gitbook/jekyll/2022-06-30-tips\_warnings\_dangers.html](https://sighingnow.github.io/jekyll-gitbook/jekyll/2022-06-30-tips\_warnings\_dangers.html)

### Cover image inside pages

The jekyll-gitbook theme supports adding a cover image to a specific page by adding a `cover` field to the page metadata:

```diff
  ---
  title: Page with cover image
  author: Tao He
  date: 2022-05-24
  category: Jekyll
  layout: post
+ cover: /assets/jekyll-gitbook/dinosaur.gif
  ---
```

The effect can be previewed from

[https://sighingnow.github.io/jekyll-gitbook/jekyll/2022-05-24-page\_cover.html](https://sighingnow.github.io/jekyll-gitbook/jekyll/2022-05-24-page\_cover.html)

### License

This work is open sourced under the Apache License, Version 2.0.

Copyright 2019 Tao He.
