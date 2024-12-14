# no style, please!

A (nearly) no-CSS, fast, minimalist Hugo theme, forked from [hanwenguo/hugo-theme-nostyleplease](https://github.com/hanwenguo/hugo-theme-nostyleplease) and thanks for doing the transplant work.

<img src="https://raw.githubusercontent.com/loyistro/no-style-please/refs/heads/main/images/IMG_20241214_143715.jpg">

You can check more screenshots [here](https://github.com/loyistro/no-style-please/tree/main/images).

## Features
Here are the original features:
- Fast (**under 3kb of CSS!**)
- Light, dark and auto modes
- Responsive
- Content first (typography optimized for maximum readability)
- RSS feed (using Hugo's embedded RSS template)
- MathJax support
- Supporting details HTML tag

Additionally, I made these small changes:
- Added publish date and tags as post meta;
- Added a divider between the post meta and the footer;
- Made the footer more standard;
- Added a new "about.html" template; pages that don’t want to show post meta can use it;
- Every page (except “Home”) will have "Back" and "Home" buttons in the top bar;
- Changed the light theme’s background color to a light "beige";
- Added underlines to URL links.

## Installation
Enter your Hugo site:
```zsh
cd demo-site-name
```

run
```zsh
git init
git submodule add --depth=1 https://github.com/louistore/less-style-please.gi
```

In `config.yaml` or `hugo.yaml` add:
```yaml
theme: no-style-please
```

Copy all files in `theme/no-style-please/layout/content/` to `content/`;

run
```zsh
hugo server -D
```

Enjoy it!

**Note**: Pages shipped with theme as examples have `draft: true` in their frontmatters, use `--buildDrafts` to build them.

## Usage
In case you want do some customize yourself:
- Global settings:
	- `no-style-please/config.yaml`: Include some theme cofig;
	- `no-style-please/layout/assets/css/main.css`: Change color etc. ;
	- - `no-style-please/layout/partials/head.html`: Page head setting;
- Home page:
	- `no-style-please/layout/index.html`: Home page template;
	- `no-style-please/layout/data/menu.yaml`: Menu entries config;
	- `no-style-please/layout/partials/post_list.html`: Some rules for menu entries;
	- `no-style-please/layout/partials/menu_item.html`: List display for menu entries;
	- `no-style-please/layout/_default/baseof.html`: Common template;
- Post page:
	- `no-style-please/layout/posts/singe.html`: Higher priority;
	- `no-style-please/layout/_default/singe.html`: Lower priority;
	- `no-style-please/layout/posts/baseof.html`: Common template for post;
	- `no-style-please/layout/partials/post_meta.html`: Post meta;
- Post list Page:
	- `no-style-please/layout/posts/list.html`: Higher priority;
	- `no-style-please/layout/_default/list.html`: Lower priority;
	- `no-style-please/layout/posts/baseof.html`: Common template for list;
- Tags collection page:
	- `no-style-please/layout/_default/taxonomy.html`;
- Single tag  post page:
	- `no-style-please/layout/_default/term.html`;
- Miscellaneous:
	- `no-style-please/layout/404.html`: Missing page template;
	- `no-style-please/page/about.html`: About page template;
	- `no-style-please/partials/back_link.html`: Back link;
	- `no-style-please/partials/divider.html`: Divider;
	- `no-style-please/partials/footer.html`: Footer;
	- `no-style-please/shortcodes/details.html`: Fold text;
- Math:
	- `no-style-please/partials/mathjax.html`;
	- `no-style-please/shortcodes/texd.html`;
	- `no-style-please/shortcodes/texi.html`;

Find more detail below.

### Customize the menu
In order to add/edit/delete entries from the main menu, you have to edit the `menu.yaml` file inside `data` folder. Through that file you can define the structure of the menu. Take a look at the default configuration to get an idea of how it works and read on for a more comprehensive explanation.

The `menu.yaml` file accepts the following fields:

- `entries` define a new unordered list that will contain menu entries
- each entry is a member of the YAML array `entries` in question
- each entry can have the following attributes:
    - `title`, which defines the text to render for this menu entry (**NB: you can also specify HTML!**)
    - `url`, which can be used to specify an URL for this entry. If not specified, `title` will be rendered as-is; otherwise `title` will be sorrounded by a link tag pointing to the specified URL. Note that the URL can either be relative or absolute. Also note that you can get the same result by placing an ```<a>``` tag in the `title` field.
    - `post_list`, which can be set either to `true` or to an object. If it is true, the entry will have a list of all posts as subentries. This is used to render your post list. If you want to customize which posts to render (e.g. by section), you can add one or more of the following attributes under `post_list`:
        - `section`, which can be set to a string. It is used to render a list of posts of the specified section only. If you don't set it, then posts of all sections will be rendered.
        - `limit`, which can be set to a number. It specifies the number of posts to show. If not set, all posts will be rendered.
        - `show_more`, which can be true. If it is true and if the number of posts to show is greater than the specified `limit`, render a link to another page. To specify the URL and the text of the link, you can set `show_more_url` and `show_more_text` attributes, which are documented below.
        - `show_more_url`, which can be a string. It specifies the URL for the show more link. Use only if `show_more` is true. This will usually redirect to a page containing all posts, which you can easily create using an section page (see [section pages](#section-pages) section)
        - `show_more_text`, which can be a string. It specifies the text for the show more link. Use only if `show_more` is true.
    - `entries`, yes, you can have entries inside entries. In this way you can create nested sublists!

### Section pages
A so-called section page is a page that shows a list of posts in a specific section. It should be automatically created by hugo when a new section is created.

### Adding table of contents
You can add a table of contents by supplying the `toc: true` param to your post front matter. If you want a border around it you can also set `tocBorder: true`. The toc style behavior is handled by Goldmark and the defaults can be found in the `config.yaml` file.

### Pro tips
#### Dark mode for images
This theme provides dark mode by inverting all colors of light mode throught the CSS `invert()` function. This approach would also invert the color of all images, but, since this is not the behaviour one would expect, images are not inverted by default.

However, if you would like to force the color inversion on a specific image you can do so by applying `class="ioda"` to that image ("ioda" stands for "invert on dark appearance"). See the image in the [overview post](https://github.com/riggraz/no-style-please/blob/master/_posts/2020-07-07-overview-post.md) for an example of this approach. Note that color inversion will take place only when the theme has dark appearance!

For example, if you have a black and white image it could make sense to invert it in dark mode. On the other hand, a colorful image will probably look bad if inverted.

## Bug report
I’m a newbie in coding, and every change is helped by AI tools (thanks to the tech!). Of course, there are some bugs I haven’t found, so feel free to report any bugs.

## License
The theme is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
