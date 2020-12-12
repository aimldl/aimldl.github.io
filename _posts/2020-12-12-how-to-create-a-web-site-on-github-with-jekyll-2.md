---
layout: front
title:  "How to create a web site on Github with Jekyll-2"
date:   2020-12-12 22:35:12 +0900
categories: jekyll tutorial
---

## Overview

This is a part of series:

* [How to create a web site on Github with Jekyll (1)](2020-12-10-how-to-create-a-web-site-on-github-with-jekyll-1.md)
  * The goal is to create a working homepage as quickly as possible.
  * The default theme  `minima` is used.
* How to create a web site on Github with Jekyll (2)
  * The goal of (2) is to customize the simplest working homepage.
  * Theme  `minima` is used, but configured to my flavor.
* [How to create a web site on Github with Jekyll (3)](2020-12-12-how-to-create-a-web-site-on-github-with-jekyll-3.md)

## Summary



## How to change the configuration of the homepage 

### The default configuration

`_config.yml` consists of the core part and comments. I found the comments look different when I switched from a machine with Ubuntu 18.04 to one with Ubuntu 20.04. However the core part remains more or like the same.

| Variables        | Default                                                      |
| ---------------- | ------------------------------------------------------------ |
| title            | Your awesome title                                           |
| email            | your-email@example.com                                       |
| description      | Write an awesome description for your new site here. You can edit this   line in _config.yml. It will appear in your document head meta (for   Google search results) and in your feed.xml site description. |
| baseurl          | ""                                                           |
| url              | ""                                                           |
| twitter_username | jekyllrb                                                     |
| github_username  | jekyll                                                       |
| markdown         | kramdown                                                     |
| theme            | minima                                                       |
| plugins          | - jekyll-feed                                                |

#### The default `_config.yml`

```yaml
# Welcome to Jekyll!
#
# This config file is meant for settings that affect your whole blog, values
# which you are expected to set up once and rarely edit after that. If you find
# yourself editing this file very often, consider using Jekyll's data files
# feature for the data you need to update frequently.
#
# For technical reasons, this file is *NOT* reloaded automatically when you use
# 'bundle exec jekyll serve'. If you change this file, please restart the server process.

# Site settings
# These are used to personalize your new site. If you look in the HTML files,
# you will see them accessed via {{ site.title }}, {{ site.email }}, and so on.
# You can create any custom variable you would like, and they will be accessible
# in the templates via {{ site.myvariable }}.
title: Your awesome title
email: your-email@example.com
description: >- # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com
twitter_username: jekyllrb
github_username:  jekyll

# Build settings
markdown: kramdown
theme: minima
plugins:
  - jekyll-feed

# Exclude from processing.
# The following items will not be processed, by default. Create a custom list
# to override the default setting.
# exclude:
#   - Gemfile
#   - Gemfile.lock
#   - node_modules
#   - vendor/bundle/
#   - vendor/cache/
#   - vendor/gems/
#   - vendor/ruby/
```

#### Rendered pages with the default configuration

See how the above configuration is rendered with the `minima` theme.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/github_io-jekyll-your_asesome_title.png)



![](/assets/images/jekyll-about_rendered-default_sample.png)

### The new `_config.yml`

The default `_config.yml` is edited with a text editor and several changes are made. 

#### Default Configuration vs. Changes

| Variables                  | Default                                                      | Changes                                                      |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| title                      | Your awesome title                                           | AI ML DL                                                     |
| email                      | your-email@example.com                                       | aimldl@naver.com                                             |
| description                | Write an awesome description for your new site here. You can edit this   line in _config.yml. It will appear in your document head meta (for   Google search results) and in your feed.xml site description. | Adorable Immature Midget Lagomorph's Dream Land     where T Kim writes tech blog posts in the field of   Artificial Intelligence, Machine Learning, Deep Learning.   Copyright© 2020 All Rights Reserved |
| baseurl                    | ""                                                           | ""                                                           |
| url                        | ""                                                           | https://aimldl.github.io                                     |
| twitter_username           | jekyllrb                                                     | **(This variable is deleted)**                               |
| github_username            | jekyll                                                       | aimldl                                                       |
| markdown                   | kramdown                                                     |                                                              |
| theme                      | minima                                                       |                                                              |
| plugins                    | - jekyll-feed                                                |                                                              |
| **(Added to the changes)** |                                                              |                                                              |
| linkedin_username          |                                                              | mrtonnet                                                     |
| facebook_username          |                                                              | taehyungtkim                                                 |
| instagram_username         |                                                              | mrtonsurf                                                    |
| dockerhub_username         |                                                              | aimldl                                                       |
| languages                  |                                                              | ['en', 'ko']                                                 |
| default_lang               |                                                              | 'en'                                                         |
| exclude_from_localization  |                                                              | ['javascript', 'images', 'css']                              |
| parallel_localization      |                                                              | false                                                        |

