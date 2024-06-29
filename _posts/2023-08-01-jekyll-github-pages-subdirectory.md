---
layout: post
title: GitHub Pages - Blogging with Jekyll via Subdirectory
subtitle: A quick how-to
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [howto, jekyll, blog, github pages]
---

Jekyll (and Jekyll themes) is a great way to get started with Blogging. I have already been hosting a static homepage for myself using GitHub pages (at georgetipton.com), and wanted to create a blog without it being hosted on the root of my site (accessible via https://georgetipton.com/blog, for example). I had a surprisingly difficult time figuring out a way to easily accomplish this, so I figured I would create a quick how-to as my first blog entry!

Note: this how-to assumes you already have a GitHub pages site (such as username.github.io), and want to add a separate, external blog site page.

I'll be using Beautiful Jekyll as my Jekyll theme for the sake of this tutorial.

1. Create a Fork of [Beautiful-Jekyll](https://github.com/daattali/beautiful-jekyll) repository on GitHub, and name it whatever you'd like.
   ![Fork GitHub repo](/blog/assets/img/gh-jekyll-fork.png)
   ![Fork GitHub repo](/blog/assets/img/gh-jekyll-fork-config.png)
2. Once forked, navigate to the "Settings" page for your repository
   ![Fork GitHub repo](/blog/assets/img/gh-jekyll-settings.png)
3. Under "Code and Automation", click "Pages"
   ![Fork GitHub repo](/blog/assets/img/gh-jekyll-pages.png)
4. Configure the following settings
   - Source: Deploy from a branch
   - Branch: master
   - Folder: /(root)
5. Click save
6. Once saved, you should see that your repo is live at the specified URL
   ![Fork GitHub repo](/blog/assets/img/gh-jekyll-pages-config.png)
   ![Fork GitHub repo](/blog/assets/img/gh-jekyll-live.png)

With the generated URL, you can then simply add a link from your primary GitHub pages homepage (as seen on my site, https://georgetipton.com)

Resources:

- [Publishing Source for Your GitHub Pages Site](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
