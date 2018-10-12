# Getting Started

## System Requirements

* [Node `^6 || ^8 || ^10`](https://nodejs.org/)
* [NPM `^5.2 || ^6`](https://www.npmjs.com/)
* [PHP `5.6 || ^7`](https://php.net/)
* [Composer `^1`](https://getcomposer.org/)

## Install System Dependencies

{% hint style="success" %}
Skip to installing Particle if you already have Node, NPM, PHP, and Composer installed.
{% endhint %}

Run `source ~/.bashrc` or `source ~/.zshrc` after each step to ensure command is registered

### OS-specific Instructions

{% tabs %}
{% tab title="macOS" %}
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

## Install Particle

{% tabs %}
{% tab title="Via NPM" %}
```bash
npm create @phase2/particle particle && cd particle
```
{% endtab %}

{% tab title="Via Git" %}
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

### Open Particle

Simply visit [http://0.0.0.0:8080/pl](http://0.0.0.0:8080/pl) or [http://localhost:8080/pl](http://localhost:8080/pl) and start editing files!



