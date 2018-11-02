# Coding and Linting

## Editor Setup

Install an [EditorConfig](http://editorconfig.org/) plugin for Particle coding conventions.

* [Atom](https://github.com/sindresorhus/atom-editorconfig)
* [JetBrains \(\*Storm\)](https://plugins.jetbrains.com/plugin/7294-editorconfig)
* [Sublime Text](https://github.com/sindresorhus/editorconfig-sublime)
* [VSCode](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)

## Linting

> "It's going to hurt your feelings."

{% hint style="info" %}
Both linters can be disabled per-line, per-section, and/or per-file if need be. Check their respective docs for more info.
{% endhint %}

### Javascript Linting

JavaScript linting generally follows the AirBnB standards, with some extras to help out Webpack and Jest. To make changes to the default rules, edit `.eslintrc.js`

[ESlint docs](http://eslint.org/docs/rules/)

### Style Linting

Sass linting defaults to Phase2's blend of sane house rules, but can be edited to whatever your project requires. To make changes to the default rules, edit `.stylelintrc`

[stylelint docs](http://stylelint.io/user-guide/)

