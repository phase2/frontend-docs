Most of the Design System lives in the source folders from `00-protons` to `03-organisms`. The next two folders in source are also part of the design system, but tend to get structured slightly differently than the rest here at Phase2.

# Templates
Templates are meant to be leaner. They may or may not be used explicitly by templates in Drupal and elsewhere, but they provide guidance for where classes need to be applied, and a reliable mock for Pattern Lab.

# Pages
Pages are treated purely as _demo_ patterns. They are used _solely_ by Pattern Lab to mock up working designs prior/in parallel to Drupal entities being constructed. They _use_ the template patterns for structure, and import their own demo images that are not included in the overall design system's dependency chain. You'll notice by default, there are no individual page "components", everything lives comfortably inside a /demo/ folder.

This is one reason that the static PL bundle is so much larger than other production app bundles-- it explicitly includes the full demoPages item, as part of the demo glob inside of `apps/pl/index.js`.

This split is the reason there are no demo folders inside of individual template components. Pages is a conglomeration of all template demos.
