---
layout: post
title:  "Create a Site with Jekyll and GitHub Pages"
subtitle: "So you can have an amazing, super awesome site like this one."
date:   2017-04-04 15:36:48 -0400
author: "Matt Flowers"
header-img: "assets/img/post-bg-02.jpg"
---

[Jekyll](https://jekyllrb.com/) is an awesome tool that is written in Ruby and used to generate 
static sites and blogs.
It is especially awesome when used alongside [GitHub Pages](https://pages.github.com/). This is because GitHub Pages is a way of
hosting static sites and pages offered by GitHub. Since Jekyll generates static sites based on provided
layouts, includes, and configurations, you are able to create and deploy a large static site with very
little effort. Jekyll is what I used to create this site and blog that you are reading now. Getting
started with Jekyll might be difficult or confusing, so I will be going over how to get a blog up and
running. Jekyll has very good documentation, so if you would rather view that, it is right [here](https://jekyllrb.com/docs/home/).

## Setup

The only real requirement for this setup is to be running Linux or macOS. We will also be needing GCC and make, but those usually come installed on Linux and Mac systems. The other requirements are Ruby and RubyGems, but we will take care of both of those using RVM

### Installing RVM

RVM stands for Ruby Version Manager. It allows you to install and switch between different versions of ruby.

You first need to install the public key:

```
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
```

Then you can run this command to download and run RVM's installation script:

```
\curl -sSL https://get.rvm.io | bash -s stable
```

This will successfully install the latest stable version of RVM. Once the installation is over you need to exit out of your terminal and open it back up again.

### Installing Ruby and Jekyll

Now that RVM is installed, the rest of the process is very easy. In order to install Ruby
type:
```
rvm install 2.4
```

This will install ruby version 2.4, which is the version I used. If you would like to install
a different version, or are following this tutorial a good while after I posted it, you can
view all possible versions with `rvm list known`. Install the version you want using
`rvm install x.x`, or use `rvm install ruby` for the latest version.

After it is done installing, you can set it as your default version by typing:
```
rvm use --default 2.4
```

This will also install RubyGems, so now all you need to do is install Jekyll and Bundler:

```
gem install jekyll bundler
```

## Creating Your Site

Since all of the requirements are met, we can generate our site. This is simply done with:
```
jekyll new site_name
```

Navigate into you site directory and serve it locally:
```
cd site_name
bundle exec jekyll serve
```

You now have a running Jekyll site!

I would take a look at Jekyll's documentation to get an idea of how to format blog posts and how the directory
structure works. If you want to remove the preinstalled theme so you can start entirely from scratch and create
your own look, just remove the `theme: minima` line from your `_config.yml`, as well as the `gem "minima"` line
in your `Gemfile`.

## Publishing to GitHub

When your site is ready to be published, initialize a git repository in the project directory:

```
git init
git add .
git commit -m "Initial commit"
```

Now create an empty, public GitHub repository and name it __*username*.github.io__ where __*username*__ is your
GitHub username. My project was named __*mattflow*.github.io__.

Now go back to your project and add the repository as a remote and push:

```
git remote add origin git@github.com:username/username.github.io.git
git remote push -u origin master
```

Congratulations! If there were no build erros, you now have your Jekyll site running live on your GitHub
Pages site. Head over to __https://*username*.github.io__ to check it out.