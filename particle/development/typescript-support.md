# TypeScript in Particle

## Getting Started

As of 10.3, TypeScript is available as a development option instead of JavaScript. TypeScript brings static typing to JavaScript for more robust code and the ability to identify type errors at compile time rather than runtime. It is completely opt-in and can be used with both `.js` files as well as `.vue` files.

To convert a JavaScript file to TypeScript change the file extension from `.js` to `.ts`. This will tell the Typescript compiler to parse the file and identify any type errors. Typescript file extensions are auto-resolved by Webpack and can be omitted in the import path, similar to a JavaScript module. Example: `import Component from ‘../typescript-component’;`

Note: if you are using TypeScript with React you must use the `.tsx` extension.

## Add TypeScript to a Vue Single File Component (SFC)

You can also add Typescript to `.vue` files to get all of the benefits of Typescript and single file components in Vue. **Note: This process differs slightly from converting a `.js` file.**

In order to use Typescript in a Vue component three things must be converted:

1. Add `lang="ts”` to the script tag of your component.
2. Import Vue at the top of your script block. `import Vue from ‘vue’;`
3. Wrap your Vue export in `Vue.extend()`

There are some unique behaviors with regard to linting and type checking Vue SFCs. Since the file extension does not terminate in `.ts` they will not be picked up by the TypeScript specific scripts in the package.json. They are linted through an extension of ESLint due to their unique structure containing templates and styles. In order to check the types within a SFC, the dev server must be running and will print errors to the console.

The Webpack configuration appends a `.ts` extension to Vue files so that they are parsed through TypeScript before being passed on to Babel. This does not affect Vue components which are using JavaScript. They will simply pass through the TypeScript loader to the Babel loader.

## TypeScript related package scripts

Several new scripts were created to aid development when working with TypeScript in Particle:

- `npm run type-check`: This script will run the TypeScript compiler in watch mode and print out errors to the console. It will auto update with each file save and can be run without starting the dev server. If you are running the dev server, type errors will be printed to that process, similar to the existing ESLint loader.
- `npm run lint:ts`: This script will lint TypeScript files through TSLint and attempt to automatically resolve issues where it can. TSLint is a separate linter than ESLint and it's configuration lives at `/tslint.json`.
- `npm run fmt:ts` This script runs Prettier with TypeScript defined as the parser and will write changes to the existing file.

## Images.d.ts file

Typescript relies on understanding how to parse each imported module it receives. This includes images which are handled by Webpack. To tell Typescript that these imports are modules without a specific type structure we declare them once in `tools/typings/images.d.ts`. A base level of files has already been provided but may need to be tweaked or added to on a per project basis.

The Typescript compiler will let you know if it does not understand how to parse a module. If the module is a third party library look at Definitely Typed. If it is a media file, you will likely need to add it to the images definition file. The format for these declarations is `declare module '*.svg’` where ‘svg’ is the associated file extension.

## How to Type Entry Files

Particle already has type declarations installed for common dependencies: Node, Jest, jQuery, and Bootstrap. The root index file for a component can also be converted to TypeScript which allows for typing of custom settings that may exist. An example file can be found at `source/default/_patterns/02-molecules/carousel/index.ts`. There are a couple of changes that will be made to each file using TypeScript:

- The jquery import will need to be changed from `import $ from 'jquery';` to `import * as $ from 'jquery';` for proper type resolution.
- Any reference to `$context` will need to be annotated with the JQuery type. For example: `export function enable($context: JQuery, { carousel = {} }) {...}`. This tells TypeScript that context is of type JQuery.
