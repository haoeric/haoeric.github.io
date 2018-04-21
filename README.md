
## Blog Build Information

- This website is built using [jekyll](https://jekyllrb.com), hosted by [GitHub Pages](https://pages.github.com) and modified from [Poole](https://github.com/poole/poole)

- Then Rmarkdown is supported thanks to [Publishing R Markdown using Jekyll](https://chepec.se/2014/07/16/knitr-jekyll.html) 

- There is a quick a way to start: [Jekyll-Bootstrap](http://jekyllbootstrap.com) -- a full blog scaffold for Jekyll based blogs. Follow this [quick start guide](http://jekyllbootstrap.com/usage/jekyll-quick-start.html) to host your blog on github in 3 minutes.


## Jekyll installation on mac

Since OS X ships with a copy of `Ruby` in `/Library/Ruby`, a directory which is owned and controlled by the OS. If we install `jelyll` using system `gem`, we will have permission issues which will be quite annoying for development. So better to install own version of `Ruby` using `homebrew`, then export the path to use this as default. Refer to document [here](https://jekyllrb.com/docs/troubleshooting/#jekyll--mac-os-x-1011) 
    
## File Structure

- `_cache` -- store all caches from knitr the rmarkdown files in `_knitr` (ignored by gitignore, only kept locally).
- `_knitr` -- stores all rmarkdown files and the `render_post.R` scrip.
- `figures` -- All figures generated from knitr will be saved here and used by post in Data Analysis category.
- `images` -- Images stored for blog markdown file except for Data Analysis category


## Configuration

- add formula support: add file `mathJax_support.html` under `_include`[^1], and modify the `styles.scss` file[^2]. Now can use [LaTeX](https://en.wikibooks.org/wiki/LaTeX/Mathematics) syntax to write formulas.
  [^1]: http://www.cnblogs.com/mo-wang/p/5117819.html
  [^2]: http://galaxysd.us/blog/20120723/latex-in-jekyll
  
- add code highlight: add file `_sass/_syntax.scss` with contents copied from[^3], modify the fonts in `_sass/_code.scss` with `font-family:  "Courier New", "Courier New", "Courier New", "Courier New";`. In `_config.yml` file, add `syntax_highlighter: rouge` following[^4].
  [^3]: https://gist.github.com/demisx/8408522
  [^4]: https://sacha.me/articles/jekyll-rouge/
  
  



