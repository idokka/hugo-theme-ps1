# $PS1 Theme for Hugo

![$PS1][screenshot]

### DEMO - https://hugo-theme-ps1-idokkas-projects.vercel.app/ <a id="demo" />

---

- [$PS1](#ps1)
  - [Features](#features)
      - [Built-in shortcodes](#built-in-shortcodes)
      - [Code highlighting](#code-highlighting)
      - [Improved RSS Feed](#improved-rss-feed)
  - [How to start](#how-to-start)
  - [How to run your site](#how-to-run-your-site)
  - [How to configure](#how-to-configure)
  - [How to add a cover image to your posts](#how-to-add-a-cover)
  - [How to display the Last Modified Date in your posts](#display-the-last-modified-date)
  - [How to hide "Read more" button](#how-to-hide-read-more-button)
  - [Add-ons](#add-ons)
  - [How to edit the theme](#how-to-edit)
  - [Found a bug?](#bug)
  - [New cool idea or feature](#feature)
  - [`$PS1` theme user?](#ps1-theme-user)
  - [License](#license)

## Features

- **dark/light mode**, depending on your preferences (the theme of your operating system is default, but you can change it)
- great reading experience thanks to [**Inter font**][font], made by [Rasmus Andersson][font-about]
- nice code highlighting thanks to [**PrismJS**](https://prismjs.com)
- fully responsive

#### Built-in shortcodes

- **`image`** (prop required: **`src`**; props optional: **`alt`**, **`position`** (**left** is default | center | right), **`style`**)
  - eg: `{{< image src="/img/hello.png" alt="$PS1" position="center" style="border-radius: 8px;" >}}`
- **`figure`** (same as `image`, plus few optional props: **`caption`**, **`captionPosition`** (left | **center** is default | right), **`captionStyle`**
  - eg: `{{< figure src="/img/hello.png" alt="$PS1" position="center" style="border-radius: 8px;" caption="$PS1" captionPosition="right" captionStyle="color: red;" >}}`
- **`imgproc`** Hugo shortcode for image processing, plus additional **`position`** param [ left | center | right ] (optional).
  - eg: `{{< imgproc "img/hello.png" Resize "250x" center />}}`
  - More detailed info on processing commands at the [documentation](https://gohugo.io/content-management/image-processing/)
- **caption** same as `figcaption` but without figure itself. Has the optional props: **`align`** (left | **center** is default | right), **`style`**
  - eg: `{{< caption align="center" style="font-style: italic;" >}}`
- **epigraph** same as `blockquote`, i.e. markdown quotation, but left-alignmented.
  - e.g. `{{< epigraph >}}The years ago..{{< /epigraph >}}`
- **`code`** (prop required: **`language`**; props optional: **`title`**, **`id`**, **`expand`** (default "△"), **`collapse`** (default "▽"), **`isCollapsed`**)
  - eg:
  ```go
  {{< code language="css" title="Really cool snippet" id="1" expand="Show" collapse="Hide" isCollapsed="true" >}}
  pre {
    background: #1a1a1d;
    padding: 20px;
    border-radius: 8px;
    font-size: 1rem;
    overflow: auto;

    @media ($phone) {
      white-space: pre-wrap;
      word-wrap: break-word;
    }

    code {
      background: none !important;
      color: #ccc;
      padding: 0;
      font-size: inherit;
    }
  }
  {{< /code >}}
  ```
  - also can be used to import snippet file from page resources, eg:
  ```go
  ---
  resources:
   - src: snippet.js
  ---
  {{< code snippet.js css />}}
  ```

#### Code highlighting

By default the theme is using PrismJS to color your code syntax. All you need to do is to wrap you code like this:

<pre>
```html
  // your code here
```
</pre>

Supported languages via [documentation][prismjs-langs].

#### Improved RSS Feed

Some enhancements have been made to Hugo's [internal RSS][internal-rss] generation code.

**A page's cover image now appears at the top of its feed display**. This image is set manually using [the cover params](#how-to-add-a-cover). If unset, the RSS generator searches for the first image file in the page bundle whose name includes 'featured', 'cover', or 'thumbnail'.

**You can optionally display the full page content in your RSS feed** (default is Description or Summary data from Front Matter). Set `rssFullText: true` in your `hugo.yaml` file to enable this option.

**You can choose a site image to be displayed when searching for your RSS feed.** Set `rssImage: 'image/url/here'` in your `hugo.yaml` file to enable this option.

## How to start

You can download the theme manually by going to [repository][repo] and pasting it to `themes/ps1` in your root directory.

You can also choose **one of the 3 possibilities** to install the theme:

1. as Hugo Module
2. as a standalone local directory
3. as a git submodule

⚠️ **The theme needs at least Hugo **Extended** v0.147.x**.

### Install theme as Hugo Module

```bash
# If this is the first time you're using Hugo Modules
# in your project. You have to initiate your own module before
# you fetch the theme module.
#
# hugo mod init [your website/module name]
hugo mod get github.com/idokka/hugo-theme-ps1.git
```

and in your config file add:

```yaml
module
  # This is needed when you fetch the theme as a submodule to your repo.
  # replacements: 'github.com/idokka/hugo-theme-ps1 -> themes/ps1'
  imports:
    path: 'github.com/idokka/hugo-theme-ps1.git'
```

Keep in mind that the theme by default won't show up in the `themes` directory. This means that you are using the theme as it was on the repository at the moment you fetched it. Your local `go.sum` file keeps all the references. Read more about Hugo Modules in the [official documentation][hugo-modules].

⚠️ If you encounter any issues with:

```bash
Error: module "ps1" not found; either add it as a Hugo Module or store it in "[...your custom path]/themes".: module does not exist
```

then please try to remove `theme: 'ps1'` from your config file.

### Install theme locally

```bash
git clone https://github.com/idokka/hugo-theme-ps1.git themes/ps1
```

This will clone the repository directly to the `themes/ps1` directory.

### Install theme as a submodule

```bash
git submodule add -f https://github.com/idokka/hugo-theme-ps1.git themes/ps1
```

This will install the repository as a sumbodule in the `themes/ps1` directory.

## How to run your site

From your Hugo root directory run:

```
hugo server -t ps1
```

and go to `localhost:1313` in your browser. From now on all the changes you make will go live, so you don't need to refresh your browser every single time.

## How to configure

The theme doesn't require any advanced configuration. Just copy:

```yaml
baseUrl: '/'
languageCode: 'en-us'
# Add it only if you keep the theme in the `themes` directory.
# Remove it if you use the theme as a remote Hugo Module.
theme: 'ps1'
# Override to place own footer string
# copyright: 'panr/idokka'

# pagination:
#   pagerSize: 5

# services:
#   googleAnalytics:
#     id: '***'

params:
  # dir name of your blog content (default is `content/posts`)
  contentTypeName: 'posts'
  # OS theme is default when not provided, but you can force it to "light" or "dark"
  defaultTheme: 'dark'
  # If you set this to 0, only submenu trigger will be visible
  showMenuItems: 2
  # Show reading time in minutes for posts
  showReadingTime: false
  # Show table of contents at the top of your posts (defaults to false)
  # Alternatively, add this param to post front matter for specific posts
  # toc: true
  # Show full page content in RSS feed items
  # (default is Description or Summary metadata in the front matter)
  # rssFullText: true

  # All supported icons you can find in layouts\partials\svg.html
  social:
  - name: 'github'
    url: 'https://github.com/idokka/hugo-theme-ps1'

languages:
  en:
    title: 'Your site title'
    subtitle: 'Your site subtitle'
    keywords: ''
    menuMore: 'Show more'
    writtenBy: 'Written by'
    readMore: 'Read more'
    readOtherPosts: 'Read other posts'
    newerPosts: 'Newer posts'
    olderPosts: 'Older posts'
    dateFormatSingle: 2006-01-02
    dateFormatList: 2006-01-02
    # Leave empty to disable, enter display text to enable
    # lastModDisplay: 'Modified'
    
    params:
      logo:
        logoText: '$PS1'
        logoHomeLink: '/'
    #   or
    #
    #   path: '/img/your-example-logo.svg'
    #   alt: 'Your example logo alt text'
    
    menu:
      main:
      - identifier: 'about'
        name: 'About'
        url: '/about'
      - identifier: 'showcase'
        name: 'Showcase'
        url: '/showcase'

```

to `hugo.yaml` file in your Hugo root directory and change params fields.

**NOTE:** Please keep in mind that currently main menu doesn't support nesting.

## How to add a cover image to your posts <a id="how-to-add-a-cover" />

Adding a cover image to your post is simple and there are two options when you edit your `index.md` file in `content/posts/blog-entry-xy/index.md`:

* Use `cover: '/path/to/absolute/img.jpg'` to link an absolute image
  * Resulting in `https://www.yourpage.com/path/to/absolute/img.jpg`
* Use `cover: 'img.jpg'` and `useRelativeCover: true` to link the image relative to the blog post folder
  * Resulting in `https://www.yourpage.com/posts/blog-entry-xy/img.jpg`
* Use `coverAlt: 'description of image'` to add custom alt text to the cover image (defaults to post or page title as alt text)
* Use `coverCaption: 'Image Credit to [Barry Bluejeans](https://unsplash.com/)'` to add a caption for the cover image.

## How to display the Last Modified Date in your posts <a id="display-the-last-modified-date" />

Add `lastModDisplay: '[your display text]'` to `hugo.yaml` to enable last modified date on your posts. Note - an empty string value `""` does not display anything.

Example: `lastModDisplay: 'Modified:'` --> "Modified: Jan 01, 0001"

:octocat: Hugo's `enableGitInfo` option is a nice complement to this feature.

## How to hide "Read more" button

In a post's front matter you have to add `hideReadMore` param set to `true`. This will result in that the post won't have "Read more" button in the list view.

## Add-ons

- **Archive** — Theme has built-in `archive` page for main content (see `contentTypeName` variable in config). If you need archive on your blog just copy [archive.md][archive.md] to your `content` dir. If you need multilangual archives, duplicate `content/archive.md` and add `.Lang` variable, eg: `content/archive.pl.md` (remember to change `url` in duplicated file).
- **Comments** — for adding comments to your blog posts please take a look at [`layouts/partials/comments.html`][comments.html].
- **Prepended `<head>`** — if you need to add something inside `<head>` element, and before any of the theme's `<script>` and `<link>` tags are declared, please take a look at [`layouts/partial/prepended_head.html`][prepended_head.html]
- **Extended `<head>`** — if you need to add something inside `<head>` element, after all of all of the theme's `<script>` and `<link>` tags are declared, please take a look at [`layouts/partial/extended_head.html`][extended_head.html]
- **Extended `<footer>`** — if you need to add something before end of `<body>` element, please take a look at [`layouts/partial/extended_footer.html`][extended_footer.html]

[archive.md]: exampleSite/content/archive.md
[comments.html]: layouts/partials/comments.html
[prepended_head.html]: layouts/partials/prepended_head.html
[extended_head.html]: layouts/partials/extended_head.html
[extended_footer.html]: layouts/partials/extended_footer.html

## How to edit the theme <a id="how-to-edit" />

If you are using as a remote Hugo Module (you don't have the theme files in the `theme/ps1`) and you have to override only some of the styles, you can do this easily by adding `static/style.css` in your root directory and point things you want to change.

If you have the theme files in the theme directory, then you can directly edit anything in the theme, you just have to go to `themes/ps1` and modify the files. No compilation step needed.

## Found a bug? <a id="bug" />

If you spot any bugs, please use [Issue Tracker][issues] or create a new [Pull Request][pulls] to fix the issue.

[issues]: https://github.com/idokka/hugo-theme-ps1/issues
[pulls]: https://github.com/idokka/hugo-theme-ps1/pulls

## New cool idea or feature? <a id="feature" />

The theme is in constant development since 2019 and has got many cool features that helped many of you and made the theme better. But there were also many features that I wasn't sure about because I want to keep the theme as simple as possible.

So, let's say you have an idea of how to extend the theme. That's cool and you're welcome to do that, just follow these steps:

- fork the theme
- implement the feature
- write an instruction how to use the feature
- give a working example of the implementation for other users
- add info about your work to `COMMUNITY-FEATURES.md`
- make a PR with edited `COMMUNITY-FEATURES.md`

This will help keeping the theme close to its roots, and also allow anyone who wishes to improve it and match their needs, to do whatever they want.

Sounds OK? Cool, let's rock! 🤘

## `$PS1` theme user?

I'd be happy to know more about you and what you are doing. If you want to share it, please make a contribution and [add your site to the list](USERS.md)! 🤗

## License

Copyright © 2019-2022 Radosław Kozieł 🇵🇱 ([@panr](https://twitter.com/panr))  
Copyright © 2023-2026 Oleksii M. 🇺🇦 ([@idokka](https://www.linkedin.com/in/omyronenko))

The theme is released under the [MIT License](LICENSE.md).

---
[screenshot]: https://raw.githubusercontent.com/idokka/hugo-theme-ps1/refs/heads/master/images/screenshot.png
[font]: https://rsms.me/inter/
[font-about]: https://rsms.me/about/
[prismjs-langs]: https://prismjs.com/#supported-languages
[internal-rss]: https://github.com/gohugoio/hugo/blob/25a6b33693992e8c6d9c35bc1e781ce3e2bca4be/tpl/tplimpl/embedded/templates/_default/rss.xml
[repo]: https://github.com/idokka/hugo-theme-ps1
[hugo-modules]: https://gohugo.io/hugo-modules
