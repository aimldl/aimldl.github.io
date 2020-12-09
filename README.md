* Rev.1: 2020-12-09 (Wed)
* Draft: 2020-05-25 (Mon)
# README https://aimldl.github.io/
## Websites for you and your projects

* For details, see https://pages.github.com/

Note directory `~/github` has already been created.

```bash
$ cd ~/github
$ git clone https://github.com/aimldl/aimldl.github.io
$ cd aimldl.github.io/
$ echo "Hello World" > index.html
$ git add --all
$ git commit -m "Initial commit"
$ git push
Username for 'https://github.com': aimldl
Password for 'https://aimldl@github.com': 
  ...
$
```

Open a browser and go to https://aimldl.github.io/.

<img src='images/github_io-hello_world.png'>

## [Blogging with Jekyll](https://help.github.com/articles/using-jekyll-with-pages)

Using [Jekyll](https://jekyllrb.com/), you can blog using beautiful Markdown syntax, and without having to deal with any databases. [Showcase](https://jekyllrb.com/showcase/) presents some company websites powered by Jekyll. Some of my favorite samples are below.

<img src='images/jekyll-showcase-my_favorites.png'>

A part of `GETTING STARTED` at https://jekyllrb.com/docs/ is summarized below.

- [Quickstart](https://jekyllrb.com/docs/)
- [Installation](https://jekyllrb.com/docs/installation/)
- [Ruby 101](https://jekyllrb.com/docs/ruby-101/)
- [Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)

### [Ruby 101](https://jekyllrb.com/docs/ruby-101/)

> Jekyll is written in Ruby. If you’re new to Ruby, this page helps you learn some of the terminology.
>
> **Gems** are code you can include in Ruby projects. 
>
>
> A **Gemfile** is a list of gems used by your site. Every Jekyll site has a Gemfile in the main folder.
>
> **Bundler** is a gem that installs all gems in your Gemfile.
>
> For details, see [Ruby 101](https://jekyllrb.com/docs/ruby-101/).
>
> Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed. Bundler is an exit from dependency hell, and ensures that the gems you need are present in development, staging, and production. Starting work on a project is as simple as `bundle install`.
>
> For details, refer to https://bundler.io/.

### [Learn how to set up Jekyll](https://jekyllrb.com/docs/)

#### [Instructions](https://jekyllrb.com/docs/#instructions)

##### 1. Install all [prerequisites](https://jekyllrb.com/docs/installation/) 

Install the prerequisites on the machine where `git clone` has been executed. For example, my machine is a desktop with Ubuntu 18.04.

**Ruby**

```bash
$ sudo apt install -y ruby
```

RubyGems, GCC, and Make are preinstalled with Ubuntu 18.04. To verify, run:

```bash
$ gem -v  
$ gcc -v
$ g++ -v
$ make -v
```

##### 2. Install the jekyll and bundler.

Before installing `jekyll` and `bundler`, configure `GEM_HOME`. For details, see [Appendix A](appendix_a.md).

```bash
# Run these commands first
$ mkdir ~/.ruby
$ echo 'export GEM_HOME=~/.ruby/' >> ~/.bashrc
$ echo 'export PATH="$PATH:~/.ruby/bin"' >> ~/.bashrc
$ source ~/.bashrc
# Command in the instructions is changed
$ sudo apt install -y jekyll bundler
```

Notice the original command `gem install jekyll bundler` has been changed to `sudo apt install -y jekyll bundler`.  

##### 3. Create a new Jekyll site at ./myblog

```bash
$ jekyll new myblog
New jekyll site installed in /home/aimldl/github/aimldl.github.io/myblog.
$
```

##### 4. Change into your new directory.

```bash
$ cd myblog
```

##### 5. Build the site and make it available on a local server.

[Appendix. B](appendix_b.md) explains why the first two commands are added to the original command in the instructions.

```bash
# Initialize bundle and add jekyll first
$ bundle init
$ bundle add jekyll
# And then run the command in the insturctions
$ bundle exec jekyll serve
```

The message is

```bash
  ...
Auto-regeneration: enabled for '/home/aimldl/github/aimldl.github.io/myblog'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

If the following error occurs, run `bundle install` and then run `bundle exec jekyll serve` again.

```bash
$ bundle exec jekyll serve
Could not find public_suffix-4.0.6 in any of the sources
Run `bundle install` to install missing gems.
$ bundle install
  ...
HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
But that may break your application.

If you are upgrading your Rails application from an older version of Rails:

Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.

If you are starting a NEW Rails application, you can ignore this notice.

For more info see:
https://github.com/svenfuchs/i18n/releases/tag/v1.1.0
$
```



##### 6. Browse to http://localhost:4000

Open a web browser and go to either:

* http://localhost:4000
* http://127.0.0.1:4000/

Note `localhost` is equivalent to `127.0.0.1`.

<img src='images/github_io-jekyll-your_asesome_title.png'>

Later, I found the following article and present it for future reference.

[Troubleshooting 3 issues when configuring Jekyll on Github Pages](https://medium.com/@khwongk12/troubleshooting-3-issues-when-configuring-jekyll-on-github-pages-5d882585c6f5), medium

## The new website in action!

So far `index.html` is the hello world page.

<img src='images/github_io-hello_world.png'>

I've moved all the files in the `myblog` directory to the parent directory.

```bash
~/github/aimldl.github.io$ ls
Gemfile       _config.yml  _layouts  _sass  about.md  feed.xml    js
Gemfile.lock  _includes    _posts    _site  css       index.html
~/github/aimldl.github.io$
```

In this process, the old hello world `index.html` is removed and the `Your awesome title` page has become the new `index.html`.

<img src='images/github_io-jekyll-your_asesome_title.png'>

And then pushed this repository to github.

```bash
~/github/aimldl.github.io$ git add .
~/github/aimldl.github.io$ git commit -m 'Add jekyll for the first time'
~/github/aimldl.github.io$ git push
```

After waiting  a while, go to the website `aimldl.github.io` and saw the new index page in action!

<img src='images/github_io-your_awesome_title-online.png'>



## Running the local server

All the files in the `myblog` are moved to the parent directory, specifically `~/github/aimldl.github.io`. The server can be executed with the same command as follows.

```bash
~/github/aimldl.github.io$ bundle exec jekyll serve
Configuration file: /home/aimldl/github/aimldl.github.io/_config.yml
            Source: /home/aimldl/github/aimldl.github.io
       Destination: /home/aimldl/github/aimldl.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.149 seconds.
 Auto-regeneration: enabled for '/home/aimldl/github/aimldl.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

<img src='images/github_io-jekyll-your_asesome_title.png'>

## Jekyll

Let's see what the sample website looks like.

### Sample Website

#### https://aimldl.github.io/

<img src='images/jekyll-index_html-default_sample.png'>

#### index.html

```bash
---
layout: default
---
<div class="home">
  <h1 class="page-heading">Posts</h1>
  <ul class="post-list">
    {% for post in site.posts %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
        <h2>
          <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
        </h2>
      </li>
    {% endfor %}
  </ul>
  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>
</div>
```

#### https://aimldl.github.io/about/

<img src='images/jekyll-about_rendered-default_sample.png'>

#### about.md

<img src='images/jekyll-about_md-default_sample.png'>

##### Welcome to Jekyll! https://aimldl.github.io/jekyll/update/2020/12/09/welcome-to-jekyll.html

<img src='images/jekyll-wecome_to_jekyll_rendered-default_sample.png'>

##### _posts/2020-12-09-welcome-to-jekyll.markdown

<img src='images/jekyll-wecome_to_jekyll_markdown-default_sample.png'>

### [Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)

https://jekyllrb.com/docs/step-by-step/01-setup/

1. [Setup](https://jekyllrb.com/docs/step-by-step/01-setup/)
2. [Liquid](https://jekyllrb.com/docs/step-by-step/02-liquid/)
3. [Front Matter](https://jekyllrb.com/docs/step-by-step/03-front-matter/)
4. [Layouts](https://jekyllrb.com/docs/step-by-step/04-layouts/)
5. [Includes](https://jekyllrb.com/docs/step-by-step/05-includes/)
6. [Data Files](https://jekyllrb.com/docs/step-by-step/06-data-files/)
7. [Assets](https://jekyllrb.com/docs/step-by-step/07-assets/)
8. [Blogging](https://jekyllrb.com/docs/step-by-step/08-blogging/)
9. [Collections](https://jekyllrb.com/docs/step-by-step/09-collections/)
10. [Deployment](https://jekyllrb.com/docs/step-by-step/10-deployment/)

