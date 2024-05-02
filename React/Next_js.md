# About Next.js

Keturah Smith, April 28th 2024

References:

- [Code with Mosh Tutorial](https://members.codewithmosh.com/courses/enrolled/2187934)
- [Official Next.js Docs](https://nextjs.org/docs)
- [on server components](https://nextjs.org/docs/app/building-your-application/rendering/server-components#dynamic-functions)

## Basic overview

### What is it?

A framework for build fast search enginer friendly apps in react.

### How does it do that?

Fast: Serverside rendering for components that aren't marked as a client component. This allows for static rendering and data caching in the memory / file system / Network.
Search Engine Friendly: Meta data configurable to every page.

### What does it look like?

Theres different routing systems, but the newer one is App router and looks like this...

Folder Structure for App router:

```
My-App
  * app
    * api
      * cars
        - route.ts // API endpoint for http:domain/api/cars
      * roads
        - route.ts // API endpoint for http:domain/api/roads
    * cars
      - page.tsx // UI for http:domain/cars
    - page.tsx // UI for http:domain/
```

## Core Concepts

- Routing
- Server Components
- Server Actions
- Caching
- "Optimistic Updates"
- SSR / SSG
- Patters & Best Practices (data fetching, serverside validation, avoiding leaks)

### Server Components

---

Components created in the next.js environment are server components by default, and this only changes if turned into client component with adding 'use client' at the top of the component file.

These allow for caching on fetched data, which means storing the data where it is faster to access:

- Memory
- File System
- Network

The farther down that list, the slower the access, but all these are available to server components via caching.

**Rendering:**

Client renders on the browser, but server component can be either statically rendered (at build time) or dynamically rendered (at request time). You can make server components dynamically render by adding something like this at the bottom of the server component file:

```js
export const dynamic = "force-dynamic";
```

Also using `cookies()`, `headers()` or `searchParams` in a server component also automatically opts it for dynamic renders

> "cookies() and headers(): Using these in a Server Component will opt the whole route into dynamic rendering at request time."

> "searchParams: Using the searchParams prop on a Page will opt the page into dynamic rendering at request time."

## Server Actions

[Good fast paced tutorial](https://youtu.be/O94ESaJtHtM?si=d8mrSkKOXixSuoyj). [Official Next docs](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations)

Eliminates the need for POST api endpoint defined in api/blank/route.ts and calling in a component! Allows for data mutation without rerendering the whole component. Can be defined within a server component or in a seperate file and then imported.

Primarily used in forms but the function can also be used to adjust data like displaying the value of likes.
