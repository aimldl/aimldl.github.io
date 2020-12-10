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

## Summary: [How to create a web site on Github with Jekyll (1)](2020-12-10-how-to-create-a-web-site-on-github-with-jekyll-1.md)  

The previous post [How to create a web site on Github with Jekyll (1)](2020-12-10-how-to-create-a-web-site-on-github-with-jekyll-1.md) talks about:

* a quick introduction on creating a website on Github with Jekyll

* installing the requires packages to use a local web server

  * `$ bundle exec jekyll server ` in the terminal
  * http://localhost:4000 in a web browser

* creating a simple page by

  * creating a file, say `contact.md`, under the project root directory where `index.html` exists

  * starting off with YAML front matter

    ```text
    layout: page
    title: Contact
    permalink: /contact/
    ```
    
* followed by text in the markdown format
  
* creating a simple post

  * creating a file, say `YEAR-MONTH-DAY-title.MARKUP` under sub-directory `_posts`
  * starting off with YAML front matter

  ```text
  ---
  layout: post
  title:  "This is the title"
  ---
  ```

  * followed by text in the markdown format

* adding an image to a page or post by

  * creating a directory `assets` to store the image files

  ```bash
  assets/
  └── images
      ├── image-1.jpg
            ...
      └── image-n.jpg
  ```

  * referencing the path to an image file like

  ```text
  ![image-title](/assets/images/image-1.jpg)
  ```

  * Caution: `/assets/`, not `assets/`



## Next

* [How to create a web site on Github with Jekyll (3)](2020-12-12-how-to-create-a-web-site-on-github-with-jekyll-3.md)