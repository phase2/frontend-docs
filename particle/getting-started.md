---
description: Everything needed to get Particle installed and running.
---

# Getting Started

## System Requirements

* [Node `^6 || ^8 || ^10`](https://nodejs.org/)
* [NPM `^5.2 || ^6`](https://www.npmjs.com/)
* [PHP `5.6 || ^7`](https://php.net/)
* [Composer `^1`](https://getcomposer.org/)

## Install System Dependencies

1. Skip steps if you already have the tools listed
2. Run `source ~/.bashrc` or `source ~/.zshrc` after each step to ensure command is registered

{% tabs %}
{% tab title="OSX" %}
### Install [Homebrew](https://brew.sh/)​

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Update Homebrew

```bash
brew update && brew upgrade
```

### Install PHP 7.2 {#install-php-7-2}

```bash
brew install php72
```

### Install Composer

```bash
brew install composer
```
{% endtab %}

{% tab title="Debian" %}

{% endtab %}

{% tab title="Windows" %}
{% hint style="success" %}
All Windows instructions are for WSL \("Bash on Ubuntu on Windows"\).
{% endhint %}
{% endtab %}
{% endtabs %}

### Install NVM

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

### Install Node 10

{% hint style="warning" %}
This sets the system-wide Node to v10.
{% endhint %}

```bash
nvm install v10 && nvm alias default v10
```

### Install NPM

```bash
npm install -g npm@latest
```

### Install Particle

{% tabs %}
{% tab title="Via script" %}
```bash
npx phase2/create-particle particle && cd particle
```
{% endtab %}

{% tab title="Via clone" %}
```bash
git clone git@github.com:phase2/particle.git && cd particle
```
{% endtab %}
{% endtabs %}

### Install Particle Dependencies

{% hint style="info" %}
Run this at the start of a project and any time `package.json changes.`
{% endhint %}

```bash
npm install && npm run setup
```

### Start Particle

```bash
npm start
```

