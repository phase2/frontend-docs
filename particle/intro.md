---
description: >-
  Particle is an opinionated toolkit for building application-agnostic design systems built with love by Phase2.
---

# What is it?

![Astrogoat is the official logo of Particle, by Lisa Jansen](../.gitbook/assets/astrogoat.png)

## What is Particle?

Particle is an opinionated set of tools and examples to:

1. Build one or more application-agnostic **design systems** made of assets like Twig, Sass, JavaScript, images, etc
2. Apply those **design systems** to a locally-served Pattern Lab for rapid prototyping
3. Apply those **design systems** to other consuming apps like, Drupal, Grav, or \(soon\) Wordpress

## Particle Features

* Drupal theme, Grav theme, and Pattern Lab instances
* Strict [Atomic Design](http://atomicdesign.bradfrost.com/) component structure
* Robust Webpack bundling of all CSS, JavaScript, font, and static assets for multiple targets
* [Webpack Dev Server](https://github.com/webpack/webpack-dev-server) for local hosting and hot reloading of assets into Pattern Lab
* [Twig namespaced paths](https://symfony.com/doc/current/templating/namespaced_paths.html) automatically added into Drupal theme and Pattern Lab config; within any Twig file, `@atoms/thing.twig` means the same thing to Drupal theme and Pattern Lab
* Iconfont auto-generation
* Bootstrap 4 integration, used for all starting example components
* Auto-linting against the [AirBnB JavaScript Style Guide](https://github.com/airbnb/javascript) and sane Sass standards
* All Webpack and Gulp files are fully configurable