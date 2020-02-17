# Getting Started

## System Requirements

* [Node `^8 || ^10`](https://nodejs.org/)
* [NPM `^5.2 || ^6`](https://www.npmjs.com/)
* [PHP `^7`](https://php.net/)

## Install System Dependencies

!> Skip to [Install Particle](#install-particle) if you already have Node, NPM, PHP installed.

Run `source ~/.bashrc` or `source ~/.zshrc` after each step to ensure command is registered

### OS-specific Instructions

<!-- tabs:start -->

#### ** macOS **

1. Install [Homebrew](https://brew.sh/)

    ```bash
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```

1. Update Homebrew

    ```bash
    brew update && brew upgrade
    ```

1. Install PHP 7.2  <a id="install-php-7-2"></a>

    ```bash
    brew install php72
    ```

#### ** Windows **

!> Use WSL \("Bash on Ubuntu on Windows"\), then follow the Debian instructions.

#### ** Debian **
 
?> This guide also works on Debian-based distros like Ubuntu, Mint, etc.

1. Update APT

    ```bash
    sudo apt-get update && apt-get upgrade
    ```

1. Install PHP 7.2

    ```bash
    sudo apt-get install php7.2 php7.2-common
    ```

<!-- tabs:end -->

### Install NVM

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

### Install Node 10

!> This sets the system-wide Node to v10.

```bash
nvm install v10 && nvm alias default v10
```

### Install NPM

```bash
npm install -g npm@latest
```

## Install Particle

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

### Install Particle Dependencies

!> Run this at the start of a project and any time `package.json changes.`

```bash
npm install && npm run setup
```

### Start Particle

```bash
npm start
```

### Open Particle

Simply visit [http://0.0.0.0:8080/pl](http://0.0.0.0:8080/pl) or [http://localhost:8080/pl](http://localhost:8080/pl) and start editing files!

# Drupal 8

Particle provides a Drupal 8 theme, although the starting steps are slightly different:

1. [Download the latest release](https://github.com/phase2/particle/releases)
2. Extract to `themes/` at the root of your Drupal 8 install. \(i.e. this readme should be at `{drupal-root}/themes/particle/README.md`\)
3. Download and install the [Component Libraries module](https://www.drupal.org/project/components):

   `drush dl components drush en components -y`

   or

   `drupal module:install components`

4. Within `{drupal-root}/themes/particle/` run:

```bash
npm install
npm run setup
npm run build:drupal
```

This will compile all assets and provide all namespaced Twig paths to the Drupal theme. Make sure to choose this theme in Drupal Appearance settings and `drush cr` or `drupal cr all` to clear cache.

For rapid, development-mode recompile and Drupal cache clear, edit `webpack.drupal.dev.js`, find the `onBuildEnd` plugin and edit it from:

```text
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

```text
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

```text
npm run dev:drupal
```

You can still work in Pattern Lab while also working in Drupal by also running in another terminal:

```text
npm start
```

Just like in the regular Quickstart, when Webpack output appears, visit [http://0.0.0.0/pl](http://0.0.0.0/pl) \(or [http://localhost/pl](http://localhost/pl)\) to immediately start building and previewing your design system in Pattern Lab.

For more information on developing Drupal alongside Particle, check the [Drupal section of Apps](../apps/drupal.md).

