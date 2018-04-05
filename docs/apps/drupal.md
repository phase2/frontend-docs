
`apps/drupal/`

(REVAMP) - templates/ - Drupal twig templates. These often will `include`, `embed`, or `extend` the Twig templates found in Pattern Lab like this: `{% include "@molecules/branding/branding.twig" with { url: path('<front>') } %}`. We keep the components in Pattern Lab "pure" and ignorant of Drupal's data model and use these templates to map the data between the two. Think of these as the Presenter templates in the [Model View Presenter](https://en.wikipedia.org/wiki/Model–view–presenter) approach. Also, Drupal Twig templates that have nothing to do with Pattern Lab go here.

## Drupal integration of design system Twig files

Drupal Twig templates in `templates/` can `{% include %}`, `{% extends %}`, and `{% embed %}` the Twig patterns within `source/_patterns/`. See the [Atomic Design and Namespaces](#atomic-design-and-namespaces) section above for details, but implementing, say, an organism is pretty straightforward:

```twig
{% include "@organisms/path/to/file.twig" with {
  title: label,
  imageUrl: field_name.raw.path,
  largeCTA: true,
} %}
```

(Note: update this) For a demonstration in a sample codebase of how exactly to integrate templates, see the [`drupal-lab`](https://github.com/phase2/drupal-lab) repo; in particular note how both a [node teaser template](https://github.com/phase2/drupal-lab/blob/master/web/themes/dashing/templates/content/node--article--teaser.html.twig) and a [views field template](https://github.com/phase2/drupal-lab/blob/master/web/themes/dashing/templates/views/views-view-fields--newspage--page.html.twig) in the Drupal `templates/` folder can embed the [card template](https://github.com/phase2/drupal-lab/blob/master/web/themes/dashing/pattern-lab/source/_patterns/02-molecules/cards/card.twig) from Pattern Lab while formatting the data.
