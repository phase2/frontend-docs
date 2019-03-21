# Colors

## Colors

Adding colors to a Particle project is quick and painless.

## Adding a New Color

1. Navigate to `source/{design-system}/_patterns/00-protons` and open the `non-printing` folder.
2. Open the `_colors.scss` file and assign a variable to the hex code of the color you're adding.

   ```css
   $phase2-orange: #FE7900;
   ```

   * To add your color to the global theme colors, also append it to the `$theme-colors` map like so:

     \`\`\`scss $theme-colors: \( 'phase2-orange': $phase2-orange, \)

### Using Your New Color

Because Particle uses Sass, using your new color is as simple as adding the variable name into your code like so:

```css
.my-class {
  color: $phase2-orange;
}
```

### Using a Theme Color

If the color you want to use is in the `$theme-colors` map, you can reference it like so:

```css
.my-class {
  color: theme-color("phase2-orange");
}
```

