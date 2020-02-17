# Frontend Development

!> TODO: REWRITE ALL OF THIS

Frontend development involves the architecture and development of anything visible within a browser. To quote the exhaustive [Front-end Developer Handbook](https://frontendmasters.com/books/front-end-handbook/2019/#2),

> A front-end developer architects and develops websites and web applications using web technologies \(i.e., [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML), [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS), and [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)\), which typically runs on the [Open Web Platform](https://en.wikipedia.org/wiki/Open_Web_Platform) or acts as compilation input for non-web platform environments \(i.e., [React Native](https://facebook.github.io/react-native/)\).

## Thinking

### Philosophy

Building for the web and mobile experiences requires systems of design. Design systems ensure reusability and scalability of applied design. Working collaboratively early in the design process allows developers and designers the opportunity to catalog shared tokens and components within the design system. Once a design system is established, coding components with the intention of integration to other systems is streamlined.

### Points

1. All frontend builds start as design systems. We apply design systems to frameworks.
2. All design systems are actually hundreds of design tokens. All components of a design system should be built from preexisting tokens.
3. Every component in a design system must declare its schema. Design cannot exist without a data shape. No components can be written until information architecture is established. Make a spreadsheet.
4. Any component using constants \(numbers, font names, pixel values\) within its styles is a code smell. All "proton" level variables should already be defined.
5. Developers should be involved in the design process at the point where components are being defined onward.

### Process

1. An understanding of stakeholders and the design/develop workflow
2. Collaboration with designers in establishing the design system
3. Rapid mocks using components and tokens identified in the collaboration step
4. Coding/prototyping all appropriate pieces of the design system using Atomic Design principles
5. After sign-off of prototype, integration of appropriate components to the integrating system \(Drupal, Wordpress, custom React app, etc\)
6. Training and establishing Governance Processes

## Atomic Design

Particle uses atomic design for organization.  [Atomic design](http://atomicdesign.bradfrost.com/table-of-contents/) is a tool to break down designs into re-usable pieces.  These pieces act like lego bricks,  combining smaller pieces to create larger and larger components.  In particle we start with protons, and eventually work up to pages. 

`Protons -> Atoms -> Molecules -> Organisms -> Templates -> Pages`

## Best Practices

### Philosophy 

Particle is an opinionated set of tools and a methodology for design implementation. Particle empowers users to rapidly prototype front end components by creating a living, breathing style guide and using it to create front end code.  Particle handles both dependency management and code compilation, so developers can create and modify components quickly and easily regardless of chosen design system. 

Particle comes with bootstrap installed which provides several example components.  You can choose to either use these existing components or [remove them](../particle/sprint-0.md#removing-bootstrap) depending on your needs.

### Protons

Protons are used to create your living style guide and are atomic design components unique to Particle. Protons are included globally by design, so there is no need to declare protons inside of larger twig templates. Protons are pure assets that don't result in usable twig files elsewhere, such as colors, typography, image styles and mixns.  

### **Printing vs.** Non-Printing 

Protons are divided into printing and non-printing variables.    Printing variables will generate css, while non-printing variables will not.

### Common Custom Variables

#### Colors

Particle comes with bootstrap 4, built in and displays the bootstrap color palette on the colors demo page by default.   

You can add custom color variables to your design system by declaring them  in the non-printing/\_colors.scs file.

```scss
source/default/_patterns/00-protonsprotons/non-printing/_colors.scssn                                                       

// Greyscale
$c-white: #fff;
$c-gray--light: #f0f0f0;
$c-gray: #d0d0d0;
$c-gray--dark: #878787;

//Colors
$c-primary: #ed786a;
$c-secondary: #fd887a;

```

 You can overwrite the bootstrap colors and customize your color palette demo by customizing the $theme-colors object in the non-printing/\_bootsrap-overrides.scss file.

```scss
source/default/_patterns/00-protons/non-printing/_bootstrap-overrides.scss

$theme-colors: (
  'white': $c-white,
  'background': $c-background,
  'icon': $c-icon,
  'gray': $c-gray,
  'primary': $c-primary,
  'secondary': $c-secondary,
  'dark': $c-dark
);
```

Since colors are reused for a variety of components, unlike mixins they are not named for their function but rather by shade or frequency of use.    \(Ie**.** Primary, Secondary, Gray--Light, Gray--Dark\).   If you use the same name as a bootstrap predefined color in these two files \(ie primary, secondary, success etc\) , the design system will override the bootstrap variable, with your new custom colors. 

We strongly encourage limiting the number of shades of each color to just a few of each in order to keep things getting out of hand.  Using the demo page to display colors is a great tool to trim down your palette since it allows you to see the rbg values of colors next to one each other. 

### Typography

#### Font Families

You can add custom fonts to your design system in two steps.  First you need to import the font in printing/\_type.scss file

```
source/default/_patterns/00-protons/printing/_type.scss

//Google Fonts
@import url('https://fonts.googleapis.com/css?family=Arvo');
@import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');
```

After importing, you should make a variable in non-printing/\_type.scss file for each custom font family. 

```text
source/default/_patterns/00-protons/non-printing/_type.scss

//Font Family
$ff--arvo: 'Arvo', serif;
$ff--sourcesans: 'Source Sans Pro', sans-serif;
```

#### Font Weight, Size, Spacing etc 

Like font families, should should declare your other typography variables in the non-printing/\_type.scss file.  

```text
source/default/_patterns/00-protons/non-printing/_type.scss

//Font Weights
$fw--300: 300; // light
$fw--400: 400; // normal/regular
$fw--600: 600; // semi-bold/demi-bold
$fw--700: 700; // bold


//Font Sizes
$fs--s: 16px;
$fs--m: 20px;
$fs--l: 33px;

//Letter Spacing
$letter-spacing--sm: 2px;
$letter-spacing--md: 4px;
$letter-spacing--lg: 13px;

//Spacing
$spacing--sm: 10px;
$spacing--md: 25px;
$spacing--lg: 33px;
$spacing--xl: 40px;
```

### Mixins

Mixins can live in the same file as the variables relevant to them. For example, typography mixings can be delcared in the non-printing/\_type.scss file.  

Mixin names are based on the purpose of the mixin \(ie. word-wrap, heading etc.\) In order to keep code dry, we encourage grouping of similar mixins and taking advantage of the fact that mixins can call on each other.   

```text
source/default/_patterns/00-protons/non-printing/_type.scss

@mixin heading() {
  font-family: $ff--sourcesans;
  color: $c-button;
  text-transform: uppercase;
}

@mixin section_heading() {
  @include heading();
  font-size: $fs--l;
  letter-spacing: $letter-spacing;
  font-weight: $fw--400;
  margin: ($spacing-xxl*2) 0 $spacing-xxl 0;
}

@mixin article_heading() {
  @include heading();
  font-size: $fs--m;
  font-weight: $fw--600;
  letter-spacing: $letter-spacing--sm;
  margin: $spacing-xxl 0 $spacing--md 0;
}
```

### Image Styles

Particle comes with custom image styles from bootstrap baked in.  You can customize these styles by adding your own to the object in the image style folder. 

```text
source/default/_data/imageStyles.yml

imageStyles:
  thumbnail:
    width: 180
    height: 180
  card:
    width: 348
    height: 233
  medium:
    width: 753
    height: 293
```

## Svgs

#### Font Awesome

Particle comes with font awesome built in, but it does not  import all icons by default.   In order to use a font icon, import it in svgicon/fontawesome.js.  

Note that while most font awesome icons live in '@fortawesome/free-solid-svg-icons' not all do and need to be imported separately \(ie brand icons\) 

```text

source/default/_patterns/01-atoms/svgicon/fontawesome.js

import { library, dom } from '@fortawesome/fontawesome-svg-core';
// Import specific icons required
import {
  faUserAstronaut,
  faRocket,
  faSpaceShuttle,
  faRetweet,
} from '@fortawesome/free-solid-svg-icons';

import {
  faTwitter,
  faInstagram,
  faFacebook,
} from '@fortawesome/free-brands-svg-icons';

library.add(
  faUserAstronaut,
  faRocket,
  faSpaceShuttle,
  faRetweet,
  faTwitter,
  faInstagram,
  faFacebook
);

export default () => dom.watch();

```

## Style Guide Demo  

In order for your custom variables to show up properly on the demo pages you need to overwrite the default objects in \_scss2json.scss.



```text
apps/pl/scss/_scss2json.scss

@include export-data(
  'scssVariables.json',
  (
    scssColors: $theme-colors,
    scssBreakpoints: $grid-breakpoints,
    scssSpacing: $spacing-demo,
    fontFamilies: $font-families-demo,
    fontSizes: $font-sizes-demo,
    fontWeights: $font-weights-demo,
    scssIcons: $svgicons,
  )
);

$font-families-demo: (
  '$ff--arvo': $ff--arvo,
  '$ff--sourcesans': $ff--sourcesans,
);

$font-sizes-demo: (  
  base: $font-size-base,
  lg: $font-size-lg,
  sm: $font-size-sm,
);

$font-weights-demo: (
  light: $font-weight-light,
  normal: $font-weight-normal,
  bold: $font-weight-bold,
);

$spacing-demo: $spacers
```

## YML

Particle uses yml for modeling data.   There are no need for quotes in yml files, unless you are using special characters, in which case you should use single quotes. 



```text
source/default/_patterns/01-atoms/icon-button/demo/icon-buttons.yml

icon_button_rectangle:
  text: Aenean sit.
  icon: file
  color: primary
  type: rectangle

icon_button_circle:
  icon: file
  color: dark
  type: circle
  
 credit: © Untitled. All rights reserved.
      -
        credit: 'Design: HTML5 UP'
      -
        credit: 'Demo images: regularjane'
```

## BEM

We strongly encourage the use of [BEM syntax](http://getbem.com/introduction/)  for your template markup and stylesheets. 

### Why BEM

Using BEM \(Block-Element-Modifier\) syntax will keep your code organized, easy to read and consistent throughout the design system, making it easier to refactor and squash front end bugs in the future.  

### Parts of BEM

* Block: The outer most container  \(ie icon-button\)
* Element: An element that is a child of the block \(ie button\)
* Modifier: A class that describes the 'flavor' relevant to the specific block or element  \(ie --round \) 

### Class Naming Convention 

When using BEM do not style raw elements, rather assign the element a BEM class and target that class. 

Often the block name for any given template will be the same as the component name in particle.  For example in the code below our block name is "featured-article-card" and "text-wrapper" is the modifier. 

When using helper classes, like those from bootstrap,  custom BEM classes go first, like in the example below. 

```markup
source/default/_patterns/01-atoms/icon-button/demo/icon-buttons.twig

<div class="icon-button"> . <-- BLOCK 
  <div class="row">
    <div class="col">
      <button type="button"  <-- ELEMENT 
              class=
              "icon-button__btn--round"> <--MODIFIER
        <i class="fas fa-{{ icon_button.icon }}" aria-hidden="true"></i>
          {{ icon_button.text | upper }}
      </button>
    </div>
  </div>
```

### Don't Nest 

Don't nest your scss.  While it may look clean in development, in production it can make it harder to track down and squash bugs. 

```text
source/default/_patterns/01-atoms/icon-button/_icon-button.scss


.icon-button__btn--rectangle {
  @include rectangle-btn();
}

.icon-button__btn--round {
  @include round-btn();
  }
```



## ATOMS, MOLECULES & ORGANISMS

Atoms, Molecules and Organisms, are all building blocks that consume smaller blocks to make components.  Files in these components are divided into two categories, pure files and demo files. 

#### Pure Files

These are the files where the components get build in twig, and the files that your design system compiles down in the end.  These files are hidden from pattern lab but consumed by it, 

```text
# ./source/{design-system}/_patterns/01-atoms/icon-button/
.
├── demo                            # Demo implementations; can be removed on deploy to prod            
├── _icon-button.scss                # Most components require styles, underscore required
├── _icon-button.twig                # The pure component template, underscore required to hide from PL UI
└── index.js                        # Component entry point
```



```text
source/default/_patterns/01-atoms/icon-button/_icon-button.twig

<div class="icon-button">
  <div class="row">
    <div class="col">
      <button type="button" class="icon-button__btn--{{ icon_button.type }} btn btn-{{ icon_button.color }}">
        <i class="fas fa-{{ icon_button.icon }}" aria-hidden="true"></i>
        {{ icon_button.text | upper }}
      </button>
    </div>
  </div>
</div>
```

#### Demo Files

These are files used to demo your components on a sever for rapid prototyping.   Allows you to show off a variety of styles using the same twig template with different data.   Note: These files do not get compiled into production. 

```text
# ./source/{design-system}/_patterns/01-atoms/icon-button/demo

├── index.js                    # Pulls in Twig, YAML, MD inside demo/ so Webpack is aware
├── icon-buttons.md                  # Markdown with extra notes, visible in PL UI
├── icon-buttons.twig                # Demonstrate with a plural name, visible to PL since no underscore
└── icon-buttons.yml                 # Data provided to the demo pattern
```



```text
source/default/_patterns/01-atoms/icon-button/demo/icon-buttons.twig

{% include '@atoms/_icon-button.twig' with
  { icon_button: icon_button_rectangle }
%}

{% include '@atoms/_icon-button.twig' with
  { icon_button: icon_button_circle }
%}
```

 

## TEMPLATES & PAGES 

Templates are a tool to quickly prototype different layouts.  Pages are the culmination of all demos and use real data to create responsive digital mockups.   For this reason, templates do not have demo files like other components. 

### Twig Blocks

Particle relies on twig blocks for building templates and pages.    Blocks allow for inheritance between templates and pages.  When using blocks its best practice to include to block name on the end block tag, in order to maintain readability,    



```text
source/default/_patterns/04-templates/basic-page/_basic-page.twig 


<div class="basic-page">
  <div class="basic-page__inner">

    {% block header %}

      {% include '@organisms/_header.twig' with {
        "header": {
          title: "Strongly Typed",
          eyebrow: "A RESPONSIVE HTML5 SITE TEMPLATE. MANUFACTURED BY HTML5 UP.",
          navbar: [
            {
              icon: "home",
              text: "Introduction"
            },
            {
              icon: "chart-bar",
              text: "Dropdown"
            },

            {
              icon: "cog",
              text: "Left Sidebar"
            },
            {
              icon: "retweet",
              text: "Right Sidebar"
            },
            {
              icon: "sitemap",
              text: "No Sidebar"
            }
          ]
        }
      } %}

    {% endblock header %}

    {% block content %}{% endblock content %}

    {% block footer %}

      {% include '@organisms/_footer.twig' with {

        "footer": {
          headline: "Questions or Comments?",
          emphasis: "Get in touch:",
          summary: "Erat lorem ipsum veroeros consequat magna tempus lorem ipsum consequat Phaselamet mollis tortor congue. Sed quis mauris sit amet magna accumsan tristique. Curabitur leo nibh, rutrum eu malesuada.",
          form:
            {
              name: "Name",
              email: "Email",
              message: "Message"
            },
          button: {
            text: "Send Message",
            color: "primary",
            type: "rectangle",
            icon: "envelope"
          },
          links: [
            {
              icon: "home",
              icon_type: "s",
              text: "1234 Somewhere Road Nashville, TN 00000 USA.",

            },
            {
              icon: "phone",
              icon_type: "s",
              text: "(000) 000-0000"
            },

            {
              icon: "envelope",
              icon_type: "s",
              text: "info@untitled.tld"
            },
            {
              icon: "twitter",
              icon_type: "b",
              text: "@untitled"
            },
            {
              icon: "instagram",
              icon_type: "b",
              text: "instagram.com/untitled"
            },
            {
              icon: "dribbble",
              icon_type: "b",
              text: "dribbble.com/untitled"
            },
            {
              icon: "facebook",
              icon_type: "b",
              text: "facebook.com/untitled"
            }
          ],
          credits: [
            {
              credit: "© Untitled. All rights reserved."
            },
            {
              credit: "Design: HTML5 UP"
            },
            {
              credit: "Demo images: regularjane"
            }
          ]
        }
      } %}

    {% endblock footer %}

  </div>
</div>

<div class="basic-page">
  <div class="basic-page__inner">

    {% block header %}

      {% include '@organisms/_header.twig' with {
        "header": {
          title: "Strongly Typed",
          eyebrow: "A RESPONSIVE HTML5 SITE TEMPLATE. MANUFACTURED BY HTML5 UP.",
          navbar: [
            {
              icon: "home",
              text: "Introduction"
            },
            {
              icon: "chart-bar",
              text: "Dropdown"
            },

            {
              icon: "cog",
              text: "Left Sidebar"
            },
            {
              icon: "retweet",
              text: "Right Sidebar"
            },
            {
              icon: "sitemap",
              text: "No Sidebar"
            }
          ]
        }
      } %}

    {% endblock header %}

    {% block content %}{% endblock content %}

    {% block footer %}

      {% include '@organisms/_footer.twig' with {

        "footer": {
          headline: "Questions or Comments?",
          emphasis: "Get in touch:",
          summary: "Erat lorem ipsum veroeros consequat magna tempus lorem ipsum consequat Phaselamet mollis tortor congue. Sed quis mauris sit amet magna accumsan tristique. Curabitur leo nibh, rutrum eu malesuada.",
          form:
            {
              name: "Name",
              email: "Email",
              message: "Message"
            },
          button: {
            text: "Send Message",
            color: "primary",
            type: "rectangle",
            icon: "envelope"
          },
          links: [
            {
              icon: "home",
              icon_type: "s",
              text: "1234 Somewhere Road Nashville, TN 00000 USA.",

            },
            {
              icon: "phone",
              icon_type: "s",
              text: "(000) 000-0000"
            },

            {
              icon: "envelope",
              icon_type: "s",
              text: "info@untitled.tld"
            },
            {
              icon: "twitter",
              icon_type: "b",
              text: "@untitled"
            },
            {
              icon: "instagram",
              icon_type: "b",
              text: "instagram.com/untitled"
            },
            {
              icon: "dribbble",
              icon_type: "b",
              text: "dribbble.com/untitled"
            },
            {
              icon: "facebook",
              icon_type: "b",
              text: "facebook.com/untitled"
            }
          ],
          credits: [
            {
              credit: "© Untitled. All rights reserved."
            },
            {
              credit: "Design: HTML5 UP"
            },
            {
              credit: "Demo images: regularjane"
            }
          ]
        }
      } %}

    {% endblock footer %}

  </div>
</div>

```

You can override any part of a template by simply wrapping it in a block, and replacing with new content in your page. 

```text

source/default/_patterns/05-pages/intro-page/_intro-page.twig

{% extends '@templates/_basic-page.twig' %}

{% block content %}
  {% include '@organisms/_featured-article-grid.twig' with {
    featured_article_grid: intro_page.featured_article_grid,
  } %}

  {% include '@molecules/_banner.twig' with {
    banner: intro_page.banner,
  } %}


  <div class="container">
    <div class="row">
      <div class="col-8">
        {% include '@organisms/_main-article.twig' with {
          main_article: intro_page.main_article1,
        } %}

        {% include '@organisms/_main-article.twig' with {
          main_article: intro_page.main_article2,
        } %}
      </div>

      <div class="col-4">
        {% include '@organisms/_sidebar.twig' with {
          sidebar: intro_page.sidebar,
        } %}
      </div>

    </div>
  </div>

{% endblock content %}

{% block footer %}
  <h2> My Custom Footer Message </h2>
{% endblock footer %}

```

 



### Local Assets 

  
**Why do components have enable/disable/ name variables exported and how does it fit into wider design system**

## Drupal Templates



\* Install PL in Drupal 

Put in custom themes, run commands \(see getting started doc\)



fin drush when using docksal 

* remember to change theme on drupal to see pl 



## Acessbility 



Use sr-only from bootstrap - for screen readers on button etc 



araia true 





