# About Prisma

Keturah Smith, April 30th 2024
References:

## _Description_:

An ORM (object relational mapping) that provides a **client** that is used to allow the application to work with a database. When installed, it generates a prisma.schema file that uses its own syntax to define the schema of database tables.

On **migration**, prisma will generate the changes made in the schema in the database provider's syntax.

## Core Concepts:

### Important CLI commands:

- prisma format -> makes the prisma schemas "pretty"
- prisma migrate dev -> do after making changes to the schema file

## Setup

- install prisma at root of project: `npm i prisma`
- initialize prisma in the project: `npx prisma init`
  - this creates a prisma folder, and generates a schema.prisma file in the folder.
- change the datasource provider to that of your choosing
- in .env file, set DATABASE_URL to the database url you want to interact with
- implement models in the schema.prisma

```
model Issue {
  id          Int      @id @default(autoincrement())
  title       String   @db.VarChar(255)
  description String   @db.Text
  status      Status   @default(OPEN)
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
}

enum Status {
  OPEN
  IN_PROGRESS
  CLOSED
}
```

## Interacting with Google Provider

This is actually done through NextAuth, but for time being it will live here. It's somewhat relevent because the NextAuth needs a Prisma Adapter anyway for storing user data. But, this info will be relocated to the NextAuth Doc when it's created.

<!-- TODO: Add this section to NextAuth doc -->

1. Need to set up the project on https://console.developers.google.com/

- click create a new prjoject by selecting dropdown in nav
- (.. to be continued)

## _When adding authorized redirects:_

This is neccessary when moving from the local machine to the hosted domain. Only authorized redirects may interact with the the registered google project.

- Go to https://console.developers.google.com/
- Go to Credentials
- Click on the Project's name under "OAuth Client IDs"
- Add domain name in place of local host URI, following this format: http://localhost:3000/api/auth/callback/google

### Projects Used:

- [issue tracker](https://github.com/KeturahDev/issue-tracker)
- [next app demo](https://github.com/KeturahDev/next-app)
