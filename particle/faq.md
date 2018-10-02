# FAQ

## Can I change the Pattern Lab app to not open a new tab on every start?

Adjust **wepback-dev-server** _development_ mode behavior for Pattern Lab within `apps/pl/webpack.pl.js` by setting `open` to `false`:

{% code-tabs %}
{% code-tabs-item title="apps/pl/webpack.pl.js" %}
```javascript
const dev = {
  // ...
  open: false, // defaults to true
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Which browsers does Particle support?

Particle uses Browserslist to communicate transpiling and polyfill needs to all tooling. From the `.browserslistrc` file, these browsers should be fully functional with compiled Particle assets:

{% code-tabs %}
{% code-tabs-item title=".browserslistrc" %}
```text
last 2 versions
not dead
> 1% in US
ie 11
```
{% endcode-tabs-item %}
{% endcode-tabs %}

To see the specific browsers this translates to at your date and time, run:

```bash
npx browserslist
```

## How do I allow the Pattern Lab app to be accessible from within a Docker container?

See FA project config here.



