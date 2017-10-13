## Pattern Lab

Refer to the [Pattern Lab Documentation](http://patternlab.io/docs) for extensive info on how to use it. This theme starter is a custom Pattern Lab 2 *Edition* that is heavily influenced by the [Drupal Edition of Pattern Lab](https://github.com/pattern-lab/edition-php-drupal-standard) and uses the Twig engine to bring it inline with Drupal 8's use of Twig.

### Folder Structure Differences

Our folder structure makes a slight but convenient alteration to the typical Pattern Lab folder setup. Basically we move `pattern-lab/source/` up one level because we keep Sass in there too and it's the "source" for much of the theme. Here's the difference between the typical and our structure (few folders mentioned for brevity; please see Orientation above for a more thorough list).

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
- pattern-lab/
  - config/
  - public/
  - composer.json