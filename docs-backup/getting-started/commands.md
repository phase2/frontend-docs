Start up watches and a local server for Pattern Lab in dev mode. All assets will be served very fast from memory:

```bash
npm start # An alias for npm run dev:pl
```

Start up watches and compile assets to disk for Drupal on changes (see above for enabling Drupal cache clears as part of this):

```bash
npm run dev:drupal
```

Compile production assets for Pattern Lab (e.g. for a static file host):

```bash
npm run build:pl
```

Compile production assets for Drupal

```bash
npm run build:drupal
```

Compile production assets for Grav

```bash
npm run build:grav
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
npm run gulp -- gulpTaskName
# For instance, running a full Pattern Lab compile
npm run gulp -- compile
```