# Sprint 0

So you've just started a project and you're using Particle? Awesome! This Sprint 0 Guidebook is here to help get your files and project in order to start Sprint 1 with a bang.

## Removing Apps

The first thing you might want to do is remove apps you don't plan on using. By default, Particle ships with a Drupal, Pattern Lab and Grav app. Let's take a look at removing Grav step-by-step:

* Remove Grav Directory
* Remove Grav Scripts from particle root `package.json`
* Remove twig-namespaces tasks from particle's `gulpfile.js`
* GRAV ONLY: Remove the root `particle.yml` file.

That's it! Your Particle is now 100% Grav-free.

## Removing Default Patterns

Particle comes by default with many different patterns based on [Bootstrap 4](https://getbootstrap.com/). If you would like to remove these default patterns in reverse order: Pages => Templates => Organisms => Molecules => Atoms. Here are a few gotchas:

* Don't Remove Protons: these "patterns" contain largely config. Simply put, they contain a bit of the magic that makes Particle great. Once you know more about how these are working you can override them.
* Don't Remove Atoms/Images or Atoms/SvgIcon right away: while these patterns are replaceable, they're used in a few places that may result in angry console output.
* Organisms/Carousel: This default pattern implements Bootstrap 4's Carousel, but also stands as a method for the Drupal app to have settings overridden. Remove Carousel as well as the settings overrides in the [Drupal app's](https://github.com/phase2/particle/blob/master/apps/drupal/index.js) `index.js` file.

## Now You're Linting with Power. AirBnB Power

No but seriously, your linter might get mad at you. For full instruction, see config_structure.md. However just be aware by default there are several config files at the root of Particle that govern our code structure. See below for the file and associated docs:

* Babel Config File: [.babelrc](https://babeljs.io/docs/en/)
* Browserlist: [.browserslistrc](https://github.com/browserslist/browserslist)
* EditorConfig: [.editorconfig](https://editorconfig.org/)
* ESLint: [.eslintrc.js](https://eslint.org/) [AirBnb JS Style Guide](https://github.com/airbnb/javascript)
* Prettier: [.prettierrc.js](https://prettier.io/)
* Stylelint: [.stylelintrc](https://stylelint.io/user-guide/)

## Removing Bootstrap

WIP - Help Requested

## Renaming Drupal Theme

While not entirely necessary, you may make the decision at some point to rename your Drupal theme contained in your Drupal app folder. By default the name is listed as Particle, but it really can be anything you wish. Let's say you want your theme to be the Kittens theme:

* Update `particle.info.yml` to `kittens.info.yml`
* Update Particle theme functions file from `particle.theme` to `kittens.theme`
 * * Update your theme function names from `particle_` to `kittens_`.
* Update `particle.libraries.yml` to `kittens.libraries.yml`
* Note that Particle bypasses Drupal's default jQuery library.
