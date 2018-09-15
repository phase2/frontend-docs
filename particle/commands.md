---
description: >-
  Particle features a lot of commands to help all aspects of frontend
  development.
---

# Commands

Start the local webpack-dev-server for Pattern Lab, hot-reload all frontend assets, automatically recompile all assets and Pattern Lab on file change.

```bash
npm start
```

Start file watchers and compile assets to disk for Drupal on changes.

```bash
npm run dev:drupal
```

Compile production assets for Pattern Lab \(e.g. for a static file host\):

```bash
npm run build:pl
```

Compile production assets for Drupal

```bash
npm run build:drupal
```

Reinstall and setup Pattern Lab

```bash
npm run setup
```

Run all linters:

```bash
npm run lint
```

Run only Javascript linters:

```bash
npm run lint:js
```

Run only Sass linters:

```bash
npm run lint:scss
```

Run all tests:

```bash
npm test
```

Run only unit test:

```bash
npm run test:unit
```

Run only pa11y accessibility tests:

```bash
npm run test:pa11y
```

Run Yeoman generator to make new component:

```bash
npm run new
```

Run any Gulp task:

```bash
# See gulpfile.js for gulp tasks
npx gulp gulpTaskName
# For instance, running a full Pattern Lab compile
npx gulp compile:pl
```

