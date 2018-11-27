# Webpack

[Webpack](https://webpack.js.org/) is a bundling tool to handle the various assets of the project in a build step. It accepts one or more [entry points](https://webpack.js.org/concepts/entry-points/) and then tracks their various dependencies recursively to assemble the [dependency graph](https://webpack.js.org/concepts/dependency-graph/). This dependency chain allows us to readily include files to be emitted to the built assets of the project. The Webpack configuration in Particle has been set up to handle commonly used file types such as: Twig, Sass, JavaScript, TypeScript, SVGs, image assets, and more.

## The Inheritance model of Particle's Webpack config

Particle utilizes a multi-level inheritance model for it's various configurations. This allows the configuration to be extensible across multiple applications as well as multiple design systems. Configuration objects are merged together from generic to most specific.

**Root webpack config**: The root `webpack.config.js` file contains the base configuration and [loaders](https://webpack.js.org/concepts/loaders/) that most applications and design systems share. This includes loaders for: Vue, Sass/CSS, image and other file assets, JavaScript, TypeScript, and Twig. Stylesheets also are passed through PostCSS which uses the `.browserslistrc` file to autoprefix CSS attributes as well as minify CSS in production. This is the base configuration that all other configurations extend from.

**Design system config**: Each design system has it's own configuration object which is merged onto the root webpack config. This config generally sets three items which are used throughout the implementation of the specific design system. The first config item is the ability to generate JSON from the design system's Sass variables as well as the includePaths for Sass to import other components. This config also initializes the [SVGSpritemapPlugin](https://github.com/cascornelissen/svg-spritemap-webpack-plugin) with the path to SVGs and some basic options. This plugin creates Sass mixins to include SVG icons as well as a spritesheet of SVG assets. For a detailed list of how Particle handles SVGs, check out the Atoms > Svgicon page in Pattern Lab. Finally, this config imports the namespaces of the project and adds them to Webpack's alias resolver. This enables shorter imports such as `import thing from 'atoms/thing';`.

**App specific config**: Each application contains it's own webpack configuration to specify settings needed to run it. This may include dev server settings, overrides to previously established file loaders, as well as the entry and output points for the app. Each app config has a webpack object for `shared`, `dev`, and `prod`. If there are no specific settings for one of these environments the variable is an empty object. Each app configuration exports a call to the particle function from `particle.js` to create the webpack configuration object for that application.

## Understanding CSS Modes

The particle function exported from `particle.js` also accepts a `cssMode` key on the options object. The cssMode can be set to `'hot'` or `'extract'` to alter how Webpack handles the CSS assets. If no key is passed, particle will default to extract mode. Hot mode loads the styles within the JavaScript bundle in memory and allows for hot reloading to be utilized. It is meant for fast development experiences, but should not be used in production. Extract mode emits the CSS assets as CSS files on disk. This is desirable for production environments so that JavaScript does not need to be parsed and executed to load the stylesheets. The CSS Modes option is set in each app specific config.

## JavaScript polyfill

Babel transpiles JavaScript during the build process to convert from newer ES6+ syntax to ES5 syntax that browsers can process. Particle also ships with the Babel polyfill on production builds. This covers changes to the actual language which may not exist in older browsers. For example, the `fetch` protocol is a relatively recent addition and does not exist on certain versions of IE. In order for the code to function properly a polyfill must be used to bridge that functionality. Babel's polyfill reads from the `.browserslistrc` file to only polyfill the features that are needed for the targeted browsers.

## Bundle Warnings during build

The default Particle install will emit Webpack warnings when running the `build:pl` script. These warnings are: `WARNING in asset size limit`, and `WARNING in entrypoint size limit`. The asset size limit is a result of the Font Awesome SVG map. This raw asset is tree-shaken during the build process to only utilize the icons used and referenced in the code base. The entrypoint size limit is a result of the decision to bundle everything into one entrypoint for initial install and ease of use. This can be optimized through creating multiple entry points, or code-splitting the bundle as described in the section below. Additionally, if you don't need libraries such as Vue for your application, the bundle size can be reduced by removing Vue examples from the dependency chain. These examples are located at `source/default/_patterns/02-molecules/vue-widget/`.

## Analyze your bundle

Analyzing your bundle output from Webpack allows you to utilize data visualization and inspect what comprises the bundle. This is useful for identifying potential performance bottlenecks, packages which are not [tree shaking](https://webpack.js.org/guides/tree-shaking/) properly, as well as discovering potential areas for [code splitting](https://webpack.js.org/guides/code-splitting/).

To analyze the bundle of an app, we'll generate a stats profile and then analyze it. Let's use the Pattern Lab app as an example.

First, run a full PL build \(this may take a looooong time as it uglifies the JavaScript and CSS\):

```bash
npm run build:pl
```

Then, we're going to generate a profile stats file:

```bash
NODE_ENV=production npx webpack --config apps/pl/webpack.config.js --profile --json > dist/app-pl/assets/stats.json
```

Finally, let's fire up an interactive view of our bundle:

```bash
npx webpack-bundle-analyzer dist/app-pl/assets/stats.json
```

You'll be greeted with an open browser tab featuring a visualization at [http://localhost:8888](http://localhost:8888/):

![webpack-bundle-analyzer showing stats for the default Pattern Lab app bundle](../.gitbook/assets/image.png)
