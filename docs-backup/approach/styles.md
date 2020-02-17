## Sass

Particle makes a very clear distinction between *printing* and *non-printing* Sass in components.

> Printing Sass generates actual, rendered CSS output.

This results in rendered CSS:

```scss
.thing {
  background: blue;
}
```

> Non-printing Sass results in no CSS

This won't output any CSS:

```scss
$rando-var: 33px;
@mixin doThing() {
  background: blue;
}
```

There is a distinct role for each in the component system of Particle. In the `button` component featured above in [Anatomy of a Component](/architecture/components/#anatomy-of-a-component), note this import:

```javascript
// source/_patterns/01-atoms/button/_index.js
...
import './_button.scss';
...

```

Looking into `source/_patterns/01-atoms/button/_button.scss` reveals:

```scss
@import '../../00-protons/config'; // DOES NOT OUTPUT CSS!

$btn-border-radius: 0.25rem;
@import "~bootstrap/scss/buttons"; // OUTPUTS CSS!

.custom-class {
  color: red;    // OUTPUTS CSS!
}
```

This approach to component styes allows sharing non-printing Sass **configuration**, while also ensuring our component prints its custom CSS exactly once. We can now safely `@import 'atoms/button;` anywhere in our other javascript components as many times as needed and there will be no duplicate CSS output for buttons!



# BEM
This is not enforced, because it would be hellish to lint for... but we strongly encourage the use of [BEM syntax](http://getbem.com/introduction/) for your markup and stylesheets. 

# Style Rules
Our in-house code style rules are designed for readability and avoiding [specificity wars](http://www.standardista.com/css3/css-specificity/) as much as possible.