# About Javascript

Keturah Smith, May 1st 2024

References: [js cheatsheat](https://htmlcheatsheet.com/js/), [mozilla docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop), [Javascript es6 Docs](https://www.w3schools.com/js/js_es6.asp)

## _Description_:

Overview of the fundementals for Javascript.

What is it? The primary programming language for interactive and dynamic DOM manipulation for web applications in browsers. Also capable of being used in backend code via Node

## Core Concepts:

- Array Methods
- Object Methods
- ES6 changes
- Functions (arrow vs functional)
- Fetch API
- Asynchronis Code (promises, async / await)
- DOM / Web platform
- Bracket notation

## Asynchronis Code

[Doc for the difference.](https://www.geeksforgeeks.org/difference-between-promise-and-async-await-in-node-js/)

```js
const promise = new Promise(function (resolve, reject) {
  const string1 = "geeksforgeeks";
  const string2 = "geeksforgeeks";
  if (string1 === string2) {
    resolve();
  } else {
    reject();
  }
});
```

### Promises

Promise is an object representing intermediate state of operation which is guaranteed to complete its execution at some point in future.

Promises have 3 states: resolved, rejected and pending.

Error handling is done with .then() and .catch()

```js
promise
  .then(function () {
    console.log("Promise resolved successfully");
  })
  .catch(function () {
    console.log("Promise is rejected");
  });
```

### Async Await

Syntactic sugar for promises.

The await will return either the resolved or rejected state.

Error handling is managed with a try/catch wrapper.

```js
async function demoPromise() {
  try {
    let message = await helperPromise();
    console.log(message);
  } catch (error) {
    console.log("Error: " + error);
  }
}
```

## Fetch API

A JavaScript interface for accessing and manipulating application requests and responses.

Quick about:

- Promise based
- easily used in [service workers]()
- integrates advanced HTTP concepts like CORS

```js
async function logMovies() {
  const response = await fetch("http://example.com/movies.json");
  const movies = await response.json();
  console.log(movies);
}
```

## Array

A collection of values that can be accessed by their index.

<details>
  <summary>The cheatsheet blurb on arrays</summary>
  
```js
let dogs = ["Bulldog", "Beagle", "Labrador"]; 
let dogs = new Array("Bulldog", "Beagle", "Labrador");  // declaration

alert(dogs[1]); // access value at index, first item being [0]
dogs[0] = "Bull Terier"; // change the first item

for (let i = 0; i < dogs.length; i++) { // parsing with array.length
console.log(dogs[i]);
}

---

dogs.toString(); // convert to string: results "Bulldog,Beagle,Labrador"

dogs.join(" _ "); // join: "Bulldog _ Beagle \* Labrador"

dogs.pop(); // remove last element

dogs.push("Chihuahua"); // add new element to the end

dogs[dogs.length] = "Chihuahua"; // the same as push

dogs.shift(); // remove first element

dogs.unshift("Chihuahua"); // add new element to the beginning

delete dogs[0]; // change element to undefined (not recommended)

dogs.splice(2, 0, "Pug", "Boxer"); // add elements (where, how many to remove, element list)

let animals = dogs.concat(cats,birds); // join two arrays (dogs followed by cats and birds)

dogs.slice(1,4); // elements from [1] to [4-1]

dogs.sort(); // sort string alphabetically

dogs.reverse(); // sort string in descending order

x.sort(function(a, b){return a - b}); // numeric sort

x.sort(function(a, b){return b - a}); // numeric descending sort

highest = x[0]; // first item in sorted array is the lowest (or highest) value

x.sort(function(a, b){return 0.5 - Math.random()}); // random order sort

````

</details>

### Methods:

---

<details>
  <summary>.map()</summary>

### _.map()_

Returns a new Array populated with the results of calling the provided funtion on every element in the calling array.

**_Use When_**: generating a list of information based off each individual indicy

```js
const array1 = [1, 4, 9, 16];

// Pass a function to map
const map1 = array1.map((x) => x * 2);

console.log(map1);
// Expected output: Array [2, 8, 18, 32]
````

</details>
<details>
  <summary>.entries()</summary>

### _.entries()_

Returns an _array iterator object_ that contains key value pairs of each index in the array

**_Use When_**: You want to use both index and value in the output of the loop you run.

```js
const productWithIndex = [];

for (const [index, product] of products.entries()) {
  productWithIndex.push(`${index}: ${product}`);
}

console.log(productWithIndex);
// Output: ['0: Laptop', '1: Tablet', '2: Smartphone', '3: Headphones']

...

const array1 = ['a', 'b', 'c'];

const iterator1 = array1.entries();

console.log(iterator1.next().value);
// Expected output: Array [0, "a"]

console.log(iterator1.next().value);
// Expected output: Array [1, "b"]


```

</details>
<details>
  <summary>.flatMap()</summary>

### _.flatMap()_

Returns a new Array populated with the results of calling the provided funtion on every element in the calling array, and then "flattening the result by one level. Same as calling .map and .flat but slightly more efficient.

**_Use When_**: Wanting to map over an array that contain data structures that would provide arrays as that value.

```js
const arr1 = [1, 2, 1];

const result = arr1.flatMap((num) => (num === 2 ? [2, 2] : 1));

console.log(result);
// Expected output: Array [1, 2, 2, 1]
// Instead of: Array [1, [2, 2], 1]
```

</details>
<details>
  <summary>.pop()</summary>

### _.pop()_

Removes the _last_ element from the called array and returns that element. Changes the length of the called array.

**_Use When_**: Array represents progressive steps and the user wants to simulate going back.

```js
const plants = ["broccoli", "cauliflower", "cabbage", "kale", "tomato"];

console.log(plants.pop());
// Expected output: "tomato"

console.log(plants);
// Expected output: Array ["broccoli", "cauliflower", "cabbage", "kale"]
```

</details>
<details>
  <summary>.shift()</summary>

### _.shift()_

Removes the _first_ element from an array and returns that removed element. This method changes the length of the array.

**_Use When_**: Array represents a line of first come first disapear and the user is progressing.

```js
const plants = ["broccoli", "cauliflower", "cabbage", "kale", "tomato"];

console.log(plants.shift());
// Expected output: "broccoli"

console.log(plants);
// Expected output: Array ["cauliflower", "cabbage", "kale", "tomato"]
```

</details>

<details>
  <summary>.forEach()</summary>

### _.forEach()_

For each indicy in the array, the given function is executed. Does not return another array.

**_Use When_**: Wanting to execute a function for each indicy in an array.

```js
const array1 = ["a", "b", "c"];

array1.forEach((element) => console.log(element));
```

</details>

<details>
  <summary>.filter()</summary>

### _.filter()_

Return an array made of up indicies that resolve the given function as truthy.

**_Use When_**: Wanting to get a filtered array of values.

```js
const words = ["spray", "elite", "exuberant", "destruction", "present"];

const result = words.filter((word) => word.length > 6);

console.log(result);
// Expected output: Array ["exuberant", "destruction", "present"]
```

</details>

<details>
  <summary>.reduce()</summary>

### _.reduce()_

Returns a single value made up of running all the values of the given array through the provided function.

**_Use When_**: Wanting to have a single value returned from iterating over your array.

```js
const array1 = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array1.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  initialValue
);

console.log(sumWithInitial);
// Expected output: 10
```

</details>

<details>
  <summary>.sort()</summary>

### _.sort()_

Returns a reordered array based on the sort order function passed in.

**_Use When_**: Needing to have the indicies in an array in a specific order.

```js
const items = [
  { name: "Edward", value: 21 },
  { name: "Sharpe", value: 37 },
  { name: "And", value: 45 },
  { name: "The", value: -12 },
  { name: "Magnetic", value: 13 },
  { name: "Zeros", value: 37 },
];

// sort by value
items.sort((a, b) => a.value - b.value);

// sort by name
items.sort((a, b) => {
  const nameA = a.name.toUpperCase(); // ignore upper and lowercase
  const nameB = b.name.toUpperCase(); // ignore upper and lowercase
  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }

  // names must be equal
  return 0;
});
```

</details>

## Object:

A datatype that represents keyed collection and more complex entities.

```js
{name: "keturah", age: 25, friends: [{name: 'Zack', status: 'husband'}, {name: "Mattie", status 'highschool homie'}]}
```

### Methods

---

<details>
  <summary>.entries()</summary>

### _.entries()_

The Object.entries() static method returns an array of a given object's own enumerable string-keyed property key-value pairs.

**_Use When_**: Wanting to map over the content in an object's keys and values

```js
// Strings have indices as enumerable own properties
console.log(Object.entries("foo"));
// [ ['0', 'f'], ['1', 'o'], ['2', 'o'] ]

...

const object1 = {
  a: 'somestring',
  b: 42,
};

for (const [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}

// Expected output:
// "a: somestring"
// "b: 42"


```

</details>

<details>
  <summary>.fromEntries()</summary>

### _.fromEntries()_

The Object.fromEntries() static method transforms a list of key-value pairs into an object.

**_Use When_**: Wanting to generate an object based off a collection of key value pairs. Valid collection DataType's include Maps and Arrays

```js
const entries = new Map([
  ["foo", "bar"],
  ["baz", 42],
]);

const obj = Object.fromEntries(entries);

console.log(obj);
// Expected output: Object { foo: "bar", baz: 42 }
```

</details>

<details>
  <summary>.keys()</summary>

### _.keys()_

The Object.keys() static method returns an array of a given object's own enumerable string-keyed property names.

**_Use When_**: Wanting to do something with a list of keys in an object

```js
const object1 = {
  a: "somestring",
  b: 42,
  c: false,
};

console.log(Object.keys(object1));
// Expected output: Array ["a", "b", "c"]
```

</details>
<details>
  <summary>.values()</summary>

### _.values()_

The Object.values() static method returns an array of a given object's values.

**_Use When_**: Wanting to do something with a list of keys in an object

```js
const object1 = {
  a: "somestring",
  b: 42,
  c: false,
};

console.log(Object.values(object1));
// Expected output: Array ["somestring", 42, false]
```

</details>
<details>
  <summary>.seal()</summary>

### _.seal()_

The Object.seal() static method seals an object. Sealing an object prevents extensions and makes existing properties non-configurable. A sealed object has a fixed set of properties: new properties cannot be added, existing properties cannot be removed, their enumerability and configurability cannot be changed, and its prototype cannot be re-assigned. Values of existing properties can still be changed as long as they are writable. seal() returns the same object that was passed in.

**_Use When_**: Want to prevent any further changes to the object's properties.

```js
const object1 = {
  a: "somestring",
  b: 42,
  c: false,
};

console.log(Object.keys(object1));
// Expected output: Array ["a", "b", "c"]
```

</details>

## ES6 Changes

AKA ECMAScript6. The 2nd major revision to javascript. Rolled out in 2015.

**General Changes**:

- intorduced let and const
- introduced arrow functions
- introduced the spread opperator [...]
- introduced Map and Set Objects
- introduced the For / Of Loop
- javascript classes
- promises (!? I didnt know that it was that late)

### Spread Operators

- cover order for overwriting key values {...ob1, key: "lastword"}

### Map Objects

A Map holds key-value pairs where the keys can be any datatype.
A Map remembers the original insertion order of the keys.

```js
const fruits = new Map([
  ["apples", 500],
  ["bananas", 300],
  ["oranges", 200],
]);
```

You can add elements to a Map with the set() method:

```js
// Create a Map
const fruits = new Map();

// Set Map Values
fruits.set("apples", 500);
fruits.set("bananas", 300);
fruits.set("oranges", 200);
```

The set() method can also be used to change existing Map values:
`fruits.set("apples", 200);
`

The get() method gets the value of a key in a Map: `fruits.get("apples");    // Returns 500
`

### Set Objects

A JavaScript Set is a collection of unique values.
Each value can only occur once in a Set.
The values can be of any type, primitive values or objects.

```js
// Create a Set
const letters = new Set();

// Add some values to the Set
letters.add("a");
letters.add("b");
letters.add("c");
...
const letters = new Set(["a","b","c"]);

```
