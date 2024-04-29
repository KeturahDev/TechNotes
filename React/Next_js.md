# About Next.js

Keturah Smith, April 28th 2024

References:

- [Official Next.js Docs](https://nextjs.org/docs)
- [Code with Mosh Tutorial](https://members.codewithmosh.com/courses/enrolled/2187934)

## Basic overview

### What is it?

A framework for build fast search enginer friendly apps in react

### How does it do that?

Fast: Serverside rendering for components that aren't marked as a client component. This allows for static rendering and data caching in the memory / file system / Network.
Search Engine Friendly: Meta data configurable to every page

### What does it look like?

Theres different routing systems, but the newer one is App router:

Folder Structure for App router

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