#### The new `_config.yml`

```yaml
# Welcome to Jekyll!
#
# This config file is meant for settings that affect your whole blog, values
# which you are expected to set up once and rarely edit after that. If you find
# yourself editing this file very often, consider using Jekyll's data files
# feature for the data you need to update frequently.
#
# For technical reasons, this file is *NOT* reloaded automatically when you use
# 'bundle exec jekyll serve'. If you change this file, please restart the server process.

# Site settings
# These are used to personalize your new site. If you look in the HTML files,
# you will see them accessed via {{ site.title }}, {{ site.email }}, and so on.
# You can create any custom variable you would like, and they will be accessible
# in the templates via {{ site.myvariable }}.
title: AI ML DL
email: aimldl@naver.com
description: >- # this means to ignore newlines until "baseurl:"
  Adorable Immature Midget Lagomorph's Dream Land
    where T Kim writes tech blog posts in the field of
  Artificial Intelligence, Machine Learning, Deep Learning.
  Copyright© 2020 All Rights Reserved
baseurl: "" # the subpath of your site, e.g. /blog
url: https://aimldl.github.io # the base hostname & protocol for your site, e.g. http://example.com
github_username:  aimldl
linkedin_username:  mrtonnet
facebook_username:  taehyungtkim
instagram_username: mrtonsurf
dockerhub_username: aimldl

# Build settings
markdown: kramdown
theme: minima
plugins:
  - jekyll-feed

# multilang
# https://dev-yakuza.posstree.com/en/jekyll/configuration/
languages: ['en', 'ko']
default_lang: 'en'
exclude_from_localization: ['javascript', 'images', 'css']
parallel_localization: false

# Exclude from processing.
# The following items will not be processed, by default. Create a custom list
# to override the default setting.
# exclude:
#   - Gemfile
#   - Gemfile.lock
#   - node_modules
#   - vendor/bundle/
#   - vendor/cache/
#   - vendor/gems/
#   - vendor/ruby/

```

#### Changes made in `_config.yml`

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/jekyll-about_rendered-new_config_yml.png)



## How to change the default theme `minima`

The most efficient way to make the homepage pretty is to use the existing theme and customize it if necessary. There are many ways to change the default theme `minima` to something else. Here are the steps I took:

1. Have a rough idea of how the homepage should look like.
2. Look at the list of existing Jekyll themes.
3. Pick several favorite themes.
4. Select the candidate themes to test out for the homepage.
5. Download a candidate theme.
6. Back up `_config.yml` to other directory.
7. Copy the files into the directory where the files for the homepage repository exist.
8. Set up and run the local web server.
9. 
10. Decide the final theme.

#### Step 1. Have a rough idea of how the homepage should look like

To move quickly, have a rough idea about the homepage and narrow down what you like as you move forward. The vision for the homepage may be changed as you see more existing Jekyll themes in the next couple of steps.

#### Step 2. Look at the list of existing Jekyll themes.

The goal of this step is to find favorite themes. Feel free to get inspired by the cool designs and functionalities in the [list](http://jekyllthemes.org/). The rough idea on the vision, purpose, and requirements of the homepage may evolve and become more concrete.

Search for `jekyll theme`.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/google_search-jekyll_theme-top_3_results.png)

Go to http://jekyllthemes.org/ and look at the list of themes. 

#### Step 3. Pick several favorite themes.

Looking around the themes takes time. Make sure to click `demo` and look at the demo website.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/jekyll_theme-lagrange.png)

Ask yourself whether you like a theme or not. If you like a theme, add it to the list of your favorites. Note no theme fits for all the homepage requirements. There are many themes in 23 pages. My favorite themes are narrowed down to six themes. 

The demo pages of the six favorite themes are:

* https://business-jekyll-theme.github.io/
* https://alainpham.github.io/
* https://hydrogen.atlinker.cn/
* https://lenpaul.github.io/Lagrange/
* https://volny.github.io/stylish-portfolio-jekyll/
* https://binai.in/clean/

#### Step 4. Select the candidate themes to test out for the homepage.

The goal of this step is to find candidate themes which fit to the purpose and requirements of the homepage. Looking at the existing Jekyll themes might have affected the rough initial vision of the homepage. It is time to consider the purpose and requirements of the homepage. 

In my case, I decided to create a homepage for  

* a career portfolio,
* a tech blog to publish articles in the field of Artificial Intelligence, Machine Learning, and Deep Learning.

