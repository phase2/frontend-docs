# Structure

The following are significant items at the root level:

    # ./
    .
    ├── apps                           # Things that use the compiled design system. Drupal theme & PL
    ├── dist                           # Bundled output: CSS, js, images, app artifacts (like PL html)
    ├── source                         # The design system. All assets compiled to dist/
    ├── tools                          # Gulp plugins and node tools
    ├── gulpfile.js                    # Defines the few tasks required in the workflow
    ├── webpack.particle.dev.js        # Shared bundle configuration for all dev entry points
    ├── webpack.particle.prod.js       # Shared bundle configuration for all prod entry points
    └── ...                            # Mostly just config

# Source structure
`source/` holds all assets for the design system and looks like this:

    # ./source/
    .
    ├── _patterns                      # All assets live within an Atomic "pattern"
    │   ├── 01-atoms                   # Twig namespace: @atoms, JS/Sass namespace: atoms
    │   │   ├── button                 # For instance, the button atom
    │   │   │    ├── __tests__         # Jest javascript unit tests
    │   │   │    ├── demo              # Patterns feature a demo folder to show implementation
    │   │   │    │   ├── index.js      # Pulls in twig, yaml, md inside demo/ so webpack is aware
    │   │   │    │   ├── buttons.twig  # Demonstrate with a plural name, visible to PL since no underscore
    │   │   │    │   └── buttons.yml   # Data provided to the demo pattern
    │   │   │    ├── _button.scss      # Most components require styles, underscore required
    │   │   │    ├── _button.twig      # The pure component template, underscore required
    │   │   │    └── index.js          # Component entry point (See "Anatomy of a Component below)
    │   │   └── ...                    # Other @atoms
    │   └── ...                        # @protons, @atoms, @molecules, @organisms, @templates, @pages
    └── design-system.js               # The ultimate importer/exporter of the design system pieces

>The design system is *consumed by* "apps". The three apps included are a Drupal theme, Grav theme, and a Pattern Lab installation.

# App structure
`apps/pl/` holds the *entry point* for all Pattern Lab assets, as well as the PHP engine:

    # ./app/pl/
    .
    ├── pattern-lab/                   # Holds the Pattern Lab installation
    │   ├── ...                        # composer.json, config, console php, ...
    ├── scss                           # PL-only Sass; styles that shoudln't junk up the design system
    │   ├── _scss2json.scss            # Output certain Sass variables into json for demo in PL
    │   └── _styleguide.scss           # Custom PL UI styles
    ├── demo                           # Holds things related to just "demos" for the design system
    │   └── demos.glob                 # Special file used by webpack to "glob" all demos within source/
    ├── webpack.pl.shared.js           # Webpack config shared between PL dev and PL prod
    ├── webpack.pl.dev.js              # Webpack config unique to dev, or that overrides shared
    ├── webpack.pl.prod.js             # Webpack config unique to prod, or that overrides shared
    └── index.js                       # Imports and applies the design system to a bundle for PL

`apps/drupal/` holds the *entry point* for all Drupal 8 theme assets, as well as templates, yml, etc:

    # ./app/drupal/
    .
    ├── scss/                          # Theme-only Sass, tweaks to Drupalisms that need not be in the DS
    │   └── _drupal-styles.scss        # Add more drupal styles here, like _views.scss, _field.scss etc
    ├── templates                      # Templates integrate Drupal data with design system patterns
    │   ├── block.html.twig            # Example Drupal template integrating, say @molecules/_card.twig
    │   └── ...                        # There wil be many Drupal templates
    ├── index.js                       # Imports and applies the design system to a bundle for Drupal
    ├── particle.info.yml              # Theme information. DS namespaces are auto-injected!
    ├── particle.libraries.yml         # The output js and css bundles are included here
    ├── particle.theme                 # Drupal preprocess functions
    ├── webpack.drupal.shared.js       # Webpack config shared between drupal dev and drupal prod
    ├── webpack.drupal.dev.js          # Webpack config unique to dev, or that overrides shared
    ├── webpack.drupal.prod.js         # Webpack config unique to prod, or that overrides shared
    └── index.js                       # Imports and applies the design system to a bundle for Drupal