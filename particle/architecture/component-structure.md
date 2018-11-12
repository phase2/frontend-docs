# Component Structure

## Generating a Component

Components have a specific file structure. Instead of making a developer create all required files by hand, we use a [Yeoman](http://yeoman.io/) generator to easily create new component folders by running the following command:

```text
npm run new
```

Follow the onscreen prompts for the location, included files, and name of the new component.

## Anatomy of a Component

All components require a set of files:

```text
# ./source/_patterns/01-atoms/button/
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
# ./source/_patterns/01-atoms/button/
.
├── __test__                        # Jest unit tests. Read automatically during "npm run test:unit"
│   └── button.test.js              # Unit test JS functions. Limited DOM manipulation
├── ...
```

## Importing Assets

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

## Using Demos

Every component has an optional demo folder, which is automatically pulled into Pattern Lab. These files are not built to destination apps at all, so you should never do work in them that you expect to see in a final product.

The Yeoman generator creates four files by default in this folder, which describe the general Phase2 way to demonstrate how to use a new component:

### index.js
Describes to Webpack the files to include when generating the Pattern Lab demos. This most likely will only need to be touched when you are creating multiple demo pages for a single component.

### component.twig
This should serve as an example twig file that shows an inclusion of the new pattern, placed with example variables and layouts so that it will appear like an intended component when viewed in the demos.

The default .twig file places a standard Twig-style `include` of your new component, but you can (and should) modify this page to meet your design system better. Look at the default patters for good examples of how to create a demo template.

### component.md
An additional readme that may describe how to use your demo, its implications, or others. By default the variables that a component requires are often documented here, in addition to in the component's _component.twig file.

### component.yml
An optional way to override the data in `/_data/data.yml`, to display something specific in your demo. These data structures are only included in their respective page's demos when rendering the demo's template, so they are safely separated from other pattern demos.

**Note:** If you would like to create demo data to be global between all patterns, add the variables to `/_data/data.yml`.

For more information about how Pattern Lab expects variables to be added for use in patterns, see the [Pattern](https://patternlab.io/docs/data-overview.html) Lab docs.
