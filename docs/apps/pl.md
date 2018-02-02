# Pattern Lab

Refer to the [Pattern Lab Documentation](http://patternlab.io/docs) for extensive info on how to use it. This toolset is built upon a custom Pattern Lab 2 *Edition* that is heavily influenced by the [Drupal Edition of Pattern Lab](https://github.com/pattern-lab/edition-php-drupal-standard) and uses the Twig engine to bring it inline with Drupal 8's use of Twig. 

## Folder Structure Differences

Our folder structure makes some convenient alterations to the typical Pattern Lab folder setup. Basically we move `pattern-lab/source/` up one level because it's the "source" for the entirety of the design system. Here's the difference between the typical and our structure. See [architecture](../appendix/architecture.md)

### Typical Folder Structure

- pattern-lab/
    - config/
    - public/ (compiled patternlab files)
    - source/
        - _patterns/ (contains atoms, molecules, etc folders)
    - composer.json

### Our Folder Structure

- source/
    - _patterns/ (contains atoms, molecules, etc folders)
- apps/
    - pl/
        - scss/ (pl-only styles that don't need to junk up full design system)
        - pattern-lab/
            - config/
            - composer.json
        - index.js (webpack entry point for pl)
- dist/
    - assets/ (compiled design system files)
    - pl/ (compiled patternlab files)
    
## 