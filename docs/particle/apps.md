# Apps

## About

!> TODO: "apps" concept expained here

## Adding or Removing Apps

Particle makes adding or removing apps a snap! By default Particle has a Pattern Lab installation, a Drupal theme, and a Grav theme included. These can be added to, removed, or changed easily. If you'd like to make changes, see these pieces:

* Add or delete the app's folder in the `apps/` folder
* `module.exports` in `config.js`
* Path imports in `gulpfile.js`
* `dev` and `build` scripts in `package.json`
* If the app is Twig-based, `twigNamespaces` task in `gulpfile.js`

## Pattern Lab

**App Root:**

`apps/pl/`

Refer to the [Pattern Lab Documentation](http://patternlab.io/docs) for extensive info on how to use it. Particle implements a custom Pattern Lab 2 _Edition_ that is heavily influenced by the [Drupal Edition of Pattern Lab](https://github.com/pattern-lab/edition-php-drupal-standard) and uses the Twig engine to bring it inline with Drupal 8's use of Twig.

The `app/pl` folder simply imports the design system from `source/` and provides its own custom Sass for UI and JSON generation. Any Twig files that change in `source/` cause a full Pattern Lab rebuild. The Pattern Lab engine and configuration lives within `apps/pl/pattern-lab`.

## Drupal

_For information on getting Drupal theming started in Particle, check the \[\_Drupal 8 Quickstart Guide_\]\(../getting-started/drupal-8.md\).\_

**App Root:**

`apps/drupal/`

**Templates**

`~templates/` - Drupal twig templates. These often will `include`, `embed`, or `extend` the Twig templates found in Pattern Lab like this:

\`

\`.

We keep the components in Pattern Lab "pure" and ignorant of Drupal's data model and use these templates to map the data between the two. Think of these as the Presenter templates in the [Model View Presenter](https://en.wikipedia.org/wiki/Model–view–presenter) approach. Also, Drupal Twig templates that have nothing to do with Pattern Lab go here.

## Integration of Design System Twig Files

Drupal Twig templates in `~templates/` can \`

`,`

`, and`

`the Twig patterns within`source/\_patterns/\` folder. See the [Atomic Design and Namespaces](https://phase2.github.io/frontend-docs/apps/drupal/#atomic-design-and-namespaces) section above for details, but implementing an organism, for example, is pretty straightforward:

```text
{% include "@organisms/path/to/file.twig" with {
  title: label,
  imageUrl: field_name.raw.path,
  largeCTA: true,
} %}
```

\(Note: requires updating\) For a demonstration in a sample codebase of how exactly to integrate templates, see the [`drupal-lab`](https://github.com/phase2/drupal-lab) repo; in particular note how both a [node teaser template](https://github.com/phase2/drupal-lab/blob/master/web/themes/dashing/templates/content/node--article--teaser.html.twig) and a [views field template](https://github.com/phase2/drupal-lab/blob/master/web/themes/dashing/templates/views/views-view-fields--newspage--page.html.twig) in the Drupal `~templates/` folder can embed the [card template](https://github.com/phase2/drupal-lab/blob/master/web/themes/dashing/pattern-lab/source/_patterns/02-molecules/cards/card.twig) from Pattern Lab while formatting the data.

