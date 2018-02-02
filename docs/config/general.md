A small `config.js` file at the root of the project provides basic path settings. Developers are encouraged to edit the Gulp and Webpack files directly to suit their needs.

`package.json` contains all the usual things. It's worth familiarizing yourself with the different commands that can be run related to compiling different apps, linting, testing, and the like. There are gulp wrappers for some of them. `package.json` also contains the browserslist config for the autoprefixr plugin defined and used in the `webpack.shared.config.js` (I know, I know, it's just how life is sometimes). This can easily be adjusted to support an ancient iPad Air running Safari 7, if that's what the client orders.

`.babelrc` contains the Babel settings used by Webpack. 

`jest.config.js` contains settings for JS unit tests for components.

`.editorconfig` contains Particle coding conventions. Install an [EditorConfig](http://editorconfig.org/) plugin for Particle coding conventions.