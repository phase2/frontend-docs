Particle provides the starting point for various types of testing. Tests are located under the tools directory:

    # ./particle/
    .
    ├── tools/
    │   ├── tasks/
    │   └── tests/
    │   │   └── accessibility/
    │   │   └── unit/
    │   │   └── vrt/
    │   └── ...
    └── ...

# Accessibility Testing

To run [pa11y](http://pa11y.org/) accessibility testing on Pattern Lab rendered output, first you'll need to install the pa11y npm package:

```bash
npm install pa11y@5.0.0-beta.7 pa11y-reporter-cli
```

To save these devDependencies to your project *permanently*, run the following instead:

```bash
npm install --save-dev pa11y@5.0.0-beta.7 pa11y-reporter-cli
```

Then whenever you want to run your tests, simply start the local Pattern Lab dev server in one session:

```bash
npm run start
```

And the kick off the pa11y tests in another session:

```bash
npm run test:pa11y
```

See `./tools/pa11y.js` for configuration [options](https://github.com/pa11y/pa11y/tree/5.x#configuration). Note the ignore options are for example only, add your needed updates to the options object. Add additional pages to the test via the `testPaths` array.

```js
const options = {
  standard: 'WCAG2AAA',
  ignore: [
    'WCAG2AAA.Principle3.Guideline3_1.3_1_1.H57.2',
  ],
  log: {
    debug: console.log,
    error: console.error,
    info: console.log,
  },
};
```

If Docker is part of your stack, you may want to try [docker-pa11y](https://github.com/phase2/docker-pa11y), which simplifies a large chunk of the above, and keeps everything neatly containerized. Just saying.

# Unit Testing

Particle provides unit testing as well using [Jest](https://facebook.github.io/jest/docs/en/tutorial-jquery.html).

Simply run the following to run Jest tests against the design system:

```js
npm run test:unit
```

Note the `__tests__` folders within components for examples.

# Visual Regression Testing

Particle does not currently include any VRT tools by default, but we're big fans. Hopefully coming soon.