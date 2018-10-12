# Folder Structure

## General Structure {#structure}

The following are significant items at the root level:

```text
# ./
.
├── apps                           # Things that use the compiled design system (e.x. Drupal)
├── dist                           # Bundled output: CSS, JS, images, app artifacts (like PL HTML)
├── source                         # The design system. All assets compiled to dist/
└── tools                          # Gulp plugins and Node tools
```

## Source structure {#source-structure}

`source/` holds all assets for the design system and looks like this:

```text
# ./source/
.
├── _patterns                      # All assets live within an Atomic "pattern"
│   ├── 01-atoms                   # Twig namespace: @atoms, JS/Sass namespace: atoms
│   │   ├── button                 # For instance, the button atom
│   │   │    ├── __tests__         # Jest JavaScript unit tests
│   │   │    │   └── ...           #
│   │   │    ├── demo              # Patterns feature a demo folder to show implementation
│   │   │    │   ├── index.js      # Pulls in Twig, YAML, MD inside demo/ so Webpack is aware
│   │   │    │   ├── buttons.twig  # Demonstrate with a plural name, visible to PL since no underscore
│   │   │    │   └── buttons.yml   # Data provided to the demo pattern
│   │   │    ├── _button.scss      # Most components require styles, underscore required
│   │   │    ├── _button.twig      # The pure component template, underscore required
│   │   │    └── index.js          # Component entry point (See "Anatomy of a Component below)
│   │   └── ...                    # Other @atoms
│   └── ...                        # @protons, @atoms, @molecules, @organisms, @templates, @pages
└── design-system.js               # The ultimate importer/exporter of the design system pieces
```

The design system is consumed by "apps". The three apps included are a Drupal theme, Grav theme, and a Pattern Lab installation.

## App structure {#app-structure}

### Pattern Lab

`apps/pl/` holds the _entry point_ for all Pattern Lab assets, as well as the PHP engine:

```text
# ./apps/pl/
.
├── demo                           # Holds things related to just "demos" for the design system
│   └── demos.glob                 # Special file used by Webpack to "glob" all demos within source/
├── pattern-lab                    # Holds the Pattern Lab installation
│   └── ...                        # composer.json, config, console PHP, ...
├── scss                           # PL-only Sass; styles that shoudln't junk up the design system
│   ├── _scss2json.scss            # Output certain Sass variables into JSON for demo in PL
│   └── _styleguide.scss           # Custom PL UI styles
├── index.js                       # Imports and applies the design system to a bundle for PL
├── webpack.pl.dev.js              # Webpack config unique to dev, or that overrides shared
├── webpack.pl.prod.js             # Webpack config unique to prod, or that overrides shared
└── webpack.pl.shared.js           # Webpack config shared between PL dev and PL prod
```

### Drupal

`apps/drupal/` holds the _entry point_ for all Drupal 8 theme assets, as well as templates, YAML, etc:

```text
# ./app/drupal/
.
├── scss/                          # Theme-only Sass, tweaks to Drupalisms that need not be in the design system
│   └── _drupal-styles.scss        # Add more Drupal styles here, like _views.scss, _field.scss, etc.
├── templates                      # Templates integrate Drupal data with design system patterns
│   ├── block.html.twig            # Example Drupal template integrating, say @molecules/_card.twig
│   └── ...                        # There can be many Drupal templates
├── index.js                       # Imports and applies the design system to a bundle for Drupal
├── particle.info.yml              # Theme information. Design system namespaces are auto-injected!
├── particle.libraries.yml         # The output JS and CSS bundles are included here
├── particle.theme                 # Drupal preprocess functions
├── index.js                       # Imports and applies the design system to a bundle for Drupal
├── webpack.drupal.dev.js          # Webpack config unique to dev, or that overrides shared
├── webpack.drupal.prod.js         # Webpack config unique to prod, or that overrides shared
└── webpack.drupal.shared.js       # Webpack config shared between Drupal dev and Drupal prod
```

