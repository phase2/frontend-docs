# Buttons

Buttons are located in the `_patterns/01-atoms/button` directory of your design system.

## Creating a New Button

If you want to add a completely new button type to your design system, perform the following:

1. Create a copy an existing button layout and rename it, keeping the `_button-<name>.twig` naming convention.
1. Add any custom flags, classes, IDs, etc. to your template as necessary.
1. In the `_buttons.scss` file, add any necessary styling for your button.
1. Open `demo/buttons.twig` and find the *\<h1>Button Colors\</h1>* header. Add a few new lines between it and the section above it.
1. In this new section, add a header for your button.
1. Open a Twig code block (`{% %}`) and include your new button's template using the `atoms` namespace (`@atoms/buttons/_button-<name>.twig`), adding `with {` to the end.
   - If you want to show your button with each color available to your design system, wrap your code in the following: `{% for name, rgb in scssColors %}`. Note that to use this, your button should either extend `_buttons.twig` or include code to handle colorization.
1. Inside your `with` brackets, add any flags, classes, IDs, etc. your button requires.
1. Close your `with` statement (and `for` loop if you have one) and view in Particle. You should see your new button on the screen! You can now call your button using `@atoms/buttons/_button-<name>.twig` elsewhere in your design system.

---

## Overriding Bootstrap Styles

You can override the Bootstrap default styles by adding your Sass rules to `_button.scss`.
