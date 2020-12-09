* Draft: 2020-05-25 (Mon)
# README (aimldl.github.io)
* This repository is my GitHub page at https://aimldl.github.io/

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

Using [Jekyll](https://jekyllrb.com/), you can blog using beautiful Markdown syntax, and without having to deal with any databases.

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

Before installing `jekyll` and `bundler`, configure `GEM_HOME`. For details, see Appendix A.

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

###### 6. Browse to http://localhost:4000

Open a web browser and go to either:

* http://localhost:4000
* http://127.0.0.1:4000/

Note `localhost` is equivalent to `127.0.0.1`.

<img src='images/github_io-jekyll-your_asesome_title.png'>

Later, I found the following article and present it for future reference.

[Troubleshooting 3 issues when configuring Jekyll on Github Pages](https://medium.com/@khwongk12/troubleshooting-3-issues-when-configuring-jekyll-on-github-pages-5d882585c6f5), medium



## Appendix A. Fixing the errors in `Install the jekyll and bundler`.

### Problem

Running the original command in the instructions results in an error. 

```bash
$ jekyll new myblog
bash: /usr/bin/jekyll: No such file or directory
$
```

Without configuring `GEM_HOME`, the following error occurs. 

```bash
$ gem install jekyll bundler
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /var/lib/gems/2.5.0 directory.
$
```

### Hint

Google search: "ERROR: While executing gem ... (Gem::FilePermissionError) You don't have write permissions for the /var/lib/gems/2.5.0 directory."

### Solution

*  [You don't have write permissions for the /var/lib/gems/2.3.0 directory](https://stackoverflow.com/questions/37720892/you-dont-have-write-permissions-for-the-var-lib-gems-2-3-0-directory)

> If you want to use the distribution Ruby instead of rb-env/rvm, you can set up a `GEM_HOME` for your current user. Start by creating a directory to store the Ruby gems for *your* user:
>
> ```
> $ mkdir ~/.ruby
> ```
>
> Then update your shell to use that directory for `GEM_HOME` and to update your `PATH` variable to include the Ruby gem bin directory.
>
> ```
> $ echo 'export GEM_HOME=~/.ruby/' >> ~/.bashrc
> $ echo 'export PATH="$PATH:~/.ruby/bin"' >> ~/.bashrc
> $ source ~/.bashrc
> ```
>
> (That last line will reload the environment variables in your current shell.)
>
> Now you should be able to install Ruby gems under your user using the `gem` command. I was able to get this working with Ruby 2.5.1 under Ubuntu 18.04. If you are using a shell that is not Bash, then you will need to edit the startup script for that shell instead of `bashrc`.



## Appendix B. Fixing the errors in the `bundle exec jekyll serve` command

### Problem

The command in the instructions fails.

```bash
$ bundle exec jekyll serve
Could not locate Gemfile or .bundle/ directory
$
```

### Hint

Google search: bundle exec jekyll serve Could not locate Gemfile or .bundle/ directory

### Solution

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

