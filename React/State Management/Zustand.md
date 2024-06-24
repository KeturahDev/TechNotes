# About Zustand

### Keturah Smith, April 28th 2024

references:

- [official zustand docs](https://docs.pmnd.rs/zustand/getting-started/introduction#installation)

## _Description_

Zustand is a state management library for React that provides a simple and lightweight way to handle state in your application. Here are some key concepts:

Built to deal with common pitfalls, like the dreaded [zombie child problem](https://react-redux.js.org/api/hooks#stale-props-and-zombie-children), [React concurrency](https://github.com/bvaughn/rfcs/blob/useMutableSource/text/0000-use-mutable-source.md), and [context loss](https://github.com/facebook/react/issues/13332) between mixed renderers.

(zombie children are comonents that should have been desroyed, but momentarily aren't)
(react concurency is the enabling of time-slicing and priority scheduling)
(context loss between mixed renders... self explanatory.)

## Core Concepts:

### Redux-like API

Zustand follows a similar pattern to Redux, with actions, state, and selectors.

- Both are based on an immutable state model. However, _Redux requires your app to be wrapped in context providers; Zustand does not._

<table>
<tr>
<th>Zustand</th>
<th>Redux</th>
</tr>
<tr>
<td>

```typescript
import { create } from "zustand";

type State = {
  count: number;
};

type Actions = {
  increment: (qty: number) => void;
  decrement: (qty: number) => void;
};

type Action = {
  type: keyof Actions;
  qty: number;
};

const countReducer = (state: State, action: Action) => {
  switch (action.type) {
    case "increment":
      return { count: state.count + action.qty };
    case "decrement":
      return { count: state.count - action.qty };
    default:
      return state;
  }
};

const useCountStore = create<State & Actions>((set) => ({
  count: 0,
  dispatch: (action: Action) => set((state) => countReducer(state, action)),
}));
```

</td>
<td>

```typescript
import { createStore } from 'redux'
import { useSelector, useDispatch } from 'react-redux'

type State = {
  count: number
}

type Action = {
  type: 'increment' | 'decrement'
  qty: number
}

const countReducer = (state: State, action: Action) => {
  switch (action.type) {
    case 'increment':
      return { count: state.count + action.qty }
    case 'decrement':
      return { count: state.count - action.qty }
    default:
      return state
  }
}

const countStore = createStore(countReducer)

.......


import { createSlice, configureStore } from '@reduxjs/toolkit'

const countSlice = createSlice({
  name: 'count',
  initialState: { value: 0 },
  reducers: {
    incremented: (state, qty: number) => {
      // Redux Toolkit does not mutate the state, it uses the Immer library
      // behind scenes, allowing us to have something called "draft state".
      state.value += qty
    },
    decremented: (state, qty: number) => {
      state.value -= qty
    },
  },
})

const countStore = configureStore({ reducer: countSlice.reducer })
```

</td>
</tr>
</table>

**Immutable State**: State in Zustand is immutable, meaning you create new state objects instead of mutating existing ones.

**Centralized Store**: Zustand has a single, centralized store that holds the entire state of your application.

**Hooks-based API**: Zustand uses React hooks to interact with the store, making it easy to integrate with functional components.

**Middleware Support**: Like Redux, Zustand supports middleware for handling side effects, logging, and other cross-cutting concerns.

**Devtools Integration**: Zustand integrates with the Redux DevTools extension, allowing you to inspect and debug your application's state.

**Minimal Boilerplate**: Zustand aims to be a minimal, boilerplate-free solution for state management, making it easy to get started and maintain.

**Modular Store**: Zustand supports splitting your store into multiple slices, making it easier to manage and scale your application's state as it grows.
