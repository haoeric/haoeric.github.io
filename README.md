
## Blog Build Information

- This website is built using [jekyll](https://jekyllrb.com), hosted by [GitHub Pages](https://pages.github.com) and modified from [Poole](https://github.com/poole/poole)

- Then Rmarkdown is supported thanks to [Publishing R Markdown using Jekyll](https://chepec.se/2014/07/16/knitr-jekyll.html) 

- There is a quick a way to start: [Jekyll-Bootstrap](http://jekyllbootstrap.com) -- a full blog scaffold for Jekyll based blogs. Follow this [quick start guide](http://jekyllbootstrap.com/usage/jekyll-quick-start.html) to host your blog on github in 3 minutes.


## File Structure

- `_cache` -- store all caches from knitr the rmarkdown files in `_knitr` (ignored by gitignore, only kept locally).
- `_knitr` -- stores all rmarkdown files and the `render_post.R` scrip.
- `figures` -- All figures generated from knitr will be saved here and used by post in Data Analysis category.
- `images` -- Images stored for blog markdown file except for Data Analysis category


## Configuration

- add formula support: add file `mathJax_support.html` under `_include`[^1], and modify the `styles.scss` file[^2].
  
- add code highlight: add file `_sass/_syntax.scss` with contents copied from[^3], modify the background color to `#04213a`, modify the fonts in `_sass/_code.scss` with `font-family:  "Courier New", "Courier New", "Courier New", "Courier New";`. In `_config.yml` file, add `syntax_highlighter: rouge` following[^4].


[^1]: [用Markdown写blog的常用操作](http://www.cnblogs.com/mo-wang/p/5117819.html)  
[^2]: [让Jekyll支持Latex](http://galaxysd.us/blog/20120723/latex-in-jekyll)  
[^3]: https://github.com/vgaidarji/vgaidarji.github.io/blob/master/css/theme-son-of-obsidian.css  
[^4]: https://sacha.me/articles/jekyll-rouge/  
    


