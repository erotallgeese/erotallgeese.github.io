---
layout: post
title:  "Jekyll servey - part 1"
date:   2017-08-18
categories: jekyll servey
---

# History
Someday i found an blog of my frined is locatled at github. So, i make some search and a try on it.
The blog on github is build using Jekyll called `github page`.

The main difference is that the page is called static page without database. As i known, if someone want write an blog, he need find some web servic and database service (i.e. Azure or AWS ..etc). I think it's an main feature for this solution.

[Here](https://help.github.com/categories/customizing-github-pages/) is the official reference about the history of Jekyll and some troubleshooting.


# Installation
Here is just my walk through to install and setup.

My dev environment is Windows, so i choose to use docker.
```docker
    docker pull jekyll/jekyll
    docker run -p 4000:4000 -v /c/Users/erotallgeese/Documents/docker_jekyll/:/srv/jekyll -it jekyll/jekyll /bin/bash
```

Then it could enter the container. The above commands would run jekyll docker container and bind the port and local folder to that path. After enter the container, there could create an new jekyll project using jekyll commands.
The following is the commands which would be used frequently
```jekyll
    jekyll build
```
This command would check gemfile and download needed gems and then build your project.

```jekyll
    jekyll serve
```
This command would start the server at default port 4000 locally. If it work normally, there could see your blog at your at browser.

# Customization
Github page has mentioned that it could change the theme using `Jekyll Theme Chooser` for your blog site. It's very cool feature i thought. After i create an new empty site and push to github, i use their theme chooser but i get an empty page...

I make some try and search, the reason why i get an empty page after i change the theme:
* no layout for the page.
That is, after changing the theme from "minima" to "jekyll-theme-midnight", it's still need to check and change the layout setting in the [`Front Matter`](https://jekyllrb.com/docs/frontmatter/) of each md.

That new created project's layout setting in `index.md` is "home", but the theme, "jekyll-theme-midnight" doesnot contain this layout. And this is the reason why i got an empty page.

After i change the layout to "default", i finally see the page in dark theme but it doesnot show the post list...
And then i realized that i must misunderstand some things. After some seach, here is the my little conclusions:
* For the theme, `"jekyll-theme-midnight"`, there should check its [git](https://github.com/pages-themes/midnight) for its [layout](https://github.com/pages-themes/midnight/blob/master/_layouts/default.html).
    * It only contain an base layout, "default"
    * I need overwrite this layout or create my layout for my page. (i.e. if i want show post lists in my index page, i need create the layout and using its style)
    * There is need to add the theme to the gemfile to show the page locally.
* For the theme, `"minima"`, there should check its [git](https://github.com/jekyll/minima)
    * This theme seems more flexiblie than jekyll-theme that it could be able to customize the header or footer partially.
    * Well defined layouts for home, page and post. It's more friendly for beginner to study.

# Remark
This is my first post. There should be some introduction for `Front Matter` and `Liquid` to customize the page at part 2. (If existed..)