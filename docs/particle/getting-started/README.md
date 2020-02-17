# Getting Started

## System Requirements

* [Node `^8 || ^10`](https://nodejs.org/)
* [NPM `^5.2 || ^6`](https://www.npmjs.com/)
* [PHP `^7`](https://php.net/)

## Install System Dependencies

{% hint style="success" %}
Skip to installing Particle if you already have Node, NPM, PHP installed.
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

### Install PHP 7.2  <a id="install-php-7-2"></a>

```bash
brew install php72
```
{% endtab %}

{% tab title="Windows" %}
{% hint style="success" %}
Use WSL \("Bash on Ubuntu on Windows"\), then follow the Debian instructions.
{% endhint %}
{% endtab %}

{% tab title="Debian" %}
{% hint style="info" %}
This guide also works on Debian-based distros like Ubuntu, Mint, etc.
{% endhint %}

### Update APT

```bash
sudo apt-get update && apt-get upgrade
```

### Install PHP 7.2

```bash
sudo apt-get install php7.2 php7.2-common
```
{% endtab %}
{% endtabs %}

### Install NVM

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
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

