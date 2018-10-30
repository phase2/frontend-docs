# TypeScript

TypeScript is a superset of JavaScript, meaning that it has the same functionality of JavaScript, but with the added benefit of static typing with decorators. All valid JavaScript is valid TypeScript. The main differentiator is that TypeScript will enforce strong and static typing. TypeScript is compiled to JavaScript that can then be consumed natively or included in module bundlers.

## Breakdown of types

There are two differing spectrum in effect when considering the type system of a language. The first is whether the language enforces dynamic or static type checking. Dynamic type checking happens at runtime and a type error will throw an exception in the runtime such as `undefined is not a function`. Depending on the error and the error handling this may result in the catastrophic failure of the script or application. Static typing checks for type errors at compile time as the developer is writing the code. Some compilers will also fail to compile the code if they encounter an error. Elm and ReasonML do this by default and TypeScript can be configured to do so if desired. This provides the benefit of identifying type issues as the code is being written or refactored.

The second spectrum to consider is whether the language enforces strong or weak typing. A language which employs strong typing will generally require explicit type coercions and identify if an operation is expecting a different type than what it is supplied. Conversely, a language which employs weak typing will attempt to coerce values together which may lead to unanticipated results such as `1 + “2” = “12”`.

Type Safety is the combination of these two spectrum to represent the extent that a language discourages or prevents type errors. JavaScript is both a weak and dynamically typed language. It does type coercion regularly (see example above) and will rapidly disassemble when encountering type errors at runtime. It does nothing to warn about type errors at compile time since it is compiled just before runtime. Additionally, JavaScript does a poor job in handling values which may potentially be null or undefined. TypeScript utilizes static and strong typing to allow these sorts of errors to be identified before runtime through editor integration and CLI tools.

## Additional functionality

TypeScript brings several additional pieces of functionality that are not present in Vanilla JavaScript. Below are some highlights, but the complete list of types available in TypeScript can be found HERE.

- True use of enums
- The ability to create a union type of various set string values, for example different variants a component may have.
- Explicit handling of maybe types where data may or may not be present. If there is a maybe type present, TypeScript will force you to handle both the case when the value is there and when it is not. See example below.
- Tuples for fixed length arrays of set types at each position

```typescript
    interface Person {
    	firstName: string;
    	lastName: string;
    	age?: number;
    }
    
    function isOver21(person: Person): boolean {
    	if (person.age >= 21) {
    		return true;
    	} else if (!person.age || person.age < 21) {
    		return false;
    	}
    }
```

## Third Party Libraries

Third party libraries will need to have accompanying type definitions for the modules. Some libraries are themselves written in TypeScript and include an index.d.ts file which contains the type definitions for the library. If you are getting type errors when importing a third party library, it does not have associated types shipped with it. [DefinitelyTyped](http://definitelytyped.org/) is an open source collection of type definitions for third party libraries that can be installed as an npm package.

## Additional Resources

- [TypeScript Homepage](https://www.typescriptlang.org/)
- [Migrating from JavaScript - TypeScript docs](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)
- [What problems types solve](https://www.phase2technology.com/blog/embracing-type-systems-in-javascript)
- [Swipe Left, Uncaught TypeError: Learning to Love Type Systems by Lauren Tan](https://www.youtube.com/watch?v=y3uXazpAdwo)
