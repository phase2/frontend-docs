# Development Guides

## Overview

If you haven't already, be sure to check out the [Development Approach](../development/approach.md) document for a brief overview of the fundamentals of how Particle handles various files and types.

## Colors

Adding colors to a Particle project is quick and painless.

### Adding a New Color

1. Navigate to `source/{design-system}/_patterns/00-protons` and open the `non-printing` folder.
2. Open the `_colors.scss` file and assign a variable to the hex code of the color you're adding.

   ```scss
   $phase2-orange: #FE7900;
   ```

   * To add your color to the global theme colors, also append it to the `$theme-colors` map like so:

     \`\`\`scss $theme-colors: \( 'phase2-orange': $phase2-orange, \)

### Using Your New Color

Because Particle uses Sass, using your new color is as simple as adding the variable name into your code like so:

```scss
.my-class {
  color: $phase2-orange;
}
```

### Using a Theme Color

If the color you want to use is in the `$theme-colors` map, you can reference it like so:

```scss
.my-class {
  color: theme-color("phase2-orange");
}
```

## Fonts and Typefaces

Custom typefaces can be added to Particle and can even override the system defaults with only a few additions to the platform.

### Adding a New Font

1. Navigate to `source/{design-system}/_patterns/00-protons` and open the `printing` folder.
2. Open the `_type.scss` file and add your `@import` rules for remote fonts and/or `@font-face` for locally hosted fonts.

   ```css
   @import url('...');

   @font-face {
     font-family: 'My Font';
     src: local('My Font'), local('My-Font'), url('../fonts/My-Font-Medium.ttf') format('truetype');
   }
   ```

   * If your font is being hosted locally, place your font files in the `fonts` folder inside of the Protons directory.

3. Navigate to the `non-printing` folder in the Protons directory and open the `_type.scss` file. Add a variable for your newly added font for quick reference later.

   ```scss
   $font-family-custom: 'My Font', 'Backup Font', Arial, ...;
   ```

### Overriding a Global Font

Particle uses Bootstrap for it's styling and has a ton of variables set by default, but we can also override them.

1. Perform _Adding a New Font_ above.
2. In the `non-printing` folder in the Protons directory and find the `_bootstrap-overrides.scss` file. Above the `@import` rules, set the variable you want to override and the fonts you want to use.

   ```scss
   $font-family-base: $font-family-custom;

   @import ...
   ```

   There are four Bootstrap variables for font face that can be overriden:

   * `$font-family-base:` Global default; defaults to `$font-family-sans-serif`
   * `$font-family-monospace:` Used for code samples.
   * `$font-family-sans-serif:` Used for content and body text.
   * `$headings-font-family:` Used for header tags and classes; defaults to `inherit` and will use the base font family.

### Using Your New Font

Because Particle uses Sass, using your new font is as simple as adding the variable name into your code like so:

```scss
.my-class {
  font-family: $font-family-custom;
}
```

### Misc. Default Font Variables

You can also override the default font settings from Bootstrap in a similar fashion. As above in _Overriding a Global Font_'s second step, assign a variable in `non-printing/_types.scss` with the updated value, and then assign that new variable to the global default variable you're overriding in `non-printing/_bootstrap-overrides.scss`. For example, if you wanted to change the weight of all headings you would add the following code to these files:

```scss
// source/{design-system}/_patterns/00-protons/non-printing/_types.scss
$headings-font-weight-custom: 700;

// source/{design-system}/_patterns/00-protons/non-printing/_bootstrap-overrides.scss
$headings-font-weight: $headings-font-weight-custom;
```

All of the default Bootstrap variables and their values can be found in the `node_modules/bootstrap/scss/_variables.scss`.

?> If you're missing the `node_modules` root folder, run the install and/or setup commands in the [Commands](../commands.md) guide.

