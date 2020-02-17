# What is Particle?
[Particle](https://github.com/phase2/particle/) is an opinionated toolkit for building application-agnostic design systems built with love by [Phase2](https://www.phase2technology.com/).

![Particle Logo Astrogoat](img/astrogoat.png)

Particle is an opinionated set of tools and examples to:

1. Build an application-agnostic **design system** of asset files like Twig, Sass, javascript, and images
1. Apply that design system to a locally-served **Pattern Lab** for rapid prototyping
1. Apply that design system to a **Drupal or Grav theme**

## Provides

- Drupal theme, Grav theme,  and Pattern Lab app
- Strict [Atomic Design](http://atomicdesign.bradfrost.com/) component structure
- Webpack bundling of all CSS, javascript, font, and static image assets for multiple targets (Drupal theme, Grav theme, Pattern Lab)
- [Webpack Dev Server](https://github.com/webpack/webpack-dev-server) for local hosting and hot reloading of assets into Pattern Lab
- [Twig namespaced paths](https://symfony.com/doc/current/templating/namespaced_paths.html) automatically added into Drupal theme and Pattern Lab config. Within any twig file, `@atoms/thing.twig` means the same thing to Drupal theme and Pattern Lab.
- Iconfont auto-generation
- Bootstrap 4 integration, used for all starting example components
- Auto-linting against the [AirBnB JavaScript Style Guide](https://github.com/airbnb/javascript) and sane Sass standards
- All Webpack and Gulp files are fully configurable
