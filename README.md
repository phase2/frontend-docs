# Intro

Particle is an opinionated set of tools and examples to:

1. Build an application-agnostic **design system** made of assets like Twig, Sass, JavaScript, images, etc
2. Apply that **design system** to a locally-served Pattern Lab for rapid prototyping
3. Apply that **design system** to other consuming apps like, Drupal, Grav, or \(soon\) Wordpress

## Particle Features

* Drupal theme, Grav theme, Pattern Lab instance
* Strict [Atomic Design](http://atomicdesign.bradfrost.com/) component structure
* Robust Webpack bundling of all CSS, JavaScript, font, and static assets for multiple targets
* [Webpack Dev Server](https://github.com/webpack/webpack-dev-server) for local hosting and hot reloading of assets into Pattern Lab
* [Twig namespaced paths](https://symfony.com/doc/current/templating/namespaced_paths.html) automatically added into Drupal theme and Pattern Lab config; within any Twig file, `@atoms/thing.twig` means the same thing to Drupal theme and Pattern Lab
* Iconfont auto-generation
* Bootstrap 4 integration, used for all starting example components
* Auto-linting against the [AirBnB JavaScript Style Guide](https://github.com/airbnb/javascript) and sane Sass standards
* All Webpack and Gulp files are fully configurable
* [PostCSS](https://github.com/postcss/postcss/blob/master/README.md) automation and expansion, with [Autoprefixer](https://github.com/postcss/autoprefixer/blob/master/README.md).

## Documentation To-Do List

* Go over basics of Pattern Lab, the specific way Particle has Pattern Lab set up by default, and suggested uses.
* Folder & config structure need updated to current Webpack structure
* Explain Particle.js and how the `Particle()` function smashes various Webpack configs together
* Explain Webpack structure \(CSS modes, etc.\)
* Expand on technologies Particle automatically includes to make Sass/JS faster.
* Troubleshooting cleanup \("nothing to see here", datetime error?, etc.\)
* Testing notes \(Jest, Pa11y, Cypress?\)
* Vue-related notes
* Example workflows
* Flesh out the "thinking" sections
* Update the Drupal apps section \(what goes here vs. Drupal under Frontend?\)

