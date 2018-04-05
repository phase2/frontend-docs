### Font Icons

Useful for small, frequently used icons that are a single color which is changeable via CSS.

1. Place `filename.svg` in `source/_patterns/01-atoms/icon/svg/`
1. Start up active server with `npm start` or compile via `npm run compile:pl|drupal`
1. View new font icon demo page in Pattern Lab at [Atoms > Icon > Icons](http://localhost:8080/pl/?p=atoms-icons)
1. Use either way:
    - HTML class: `icon--filename`
    - Sass Mixin: `@include icon(filename)`

> IMPORTANT: Font icons are only compiled at the start of a webpack build. The webpack dev server will have to be restarted to see new icons appear in the font.

#### Inline SVG

Useful for larger, less frequently used vector images that potentially could be multi-color or able to animate.

1. Place `file.svg` within a namespaced folder, like `source/_patterns/01-atoms/icon/svg/`.
1. Use the special `_svg.twig` pattern to inline it completely. For instance, using the path in step 1, include it like so:
    ```twig
    {% include '@atoms/image/_svg.twig' with {
      svgpath: '@atoms/icon/svg/file.svg',
    } %}
    ```
1. OR just use the [`source`](https://twig.symfony.com/doc/2.x/functions/source.html) function provided by Twig: `{{ source('@atoms/icon/svg/file.svg') }}`

### Static images

If your component uses a static image and you need it to be available for the final bundled output, you **must** import it in the dependency chain. In your component's `index.js`, remember to `@import 'path/to/static-image.png';`! A component should import _every_ asset that it uses. This ensures that webpack bundles all necessary production assets into the correct location in the dist folder, and correctly lines up the filepaths.


This is also how demo patterns consumed by Pattern Lab get any local static images. Importing images in `a-component/demo/index.js` will ensure that they are available for Pattern Lab's demo without junking up the overall production bundle. See `source/_patterns/01-atoms/image/demo/index.js` for an example.
