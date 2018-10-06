# Folder Structure

## General Structure {#structure}

The following are significant items at the root level:

```text
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
```

## Source structure {#source-structure}

`source/` holds all assets for the design system and looks like this:

```text
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
```

> The design system is consumed by "apps". The three apps included are a Drupal theme, Grav theme, and a Pattern Lab installation.

## App structure {#app-structure}

`apps/pl/` holds the _entry point_ for all Pattern Lab assets, as well as the PHP engine:

```text
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
```

`apps/drupal/` holds the _entry point_ for all Drupal 8 theme assets, as well as templates, yml, etc:

```text
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

