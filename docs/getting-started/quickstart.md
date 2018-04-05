Particle builds design systems in dev mode for local hosting, or production mode for optimized asset generation.

## Quickstart anywhere

1. [Download the latest release](https://github.com/phase2/particle/releases)
1. Extract anywhere (i.e. the readme should be at `any/where/particle/README.md`)
1. Within the extracted folder run:

```bash
npm install
npm run setup
npm start
```

Simply wait until the webpack bundle output appears then visit [http://0.0.0.0:8080/pl](http://0.0.0.0:8080/pl) (or [http://localhost:8080/pl](http://localhost:8080/pl)) and start working.

## Quickstart with Drupal 8

Particle provides a Drupal 8 theme, the starting steps are slightly different:

1. [Download the latest release](https://github.com/phase2/particle/releases)
1. Extract to `themes/` at the root of your Drupal 8 install. (i.e. this readme should be at `{drupal-root}/themes/particle/README.md`)
1. Download and install the [Component Libraries module](https://www.drupal.org/project/components):
       
    ```
    drush dl components
    drush en components -y
    ```
    
    or
    
    ```
    drupal module:install components
    ```

1. Within `{drupal-root}/themes/particle/` run:

    ```bash
    npm install
    npm run setup
    npm run build:drupal
    ```

This will compile all assets and provide all namespaced Twig paths to the Drupal theme. Make sure to choose this theme in Drupal Appearance settings and `drush cr ` or `drupal cr all` to clear cache.

For rapid, development-mode recompile and Drupal cache clear, edit `webpack.drupal.dev.js`, find the `onBuildEnd` plugin and edit it from:

```js
// ORIGINAL
plugins: [
  new WebpackShellPlugin({
    onBuildEnd: [
      // CHANGE THE FOLLOWING LINE
      'echo \nWebpack drupal dev build complete! Edit apps/drupal/webpack.drupal.dev.js to replace this line with `drupal cr all` now.',
    ],
    dev: false, // Runs on EVERY rebuild
  }),
],
```

to:

```js
// UPDATED
plugins: [
  new WebpackShellPlugin({
    onBuildEnd: [
      'drupal cr all',
    ],
    dev: false, // Runs on EVERY rebuild
  }),
],
```

Now you have active Drupal development-mode compilation and cache clearing by just running:

```bash
npm run dev:drupal
```

You can still work in Pattern Lab while also working in Drupal by also running in another terminal:

```bash
npm start
```

Just like in the regular Quickstart, when Webpack output appears, visit [http://0.0.0.0/pl](http://0.0.0.0/pl) (or [http://localhost/pl](http://localhost/pl)) to immediately start building and previewing your design system in Pattern Lab.
