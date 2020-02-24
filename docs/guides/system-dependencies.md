# Install System Dependencies

!> Looking for how to install [Install Particle](particle/getting-started.md) instead?

Run `source ~/.bashrc` or `source ~/.zshrc` after each step to ensure command is registered

## Install PHP

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

## Install NVM

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

## Install Node 10

!> This sets the system-wide Node to v10.

```bash
nvm install v10 && nvm alias default v10
```

## Install NPM

```bash
npm install -g npm@latest
```