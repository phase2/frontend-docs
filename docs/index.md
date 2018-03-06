# What is Particle?
[Particle](https://github.com/phase2/particle/) is an opinionated toolkit for building application-agnostic design systems built with love by [Phase2](https://www.phase2technology.com/).

![Particle Logo Astrogoat](img/astrogoat.png)


## Provides
- Drupal theme and Pattern Lab app
- Strict [Atomic Design](http://atomicdesign.bradfrost.com/) component structure
- Webpack bundling of all CSS, javascript, font, and static image assets for multiple targets (Drupal theme and Pattern Lab)
- Webpack Dev Server for local hosting and auto asset injection into Pattern Lab and Drupal
- [Twig namespaced paths](https://symfony.com/doc/current/templating/namespaced_paths.html) automatically added into Drupal theme and Pattern Lab config. Within any twig file, `@atoms/thing.twig` means the same thing to Drupal theme and Pattern Lab.
- Bootstrap 4 integration, used for all starting example components
- Iconfont auto-generation
- FontAwesome, if you don't need to generate your own icons
- Auto-linting against the [AirBnB JavaScript Style Guide](https://github.com/airbnb/javascript) and sane Sass standards
- All Webpack and Gulp files are fully configurable
