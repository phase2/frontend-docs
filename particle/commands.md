# Commands

## Start a Server

Start the local Webpack dev server for Pattern Lab, hot-reload all frontend assets, and automatically recompile all assets and Pattern Lab on file change

```bash
npm start
```

Start file watchers and compile assets to disk for Drupal on changes

```bash
npm run dev:drupal
```

Start file watchers and compile assets to disk for Grav on changes

```bash
npm run dev:grav
```

## Compile Assets

Compile production assets for Drupal

```bash
npm run build:drupal
```

Compile production assets for Grav

```bash
npm run build:grav
```

Compile production assets for Pattern Lab \(e.g. for a static file host\)

```bash
npm run build:pl
```

## Code Formatting

Lint and Prettier both JavaScript and Sass

```bash
npm run fmt
```

Lint and Prettier only JavaScript

```bash
npm run fmt:js
```

Lint and Prettier only Sass

```bash
npm run fmt:scss
```

## Code Linting

Run all linters:

```bash
npm run lint
```

Run only Javascript linters

```bash
npm run lint:js
```

Run only Sass linters

```bash
npm run lint:scss
```

Run only Twig linters

```bash
npm run lint:twig
```

Run only Twig linters for Drupal

```bash
npm run lint:twig:drupal
```

Run only Twig linters for Grav

```bash
npm run lint:twig:grav
```

Run only Twig linters for Pattern Lab

```bash
npm run lint:twig:source
```

## Automated Testing

Run all tests:

```bash
npm test
```

Run only Pa11y accessibility tests

```bash
npm run test:pa11y
```

Run only unit tests
```bash
npm run test:unit
```

## Additional Commands

Run any Gulp task:

```bash
# See gulpfile.js for gulp tasks
npx gulp gulpTaskName
# For instance, running a full Pattern Lab compile
npx gulp compile:pl
```

Run Yeoman generator to make new component

```bash
npm run new
```

Reinstall and setup Pattern Lab

```bash
npm run setup
```