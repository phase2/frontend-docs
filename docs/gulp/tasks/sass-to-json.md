This gulp task watches our global configuration-related sass files, ie the ones that are setting variables, in order to generate sample data objects for our configuration-related patterns.
 
Basically, it's looking for any variables prefixed with certain strings, as defined in the gulpfile configuration, to write those variables into an array of individual json objects that a few patterns are looking at.

By default, it checks for:

- colors (**$c-**)
- font families (**$ff--**)
- font sizes (**$fs--**)
- breakpoints (**$bp--**)
- spacing (**$spacing--**)