# Apps

## Adding or Removing Apps

Particle makes adding or removing apps a snap! By default Particle has a Pattern Lab installation, a Drupal theme, and a Grav theme included. These can be added to, removed, or changed easily. If you'd like to make changes, see these pieces:

- Add or delete the app's folder in the `apps/` folder
- `module.exports` in `config.js`
- Path imports in `gulpfile.js`
- `dev` and `build` scripts in `package.json`
- If the app is Twig-based, `twigNamespaces` task in `gulpfile.js`

## Removing Grav

To remove Grav from your project, delete the `particle.yaml` file in the root folder.
