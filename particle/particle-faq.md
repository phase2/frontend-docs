---
description: >-
  Common questions about Particle. Questions here should link to solutions
  within documentation.
---

# Particle FAQ

## Can I change the Pattern Lab app to not open a new tab on every start?

Adjust **wepback-dev-server** _development_ mode behavior for Pattern Lab within `apps/pl/webpack.pl.js` by setting `open` to `false`:

{% code-tabs %}
{% code-tabs-item title="webpack.pl.js" %}
```javascript
const dev = {
  // ...
  open: false, // defaults to true
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## How do I allow the Pattern Lab app to be accessible from within a Docker container?

See FA project config here.