However it will be convenient if I can use the homepage as:

* a front page to organize the contents in my GitHub repositories,
* a single point of reference, e.g. "Go to my homepage to see blah-blah-blah." or "The tutorial is at http://my.homepage/this_is_the_tutorial. "

I like these more than the rest among the favorite themes.

1. https://volny.github.io/stylish-portfolio-jekyll/
2. https://business-jekyll-theme.github.io/

I didn't like the following themes as much as two finalists.

https://binai.in/clean/

I liked this design the most, but the mobile version of the homepage gets corrupted on my iPhone 7 plus. `stylish-portfolio-jekyll` works perfectly both on a PC and a mobile phone. So I dropped this theme.

https://alainpham.github.io/ and https://hydrogen.atlinker.cn/

These themes were not my first choice. The homepage does not look as clean as either `clean` or `stylish-portfolio-jekyll` themes. But the `TAGS` page seems convenient.

https://lenpaul.github.io/Lagrange/

I didn't like the design after looking at `clean` and `stylish-portfolio-jekyll` themes.

##### Step 5. Download a candidate theme.

##### Skylish Portfolio

Go to http://jekyllthemes.org/themes/stylish-portfolio/

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/jekyllthemes_org-stylish_portfolio-homepage.png)

Click the `Download` button and `stylish-portfolio-jekyll-master.zip` will be downloaded to your `Download` folder for the web browser.

Uncompress the downloaded file and a directory `stylish-portfolio-jekyll-master` will be created. 

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/ubuntu_20_04-files-home-download-with_stylish_portfolio.png)

The directory `stylish-portfolio-jekyll-master` contains the following files.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/ubuntu_20_04-files-home-download-stylish-portfolio-jekyll-master.png)

##### Step 6. Back up `_config.yml` to other directory.

##### Step 7. Copy the files into the directory where the files for the homepage repository exist.

In my case, the files for the homepage are stored under `~/github/aimldl.github.io`. Copy the files for the new theme to the homepage directory. When you are asked to overwrite `_config.yml`, DO NOT replace the existing `_config.yml`.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/ubuntu_20_04-files-home_github_aimldl_github_io-files_at_the_beginning.png)

##### Step 8. Set up and run the local web server 

In the homepage directory, e.g.  `~/github/aimldl.github.io`, starting the local web server with the `bundle exec jekyll server` will fail because 'The minima theme coult not be found.`

Set up to run the local web server.

```bash
$ rm Gemfile
$ bundle init
Writing new Gemfile to /home/aimldl/github/aimldl.github.io/Gemfile
$ bundle add jekyll
Fetching gem metadata from https://rubygems.org/..........
  ...
Using jekyll 3.8.7
$ bundle exec jekyll serve
  ...
jekyll 3.8.6 | Error:  The minima theme could not be found.
  ...
/usr/lib/ruby/vendor_ruby/jekyll/theme.rb:84:in `rescue in gemspec': The minima theme could not be found. (Jekyll::Errors::MissingDependencyException)
$
```

`_config.yml` for Stylish Portfolio is below.

```yaml
# Site settings
title:
email:
description: > # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
baseurl: "" # the subpath of your site, e.g. /blog/
url: "" # the base hostname & protocol for your site

# User setting
owner:
email:
facebook_username:
twitter_username:
github_username:
address:
  - line:
  - line:
  # Feel free to add more lines here 
telephone:
copyright:

# API settings
google_api_key:

# Build settings
markdown: kramdown
```

Reference the above YAML file and change the existing `_config.yml` like below.

```yaml
title: AI ML DL
email: aimldl@naver.com
description: >- # this means to ignore newlines until "baseurl:"
  Adorable Immature Midget Lagomorph's Dream Land
    where T Kim writes tech blog posts in the field of
  Artificial Intelligence, Machine Learning, Deep Learning.
  Copyright© 2020 All Rights Reserved
baseurl: "" # the subpath of your site, e.g. /blog
url: https://aimldl.github.io # the base hostname & protocol for your site, e.g. http://example.com
github_username:  aimldl
linkedin_username:  mrtonnet
facebook_username:  taehyungtkim
instagram_username: mrtonsurf
dockerhub_username: aimldl

# User setting
owner:
email:
facebook_username:
twitter_username:
github_username:
address:
  - line:
  - line:
  # Feel free to add more lines here 
telephone:
copyright:

# API settings
google_api_key:

# Build settings
markdown: kramdown
plugins:
  - jekyll-feed

# multilang
# https://dev-yakuza.posstree.com/en/jekyll/configuration/
languages: ['en', 'ko']
default_lang: 'en'
exclude_from_localization: ['javascript', 'images', 'css']
parallel_localization: false
```

Now run the local web server

```bash
$ bundle exec jekyll serve
```

and go to `http://localhost:4000` in a web browser.

