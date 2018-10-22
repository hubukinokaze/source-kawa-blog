---
title: Continuous Integration with CircleCI
date: 2018-10-17 22:04:07
tags: [hexo, circleci, githubpages]
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
cd [name-of-your-website]
npm install
hexo server
```

Go to your browser and enter `http://localhost:4000/`. You should be able to see your website running locally.

In order to safely stop the local server, just hit ctrl+c twice.

##### Hooking Up Your Project to GitHub

mindplace created instructions on hooking your project in detail if this one is too vague: [link](https://gist.github.com/mindplace/b4b094157d7a3be6afd2c96370d39fad).
Your project isn't on GitHub yet since it was newly created and git hasn't been initialized. First step to hooking it up is to run the command:

``` bash
git init
```

Now copy the HTTPS link from your repo on GitHub. It should be a green button labeled "Clone or download". The link should look something like this: `https://github.com/username/repo-name.git`. Now commit and push your project by running the commands:

``` bash
git remote add origin [copied link] #No brackets
git push origin master
```

If everything turned out successful, all of your project files should now be in your repo on GitHub.

##### Setting Up CircleCI

We finally can setup the continuous integration portion of the project. This will allow your projects to be deployed to github pages automatically whenever you push your changes. You can change settings around to your preference like to make it deploy on certain circumstances.

Go to CircleCI's website and sign up for a free account with your GitHub account. After signing in, click on `Add Projects` located on the left sidebar, find your project in the list, and click on the `Sign Up Project` button. It should take you to a new page (don't worry about anything on this page) and just click on the `Start Building` button. That's it for this portion, but we still need to add some configurations so CircleCI knows what you want it to do.

##### Configuring CircleCI

Go back to your project on GitHub and click on the `Create new file` button. Type in `.circleci/config.yml` for the name and copy/paste the code below into the body:

``` yml
version: 2
jobs:
  build:
    branches:
      ignore: gh-pages 
    docker:
      - image: circleci/node:8
    environment:
      - SOURCE_BRANCH: master
      - TARGET_BRANCH: gh-pages
    steps:
      - checkout
      - run:
          name: Install Hexo
          command: sudo npm install -g hexo-cli
      - restore_cache:
          keys:
          - v1-dependencies-{{ checksum "package.json" }}
          - v1-dependencies-
      - run:
          name: Install dependencies
          command: npm install
      - save_cache:
          paths:
            - node_modules
          key: v1-dependencies-{{ checksum "package.json" }}
      - run:
          name: Generate static website
          command: |
            hexo clean
            hexo generate
            git config --global user.email $GH_EMAIL
            git config --global user.name $GH_NAME
            hexo deploy
```
