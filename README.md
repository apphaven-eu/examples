# AppHaven deployment examples

Deploy Node.js, Python, Java, PHP, Go, and Next.js applications with managed PostgreSQL on
[AppHaven](https://apphaven.eu), a European application hosting platform. Each repository is a
complete starting point with source code, a Dockerfile, local setup instructions, and an AppHaven manifest.

Every example implements the same small Todo application: list the current items, add an item,
delete an item. Each one stores its data in AppHaven-managed PostgreSQL and carries an `apphaven.yaml` manifest
next to its `Dockerfile`. Since the application is the same everywhere, the repositories can be
read side by side to compare what a given stack looks like on AppHaven.

## The examples

| Repository | Language | Framework | What it shows |
| --- | --- | --- | --- |
| [example-node](https://github.com/apphaven-eu/example-node) | JavaScript | Express | Server-rendered pages with the `pg` driver and plain SQL |
| [example-python](https://github.com/apphaven-eu/example-python) | Python | FastAPI | Form handling and HTML responses with psycopg 3 |
| [example-java](https://github.com/apphaven-eu/example-java) | Java | Spring Boot | Spring JDBC against the managed database, with a JDBC-shaped connection URL |
| [example-php](https://github.com/apphaven-eu/example-php) | PHP | No framework | The smallest version of the app: PDO and a single front controller |
| [example-go](https://github.com/apphaven-eu/example-go) | Go | Standard library | `net/http`, `html/template` and pgx, in a small static binary |
| [example-nextjs](https://github.com/apphaven-eu/example-nextjs) | TypeScript | Next.js | Server Components and Server Actions against PostgreSQL |

## What they have in common

Each repository contains:

- an `apphaven.yaml` manifest declaring a `web` container built from the repository and a managed
  `db` service of `type: postgres`;
- a `Dockerfile` that builds the application, which is the entire build pipeline on AppHaven;
- database credentials taken from the environment, never from the repository. The manifest passes
  them in with `${service.db.url}` references (or individual connection fields for JDBC),
  which AppHaven resolves at deploy time;
- the table created at startup, or on first use in Next.js;
- a `README.md` with local development instructions and the steps to deploy.

## Running one of them

Clone the example you are interested in, follow its README to run it locally against a PostgreSQL
container, then create an app in the [AppHaven console](https://console.apphaven.eu/), connect the
repository and deploy. Deploying the production branch gives you production; deploying any other
branch gives you a preview environment with its own URL and its own database.

## What deploying these examples demonstrates

AppHaven builds the container image from Git, serves the app over HTTPS, and provisions the
PostgreSQL database. Database credentials come from service references in the manifest;
managed PostgreSQL includes continuous backups with point-in-time recovery.
See [managed PostgreSQL](https://docs.apphaven.eu/services/postgres).

A non-production branch gets a preview with its own database and URL. Apps are private to project
members by default. You can make production public in the console while keeping previews private;
see [access control](https://docs.apphaven.eu/access). Every example uses a shared list, so a public
demo lets all visitors add and delete the same tasks.

These examples use standard containers and PostgreSQL drivers. You can also run them locally or
on another container host; the AppHaven-specific configuration is in `apphaven.yaml`.

## Documentation

- [Getting started](https://docs.apphaven.eu/getting-started)
- [The manifest](https://docs.apphaven.eu/manifest) and the [manifest reference](https://docs.apphaven.eu/reference/manifest)
- [Managed PostgreSQL](https://docs.apphaven.eu/services/postgres)
- [Container services](https://docs.apphaven.eu/services/container)
- [How AppHaven runs your app](https://docs.apphaven.eu/how-it-works)

## AppHaven

AppHaven hosts applications directly from a Git repository. It builds the image from your
`Dockerfile` and runs the containers your manifest declares, over HTTPS on a real domain. The
PostgreSQL database these examples use is managed by the platform, credentials and backups
included. See
[apphaven.eu](https://apphaven.eu) for the platform and [docs.apphaven.eu](https://docs.apphaven.eu)
for the documentation.

## License

[MIT](LICENSE).
