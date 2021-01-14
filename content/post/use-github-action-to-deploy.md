---
title: "Use GitHub Actions to deploy"
date: 2021-01-13T13:39:27+08:00
draft: false
summary: Use GitHub action to deploy blogs automatically
tags: ["GitHub", "Hugo"]
typora-root-url: ../../static
typora-copy-images-to: ../../static/images
---

# Use GitHub Actions to deploy

## Create access token

<https://github.com/settings/tokens/new>

create a new access token and check **repo** scopes

![image-0lhe35ktj7ii](/images/image-0lhe35ktj7ii.png)

then click **Generate token** at the bottom, keep the generated token safely

## Create repository secrets

navigate to your **\<user\>.github.io**, then go to **Settings**

![image-0zfuoom6mrj](/images/image-0zfuoom6mrj.png)

find and select **Secrets** tab, click **New repository secret** button

I'm going to name it *PUBLISH_TOKEN*, and paste the access token to the **Value** field

then click **Add secret**

## Create workflows 

create *.github/workflows/deploy.yml* to your repo

```yaml
name: Publish Hugo site
 
# https://lijingcheng.github.io/posts/hugo/
on:
  push:
    branches:
      - master
 
jobs:
  build-deploy:
    runs-on: ubuntu-20.04
    steps:
    # https://github.com/actions/checkout
    - uses: actions/checkout@v2
      with:
        submodules: true
 
    # https://github.com/peaceiris/actions-hugo
    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: '0.80.0'

    - name: Build
      run: hugo --minify

    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        # https://github.community/t/all-github-actions-suddenly-failing-with-github-token-secret-does-not-exist/16108/7
        github_token: ${{ secrets.PUBLISH_TOKEN }}
        publish_dir: ./public
```

then commit and push

after a while you should be able to see a new branch **gh-pages** in your repo

## Select *gh-pages* branch as GitHub Pages

navigate to your **\<user\>.github.io**, then go to **Settings**

scroll down and find **GitHub Pages** section, change source branch to **gh-pages** branch

visit <https://k265.github.io>, you may wait a while after changes taking affect



