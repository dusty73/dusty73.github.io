---
title: "Creating a website with Hugo - part 2"
description: "Second part on HUGO tutorial"
date: "2021-03-28"
tags: [ "web", "hugo" ]
categories: ["hugo"]
resources:
   - name: featured-image
     src: featured-image.jpeg
   - name: featured-image-preview
     src: featured-image.jpeg
---

In the first part we saw how to set up HUGO (with Docker), how to create a site and set the theme. As last step, we added a content page using ```hugo new posts/my_first_post.md```.
Let's move on and add content to the page.
<!--more-->

## Supported Formats
HUGO is able to treat many different {{< externallink link="https://gohugo.io/content-management/formats/" text="content formats">}}, in our serie we'll use **Markdown**.

I personally prefer to use Markdown, since it has a very easy and concise way to format text, and because is widely used.

## Front Matter
Any content page have what's called the **front matter**, a collection of metadata that instruct Hugo on how to manage the content. The front matter can be written in *json*, *yaml* or *toml* format.
Here's the front matter of this page:
{{< highlight yaml >}}
---
title: "Creating a website with Hugo - part 2"
description: "Second part on HUGO tutorial"
tags: [ "web", "hugo" ]
date: "2021-03-28"
---
{{</highlight>}}

In the front matter we can add also information about images and multimedia resources present in the page. This feature is called {{< externallink link="https://gohugo.io/content-management/page-bundles/" text="Page Bundle">}}.

## Content organization
Pages are created under ```/content``` folder, subdirectories are called "sections", the page we created is under section "posts". You can create other sections or group pages in categories. More information on content organization can be found {{< externallink link="https://gohugo.io/content-management/organization/" text="here">}}.

## Publish the site
Oncee you finished with the content creation it's time to publish the site. There are several alternatives that can be used. The {{<externallink link="https://gohugo.io/hosting-and-deployment/hugo-deploy/" text="hugo deploy">}} command allow us to publish on the major cloud providers. Other alternatives are:
* Netlify
* Render CDN
* Firebase
* Github
* Gitlab
* ... {{<externallink link="https://gohugo.io/hosting-and-deployment/" text="and many others">}}

For this site I chose to use Github Pages, let's see how it works.

## Github Pages
For my personal site I chose to use Github User Page, you can also use Project Pages.
The repository must be named as **githubusername.github.io**, so the site will be accessible to the URL: **https://githubusername.github.io**.

In your repo, create a branch called gh-pages, this will contain the published site:
```bash
git checkout -b gh-pages
```
Then create the Github Actions workflow for publishing the site each time we push on the main branch. Create the file ```.github/workflows/gh-pages.yml``` with the following content:
{{<highlight yaml >}}
name: github pages
on:
  push:
    branches:
      - main  # Set a branch to deploy

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
{{</highlight>}}
This workflow uses ```peaceiris``` actions to setup Hugo and launch the build. See the {{<externallink link="https://github.com/marketplace/actions/hugo-setup" text="actions marketplace">}} for further details.
Once built the ```public``` folder will be copied under the root of ```gh-pages``` branch and will become visible at the URL we saw above. 

Push all changes on Github, then go to Github site, Settings -> Pages and choose ```gh-pages``` as Source Branch.
Then go to the tab "Actions" and if you already pushed on main branch you should see the action run, if everything is fine the site is available to the user Github Page.

## Site lifecycle
From now on, each time we want to add content to the site we can work using branches, testing everything locally with hugo server, push the branch and merge it with main when we're good to go.