# About Procedural Programming

Keturah Smith, Jan 25 2025

References:

- [What it is](https://hackr.io/blog/procedural-programming)

## _Description_:

A programming paradigm- In procedural programming, each subroutine, or procedure, is executed in a specific order. The program uses variables to store data and control structures to manage the flow.

Focuses on the order in which things happen in the program (ex: hydrate the data globally depending on the local storage variables before rendering the components that have conditional rendering based on the presence of that data)

## Core Concepts:

1. Procedural Calls (Routines): Organizes code into reusable procedures or functions that perform specific tasks.
2. Linear Program Flow: Follows a sequential execution path, with clearly defined beginning and end points for a series of computational steps.
3. Top-Down Design: Breaks down complex problems into simpler, smaller procedures for easier management and understanding.
   4.Global and Local Variables: Supports the use of global and local variables to store data, accessible within or across procedures.
4. Modularity: Allows for code reusability and better organization through separate procedures or functions.
5. Parameter Passing: Enables data exchange between procedures using parameters, promoting code modularity and flexibility.
6. State Mutability: Typically involves direct manipulation of variables and data, often leading to state changes throughout the program.

Pros:

- Simple, because it's Linear: Clear, sequential flow of control, making it easy to follow the logic
- Efficieny = Direct manipulation of data with minimal overhead, often leading to faster performance.

Cons:

- Scalability Issues: Becomes hard to manage as codebase grows due to lack of modularity.
- Code Duplication: Encourages repetitive code (due to the direct ), making maintenance challenging.

### Relevence:

(for I, a mostly frontend focused developer that uses react)..
Best avoided in React, as it inherently promotes mutability and Reacts structure is based off of immutability (one of the core concepts of functional programming).

It's not bad to be used in hooks or functions that mostly tend to their own scope.

### Projects Used:

- []()
