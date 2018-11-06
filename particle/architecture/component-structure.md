# Component Structure

## Generating a Component

Components have a specific file structure. Instead of making a developer create all required files by hand, we use a [Yeoman](http://yeoman.io/) generator to easily create new component folders by running the following command:

```text
npm run new
```

Follow the onscreen prompts for the location, included files, and name of the new component.

### Versions Prior to v10.1.0

**Then make sure you edit `source/design-system.js` and add your new component.** Versions after this should update next time you build.

## Anatomy of a Component

All components require a set of files:

```text
# ./source/{design-system}/_patterns/01-atoms/button/
.
├── demo                            # Demo implementations; can be removed on deploy to prod
│   ├── index.js                    # Pulls in Twig, YAML, MD inside demo/ so Webpack is aware
│   ├── buttons.md                  # Markdown with extra notes, visible in PL UI
│   ├── buttons.twig                # Demonstrate with a plural name, visible to PL since no underscore
│   └── buttons.yml                 # Data provided to the demo pattern
├── _button.scss                    # Most components require styles, underscore required
├── _button.twig                    # The pure component template, underscore required to hide from PL UI
└── index.js                        # Component entry point
```

Optionally, you can add a `__test__` folder to your components base directory \(note the two underscores before and after\) for Jest unit testing like so:

```text
# ./source/{design-system}/_patterns/01-atoms/button/
.
├── __test__                        # Jest unit tests. Read automatically during "npm run test:unit"
│   └── button.test.js              # Unit test JS functions. Limited DOM manipulation
├── ...
```

With the power of Webpack, all static assets a component needs are `import`ed right into the `index.js` **entry point** alongside the JavaScript methods:

```javascript
// source/_patterns/01-atoms/button/index.js

// Import *EVERY* NPM dependency.
import $ from 'jquery';
// Import specific plugins this component may need
import 'bootstrap/js/src/button';

// source/_patterns/01-atoms/00-protons/index.js
import 'protons';

// Module template. Changes to this file trigger a PL rebuild
import './_button.twig';

// Import local Sass (which in turn imports Bootstrap Sass)
import './_button.scss';

// Requirement 1 of a component: name
export const name = 'button';

// Requirement 2 of a component: disable function
export function disable() {}

// Requirement 3 of a component: enable function. `$context` is `$(document)` in PL, and `context` in Drupal
export function enable($context) {

  // `.button()` is only available because of `import 'bootstrap/js/src/button';` above
  $('#blah', $context).button('toggle');
}

// Req. 4 of a component: default export is the enable function
export default enable;
```
