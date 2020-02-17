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

### Start Pattern Lab

```bash
npm start
```

### Open Pattern Lab

Simply visit [http://0.0.0.0:8080/app-node-pl/pl](http://0.0.0.0:8080/app-node-pl/pl) or [http://localhost:8080/app-node-pl/pl](http://localhost:8080/app-node-pl/pl) and start editing files!