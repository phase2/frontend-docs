---
description: Grav is a flat file CMS that uses Twig as a template engine.
---

# Grav

`apps/grav/`

Learn more [here](https://learn.getgrav.org/).

## **Grav integration of design system Twig files**

With the inclusion of the Grav plugin, [twig-namespaces](https://github.com/phase2/grav-pl-starter/tree/master/app/user/plugins/twig-namespaces), Grav Twig templates in `templates/` can `{% include %}`, `{% extends %}`, and `{% embed %}` the Twig patterns within `source/_patterns/`. Similar to Drupal above, including these patterns is done as follows:

```text
{% include "@organisms/path/to/file.twig" with {
  title: label,
  imageUrl: field_name.raw.path,
  largeCTA: true,
} %}
```

Configuration for Grav and additional docs can found at `apps/grav/README.md`.

