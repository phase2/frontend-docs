# Webpack

[Webpack](https://webpack.js.org/) is a bundling tool to help handle the various assets of the project in a build step. It accepts one or more entry points and then tracks their various dependencies recursively to assemble the dependency graph. This dependency chain allows us to readily include files to be emitted to the built assets of the project. TheWebpack configuration in Particle has been set up to handle commonly used file types such as: Twig, Sass, JavaScript, TypeScript, SVGs, image assets, and more.

## The Inheritance model of Particle's webpack config

Particle utilizes a multi-level inheritance model for it's various configurations. This allows the configuration to be extensible across multiple applications as well as multiple design systems. Configuration objects are merged together from generic to most specific.

*Root webpack config*: The root `webpack.config.js` file contains the base configuration and loaders that most applications and design systems share. This includes laoders for: Vue, Sass/CSS, image and other file assets, JavaScript, TypeScript, and Twig. Stylesheets also are passed through PostCSS which uses the `.browserslistrc` file to autoprefix CSS attributes as well as minify CSS in production. This is the base configuration that all other configurations extend from.

*Design system config*: Each design system has it's own configuration object which is merged onto the root webpack config. This config generally sets three items which are used throughout the implementation of the specific design system. The first config item is the ability to generate JSON from the design system's Sass variables as well as the includePaths for Sass to import other components. This config also initializes the SVGSpritemapPlugin with the path to SVGs and some basic options. This plugin creates Sass mixins to include SVG icons as well as a spritesheet of SVG assets. For a detailed list of how Particle handles SVGs, check out the Atoms > Svgicon page in Pattern Lab. Finally, this config imports the namespaces of the project and adds them to Webpack's alias resolver. This enables shorter imports such as `import thing from 'atoms/thing';`.

*App specific config*: 

## Understanding CSS Modes

## JavaScript polyfill

Babel transpiles JavaScript during the build process to convert from newer ES6+ syntax to ES5 syntax that browsers can process. Particle also ships with the Babel polyfill on production builds. This covers changes to the actual language which may not exist in older browsers. For example, the `fetch` protocol is a relatively recent addition and does not exist on certain versions of IE. In order for the code to function properly a polyfill must be used to bridge that functionality. Babel's polyfill reads from the `.browserslistrc` file to only polyfill the features that are needed for the targeted browsers.

## Analyze your bundle

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

