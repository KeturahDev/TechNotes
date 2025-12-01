# About Ruby on Rails

Keturah Smith, December 1st 2025

References:

## _Description_:

An MVC Framework for ruby that aims to be an all in one place to deal with everything backend- networking, routing, server management, etc.

Famous for quickly spinning up fully functioning backends by prioritizing convention over configuration.

## Core Concepts:

- MVC archetecture
- Convention over configuration- heavy use of naming conventions to make everything work
- ActiveRecord ORM layer
- Navigates traffic with Routing in config/routes.rb

---

### ActiveRecord ORM layer

_ORM stands for Object-Relational Mapping- its how classes are coordinated with database tables_

- Maps Ruby classes to database tables automatically
- Provides built in CRUD for all classes
- Allows you to write Ruby instead of SQL, while still allowing you to write SQL if you want
- Includes validation and callbacks

---

### Routing

- The config/routes.rb file defines URL → controller/action mappings.
- Supports RESTful routes by default, e.g.: resources :users
- Routing is convention-driven (looking at the name) (e.g., /posts → PostsController).

<small> RESTful is an archetecural style that uses a stateless client-server communication model, dealing with data and functionality that is managed by a uniform interface of HTTP methods (GET, POST, PUT, DELETE)</small>

---

### Rails File Structure (High-Level)

- `app/models` → business logic + database interactions
- `app/controllers` → request handlers
- `app/views` → HTML templates
- `config/` → application settings/routes/env configs
- `db/` → migrations + schema
- `app/helpers` → view helpers
- `app/assets` → JS, CSS, images (unless using import maps/JS bundlers)
- `app/jobs` → background jobs

---

### Migrations

- Ruby files that modify the database schema
- Version-controlled, reversible
- You run them with commands like:
  - `rails db:migrate`
  - `rails db:rollback`

---

### The Request Lifecycle

1. Browser hits URL
2. Route matches → directs to controller/action
3. Controller fetches/updates models
4. Controller renders view or returns JSON
5. Response goes back to browser

### Projects Used:

- []()
