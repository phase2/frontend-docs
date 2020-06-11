# Folder Structure

## General Structure  <a id="structure"></a>

The following are significant items at the root level:

```text
# ./
.
├── apps/                           # Things that use the compiled design system (e.x. Drupal)
├── dist/                           # Bundled output: CSS, JS, images, app artifacts (like PL HTML)
├── source/                         # The design system. All assets compiled to dist/
└── tools/                          # Gulp plugins and Node tools
```

## Source Structure  <a id="source-structure"></a>

`source/` holds all assets for the design system\(s\) and looks like this:

```text
# ./source/
.
├── {design-system}/                   # The design system in question, such as "default"
│  ├── _data/                          # Generated files used by PL for displaying data
│  ├── _meta/                          # Twig files for displaying live demo
│  ├── _patterns/                      # Atomic assets used by the design system
│  │   ├── 00-protons                  #
│  │   ├── 00-atoms                    #
│  │   ├── 00-molecules                #
│  │   ├── 00-organisms                #
│  │   ├── 00-templates                #
│  │   └── 05-pages                    #
│  ├── _twig-components/               # Various Twig PHP components
│  └── design-system.js                # The ultimate importer/exporter of the design system pieces
├── {design-system}/                   # Secondary design system
│  ├── _data/
│  ├── ...
```

The design system is consumed by "apps". The three apps included are a Drupal theme, Grav theme, and a Pattern Lab installation. For more information on the structure of a component in the `~_patterns/` folder, see [Component Structure](component-structure.md)

## App Structure  <a id="app-structure"></a>

### Pattern Lab

`apps/pl/` holds the _entry point_ for all Pattern Lab assets, as well as the PHP engine:

```text
# ./apps/pl/
.
├── demo/                           # Holds things related to just "demos" for the design system
│   └── demos.glob                  # Special file used by Webpack to "glob" all demos within source/
├── pattern-lab/                    # Holds the Pattern Lab installation
│   └── ...                         # composer.json, config, console PHP, ...
├── scss/                           # PL-only Sass; styles that shoudln't junk up the design system
│   ├── _scss2json.scss             # Output certain Sass variables into JSON for demo in PL
│   └── _styleguide.scss            # Custom PL UI styles
├── index.js                        # Imports and applies the design system to a bundle for PL
├── webpack.pl.dev.js               # Webpack config unique to dev, or that overrides shared
├── webpack.pl.prod.js              # Webpack config unique to prod, or that overrides shared
└── webpack.pl.shared.js            # Webpack config shared between PL dev and PL prod
```

### Drupal

`apps/drupal-default/` holds the _entry point_ for all Drupal 8 theme assets, as well as templates, YAML, etc:

```text
# ./apps/drupal-default/
.
├── particle_helper/                # Theme-only Sass, tweaks to Drupalisms that need not be in the design system
│   └── _drupal-styles.scss         # Add more Drupal styles here, like _views.scss, _field.scss, etc.
│   ├── block.html.twig             # Example Drupal template integrating, say @molecules/_card.twig
│   ├── block.html.twig             # Example Drupal template integrating, say @molecules/_card.twig
│   ├── block.html.twig             # Example Drupal template integrating, say @molecules/_card.twig
│   ├── block.html.twig             # Example Drupal template integrating, say @molecules/_card.twig
├── particle_theme/                 # Templates integrate Drupal data with design system patterns
│   ├── block.html.twig             # Example Drupal template integrating, say @molecules/_card.twig
│   ├── block.html.twig             # Example Drupal template integrating, say @molecules/_card.twig
│   ├── block.html.twig             # Example Drupal template integrating, say @molecules/_card.twig
│   ├── block.html.twig             # Example Drupal template integrating, say @molecules/_card.twig
│   └── ...                         # There can be many Drupal templates
├── .eslintrc.js                    # Linting configuration file
├── drupal-jquery.js                # Custom jQuery library that overrides Drupal's jQuery instance   
├── index.js                        # Imports and applies the design system to a bundle for Drupal
├── particle.app.config.js          # Config file that allows generated design system components to work with the Drupal theme  
└── webpack.config.js               # Webpack configuration specific for Drupal. Referenced by the "dev:drupal" and "build:drupal" commands
```

## Atomic Design and Namespaces

"Namespaces" are simply aliases to paths on a file system. Each app can define its own design system inside their `config.js`, thus allowing the namespacing to remain consistent between all apps. The design system within `source/` adheres strongly to [Atomic Design](http://atomicdesign.bradfrost.com/), with `@protons` added on.

| Path | Twig | Javascript | Sass |
| :--- | :--- | :--- | :--- |
| `source/{design-system}/_patterns/00-protons/` | `@protons` | `protons` | TBD |
| `source/{design-system}/_patterns/01-atoms/` | `@atoms` | `atoms` | TBD |
| `source/{design-system}/_patterns/02-molecules/` | `@molecules` | `molcules` | TBD |
| `source/{design-system}/_patterns/03-organisms/` | `@organisms` | `organisms` | TBD |
| `source/{design-system}/_patterns/04-templates/` | `@templates` | `templates` | TBD |
| `source/{design-system}/_patterns/05-pages/` | `@pages` | `pages` | TBD |

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

