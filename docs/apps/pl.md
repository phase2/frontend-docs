## Pattern Lab

Refer to the [Pattern Lab Documentation](http://patternlab.io/docs) for extensive info on how to use it. This toolset is built upon a custom Pattern Lab 2 *Edition* that is heavily influenced by the [Drupal Edition of Pattern Lab](https://github.com/pattern-lab/edition-php-drupal-standard) and uses the Twig engine to bring it inline with Drupal 8's use of Twig.

### Folder Structure Differences

Our folder structure makes some convenient alterations to the typical Pattern Lab folder setup. Basically we move `pattern-lab/source/` up one level because it's the "source" for the entirety of the design system. Here's the difference between the typical and our structure. See [architecture](../getting-started/architecture.md) for a more in-depth explanation of the structure.

#### Typical Folder Structure

- pattern-lab/
    - config/
    - public/
    - source/
        - _patterns/ (contains atoms, molecules, etc folders)
    - composer.json

#### Our Folder Structure

- source/
    - _patterns/ (contains atoms, molecules, etc folders)
- tools/
    - pattern-lab/
        - config/
        - composer.json
- dist/
    - public/ (compiled patternlab files)