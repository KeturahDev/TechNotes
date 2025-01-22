# About React

Keturah Smith, [month day year]

References:

## _Description_:

## Core Concepts:

- Components
- Props
- Hooks (useState, useEffect, costom hooks)
- State Management (Context API vs Zustand vs Redux)
- Styling (Tailwind & Styled Components)
- Patterns & Best Practices

## Hooks:

### useState:

used for storing local state. This persists the values between component renders! So,
Once the state is changed, the entire component rerenders

### useEffect:

This hook is required for managing code dependent on the component **_life cycle_**, such as on mount, on updateand on dismount.

Used for running code WHEN you want it to be ran... based on the dependency array (second arg). If empty, on runs once, on the first mount. Otherwise, the variables added to the array determine when the code in the forst parameter is ran again: if a variable in the dependency array changes, the code block is ran again.

- component did mount: empty dependency array.
- component rerendered: no dependency array.
- component unmount: return statement in the first arg's function.

## State Managements:

## Getting Started:

### Projects Used:

- []()