### Grav

`apps/grav/` holds the _entry point_ for all Grav theme assets, as well as templates, YAML, etc:

```text
# ./app/grav/
.
├── scss/                          # Theme-only Sass, tweaks to Grav that need not be in the design system
│   └── _grav-styles.scss          # Add more Grav styles here, like _views.scss, _field.scss, etc.
├── templates                      # Templates integrate Drupal data with design system patterns
│   ├── partials                   # Smaller template snippets for use later
│   │   └── ...                    # Headers, footers, navigation, etc.
│   ├── default.html.twig          # Example grav template integrating, say @molecules/_card.twig
│   └── ...                        # There can be many Grav templates
├── blueprints.yaml                # Grav theme information
├── index.js                       # Imports and applies the design system to a bundle for Grav
├── particle.php                   # Used by Grav for theme and plugin events
├── particle.yaml                  # Theme configuration
├── twig-namespaces.yaml           # Namespace definition
├── webpack.grav.dev.js            # Webpack config unique to dev, or that overrides shared
├── webpack.grav.prod.js           # Webpack config unique to prod, or that overrides shared
└── webpack.grav.shared.js         # Webpack config shared between Grav dev and Grav prod
```

## Atomic Design and Namespaces

"Namespaces" are simply aliases to paths on a file system. The design system within `source/` adheres strongly to [Atomic Design](http://atomicdesign.bradfrost.com/), with `@protons` added on.

| Path | Twig | Javascript | Sass |
| :--- | :--- | :--- | :--- |
| `source/_patterns/00-protons/` | `@protons` | `protons` | TBD |
| `source/_patterns/01-atoms/` | `@atoms` | `atoms` | TBD |
| `source/_patterns/02-molecules/` | `@molecules` | `molcules` | TBD |
| `source/_patterns/03-organisms/` | `@organisms` | `organisms` | TBD |
| `source/_patterns/04-templates/` | `@templates` | `templates` | TBD |
| `source/_patterns/05-pages/` | `@pages` | `pages` | TBD |

> Note: Namespaces within Sass are a work in progress!

Our reasoning for categorization of components within each is pretty close to pure [Atomic Design ](../../frontend/atomic-design.md)principals, but here's a quick explanation.

* **Protons** features Sass systems and non-consumable pattern markup. No Twig file will `@include` anything from `@protons`, but javascript and Sass will. This is a uniquely Particle convention.
* **Atoms** upward **will** be included in other Twig files.

  > "Atoms of our interfaces serve as the foundational building blocks that comprise all our user interfaces. These atoms include basic HTML elements like form labels, inputs, buttons, and others that can’t be broken down any further without ceasing to be functional. [Source.](http://atomicdesign.bradfrost.com/chapter-2/#atoms)

* **Molecules** are more complex widgets that must at least include an atom and sometimes other molecules.

  > "In interfaces, molecules are relatively simple groups of UI elements functioning together as a unit. For example, a form label, search input, and button can join together to create a search form molecule." [Source.](http://atomicdesign.bradfrost.com/chapter-2/#molecules)

* **Organisms** feature atoms, molecules, and even other organisms \(sparingly\). Think headers, footers, blog rolls.

  > "Organisms are relatively complex UI components composed of groups of molecules and/or atoms and/or other organisms." [Source.](http://atomicdesign.bradfrost.com/chapter-2/#organisms)

* **Templates** are page layouts, giving us a view into how content can possibly be laid out.

  > "Templates are page-level objects that place components into a layout and articulate the design’s underlying content structure." [Source.](http://atomicdesign.bradfrost.com/chapter-2/#templates)

* **Pages** can be considered full "prototypes" of a design systgem, with real content, images, etc.

  > "Pages are specific instances of templates that show what a UI looks like with real representative content in place." [Source.](http://atomicdesign.bradfrost.com/chapter-2/#pages)

