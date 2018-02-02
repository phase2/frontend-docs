
# Opinionated?

While particle does not care *what* application ultimately consumes your design system, it does care about how that design system is written. Particularly when it comes to linting. **The linting will hurt your feelings**.

 ESLint and Stylelint are baked into our webpack buildchain, and they look for:
 
 + Modern ES6 javascript, linted based on Airbnb's [mostly reasonable standards](https://github.com/airbnb/javascript), 
 + An in-house blend of CSS/Sass rules designed to keep Sass stylesheets sane and easy to manage.
 
 Both of these linters' rulesets can be overridden or tweaked to a project's needs in their respective .rc files.
 
 We also heavily encourage using [BEM syntax](http://getbem.com/introduction/) for your HTML/Sass. This is not enforced by anything, but we find that BEM syntax plays very nicely with Atomic Design concepts, and generally makes for clean Sass stylesheets. In the original spirit of [Pattern Lab](http://patternlab.io/), Particle is app and language agnostic-- feel free to use it in whatever manner makes sense for your project.