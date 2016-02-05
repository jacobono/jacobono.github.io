+++
categories = []
date = "2016-02-04T17:10:45-05:00"
tags = []
title = "Hello Hugo!"

+++

I kept putting off a github blog (long time) -- something about the `gh-pages` workflow was weird enough for me to continue to put it off.

I finally decided to bite the bullet and figure this thing out!

I basically had two choices:

- [jekyll](https://jekyllrb.com/)
- [hugo](https://gohugo.io/) 

Hugo seemed really easy to use, and it definitely is.

# Setting It All Up #

With a github blog, you need to create a repository of `<your-github-username>.github.io`.  For me that is `jacobo.github.io`.

Anything under the `master` branch with an `index.html` file will be served at the url `http://<your-github-username>.github.io`.

- Create your repository -- `<your-github-username>.github.io` on [github](www.github.com) 
- Install hugo -- `brew install hugo`
- Create a new hugo powered site -- `hugo new site <your-github-username>.github.io`
- `cd <your-github-username>.github.io`
- init your git repo however you see fit `git init` or through `emacs` and `magit`
- add your repo as a remote -- I use [hub](https://github.com/github/hub) `hub remote add origin <your-github-username>/<your-github-username>.github.io`

# Adding a theme #

I went with [a port of the greyshade theme from octopress](https://github.com/cxfksword/greyshade).

Clone into your folder with `hub clone https://github.com/cxfksword/greyshade themes/greyshade` and *DONT* forget to delete the `themes/greyshade/.git` directory that contains.

Add `theme = "greyshade"` to `config.toml`.

Also add the things the theme says to add in `config.toml`.

## Editing the theme ##

First time using hugo, so for me as of `v0.15` creating a new post wouldn't work because of an empty default archetype in the theme.

The docs are really good though, so after a quick search I found the [archetype docs](https://gohugo.io/content/archetypes/) showing a default that works to create a new post.

Change `themes/greyshade/archetypes/default.md`

```markdown
+++
tags = ["x", "y"]
categories = ["x", "y"]
+++
```

# Creating Your First Post #

`hugo new post/hello.md`

With the default archetype, this a going to be a real post, but you can make it a draft if you want by adding `draft = true` at the to of `content/post/hello.md`

# Run Locally #

Run `hugo server -w` will run locally and serve the site up at `http://localhost:1313`.  You can go to it and check it out there.

# Set Up `source` Branch #

However you please, create and checkout the branch `source` and make a `.gitignore` file with content

```
public
```

This branch will host all of what is in the current folder (but not the `public` folder because that will go to `master`).

Add all the files so far, and push to the `source` branch.

# Build The Static Site And Push To Master #

- Run `hugo` to build the site into the `public` folder.
- `cd public` and init a git repository here.
- add your remote as before
- commit everything in this public folder
- push to master

And thats it.  Go to your github.io page in the browser and when github reloads its servers you can see your blog, hosted by github! :smiley:

## Markdown Support ##

Install [blackfriday](https://github.com/russross/blackfriday) on your machine, to get markdown support.  It is awesome.

## Last Thoughts ##

I'm not quite sure how I like the two branches in separate folders -- it just seems so weird to me from how I normally develop day-to-day.

It does seperate things clearly though.

A better improvement might be to have a CI server push the public folder to master on every commit from source.

Another improvement could be to use gulp or something similar (and something I have never worked with) to compile and minify the asset pipeline.

That would be pretty cool to learn.

10/10 would totally do again! :bowtie:
