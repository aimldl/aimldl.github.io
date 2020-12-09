Draft: 2020-12-09 (Wed)

# Appendix B. Fixing the errors in the `bundle exec jekyll serve` command

## Problem

The command in the instructions fails.

```bash
$ bundle exec jekyll serve
Could not locate Gemfile or .bundle/ directory
$
```

## Hint

Google search: bundle exec jekyll serve Could not locate Gemfile or .bundle/ directory

## Solution

* [How to run “bundle exec jekyll new .”](https://stackoverflow.com/questions/59913903/how-to-run-bundle-exec-jekyll-new)

> The GitHub walk-through left these commands out, but Bundler's [`bundle init`](https://bundler.io/v2.0/man/bundle-init.1.html) explains it: This command is necessary to create the Gemfile:
>
> ```sh
> $ bundle init
> ```
>
> and this one to populate it with Jekyll:
>
> ```sh
> $ bundle add jekyll
> ```
>
> so that when I re-ran my setup command, it worked:
>
> ```sh
> $ bundle exec jekyll 4.0.0 new . --force
> ```
>
> The specific version of `jekyll` that GitHub uses can be found [here](https://pages.github.com/versions/).

The full messages are below.

```bash
$ bundle init
Writing new Gemfile to /home/aimldl/github/aimldl.github.io/myblog/Gemfile
$ bundle add jekyll
Fetching gem metadata from https://rubygems.org/..........
  ...
Using jekyll 4.1.1
$ bundle exec jekyll serve
Configuration file: /home/aimldl/github/aimldl.github.io/myblog/_config.yml
            Source: /home/aimldl/github/aimldl.github.io/myblog
       Destination: /home/aimldl/github/aimldl.github.io/myblog/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.146 seconds.
 Auto-regeneration: enabled for '/home/aimldl/github/aimldl.github.io/myblog'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

