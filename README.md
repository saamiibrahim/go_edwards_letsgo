# Snippetbox

Snippetbox is a small Go web application for managing and viewing short text snippets. It is structured as a simple tutorial-style project with:

- a Go web server in `cmd/web`
- application handlers in `cmd/web/handlers.go`
- routing in `cmd/web/routes.go`
- MySQL-backed snippet models in `internal/models/snippets.go`
- HTML templates in `ui/html`
- static assets in `ui/static`

## Features

- Home page rendering with Go HTML templates
- Static asset serving from `/static/`
- Basic snippet view and create routes
- Database connection pooling using `database/sql`

## Requirements

- Go 1.26+
- MySQL server

## Setup

1. Clone the repository.

```bash
git clone <repo-url> snippetbox
cd snippetbox
```

2. Create a MySQL database and user, or update the DSN in the command below.

3. Create a `snippetbox` database and the required table. For example:

```sql
CREATE DATABASE snippetbox;
USE snippetbox;

CREATE TABLE snippets (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    created DATETIME NOT NULL,
    expires DATETIME NOT NULL
);
```

4. Run the application.

```bash
go run ./cmd/web/ -addr=":4000" -dsn="web:pass@/snippetbox?parseTime=true"
```

Adjust the `-dsn` value to match your MySQL username, password, host, and database name.

## Usage

- Open `http://localhost:4000/` in your browser to view the home page.
- The app currently supports:
  - `/` — home page
  - `/snippet/view?id=<id>` — view a snippet by ID
  - `/snippet/create` — create a new snippet (POST only)

## Project Structure

- `cmd/web/main.go` — application entry point and server startup
- `cmd/web/routes.go` — HTTP route definitions
- `cmd/web/handlers.go` — request handlers and template rendering
- `cmd/web/helpers.go` — error handling helpers
- `internal/models/snippets.go` — database model for snippets
- `ui/html` — base and page templates
- `ui/static` — CSS, JavaScript, and image assets

## Notes

This project is in early development. The snippet model methods are currently placeholders and will need implementation before the app can insert or retrieve actual snippet records from the database.
