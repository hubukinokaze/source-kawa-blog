---
title: Continuous Integration with CircleCI
date: 2018-10-17 22:04:07
tags: [hexo, circleci, github pages]
---

This post will be a tutorial on how to build your own static website using [Hexo](https://hexo.io/), [CircleCI](https://circleci.com/), and [GitHub Pages](https://pages.github.com/).

## Getting Started
----------------

##### Install Dependencies

Make sure to download and install:
1. [git](https://git-scm.com/)
2. [node v8.x.x](https://nodejs.org/en/)
3. [npm v6.x.x](https://nodejs.org/en/) **npm is installed with node*
4. [Any Text Editor](https://www.sublimetext.com/) **Sublime is a free text editor*

You can check to see if you have them installed by running this command in your terminal:

``` bash
git --version
node -v
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
hexo init [name-of-your-website] #No brackets
cd {name of your website}
npm install
hexo server
```

Go to your browser and go to *http://localhost:4000/*. You should be able to see your website running locally.

In order to safely stop the local server, just hit ctrl+c twice.

##### Hooking Up Your Project to GitHub

mindplace created instructions on hooking your project in detail if this one is too vague: [link](https://gist.github.com/mindplace/b4b094157d7a3be6afd2c96370d39fad).
Your project isn't on GitHub yet since it was newly created and git hasn't been initialized. First step to hooking it up is to run the command:

``` bash
git init
```

Now copy the .git HTTPS link from your repo on GitHub. It should be a green button labled "Clone or download". The link should look something like this: `https://github.com/username/repo-name.git`. Now commit and push your project by running the commands:

``` bash
git remote add origin [copied link] #No brackets
git push origin master
```

If everything turned out successeful, all of your project files should now be in your repo on GitHub.
