---
layout: post
title:  "How to create a web site on Github with Jekyll (2)"
date:   2020-12-11 07:35:12 +0900
categories: jekyll tutorial
---

## Overview

This is a part of series:

* [How to create a web site on Github with Jekyll (1)](2020-12-10-how-to-create-a-web-site-on-github-with-jekyll-1.md)
* How to create a web site on Github with Jekyll (2)
* [How to create a web site on Github with Jekyll (3)](2020-12-12-how-to-create-a-web-site-on-github-with-jekyll-3.md)

## The Default `_config.yml` 

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

See how the above configuration is rendered below.

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/github_io-jekyll-your_asesome_title.png)

![](/assets/images/jekyll-about_rendered-default_sample.png)

## The New `_config.yml` 

```yaml
title: AI ML DL
email: aimldl@naver.com
description: >- # this means to ignore newlines until "baseurl:"
  Adorable & Immature Midget Lagomorph's Dream Land
    where
  Artificial Intelligence, Machine Learning & Deep Learning are discussed by Tae-Hyung "T" Kim, Ph.D.
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

```

## Changes made in `_config.yml`

![](/assets/images/how-to-create-a-web-site-on-github-with-jekyll/jekyll-about_rendered-new_config_yml.png)



## Next

* [How to create a web site on Github with Jekyll (3)](2020-12-12-how-to-create-a-web-site-on-github-with-jekyll-3.md)