# About TypeScript

### Keturah Howard, June 7th 2020

following [this tutorial (refered to throughout page as `father link`)](https://tutorialzine.com/2016/07/learn-typescript-in-30-minutes)

## _Description_

TypeScript is a tag along language for JS that changes the development process of writing JS code so that you can comfortably transfer into writin gJS from strictly type languages, keep a closer eye on the types that are recieved and returned throughout your code, or simply add another filter of error handling to your develpment process.

The way this is done is through the process of running, confirming there are no type errors, and compiling into js.

## Set up / Instalation

1. in terminal/bash, install with npm
   - ` npm install -g typescript`
2. confiirm instilation with version check
   - `tsc -v` _this should return a version such at '3.19.2'_

_unrelated but possible helpful_
Not installing? make sure that your Node.js / npm versions are compatible. if npm was installed globally you may need to uninstall and reinstall node/npm. The first response in [this stack overflow](https://stackoverflow.com/questions/11177954/how-do-i-completely-uninstall-node-js-and-reinstall-from-beginning-mac-os-x) was helpful in this process. nvm is the suggested process of managing node installations, but I have yet to get nvm up and running.

## Key Concepts (table of contents)

- Compiling
- Static Typing
- Interfaces
- Classes
- Generics
- Modules
- Third Party Declaration Files

### Compiling

This is necassary given TS cannot actually compile in the browser. TS is mainly used to check for errors, and then transforms into JS when no type errors are caught.

- Easiest way is by running `$ tsc filename.ts`
- This will create a js version of ts to compile to the browser (since ts can't compile to the browser. Cute.)
- can do this to multiple files: `$ tsc filename.ts filename2.ts`
- or compile all files with wildcard: `$ tsc *.ts`

### Static Typing

This means declaring the type of a variable, and the compiler assures that the types of the content and script match as expected.

### Type

`type` is a keyword in TypeScript that we can use to define the shape of data.

**Basic Types in TS:**

- String
- Boolean
- Number
- Array
- Tuple
- Enum
- Advanced types

**Primitive Types in TS**:
number, string, boolean, null, and undefined

"Type aliases" provide an alternate name for an existing type:

```
type MyNumber = number;
type User = {
  id: number;
  name: string;
  email: string;
}
```

The two type aliases below represent alternative names for the same union type: string | number. While the underlying type is the same, the different names express different intents, which makes the code more readable.

```
type ErrorCode = string | number;
type Answer = string | number;
```

### Interfaces

These are kind of like presetting blue prints for future _objects_ as types, so that when you refer to them within a function, you will say the name of the interface instead of the actual types... used in cases of checking types of objects and clarifying objects are as they should be in typescript.

## When to use interfaces or types:

- in many cases, they are interchangable, but there are times when one has an advantege over the other depending on the context.

We can use define a type alias for a primitive type: `type Address = string;`...

And we often combine primitive type with union type to define a type alias, to make the code more readable: `type NullOrUndefined = null | undefined;`

But, we can’t use an interface to alias a primitive type. The interface can only be used for an object type.
Therefore, when we need to define a primitive type alias, we use type.

### Classes

Very similar to writing classes / models in C#. You name the class, create a constructor that state the porerties and types expected of an object of that class, and state the methods.

example code from father link:

```class Menu {
  // Our properties:
  // By default they are public, but can also be private or protected.
  items: Array<string>;  // The items in the menu, an array of strings.
  pages: number;         // How many pages will the menu be, a number.

  // A straightforward constructor.
  constructor(item_list: Array<string>, total_pages: number) {
    // The this keyword is mandatory.
    this.items = item_list;
    this.pages = total_pages;
  }

  // Methods
  list(): void {
    console.log("Our menu for today:");
    for(var i=0; i<this.items.length; i++) {
      console.log(this.items[i]);
    }
  }

}

// Create a new instance of the Menu class.
var sundayMenu = new Menu(["pancakes","waffles","orange juice"], 1);

// Call the list method.
sundayMenu.list();
```

### Generics

Templets which allow the same function to acept a variation of types.

example looks like:

```// The <T> after the function name symbolizes that it's a generic function.
// When we call the function, every instance of T will be replaced with the actual provided type.

// Receives one argument of type T,
// Returns an array of type T.

function genericFunc<T>(argument: T): T[] {
  var arrayOfT: T[] = [];    // Create empty array of type T.
  arrayOfT.push(argument);   // Push, now arrayOfT = [argument].
  return arrayOfT;
}

var arrayFromString = genericFunc<string>("beep");
console.log(arrayFromString[0]);         // "beep"
console.log(typeof arrayFromString[0])   // String

var arrayFromNumber = genericFunc(42);
console.log(arrayFromNumber[0]);         // 42
console.log(typeof arrayFromNumber[0])   // number
```

### Modules

Helpful for making code out of small resusable pieces/components.

TS cannot inherently link between files for this functionality, so third party libraries come into play: require.js for front end/browser, and CommonJS for Node.js/ backend

2 files: exporter.ts / importer.ts, holding the functions that handle their referenced concepts

example process:

1.  exporter.ts:

```var sayHi = function(): void {
    console.log("Hello!");
}

export = sayHi;

```

2. importer.ts

```
import sayHi = require('./exporter');
sayHi();
```

3. now compile: `$ tsc --module amd *.ts`
   - --module amd informs typescript we are building modules for require.js

### 3rd Party Declaration Files

When working wth libraries originally intended for JS, we need to use declaration files to make them compatible with TS.

Declaration files have extention ".d.ts", and contains varrious info about library/its API.

To find pre-written ones for the library your using, check out [this popular repo, Definitely Typed](http://definitelytyped.org/)... [this one for Node.js](https://github.com/typings/typings).
