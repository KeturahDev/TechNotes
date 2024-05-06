# About React-Query

Keturah Smith, May 6th 2024

References:

- [react-query docs](https://tanstack.com/query/v5/docs/framework/react/overview)
- [react-query medium article](https://medium.com/bina-nusantara-it-division/understanding-react-query-11e56960e90c)

## _Description_:

A JavaScript library designed to simplify the complex task of data fetching and caching in React applications. It offers a set of hooks and utilities that enable you to manage data from various sources, including REST APIs, GraphQL, or even local state.

### The Problem it solves

Before react query, most devs would have to carve out their own way of fetching and updating data due to theire being a lack of structure in most web frameworks for this functionality.

> This usually means cobbling together component-based state and side-effects, or using more general purpose state management libraries to store and provide asynchronous data throughout their apps.

> While most traditional state management libraries are great for working with client state, **they are not so great at working with async or server state. This is because server state is totally different.**

How is server state different from client state:

- Is persisted remotely in a location you do not control or own
- Requires asynchronous APIs for fetching and updating
- Implies shared ownership and can be changed by other people without your knowledge
- Can potentially become "out of date" in your applications if you're not careful.

Unique things to consider with server data:

- Caching... (possibly the hardest thing to do in programming)
- Deduping multiple requests for the same data into a single request
- Updating "out of date" data in the background
- Knowing when data is "out of date"
- Reflecting updates to data as quickly as possible
- Performance optimizations like pagination and lazy loading data
- Managing memory and garbage collection of server state
- Memoizing query results with structural sharing

```tsx
import {
  QueryClient,
  QueryClientProvider,
  useQuery,
} from "@tanstack/react-query";

const queryClient = new QueryClient();

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Example />
    </QueryClientProvider>
  );
}

function Example() {
  const { isPending, error, data } = useQuery({
    queryKey: ["repoData"],
    queryFn: () =>
      fetch("https://api.github.com/repos/TanStack/query").then((res) =>
        res.json()
      ),
  });

  if (isPending) return "Loading...";

  if (error) return "An error has occurred: " + error.message;

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.description}</p>
      <strong>👀 {data.subscribers_count}</strong>{" "}
      <strong>✨ {data.stargazers_count}</strong>{" "}
      <strong>🍴 {data.forks_count}</strong>
    </div>
  );
}
```

## Core Concepts:

- Allows for internally refetching, caching, and sharing your queries throughout your application.
- Uses 2 hooks to manage interacting with datastores: useQuery and useMutate.

## Anatomy of React Query

### Set Up

To install: `npm install @tanstack/react-query
`

Need to use provider and client for React Query:

```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { QueryClientProvider, QueryClient } from "@tanstack/react-query";

const root = ReactDOM.createRoot(
  document.getElementById("root") as HTMLElement
);

const queryClient = new QueryClient();

root.render(
  <QueryClientProvider client={queryClient}>
    <App />
  </QueryClientProvider>
);
```

Now you can use the hooks.

### Hooks

---

Anatomy meaning the peices of implenting the library.

Hooks: 2 options, useQuery, useMutation.

### Difference between useQuery and useMutation

- Purpose: `useQuery` is for reading data, while `useMutation` is for modifying data.
- Typical Use Case: `useQuery` is used when you want to fetch and display data, while `useMutation` is used when you want to make changes to that data.
- Return Values: `useQuery` returns `{ data, error, isLoading, isFetching }`, while `useMutation` returns `{ mutate, data, error, isError, isLoading, isSuccess }`.
  Error Handling: Both hooks handle errors, but `useMutation` provides additional features for handling **_optimistic updates_** and **rollbacks** in case of errors during mutations.

**_For useQuery():_**

- First argument: queryKey. which is a unique key for the query. Syntax is a bracket with a string inside to label the data. This label identifies the set of data and _used internally for refetching, caching, and sharing your queries throughout your application_.
- Second argument: queryFn. A function that returns a promise that: Resolves the data, or throws an error.

```tsx
import { useQuery } from "@tanstack/react-query";

function App() {
  const result = useQuery({ queryKey: ["todos"], queryFn: fetchTodoList });
}
```

The result object contains a few very important states you'll need to be aware of to be productive. A query can only be in one of the following states at any given moment:

- isPending or status === 'pending' - The query has no data yet
- isError or status === 'error' - The query encountered an error
- isSuccess or status === 'success' - The query was successful and data is available

Beyond those primary states, more information is available depending on the state of the query:

- error - If the query is in an isError state, the error is available via the error property.
- data - If the query is in an isSuccess state, the data is available via the data property.
- isFetching - In any state, if the query is fetching at any time (including background refetching) isFetching will be true.

For most querries, it is usually sufficient to check the states in this order: isPending, isError, Success:

```tsx
// this works too:
// const { status, data, error } = useQuery({
const { isPending, isError, data, error } = useQuery({
  queryKey: ["todos"],
  queryFn: fetchTodoList,
});

if (isPending) {
  return <span>Loading...</span>;
}

// this work too:
//if (status === 'pending') {
//    return <span>Loading...</span>
//  }

if (isError) {
  return <span>Error: {error.message}</span>;
}

// We can assume by this point that `isSuccess === true`
return (
  <ul>
    {data.map((todo) => (
      <li key={todo.id}>{todo.title}</li>
    ))}
  </ul>
);
```

**_For useMutation():_**

Quick points:

- used for posts/updates/deletes.
- does not require query keys, as data is not cached

Like useQuery, Mutations can only be one status in a given moment.
Available Statuses:

- isIdle or status === 'idle' - The mutation is currently idle or in a fresh/reset state
- isPending or status === 'pending' - The mutation is currently running
- isError or status === 'error' - The mutation encountered an error
- isSuccess or status === 'success' - The mutation was successful and mutation data is available

Available information beyond status:

- error - If the mutation is in an error state, the error is available via the error property.
- data - If the mutation is in a success state, the data is available via the data property.

```tsx
function App() {
  const mutation = useMutation({
    mutationFn: (newTodo) => {
      return axios.post("/todos", newTodo);
    },
  });

  return (
    <div>
      {mutation.isPending ? (
        "Adding todo..."
      ) : (
        <>
          {mutation.isError ? (
            <div>An error occurred: {mutation.error.message}</div>
          ) : null}

          {mutation.isSuccess ? <div>Todo added!</div> : null}

          <button
            onClick={() => {
              mutation.mutate({ id: new Date(), title: "Do Laundry" });
            }}
          >
            Create Todo
          </button>
        </>
      )}
    </div>
  );
}
```

## Impmortant Defaults

- [Offical Doc about defaults](https://tanstack.com/query/v5/docs/framework/react/guides/important-defaults)

## Increasing complexity with useQuery

Theres more you can do with:

- Query Keys
- Parellel Queries
- Dependent Queries
- Background Fetching Indicators
- Paginated Quereis
- Placeholder Query Data
- Disabling / Pausing Queries

To be continued..

### Projects Used:

- []()
