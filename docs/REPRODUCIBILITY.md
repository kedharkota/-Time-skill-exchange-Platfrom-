# Reproducibility and visual sources

## Scope

This guide describes what is available in the committed project and what is required to reproduce it. The documentation update inspected source and saved outputs; it did not rerun model training or hardware/simulation experiments.

## Required inputs

The backend defaults to port 3000 and allows the frontend origin `http://localhost:5500`. It expects HTML under `public/`, while the committed HTML is at the root: create/populate a local `public/` directory or adjust the static routes before testing server-rendered pages. Review the database schema against all API queries; full integration is not verified.

## Entry point

For a visual preview, serve the repository directory:

```bash
python -m http.server 5500
```

Open http://localhost:5500. This previews the interface only.

For the backend, install Node.js and PostgreSQL. The original repo has no package manifest. In a local checkout, initialize one and install the modules required by `server.js`:

```bash
npm init -y
npm install express pg bcrypt uuid@9 jsonwebtoken cors dotenv
```

Use a UUID version supporting the existing CommonJS `require` syntax. Create a PostgreSQL database, import `dbms.sql`, and configure `.env` with `DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `DB_PORT`, `JWT_SECRET`, and optional `PORT`. Then run `node server.js`.

## Evidence and interpretation

The screenshot shows the actual landing page, without a running database. API routes and UI files are present, but a complete authenticated exchange flow was not executed. Configure a private JWT secret before using authentication.

## Visual provenance

All screenshots and experiment figures are tied to repository material. Workflow SVGs are explanatory illustrations. The full image inventory is in [assets/sources.json](assets/sources.json).

| Visual | Source |
| --- | --- |
| [overview.svg](assets/overview.svg) | New explanatory project-workflow diagram based on the committed source and documentation; not a screenshot or measured result. |
| [database-design.png](assets/database-design.png) | A5.drawio.png, original repository diagram |
| [preview.png](assets/preview.png) | Screenshot of committed index.html served over local HTTP at a 1440x1000 viewport; captured 2026-11-02. Database/model integrations were not run. |

## Validation

```bash
python tools/check_docs.py
```

The standard-library checker validates README/docs local link destinations and SVG/PNG/JPEG headers. It makes no external requests and installs no project runtime dependencies. External web links, model accuracy, image semantics, and full application execution need separate review.

## Reproduction record

For a new experiment or demo, record the source commit, environment versions, data provenance and split, configuration, command/notebook order, and resulting artifacts. Only label a measurement as reproduced after completing that run. Keep credentials and restricted datasets outside version control.
