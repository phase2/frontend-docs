# What is Particle?
[Particle](https://github.com/phase2/particle/tree/epic/v10) is an opinionated toolkit for building application-agnostic design systems.

Particle is [Phase2's](https://www.phase2technology.com/) starting point for our front-end practices. It provides a framework for creating an atomic design system. It ensures all new projects can quickly and easily create custom components, while providing an array of examples and starting assets, including Bootstrap 4 and FontAwesome icons.

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
