---
layout: default
title: Home
has_children: true
nav_order: 5
---
# Jekyll Cloudinary Liquid tag

[![Gem Version](https://badge.fury.io/rb/jekyll-responsive-cloudinary.svg)](https://badge.fury.io/rb/jekyll-responsive-cloudinary)
[![Gem Downloads](https://img.shields.io/gem/dt/jekyll-responsive-cloudinary.svg?style=flat)](http://rubygems.org/gems/jekyll-responsive-cloudinary)

`jekyll-responsive-cloudinary` is a [Jekyll](http://jekyllrb.com/) plugin adding a [Liquid](http://liquidmarkup.org) tag to ease the use of [Cloudinary](http://cloudinary.com/invites/lpov9zyyucivvxsnalc5/sgyyc0j14k6p0sbt51nw) for responsive images in your Markdown/[Kramdown](http://kramdown.gettalong.org/) posts.

It builds the HTML for responsive images in the posts, using the `srcset` and `sizes` attributes for the `<img />` tag (see [the "varying size and density" section of this post](https://jakearchibald.com/2015/anatomy-of-responsive-images/#varying-size-and-density) if this is new for you, and why it's recommended to [not use `<picture>` most of the time](https://cloudfour.com/thinks/dont-use-picture-most-of-the-time/)). URLs in the `srcset` are cloudinary URLs that [fetch on-the-fly](http://cloudinary.com/features#fetch) the post's images and resize them to several sizes.

You are in full control of the number of generated images and their sizes, and the `sizes` attribute that helps the browser decide which image to download. See the complete configuration options for details.

Here is the general syntax of this Liquid tag:

{% raw %}
```markdown
{% cloudinary cloudflare.png alt="Un schéma montrant l'apport de Cloudflare" caption="Un schéma montrant l'apport de Cloudflare" %}
```
{% endraw %}

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of contents

- [Jekyll Cloudinary Liquid tag](#jekyll-responsive-cloudinary-liquid-tag)
  - [Table of contents](#table-of-contents)
  - [To do](#to-do)
  - [Do you use the plugin on a live site?](#do-you-use-the-plugin-on-a-live-site)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
## To do

There are already [a few issues for bugs and things that should be added to the plugin](https://github.com/mavaddat/jekyll-responsive-cloudinary/issues), feel free to add your ideas!

## Do you use the plugin on a live site?

Add it to [the "Sites" page of the wiki](https://github.com/mavaddat/jekyll-responsive-cloudinary/wiki/Sites) and please let me know on Twitter: [@mavaddat](https://twitter.com/mavaddat)
