---
layout: post
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
5. Download the candidate themes one by one and see which one you like the most.
6. Decide the final theme.

#### Step 1. Have a rough idea of how the homepage should look like

This step requires some thoughts and experiences. Consider the purpose and requirements to make the homepage. To move quickly, have a rough idea and narrow down what you like. The vision for the homepage may be changed as you see the existing Jekyll themes in the next couple of steps.

In my case, I wish to use the homepage as 

* a career portfolio,
* a front page to access the contents in my GitHub repositories,
* a tech blog to publish articles in the field of Artificial Intelligence, Machine Learning, and Deep Learning.

#### Step 2. Look at the list of existing Jekyll themes.

The goal of this step is to find favorite themes which fit to the purpose and requirements for the final version of the homepage. Looking at the existing Jekyll themes may affect the vision of the final version, purpose, and requirements. Feel free to get inspired by the cool designs and functionalities in the list. The rough idea on the vision, purpose, and requirements of the homepage may evolve and become more concrete.

Search for `jekyll theme`.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/google_search-jekyll_theme-top_3_results.png)

Go to http://jekyllthemes.org/ and look at the list of themes. 

#### Step 3. Pick several favorite themes.

Looking around the themes takes time. Make sure to click `demo` and look around the demo website.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/jekyll_theme-lagrange.png)

Ask yourself whether you like a theme or not. If you like a theme, add it to the list of your favorite themes. Note no theme fits for all the homepage requirements. My favorite themes in all 23 pages are narrowed down to:

https://business-jekyll-theme.github.io/

https://lenpaul.github.io/Lagrange/

https://volny.github.io/stylish-portfolio-jekyll/

https://binai.in/clean/

#### Step 4. Select the candidate themes to test out for the homepage.











![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/ubuntu_20_04-files-home_github_aimldl_github_io-files_at_the_beginning.png)

## Next

* [How to create a web site on Github with Jekyll (3)](2020-12-12-how-to-create-a-web-site-on-github-with-jekyll-3.md)