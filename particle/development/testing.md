# Testing

Particle provides the starting point for various types of testing. Tests are located under the tools directory:

```text
# ./particle/
.
├── tools/
│   └── tests/
│   │   └── accessibility/
│   │   └── unit/
│   │   └── vrt/
│   └── ...
└── ...
```

## Unit Testing

Particle provides unit testing using [Jest](https://facebook.github.io/jest/docs/en/tutorial-jquery.html).
Simply run the following to run Jest tests against the design system:

```bash
npm run test:unit
```

Note the `__tests__` folders within components for examples.

When using the new component generator \(`npm run new`\), a basic test will be generated for you. This initial test checks that it is correctly registered in the design system.

## Accessibility Testing

To run [Pa11y](http://pa11y.org/) accessibility testing on Pattern Lab rendered output, first you'll need to install the pa11y npm package:

```bash
npm install pa11y
```

To save these dev dependencies to your project _permanently_, add the `save-dev` flag as follows:

```bash
npm install pa11y --save-dev
```

Then whenever you want to run your tests, simply start the local Pattern Lab dev server in one session:

```bash
npm run start
```

And the kick off the pa11y tests in another session:

```bash
npm run test:pa11y
```

See `./tools/pa11y.js` for [configuration options](https://github.com/pa11y/pa11y/tree/5.x#configuration). Note the ignore options are for example only; add your needed updates to the options object. Add additional pages to the test via the `testPaths` array.

```javascript
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

## Visual Regression Testing

Particle does not include VRT out of the box, but there are plenty of great options out there depending on your needs. Here are some of our favorites, in alphabetical order:

* [BackstopJS](https://github.com/garris/BackstopJS)
* [PhantomJS](https://github.com/ariya/phantomjs)
* [Puppeteer](https://github.com/GoogleChrome/puppeteer)
* [SlimerJS](https://github.com/laurentj/slimerjs)
* [WebdriverIO](http://webdriver.io/)
