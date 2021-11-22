---
layout: default
title: Installation
has_children: true
parent: Home
grand_parent: Home
nav_order: 4
---
# Installation

[Sign up **for free** on Cloudinary!](http://cloudinary.com/invites/lpov9zyyucivvxsnalc5/sgyyc0j14k6p0sbt51nw) The free account should be enough for most blogs.

Add `gem 'jekyll-responsive-cloudinary'` to the `jekyll_plugin` group in your `Gemfile`:

```ruby
source 'https://rubygems.org'

gem 'jekyll'

group :jekyll_plugins do
  gem 'jekyll-responsive-cloudinary'
end
```

Then run `bundle update` to install the gem.


