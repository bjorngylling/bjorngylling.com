+++ 
date = "2011-03-09"
title = "git commit -m 'Awesome blog-post'"
slug = "awesome-blog-post"
tags = ["Github Pages", "Git", "Jekyll", "Pygments", "Liquid", "Ruby"]
categories = []
+++

An introduction to blogging on [Github Pages](http://pages.github.com) with Git and [Jekyll](https://github.com/mojombo/jekyll/). In this post I'm going to describe how Coding (this blog) is set up. Everything is hosted on Github Pages which is completely **free** of charge, the only thing I have to pay for with this setup is the domain-name. Alright, so let's get into how this works and why it's so *great*!
# Jekyll
Github Pages serves only static content. At first it might seem like a bad idea to host a blog on a host which serves only static content. The purpose of a blog is to add content regularly right! To add new posts and link to them from the front-page while using the correct layout and make it easy for the writer to add posts Github Pages uses a Ruby gem called **Jekyll**. What Jekyll does is that it runs in a directory and generates a site with static html-pages. 
## It's a Git-repository!
Below is an example of how the directory structure looks for this blog: 
    bjorngylling.github.com
    |-- .git
    |-- _css
    | |-- images
    |-- js
    |-- _layouts
    | |-- default.html
    | |-- post.html
    |-- _posts
    | |-- 2011-03-05-lorem-ipsum-dolor.markdown
    |-- _config.yml
    |-- CNAME
    |-- index.html
A couple of things to note here; first off we have the `.git` directory. `bjorngylling.github.com` is a Git-repository hosted on my Github account. This is part of what makes Github Pages so brilliant. Making an update to your Github page is as simple as editing the file in your local repo and then pushing the commit to Github. Github Pages will then run Jekyll on your repo and put the result on your Github page.

What else is there? The folders starting with an underscore has special meaning to Jekyll. `_layouts` holds all the Liquid layouts. In my case there's two; `default` which is the overall layout of the site and `post` which is a [partial layout](abbr:which means that it in turn uses the default layout) used to display a specific post.

The `_posts` folder holds all the blog-posts. The filename of each individual post is important here, it should follow the standard `YEAR-MONTH-DATE-title.MARKUP`, this post for example has the filename `2011-03-07-git-commit-m-awesome-blog-post.markdown`. The filename will be used to generate the [permalink](https://github.com/mojombo/jekyll/wiki/Permalinks "more info on defining the permalinks") for the post. The settings for this can be specified in [_config.yml](https://github.com/mojombo/jekyll/wiki/Configuration "more info on configurating Jekyll").

## Defining a layout
Jekyll uses a template engine called [Liquid](https://github.com/tobi/liquid/wiki/Liquid-for-Designers). Not that much to say about Liquid. One thing I had problems with was using the correct variable-names at one point. In my setup I use a main layout [default.html](https://github.com/bjorngylling/bjorngylling.github.com/blob/master/_layouts/default.html) which is the overall layout. When displaying a single post I use a partial layout [post.html](https://github.com/bjorngylling/bjorngylling.github.com/blob/master/_layouts/post.html). In `default.html` I simply use `content` put in `post.html` I wanted to access the variables set up for a post such as date, title and categories. These will be available through the variable `page`. Either it was expressed very unclearly on Jekyll and I missed it or maybe it's not in there at all.

## Code highlighting
For code highlighting Jekyll uses [Pygments](http://pygments.org). The style I'm using is a slightly modified version of the syntax-highlighting found at [Railscasts](http://railscasts.com/episodes/207-syntax-highlighting "#207 - Syntax Highlightning"). It's also the [color scheme](http://railscasts.com/about) I'm using for my current editor, [Sublime Text 2](http://www.sublimetext.com/2).
A test of Ruby highlighting:
{{< highlight ruby >}}
def test_lambda_functions
  code = "foo = { |var| var + 10 }
          foo(22)"
          
  assert_equal 32, parse(code)
end
{{< / highlight >}}

# Writing a post
Posts can be written in either [Markdown](http://daringfireball.net/projects/markdown/), [Textile](http://redcloth.org/textile) or plain old HTML. Jekyll will decide how to treat it depending on the file-extension. As mentioned earlier the format of the filename is quite important, it also makes it a bit of a hassle to make a new post. However there are ways to ease the burden on the [hard](abbr:hardly)-working blogger! 

For this I use a [Rakefile](https://github.com/bjorngylling/bjorngylling.github.com/blob/master/Rakefile) with a task for generating a file (eg `rake post title='Git commit -m "Awesome blog-post"'`). What this does is create a file with the correct name as well as setup the [YAML front matter](https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter) so that I only have to add in the categories relevant for the post. The task also adds the file to the Git repo. The `Rakefile` also includes a task for updating the date for a post with the specified title (eg `rake update title='Git commit -m "Awesome blog-post"'`) which just updates the filename to use the current date.

After the file is created I write the post using Markdown. Because of the Rake-task setting the `published: false` in the YAML front matter that allows me to commit the post without it actually showing up on my Github page. 

# Use your own domain-name
Alright, the blog is up and running and it can be seen at [bjorngylling.github.com](http://bjorngylling.github.com), but I want to use my own domain [bjorngylling.com](http://bjorngylling.com)! This is quite easy to accomplish. Some of you (who am I kidding here, nobody reads this!) might've spotted the file [CNAME](abbr:Canonical NAME) in the root of the repository. This file should contain one line where you specify the domain-name you want to use, for example `bjorngylling.com`.

Next you'll want to set up a redirect from your domain to the Github page. If you want to redirect from a subdomain, say `blog.bjorngylling.com`, a CNAME recording pointing at the Github page is enough. However, in my case I wanted to redirect from a top-level domain in which case a CNAME redirect is a bad idea because it can mess up your for example your email on that domain. What you want to do instead is a A record pointing at the IP `207.97.227.245`.


The full source for this Github Page can be found at [its Github repository](https://github.com/bjorngylling/bjorngylling.github.com).