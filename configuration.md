---
layout: default
title: Configuration
has_children: true
parent: Home
nav_order: 2
---
# Configuration
{: .no_toc }
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Mandatory settings

These configurations are required to set up the plugin.
### Activating in Jekyll

Add `cloudinary` to your `_config.yml` and your Cloudinary "Cloud name" (find it in your [Cloudinary dashboard](https://cloudinary.com/console)):

```yaml
cloudinary:
  cloud_name: <put here your Cloudinary "Cloud name">
```

## Optional global settings

You can now define some global settings

```yaml
cloudinary:
  …
  verbose: true
```

### `verbose` (default: `false`)

When set to `true`, this setting will show messages in the console when something goes wrong, such as:

```
[Cloudinary] Couldn't find this image to check its width: /path/to/jekyll/_site/assets/img.jpg
```

or

```
[Cloudinary] Natural width of source image 'img.jpg' (720px) in _posts/2016-06-09-post.md not enough for creating 1600px version
```

## Optional (but highly recommended) presets

You can now define the presets you need for your posts' images, starting with the default one:

### Default preset

The default preset is the one you don't even have to mention when using the Liquid tag, and that will be used if a preset you use in the tag doesn't exist.

```yaml
cloudinary:
  …
  presets:
    default:
      min_width: 320
      max_width: 1600
      fallback_max_width: 800
      steps: 5
      sizes: "(min-width: 50rem) 50rem, 90vw"
```

This preset will generate five images 320 to 1600 pixels wide in the `srcset` and define `sizes` as `"(min-width: 50rem) 50rem, 90vw"`. The fallback image defined in the `src` will have a width of 800 pixels.

With this preset, you only have to write this in your Markdown post:

{% raw %}
```markdown
{% cloudinary /assets/img.jpg alt="beautiful!" %}
```
{% endraw %}

To get this HTML:

```html
<img
  src="http://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_800,q_auto,f_auto/https://<your-domain>/assets/img.jpg"
  srcset="
    http://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_320,q_auto,f_auto/https://<your-domain>/assets/img.jpg 320w,
    http://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_640,q_auto,f_auto/https://<your-domain>/assets/img.jpg 640w
    http://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_960,q_auto,f_auto/https://<your-domain>/assets/img.jpg 960w
    http://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_1280,q_auto,f_auto/https://<your-domain>/assets/img.jpg 1280w
    http://res.cloudinary.com/<cloud_name>/image/fetch/c_limit,w_1600,q_auto,f_auto/https://<your-domain>/assets/img.jpg 1600w
    "
  sizes="(min-width: 50rem) 50rem, 90vw"
  alt="beautiful!"
  width="480"
  height="320"
/>
```

There is a true default `default` preset, but you're strongly encouraged to override it with your own default preset.

### Additional presets

You can add other presets if you need several image sizes in your posts.

Here is an example for images that take only one third of the post width:

```yaml
cloudinary:
  …
  presets:
    …
    onethird:
      min_width: 110
      max_width: 535
      fallback_max_width: 300
      steps: 3
      sizes: "(min-width: 50rem) 17rem, 30vw"
      attributes:
        class: "one3rd"
```

To use this additional preset, you will have to write this in your Markdown post:

{% raw %}
```markdown
{% cloudinary onethird /assets/img.jpg %}
```
{% endraw %}

The generated element will also get a `class="one3rd"` that can be useful for example with this CSS:

```css
.one3rd {
  max-width: 33%;
  float: right;
  margin: 0 0 1em 1em;
}
```

## Detailed preset settings

### `figure` (default: `auto`)

This setting lets you decide what to do when there is a `caption` attribute in the Cloudinary Liquid tag.

The value can be:

- `auto` (default): will generate a `<figure>` and `<figcaption>` only if there's a caption
- `never`: will always generate a `<img>`, losing the caption
- `always`: will always generate a `<figure>` and `<figcaption>`, even if there's no `caption` attribute

If a `<figure>` is generated and there are attributes in the Liquid tag, they are added to the `<img>` if they are `alt` or `title`, or to the `<figure>`.

### `min_width` (default: `320`)

### `max_width` (default: `1200`)

### `fallback_max_width` (defaut: `1200`)

### `steps` (default: `5`)

### `sizes` (default: `"100vw"`)

### `attributes` (default: none)

Attributes are added without transformation to the generated element.

You can obviously define the `alt` attribute, mandatory for accessibility, but you can also set a `title`, a `class`, `aria-*` attributes for enhanced accessibility, or even `data-*` attributes you would like to use later with CSS or JavaScript.

The `caption` attribute is the only one that can act differently, depending on the `figure` setting.

`alt`, `title` and `caption` attributes can contain Markdown.


