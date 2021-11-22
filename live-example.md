---
layout: default
title: Live example
has_children: true
parent: Home
grand_parent: Home
nav_order: 6
---
# Live example

Go to this post: [https://nicolas-hoizey.com/2016/07/tout-change-rien-ne-change.html](https://nicolas-hoizey.com/2016/07/tout-change-rien-ne-change.html).

The source Markdown is here: [https://github.com/nhoizey/nicolas-hoizey.com/blob/master/_posts/2016/07/13-tout-change-rien-ne-change/2016-07-13-tout-change-rien-ne-change.md](https://github.com/nhoizey/nicolas-hoizey.com/blob/master/_posts/2016/07/13-tout-change-rien-ne-change/2016-07-13-tout-change-rien-ne-change.md).

The content is in french, yes, but look only at the images if you don't understand.

You'll find here:

- 2 logos floating on the right of the text (or centered on smaller screens): [Jekyll](http://jekyllrb.com/) and [Cloudinary](http://cloudinary.com/invites/lpov9zyyucivvxsnalc5/sgyyc0j14k6p0sbt51nw)
- 2 screenshots taking the whole width of the content: the [Cloudinary pricing table](http://cloudinary.com/pricing), and [Dareboost](https://www.dareboost.com/en/home)'s performance monitoring graph

These image types need different settings to deal with different sizes and position:

- screenshot always use the full content width, if they're wide enough
- logos are centered and take one half of the content width on small screens, and are floated and take one fourth of the content width on larger screens

This is how I use the Cloudinary Liquid tag for the Cloudinary logo and prices table screenshot:

{% raw %}
```markdown
{% cloudinary logo /assets/logos/cloudinary.png alt="Logo de Cloudinary" %}
{% cloudinary cloudinary-pricing.png alt="Les tarifs de Cloudinary" caption="Les tarifs de Cloudinary, dont l'offre gratuite déjà généreuse" %}
```
{% endraw %}

The only difference is that I explicitly use the `logo` preset for the logo. The other image uses the `default` preset.

Here is the necessary configuration for this:

```yaml
cloudinary:
  cloud_name: …
  verbose: false
  presets:
    default:
      min_width: 320
      max_width: 1600
      fallback_max_width: 800
      steps: 5
      sizes: '(min-width: 50rem) 50rem, 90vw'
      figure: always
    logo:
      min_width: 80
      max_width: 400
      fallback_max_width: 200
      steps: 3
      sizes: '(min-width: 50rem) 13rem, (min-width: 40rem) 25vw, 45vw'
      figure: never
      attributes:
        class: logo
```

It generates these HTML fragments (pretty printed here), for the logo:

```html
<img
  src="https://res.cloudinary.com/nho/image/fetch/c_limit,w_200,q_auto,f_auto/https://nicolas-hoizey.com/assets/logos/cloudinary.png"
  srcset="
    https://res.cloudinary.com/nho/image/fetch/c_limit,w_80,q_auto,f_auto/https://nicolas-hoizey.com/assets/logos/cloudinary.png 80w,
    https://res.cloudinary.com/nho/image/fetch/c_limit,w_240,q_auto,f_auto/https://nicolas-hoizey.com/assets/logos/cloudinary.png 240w,
    https://res.cloudinary.com/nho/image/fetch/c_limit,w_400,q_auto,f_auto/https://nicolas-hoizey.com/assets/logos/cloudinary.png 400w"
  sizes="
    (min-width: 50rem) 13rem,
    (min-width: 40rem) 25vw,
    45vw"
  class="logo"
  alt="Logo de Cloudinary"
  width="480"
  height="350"
/>
```

And for the screenshot:

```html
<figure>
  <img
    src="https://res.cloudinary.com/nho/image/fetch/c_limit,w_800,q_auto,f_auto/https://nicolas-hoizey.com/2016/07/cloudinary-pricing.png"
    srcset="
      https://res.cloudinary.com/nho/image/fetch/c_limit,w_320,q_auto,f_auto/https://nicolas-hoizey.com/2016/07/cloudinary-pricing.png 320w,
      https://res.cloudinary.com/nho/image/fetch/c_limit,w_640,q_auto,f_auto/https://nicolas-hoizey.com/2016/07/cloudinary-pricing.png 640w,
      https://res.cloudinary.com/nho/image/fetch/c_limit,w_960,q_auto,f_auto/https://nicolas-hoizey.com/2016/07/cloudinary-pricing.png 960w,
      https://res.cloudinary.com/nho/image/fetch/c_limit,w_1208,q_auto,f_auto/https://nicolas-hoizey.com/2016/07/cloudinary-pricing.png 1208w"
    sizes="(min-width: 50rem) 50rem, 90vw"
    alt="Les tarifs de Cloudinary"
    width="1208"
    height="561"
  />
  <figcaption>Les tarifs de Cloudinary, dont l'offre gratuite déjà généreuse</figcaption>
</figure>
```

There are only 4 version in the `srcset` here because 2 of the 5 expected sizes are larger than the source image, and are replaced by one using the native source image width.

And here are the relevant parts of the accompanying CSS (in Sass form):

```sass
article {
  figure, img {
    margin: 2em auto;
    display: block;
    max-width: 100%;
    height: auto;
  }
}

.logo {
  display: block;
  margin: 1em auto;
  max-width: 50%;
  height: auto;

  @media (min-width: 40em) {
    max-width: 25%;
    float: right;
    margin: 0 0 1em 1em;
  }
}
```

