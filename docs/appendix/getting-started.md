# Prerequisites

- [Node `^8.0.0`](https://nodejs.org)
- [PHP `5.6`, `^7.0.0`](https://php.net)
- [Composer `^1.0.0`](https://getcomposer.org)


Particle can be run from anywhere to work with Pattern Lab. It also provides a theme to a Drupal website. You are free to add as many other apps as you wish.

### Quickstart anywhere

1. [Download the latest release](https://github.com/phase2/particle/releases)
1. Extract anywhere (i.e. the readme should be at `any/where/particle/README.md`)
1. Within the extracted folder run:

```bash
npm install
npm run setup
npm start
```

Simply wait until the webpack bundle output appears then visit [http://0.0.0.0:8080/pl](http://0.0.0.0:8080/pl) (or [http://localhost:8080/pl](http://localhost:8080/pl)) and start working.

### Quickstart with Drupal 8

Particle provides a Drupal 8 theme, the starting steps are slightly different:

1. [Download the latest release](https://github.com/phase2/particle/releases)
1. Extract to `themes/` at the root of your Drupal 8 install. (i.e. this readme should be at `drupal-root/themes/particle/README.md`)
1. Download and install the [Component Libraries module](https://www.drupal.org/project/components):

```bash
drush dl components
drush en components -y
```

1. Within `drupal-root/themes/particle/` run:

```bash
npm install
npm run setup
npm run compile:drupal
```

This will compile all assets and provide all namespaced Twig paths to the Drupal theme. Make sure to choose this theme in Drupal Appearance settings and `drush cr` to clear cache.

For subsequent recompile and Drupal cache clear, run:

```bash
npm run compile:drupal && drush cr
```

Working rapidly in Pattern Lab is still available, simply run:

```bash
npm start
```

Just like in the regular Quickstart, when Webpack output appears, visit [http://0.0.0.0/pl](http://0.0.0.0/pl) (or [http://localhost/pl](http://localhost/pl)) to immediately start building and previewing your design system in Pattern Lab.

That's it. For **much** greater detail on the frontend approach using this project, keep reading these docs.
