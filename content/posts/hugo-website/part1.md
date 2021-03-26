---
title: "Creating a website with Hugo"
tags: [ "web", "docker", "hugo" ]
date: "2021-03-26"
---
# Introduction
In this series, I want to describe how I created and manage this web site. I started my career as developer working in a Web Agency, long time ago in 1998. At that time, creating so-called static sites was pretty normal. At that time, we developed a tool for managing templates that allowed us to generate and update pages very quickly and easily.

Then it came the "server-side" era, with .php, .asp and java as prominent technologies, that dominated the scene for many years. For simple sites like this blog, using a server-side technology just for templating seems to be a bit overkill, so I chose to return to origins, creating a static site, but with a very powerful tool that helps a lot in the management of the content and controlling the appearance.

The tool is {{< externallink link="https://gohugo.io/" text="HUGO">}}. This open source tool written in Go lets you create a static site from scratch, let's see how.

# Installation

Hugo is distributed as binary distribution for all major OSes. For classic installation, you can follow the {{< externallink link="https://gohugo.io/getting-started/installing/" text="guide">}}.

I prefer to use the Docker image. There's no official image, but Hugo site suggests to use the image created by {{< externallink link="https://hub.docker.com/r/klakegg/hugo/" text="klakegg">}}

Let's set up two aliases:
```bash
cat <<EOF > ~/.hugorc
alias hugo='docker run --rm -it -v $(pwd):/src -p 1313:1313 klakegg/hugo'
alias hugoserver='docker run --rm -it -v $(pwd):/src -p 1313:1313 klakegg/hugo server -D --bind 0.0.0.0'
EOF
```
then append the ```.hugorc``` file just created to the profile, .bashrc, .zshrc or whatever:
```bash
# bash
echo "source ~/.hugorc" >> ~/.bashrc
# zsh
echo "source ~/.hugorc" >> ~/.zshrc
```

# Create a site
Just issue the command:
```bash
$ hugo new site my-site

Congratulations! Your new Hugo site is created in /src/test.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```
this will create a folder named ```my-site``` with the following folder structure:
```bash
my-site
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── resources
├── static
└── themes
```

# Themes
Once created the site, we need to install a theme. This is the official registry: {{< externallink link="https://themes.gohugo.io/" text="themes.gohugo.io">}}. Once chosen the theme, we just need to clone the repo and activate it, see for example:
```bash
git clone https://github.com/vaga/hugo-theme-m10c.git themes/m10c
```
and we add the theme configuration to ```config.toml```:
```toml
languageCode = "en-us"
title = "..."
...
theme = "m10c"
```
Each theme has instructions on how to fine-tune the configuration, you just have to check the documentation.

# Hugo Server
It's now time to check our brand new site. Hugo implements a local development server that renders the pages on-the-fly and allow us to see the changes immediately.
Let's use the alias we set up:
```bash
$ hugoserver
Start building sites …

                   | EN
-------------------+-----
  Pages            |  7
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  1
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Built in 34 ms
Watching for changes in /src/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /src/config.toml
Environment: "DEV"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 0.0.0.0)
Press Ctrl+C to stop
```
Now, we can point our browser to {{< externallink link="http://localhost:1313/" text="http://localhost:1313">}} and see the preview.

# Basic configuration
We just saw ```config.toml```. This file contains all main configuration entries that are valid for the whole site. See here for further details: {{< externallink link="https://gohugo.io/getting-started/configuration/" text="https://gohugo.io/getting-started/configuration/">}}

# My first post
To create the first post of this site we issue:
```bash
hugo new posts/my_first_post.md
```
The command will create a file in the following path: ```content/posts/my_first_post.md```

In the next part, we'll see how to write a post.