# Getting Started

?> Need to install [Node, NPM, or PHP](guides/system-dependencies.md)?

## Particle

### Install Particle

<!-- tabs:start -->

#### ** Via NPM **

This is the recommended method, as it pulls the latest tagged release.

```bash
npm create @phase2/particle particle && cd particle
```

#### ** Via Git **

This simply clones the `master` branch, which is in active development.

```bash
git clone git@github.com:phase2/particle.git && cd particle
```

<!-- tabs:end -->

## Install Particle Dependencies

!> Run this at the start of a project and any time `package.json changes.`

```bash
npm install
```

## Pattern Lab

Pattern Lab is used to rapidly build out components and prototype.

### Setup

The following command scaffolds out a starting Pattern Lab folder structure within `apps/node-pl`. It should only need to be run once, though it's safe to run multiple times.

```bash
npm run setup
```

### Development mode

Run the following command to open Pattern Lab in "hot reloading" mode to rapidly develop design systems:

```bash
npm start
```

Simply visit [http://0.0.0.0:8080/app-node-pl/pl](http://0.0.0.0:8080/app-node-pl/pl) or [http://localhost:8080/app-node-pl/pl](http://localhost:8080/app-node-pl/pl) and start editing files!

### Production mode

Pattern Lab can also compile completely to assets written to disk for static file hosting (e.g. Apache/Nginx). Run the following:

```bash
npm run build:pl
```

Then feel free to point a domain at `dist/app-node-pl/` as a companion "Design" url beside your main development site! For example, if you're building a site at `www.mysite.com`, you could make a subdomain `design.mysite.com` which serves from `dist/app-node-pl/` and resulting in your Pattern Lab being accessible via `design.mysite.com/pl/`.

## Drupal 8

Particle provides a Drupal 8 theme, although the starting steps are slightly different:

### Setup

1. [Install the latest release](#install-particle)
1. [Install dependencies](#install-particle-dependencies)
1. Ensure the `particle/` folder is directly under `themes/` at the root of your Drupal 8 install. \(i.e. Particle's README should be at `{drupal-root}/themes/particle/README.md`\)
1. Download and install the [Component Libraries module](https://www.drupal.org/project/components):

   ```bash
   drush dl components drush en components -y
   ```

   or

   ```bash
   drupal module:install components
   ```


### Development mode

Run the following watch command for unoptimized assets and Twig files to export to `dist/app-drupal` **on every file change**:

```bash
npm run dev:drupal
```

Then ensure Drupal's development `settings.php` includes at least:

```php
$config['system.performance']['css']['preprocess'] = FALSE;
$config['system.performance']['js']['preprocess'] = FALSE;
$config['system.performance']['cache.page.max_age'] = 0;
```

And Drupal's `development.services.yml` includes at least: 

```yaml
parameters:
  http.response.debug_cacheability_headers: true
  twig.config:
    debug: true
    cache: false
services:
  cache.backend.null:
    class: Drupal\Core\Cache\NullBackendFactory
```

### Production mode

Run the following for optimized assets and Twig files exported to `dist/app-drupal/`:

```bash
npm run build:drupal
````

This will compile all assets and provide all namespaced Twig paths to the Drupal theme. Make sure to choose this theme in Drupal Appearance settings and `drush cr` or `drupal cr all` to clear cache.


### Drupal + Pattern Lab

You can still work in Pattern Lab while also working in Drupal by also running in another terminal:

```bash
npm start
```

Just like the Pattern Lab [Getting Started](#pattern-lab), when Webpack output appears, visit [http://0.0.0.0:8080/app-node-pl/pl](http://0.0.0.0:8080/app-node-pl/pl) or [http://localhost:8080/app-node-pl/pl](http://localhost:8080/app-node-pl/pl) to immediately start building and previewing your design system in Pattern Lab, while all assets are being compiled to your Drupal theme.

For more information on developing Drupal alongside Particle, check the [Drupal section of Apps](/particle/apps.md#drupal).

