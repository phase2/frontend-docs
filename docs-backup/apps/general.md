Particle features "apps" which simply consume the design system in `source/` and then present it according to their needs. 

### Adding or Removing Apps

Particle makes adding or removing apps a snap! By default Particle has a Pattern Lab installation, a Drupal theme, and a Grav theme included. But these can be added to, removed, or changed easily. If you'd like to make changes, see these pieces:

* `module.exports` in `config.js`
* Path imports in `gulpfile.js`
* If the app is twig-based, `twigNamespaces` task in `gulpfile.js`
* `dev` and `build` scripts in `package.json`
* Add or delete App folder under `/apps`
* Special: to remove Grav, delete `particle.yaml`
