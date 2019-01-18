# Using Demos

A key part of all Pattern Lab (and Particle-used) patterns is the creation of the
demo folder, which has a multitude of uses for all Pattern Lab participants.

* Developers can test their patterns and verify changes and options.
* Designers can see perfect use-cases of their designs for tweaking.
* Users can verify that designs are met and update patterns.

The demo folder is automatically pulled into Pattern Lab, and only Pattern Lab,
so you should never do work on them that you expect to see on a production app,
such as a Drupal theme.

Creating a demo folder should be one of the first steps in the development of any
new component, and updating it as development goes on should be a continuous task.

## Components and Creation

Demo folders are one of the options for creation when using Yeoman to [generate a new
component](../architecture/component-structure.md#generating-a-component). The
Yeoman generator creates four files by default in this folder, which describe the
general Phase2 way to demonstrate how to use a new component:

### index.js

Describes to Webpack the files to include when generating the Pattern Lab demos.
This most likely will only need to be touched when you are creating multiple demo
pages for a single component.

### components.twig

{% hint style="info" %}
Note the pluralization of the component name, which indicates multiple examples
of the component!
{% endhint %}

This should serve as an example twig file that shows an inclusion of the new pattern,
placed with example variables and layouts so that it will appear like an intended
component when viewed in the demos.

The default .twig file places a standard Twig-style `include` of your new component,
but you can (and should) modify this page to meet your design system better. Look
at the default patterns for good examples of how to create a demo template.

### component.md

An additional readme that may describe how to use your demo, its implications, or
others. By default the variables that a component requires are often documented
here, in addition to in the component's `_component.twig` file.

### component.yml

An optional way to override the data in `/_data/data.yml`, to display something
specific in your demo. These data structures are only included in their respective
page's demos when rendering the demo's template, so they are safely separated from
other pattern demos.

{% hint style="info" %}
If you would like to create demo data to be global between all patterns, add
the variables to a Yaml file in the `/_data` folder, such as `/_data/data.yml`.
{% endhint %}

For more information about how Pattern Lab expects variables to be added for use
in patterns, see the [Pattern Lab docs](https://patternlab.io/docs/data-overview.html).

## Placeholders

Particle includes several ways you can generate defaults for your testing, thus
supplanting the need to include placeholder images, or generate long strings of
text.

### Text with Faker

Particle includes the [Faker plugin of Pattern Lab](https://github.com/pattern-lab/plugin-php-faker),
thus letting one use the [Node.JS Faker API](https://www.npmjs.com/package/faker)
in order to generate random data. This can be used for anything from names to dates
to lorem ipsum.

{% hint style="info" %}
Faker can only be used from within `/_data/data.yml` by default, so don't try to
use this within a specific demo's .yml file; it won't work!
{% endhint %}

To use Faker, call the Faker object from a variable assignment in the source `data.yml`,
with the type of formatter and any options specific to that formatter.

For example, this will save a string variable named `site_title` that consists of
two words.

```yml
site_title: Faker.words(2, true)
```

This will save an object named `year` with two properties: one string named named
`long` which consists of a year saved in "XXXX" format, and one string named `short`
which consists of two random numbers between 01 and 99. 

```yml
year:
  long: Faker.year
  short: Faker.numberBetween(01, 99)
```

See the [full list of Faker formatters](https://github.com/fzaninotto/Faker#formatters)
for more examples and ideas of how to utilize Faker in your project, or the default
demo data under `_data/data.yml` for a host of Faker uses.

### Images with Holder

The default Image atom at `@atoms/_image` harnesses the [Holder JS](https://github.com/imsky/holder)
library for any times an image is not passed a URL. You, too, can utilize it in
your demos to ensure that any image you want to place lists the general use and
resolution, as well as fits a theme specific to that image.

Particle by default defines all of the image styles used with Holder in `_data/imageStyles.yml`,
where each image style is given a name, width, and height, although other properties
could be added with additional customization of the `@atoms/_image.twig` file.

By defining an image style in `imageStyles.yml`, themers can then set `imageStyleName`
when calling the Image component, then ensuring default placeholders are created
in the proper size and with the proper label.

A great example of how these are used is found in the default pattern `@molecules/_carousel`:

```twig
{% include '@atoms/image/_image.twig' with {
  imageStyleName: 'carousel',
  class: 'img img-fluid',
} %}
```

The property `imageStyleName` matches the image style `carousel` in `imageStyles.yml`:

```yml
  carousel:
    width: 1110
    height: 400
```

`_image.twig` checks to see if a `src` property is included, and, if not, generates
the other information Holder needs, such as theme and size, then places the Holder-generated
image on the demo page.

By modifying the width and height, or completely ignoring them, you can have variable-sized
images on your demo pages.
