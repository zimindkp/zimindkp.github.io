---
title: Running Jekyll 4+ on GitHub Pages
author: Kishan Parekh
date: 2021-02-09 20:00:00 -0500
categories: [Blogging, Jekyll]
tags: [jekyll, website]
image: /assets/img/images/octojekyll.png
---

# What is Jekyll?

Jekyll is a simple, blog-aware, static site generator perfect for personal, project, or organization sites. Think of it like a file-based CMS, without all the complexity. Jekyll takes your content, renders Markdown and Liquid templates, and spits out a complete, static website ready to be served by Apache, Nginx or another web server. Jekyll is the engine behind [GitHub Pages](https://pages.github.com/), which you can use to host sites right from your GitHub repositories.

This is a brief summary, and there is a whole lot more information on Jekyll at the official [site.](https://jekyllrb.com/)

## How I Use Jekyll

As stated above, we can use Jekyll to build our static site and deploy it using GitHub Pages. This is great for sites like this that have all the information contained in an HTML file for the page, in contrast to more dynamic websites that pull information from a database ([WordPress](https://wordpress.org/) for example). In essence, Jekyll is the software that generates the static websites without having to query a database. Furthermore, since static sites are really just text files, we can easily version a static site.

I followed the same method as described in the [guide](https://jekyllrb.com/docs/) to build this site on my Windows PC and won't dive deep into it, but a rough outline is as follows:

- Install Ruby using [RubyInstaller](https://rubyinstaller.org/) for Windows (Ruby+Devkit)
- Install Jekyll and Bundler
- Verify Jekyll was installed
- Create a new Jekyll sites
- Change to your new directory
- Build your site and serve it locally

Sounds simple enough, and it really is. The problem, and purpose of this post is that while you can run your site locally, in some cases, when trying to deploy on GitHub Pages, it fails because of missing dependencies. The github-pages gem only supports specific versions of Jekyll and other gems, so if a new or really fancy plugin you just loaded runs well locally, it could fail to build on GitHub Pages because it doesn't match the versions on GitHub Pages.

## Making GitHub Pages run with latest Jekyll

So how do we get our plugins and versions to work on GitHub Pages? To start off, let's analyze how the static site is generated. When we build our site locally using Jekyll, it converts the content in our Markdown files into HTML (which is what the browser needs to display), and creates all the necessary files in a folder called "_site". To make our site available on the internet, we simply place the contents of the _site folder on a machine that can serve them to the public, this is what GitHub Pages does for us.

There are many ways to configure our GitHub repo to trigger a Jekyll build. One of them is to have a branch called `gh-pages`. You can push your entire Jekyll project without running `jekyll build`, and GitHub will automatically do it. However, this will use the restrictive github-pages gem.

To solve this, we build the site ourselves by running `bundle exec jekyll build`, then pushing the contents of the `_site` folder to the `gh-pages` branch. (This requires you have 2+ branches, one is the `master` or main, and the other is `gh-pages`). However, running the build from the main branch, then switching to gh-pages gets tedious. Luckily, we can automate this using [GitHub Actions](https://github.com/features/actions) which allows us to automate workflows based on certain events in our repo.

For our test, we are going to create a workflow that automatically builds the site using the same versions of Jekyll and other gems in our project, then deploy it every time we push to the `master` branch. Furthermore, it will create (or reset an existing) `gh-pages` branch.

### Setting up the GitHub Actions

GitHub Actions are registered for a repository by using a YAML file inside the directory path `.github/workflows`. First, we create a workflow file, for example `github-pages.yml` and push it to the workflow directory path. An example using the base contents are as shown below:
{% highlight bash linenos %}
name: Build and deploy Jekyll site to GitHub Pages

on:
  push:
    branches:
      - master

jobs:
  github-pages:
    runs-on: ubuntu-latest
    steps:
      - name: 📂 setup
        uses: actions/checkout@v2
        uses: helaili/jekyll-action@2.0.5
        env:
          JEKYLL_PAT: ${{ secrets.JEKYLL_PAT }}
{% endhighlight %}  

The workflow can be explained as follows:
- We trigger the build using on.push condition for the `master` branch only.
- The **name** of the job matches the name of the YAML file
- The **checkout** action takes care of cloning your repository
- We specify our selected **action** and **version number** using `helaili/jekyll-action@2.0.5`
- We set a reference to a secret environment variable for the action to use. The `JEKYLL_PAT` is a Personal Access Token and is detailed in the next section.

### Providing permissions

The action needs permissions to push to your `gh-pages` branch. So you need to create a GitHub authentication token on your GitHub profile, then set it as an environment variable in your build using Secrets:

- On your GitHub profile, under **Developer Settings**, go to the **Personal Access Tokens** section.
- Create a token. Give it a name like "GitHub Actions" and ensure it has permissions to `public_repos` (or the entire `repo` scope for private repository) — necessary for the action to commit to the gh-pages branch.
- Copy the token value.
- Go to your repository’s **Settings** and then the **Secrets** tab.
- Create a token named `JEKYLL_PAT` (important). Give it a value using the value copied above.

### Build and deploy

On pushing any local changes onto `master`, the action will be triggered and the build will start.

1. Push to `master` branch of GitHub
{% highlight bash linenos %}
-- Ensure you are in main or master branch
git checkout master

-- Push to origin (GitHub) servers
git push -u origin master
{% endhighlight %}
2. Wait for the workflow to finish.
