Particle makes adding or removing apps a snap! By default Particle has Pattern Lab, Drupal and Grav included. But these can be added to, removed or changed easily! If you'd like to make changes, see these pieces:

* `module.exports` in `config.js`
* imports in `gulpfile.js`
* `twigNamespaces` in `gulpfile.js`
* `compile` scripts in `package.json`
* `webpack` scripts in `package.json`
* Add or remove `webpack.APPNAME.config.js`
* Add or remove path in `webpack.shared.config.js`
* Special: to remove Grav, delete `particle.yaml`
* Add or delete App folder under `/apps`