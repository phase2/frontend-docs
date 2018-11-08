# Approach

## Assets

### Font Icons

Useful for small, frequently used icons that are a single color which is changeable via CSS.

1. Place your SVG in `source/_patterns/01-atoms/icon/svg/`
2. Start up active server with `npm start` or compile via `npm run compile:pl|drupal`
3. View new font icon demo page in Pattern Lab at [Atoms &gt; Icon &gt; Icons](http://localhost:8080/pl/?p=atoms-icons)
4. Use either way:
   * HTML class: `icon--filename`
   * Sass Mixin: `@include icon(filename)`

{% hint style="info" %}
Font icons are only compiled at the start of a webpack build. The Webpack dev server will have to be restarted to see new icons appear in the font.
{% endhint %}

### Inline SVG

Useful for larger, less frequently used vector images that potentially could be multi-color or able to animate.

1. Place your SVG within a namespaced folder, like `source/_patterns/01-atoms/icon/svg/`.
2. Use the special `_svg.twig` pattern to inline it completely. For instance, using the path in step 1, include it like so: `twig {% include '@atoms/image/_svg.twig' with { svgpath: '@atoms/icon/svg/file.svg', } %}`
   * OR just use the [`source`](https://twig.symfony.com/doc/2.x/functions/source.html) function provided by Twig: `{{ source('@atoms/icon/svg/file.svg') }}`

### Static images

If your component uses a static image and you need it to be available for the final bundled output, you **must** import it in the dependency chain. In your component's `index.js`, remember to `@import 'path/to/static-image.png';`! A component should import _every_ asset that it uses. This ensures that webpack bundles all necessary production assets into the correct location in the dist folder, and correctly lines up the filepaths.

This is also how demo patterns consumed by Pattern Lab get any local static images. Importing images in `a-component/demo/index.js` will ensure that they are available for Pattern Lab's demo without junking up the overall production bundle. See `source/_patterns/01-atoms/image/demo/index.js` for an example.

## JavaScript

All JavaScript should be written in ES6 \(ES2015\) according to the [AirBnB JavaScript Style Guide](https://github.com/airbnb/javascript). Webpack will use Babel to transpile all JavaScript back to ES5 in emitted bundles.

@todo: add tips on how to code in PL and others.

### Breakpoints and Enquire.JS

Particle includes the Enquire.JS library for Javascript-enabled breakpoint matching. Read more about how Enquire works [here](http://wicky.nillia.ms/enquire.js/), but the basics are as follows:

* JS breakpoints are _automatically pulled in_ from the `$grid-breakpoints` variable, which you can define in `/00-protons/non-printing/_bootstrap-overrides.scss`.
* By Bootstrap default, breakpoints are created to match the following:
  ```
  xs: 0,
  sm: 600px,
  md: 768px,
  lg: 992px,
  xl: 1200px
  ```
* Before breakpoints in JS can be used, you must import the following into your JS script:
  ```
  import { mediaBreakpoint, breakpoints } from 'breakpoints';
  ```
  * `mediaBreakpoint.up(width)` returns a media query that matches all screens _above_ a certain width, such that `mediabrekpoint.up(1200px)` would return a media query for all screens over 1200px wide.
  * `mediabreakpoint.down(width)` returns a media query that matches all screens _below_ a certain width.
  * `breakpoints` houses all of the breakpoints as defined in `_bootstrap-overrides.scss`, assigned by key. so `breakpoints.sm` would return `600px`.
* Now simply register .match or .unmatch properties to a certain breakpoint!
  ```
  enquire.register(mediaBreakpoint.down(breakpoints.lg), {
    match: () => {
      console.log('Screen is below Large sized.');
    },
    unmatch: () => {
      console.log('Screen is above Large sized.');
    },
  });
  ```
  By assigning a "down" breakpoint, we can create behaviors that occur when that down behavior is matched, and then undo those behaviors when it's unmatched.
* You can see this example in `protons/utilities/breakdown/__tests__/breakpoints.test.js`.

## Sass

### Printing vs Non-printing

Particle makes a very clear distinction between _printing_ and _non-printing_ Sass in components.

> Printing Sass generates actual, rendered CSS output.

This results in rendered CSS:

```css
.thing {
  background: blue;
}
```

> Non-printing Sass results in no CSS

This won't output any CSS:

```css
$rando-var: 33px;
@mixin doThing() {
  background: blue;
}
```

There is a distinct role for each in the component system of Particle. In the `button` component featured above in [Anatomy of a Component](https://phase2.github.io/frontend-docs/architecture/components/#anatomy-of-a-component), note this import:

```javascript
// /source/_patterns/01-atoms/button/_index.js
...
import './_button.scss';
...
```

When `_button.scss` is loaded in, the Sass loader brings the `/source/_patterns/00-protons/_variables.scss` file with it, ensuring that the required functions and variables are already available. This approach to component styes allows sharing non-printing Sass **configuration**, while also ensuring our component prints its custom CSS exactly once. We can now safely `@import 'atoms/button;` anywhere in our other JavaScript components as many times as needed and there will be no duplicate CSS output for buttons!

### BEM

This is not enforced due to the difficult linting process involved, but we strongly encourage the use of [BEM syntax](http://getbem.com/introduction/) for your markup and stylesheets.

### Style Rules

Our in-house code style rules are designed for readability and avoiding [specificity wars](http://www.standardista.com/css3/css-specificity/) as much as possible.

## Twig

Most of the design system lives in the source folders from `00-protons` to `03-organisms`. The next two folders in source are also part of the design system, but tend to get structured slightly differently than the rest here at Phase2.

### Templates

Templates are meant to be leaner. They may or may not be used explicitly by templates in Drupal and elsewhere, but they provide guidance for where classes need to be applied, and a reliable mock for Pattern Lab.

### Pages

Pages are treated purely as _demo_ patterns. They are used _solely_ by Pattern Lab to mock up working designs prior/in parallel to Drupal entities being constructed. They _use_ the template patterns for structure, and import their own demo images that are not included in the overall design system's dependency chain. You'll notice by default, there are no individual page "components", everything lives comfortably inside a /demo/ folder.

This is one reason that the static Pattern Lab bundle is so much larger than other production app bundles -- it explicitly includes the full `demoPages` item, as part of the demo glob inside of `apps/pl/index.js`.

This split is the reason there are no demo folders inside of individual template components. Pages is a conglomeration of all template demos.
