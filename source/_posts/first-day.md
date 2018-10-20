---
title: Continuous Integration with CircleCI
date: 2018-10-17 22:04:07
tags: 
	- hexo
	- circleci
	- github pages
---

This post will be a tutorial on how to build your own static website using [Hexo](https://hexo.io/), [CircleCI](https://circleci.com/), and [GitHub Pages](https://pages.github.com/).

## Getting Started
----------------

##### Install Dependencies

Make sure to download and install:
1. [node v8.x.x](https://nodejs.org/en/)
2. [npm v6.x.x](https://nodejs.org/en/) **npm is installed with node*
3. [Any Text Editor](https://www.sublimetext.com/) **Sublime is a free text editor*

You can check to see if you have them installed by running this command in your terminal:

``` bash
node -v
```

``` bash
npm -v
```

##### Create a GitHub account

One of the best places to host your static website for free is GitHub Pages. In order to utilize that, you will first need to have a GitHub account.
Site: [GitHub](https://github.com/)

##### Create Repo

Create a new repository on [GitHub](https://github.com/new). The name of the repository can be anything. Initially, there will be nothing inside the repo, but we will start adding to it later on.

##### Create Hexo Project

Open your terminal and run the command:

``` bash
npm install hexo-cli -g
hexo init {name of your website}
cd {name of your website}
npm install
hexo server
```
**Replace "{name of your website}" with the actual name
Go to your browser and go to *http://localhost:4000/*. You should be able to see your website running locally.