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
Oncee you finished with the content creation 