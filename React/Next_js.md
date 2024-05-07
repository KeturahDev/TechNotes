# About Next.js

Keturah Smith, April 28th 2024

References:

- [Code with Mosh Tutorial](https://members.codewithmosh.com/courses/enrolled/2187934)
- [Official Next.js Docs](https://nextjs.org/docs)
- [on server components](https://nextjs.org/docs/app/building-your-application/rendering/server-components#dynamic-functions)
- [Fireship Tutorial](https://youtu.be/__mSgDEOyv8?si=k1UfvzbhAOBjsd0d)

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

When fetching in a server component, the values are automatically cached, but you can opt out of this when using the fetch api by adding `{cache: 'no-store}` as the second argument.

What if you're using an ORM and not making fetch() calls? There's a convention of a exporting a variety of vars where you can set it equal to a values:

```js
export const dynamic = "auto",
  dynamicParams = true,
  revalidate = 0,
  fetchCache = "auto",
  runtime = "nodejs",
  preferredRegion = "auto";
```

**Rendering:**

Client renders on the browser, but server component can be either statically rendered (at build time) or dynamically rendered (at request time). You can make server components dynamically render by adding something like this at the bottom of the server component file:

```js
export const dynamic = "force-dynamic";
```

Also using `cookies()`, `headers()` or `searchParams` in a server component also automatically opts it for dynamic renders

> "cookies() and headers(): Using these in a Server Component will opt the whole route into dynamic rendering at request time."

> "searchParams: Using the searchParams prop on a Page will opt the page into dynamic rendering at request time."

### SSR vs SSG

Server Side Rendering vs Static Site Generation.

SSR:

- SSR dynamically generates content per request
- process of rendering web pages on the server instead of the client’s browser.
- beneficial for content-rich applications and situations where real-time data is crucial.
- more suitable for frequently updated content.

SSG:

- SSG serves pre-built pages
- SSG can have an edge due to faster load times when it comes to SEO

> When implementing SSR or SSG in Next.js, consider the nature of your content and user experience. SSR is ideal for dynamic, user-specific content, while SSG suits static websites like blogs or documentation sites. Avoid common pitfalls such as over-fetching data in SSR or under-utilizing static optimizations in SSG.

## Server Actions

[Good fast paced tutorial](https://youtu.be/O94ESaJtHtM?si=d8mrSkKOXixSuoyj). [Official Next docs](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations)

Eliminates the need for POST api endpoint defined in api/blank/route.ts and calling in a component! Allows for data mutation without rerendering the whole component. Can be defined within a server component or in a seperate file and then imported.

Primarily used in forms but the function can also be used to adjust data like displaying the value of likes.

## Routing

App router:

- introduced in Next 13
- routes surrounded by brackets are "dynamic routes", can be any wildcard value. usefule for id or username vars for detail/profile pages.
- surround routes (folders) with parenthasis to be ignored by the routing system

reserved file names:

- page.ts
- loading.ts
- layout.ts
- not-found.ts

## Incremental Static Regeneration (ISR)

Revalidates the data every number of seconds.

```js
const res = await fetch("domain/api/something", {
  next: { revalidate: 10 },
});
```

## Static Regeneration

[writing this later]

### Quick fact dump

---

router.refresh() updated the router with new information without a full page refresh. Great for calling right after api calls .

### How to start proj

---

- npx create-next-app@latest
