While particle does not care *what* application ultimately consumes your design system, out of the box it does care about how that design system is written. Particularly when it comes to linting. **The linting should hurt your feelings**.

## Javascript
All javascript should be written in ES6 (ES2015) according to the [AirBnB JavaScript Style Guide](https://github.com/airbnb/javascript). Webpack will use Babel to transpile all javascript back to ES5 in emitted bundles.

To adjust the default rules edit `.eslintrc.js`

## Sass
[Stylelint](https://stylelint.io/user-guide) is included as part of our webpack buildchain. 
 
To adjust the default rules edit `.stylelintrc`
 
## Twig 
A Twig linter is not currently included in the Particle toolchain, but we recommend following the official [Twig standards](https://twig.symfony.com/doc/2.x/coding_standards.html).

## Other
We also heavily encourage using [BEM syntax](http://getbem.com/introduction/) for your HTML/Sass. This is not enforced, but we find that BEM syntax plays very nicely with Atomic Design concepts and generally makes for cleaner, more maintainable stylesheets. 
