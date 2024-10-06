---
title: Application Architecture
parent: Chapters
nav_order: 1
---

### Table of Contents
- [Application Architecture](#application-architecture)
  - [Technologies Used](#technologies-used)
    - [Frontend](#frontend)
    - [Backend](#backend)
    - [Database](#database)
    - [Architecture Diagram](#architecture-diagram)
  - [Communication between Tiers](#communication-between-tiers)
    - [Frontend \<\> Backend](#frontend--backend)
    - [Backend \<\> Database](#backend--database)


# Application Architecture
[Traboda](https://traboda.com/) has developed several modern web applications. These web applications follows a __three-tier__ application architecture, which is a modular client-server architecture that consists of 3 tiers which are independent of each other and function together to deliver the experience. The three _tiers_ are:
1. **Frontend** (or presentation tier, or user interface): offers a graphical user interface (GUI), which displays information to and collects information from the users.
2. **Backend** (or application tier): handles the business logic and processes user inputs.
3. **Database** (or data tier): is where the information is stored and managed.

## Technologies Used
Traboda web applications use the following technologies in each tier:

### Frontend
[Next.js] : A [React] framework that handles the [client-side rendering][client-side-routing] and user interface. It offers features like [server-side rendering][server-side-rendering] (SSR), [static site generation][static-site-generation] (SSG), and [client-side routing][client-side-routing].

### Backend
[Django][Django]: Handles the server-side logic, database interactions, and API endpoints. It provides a robust framework for building web applications with features like [object relational mapping][ORM] (ORM) and [templating]. Although Django has a default [authentication], Traboda projects use the [Chowkidar] library for the user authentication.

[GraphQL] using [Strawberry][Strawberry]: Acts as the API layer, providing a flexible and efficient way for clients to request data. It allows clients to specify exactly what data they need, reducing [over-fetching and under-fetching][OFUF].

### Database
[PostgreSQL][PostgreSQL]: An open-source [relational database management system][RDBMS]  (RDBMS) that provides features like [ACID] compliance, [foreign key] constraints, and full-text search.

### Architecture Diagram
```
 [Frontend]
   Next.js
     |
     | GraphQL API Requests
     |
 [Backend]
 Strawberry
   Django
     |
     | SQL commands
     |
 [Database]
  Postgres
```

## Communication between Tiers
The following sections describe how two consecutive tiers communicate.

### Frontend <> Backend
The frontend (Next.js) communicates with the backend (Django) through the GraphQL API. Next.js can make GraphQL requests to fetch data from the backend and update the UI accordingly.

GraphQL is a query language for APIs that provides a flexible way for clients to request data. It's often used as an API layer in web applications. While Django can be used to build a GraphQL API, the API itself is typically separate from the database interactions.

```
-----------------------------------------------------
| Next.js |
-----------------------------------------------------
     |
     v GraphQL Request
     |
-----------------------------------------------------
| GraphQL API |
-----------------------------------------------------
     |
     v
-----------------------------------------------------
| Django |
-----------------------------------------------------
```

### Backend <> Database
Django typically interacts with databases using ORM and database driver.

**Object-Relational Mapper (ORM)**: Django's ORM, called Django ORM, provides a high-level abstraction for interacting with databases. It maps Python classes to database tables, allowing you to work with database objects as if they were regular Python objects.

**Database Driver**: Django uses a database driver (e.g., psycopg2 for PostgreSQL) to communicate directly with the underlying database system. The driver handles the translation between Django's ORM queries and the specific SQL dialect of the database.

```
-----------------------------------------------------
| Backend: Django Models (e.g., User, Product) |
-----------------------------------------------------
          |
          v
-----------------------------------------------------
| Django ORM |
-----------------------------------------------------
          |
          v
-----------------------------------------------------
| Database Driver (e.g., psycopg2, mysqlclient) |
-----------------------------------------------------
          |
          v
-----------------------------------------------------
| Database System (e.g., PostgreSQL, MySQL) |
-----------------------------------------------------
```

[Next.js]: https://nextjs.org/docs/
[client-side-rendering]: https://nextjs.org/docs/pages/building-your-application/rendering/client-side-rendering
[server-side-rendering]: https://nextjs.org/docs/pages/building-your-application/rendering/server-side-rendering
[static-site-generation]: https://nextjs.org/docs/pages/building-your-application/rendering/static-site-generation
[client-side-routing]: https://nextjs.org/docs/pages/building-your-application/routing/linking-and-navigating
[Django]: https://docs.djangoproject.com/
[ORM]: https://opensource.com/article/17/11/django-orm
[authentication]: https://docs.djangoproject.com/en/5.1/topics/auth/
[templating]: https://docs.djangoproject.com/en/5.1/topics/templates/
[GraphQL]: https://graphql.org/
[Strawberry]: https://strawberry.rocks/
[PostgreSQL]: https://www.postgresql.org/
[RDBMS]: https://cloud.google.com/learn/what-is-a-relational-database
[ACID]: https://en.wikipedia.org/wiki/ACID
[foreign key]: https://en.wikipedia.org/wiki/Foreign_key
[React]: https://react.dev/
[Chowkidar]: https://github.com/aswinshenoy/chowkidar
[OFUF]: https://stackoverflow.com/a/44568365