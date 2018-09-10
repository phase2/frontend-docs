---
description: Everything needed to get Particle installed.
---

# Getting Started

## System Dependencies

1. Skip steps if you already have the tools listed
2. Run `source ~/.bashrc` or `source ~/.zshrc` after each step to ensure command is registered

### Install [Homebrew](https://brew.sh/)

{% hint style="warning" %}
Homebrew is OSX-only. Instructions for Ubuntu/[WSL](http://wsl-guide.org/en/latest/installation.html) coming soon.
{% endhint %}

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Update Homebrew-installed packages

```bash
brew update && brew upgrade
```

### Install PHP 7.2

```bash
brew install php72
```