Nothing shows up as follows.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/jekyll_theme-stylish_portfolio-index_md-layout_home.png)

Back to the terminal, notice the warnings. Layouts for `post`, `default`, `home`, `page` do not exist.

```bash
$ bundle exec jekyll serve
  ...
     Build Warning: Layout 'post' requested in _posts/2020-12-09-welcome-to-jekyll.markdown does not exist.
     Build Warning: Layout 'post' requested in _posts/2020-12-10-this-is-the-title.md does not exist.
     Build Warning: Layout 'post' requested in _posts/2020-12-11-appendix_b-how-to-create-a-web-site-on-github-with-jekyll.md does not exist.
     Build Warning: Layout 'post' requested in _posts/2020-12-11-appendix_a-how-to-create-a-web-site-on-github-with-jekyll.md does not exist.
     Build Warning: Layout 'post' requested in _posts/2020-12-11-how-to-create-a-web-site-on-github-with-jekyll-1.md does not exist.
     Build Warning: Layout 'default' requested in 404.html does not exist.
     Build Warning: Layout 'page' requested in about.md does not exist.
     Build Warning: Layout 'page' requested in contact.md does not exist.
     Build Warning: Layout 'home' requested in index.md does not exist.
     Build Warning: Layout 'page' requested in inspirations.md does not exist.
     Build Warning: Layout 'page' requested in todo.md does not exist.
                    done in 0.228 seconds.
/home/aimldl/.ruby/gems/pathutil-0.16.2/lib/pathutil.rb:502: warning: Using the last argument as keyword parameters is deprecated
 Auto-regeneration: enabled for '/home/aimldl/github/aimldl.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

Open `index.md`. The YAML front matter specifies the layout as `home`.

```text
---
layout: home
---
```

Check the sub-directory `_layouts`. Only `front.html` exists!

```bash
$ tree _layouts/
_layouts/
└── front.html

0 directories, 1 file
$
```

Change the layout to `front`

```text
---
layout: front
---
```

and refresh the web browser at `http://localhost:4000`.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/jekyll_theme-stylish_portfolio-index_md-layout_front.png)

It looks like this theme does not use markdown files and the only used layout is `front`. It will be easier to write a post in the markdown format. So I will have to skip this theme. Now let's try the next candidate theme.

##### Business

http://jekyllthemes.org/themes/business-jekyll-theme/

Click the `download` button and `business-jekyll-theme-master.zip` is downloaded. 

Uncompress the downloaded file and copy the files to the homepage directory.

```bash
$ bundle exec jekyll serve
Traceback (most recent call last):
	2: from /usr/bin/bundle:23:in `<main>'
	1: from /usr/lib/ruby/2.7.0/rubygems.rb:294:in `activate_bin_path'
/usr/lib/ruby/2.7.0/rubygems.rb:275:in `find_spec_for_exe': Could not find 'bundler' (1.16.0) required by your /home/aimldl/github/aimldl.github.io/Gemfile.lock. (Gem::GemNotFoundException)
To update to the latest version installed on your system, run `bundle update --bundler`.
To install the missing version, run `gem install bundler:1.16.0`
$
```

The local web server fails to start. Instead of `bundle init` followed by `bundle add jekyll`, run `bundle update --bundler`. 

```
$ bundle update --bundler
Fetching gem metadata from https://rubygems.org/..........
  ...
Installing minima 2.4.0
Warning: the lockfile is being updated to Bundler 2, after which you will be unable to return to Bundler 1.
Bundle updated!
$
```

Running `jekyll serve` does not work properly.

```bash
$ bundle exec jekyll serve
Traceback (most recent call last):
  ...
/usr/lib/ruby/vendor_ruby/jekyll/filters.rb:9:in `<module:Filters>': uninitialized constant Jekyll::Filters::DateFilters (NameError)
Did you mean?  DateTime
$
```

I've fixed error after error, but I still got a new error after fixing a couple errors.

`Dependency Error: Yikes! It looks like you don't have kramdown-parser-gfm or one of its dependencies installed.`

  ...

`/usr/lib/ruby/vendor_ruby/kramdown/parser/html.rb:113:inparse_html_attributes': uninitialized constant Kramdown::Utils::OrderedHash (NameError)`

Probably, I can fix the errors and have the theme work if I put enough time. But I will stop here and move onto another theme.





![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/



Step 6. Decide the final theme.

see which one you like the most.

## Next

* [How to create a web site on Github with Jekyll (3)](2020-12-12-how-to-create-a-web-site-on-github-with-jekyll-3.md)