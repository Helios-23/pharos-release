# Pharos Release Downloads

Public release downloads for Pharos v0.7.24.

This repository intentionally keeps its source contents minimal so the
GitHub-generated source archives contain only this public release page.

## Downloads

- [Debian package](https://github.com/Helios-23/pharos-release/releases/download/v0.7.24/pharos_0.7.24_amd64.deb)
- [macOS package](https://github.com/Helios-23/pharos-release/releases/download/v0.7.24/pharos-0.7.24-darwin.pkg)
- [Windows `.zip`](https://github.com/Helios-23/pharos-release/releases/download/v0.7.24/pharos-0.7.24-windows-x86_64-msvc.zip)
- [Developer docs app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.7.24/dev_docs-app-0.7.24.tar.gz)
- [UCAL app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.7.24/ucal-app-0.7.24.tar.gz)
- [SHA256 checksums](https://github.com/Helios-23/pharos-release/releases/download/v0.7.24/SHA256SUMS-0.7.24.txt)

## Release Notes: v0.7.24

Pharos v0.7.24 tightens the production release path, deepens the shipped demo documentation, widens runtime contract surfaces, and fixes several live application and deployment issues discovered during release hardening.

This release is centered on:

- a cleaner production release path with explicit local validation, live deploy ordering, and public artifact scoping
- deeper app-centered tutorials for `todo_list`, `commerce_spa`, `ucal`, and `dev_docs`
- runtime and contract widening for hooks, middleware, and declarative mutations
- SQLite build-boundary and version-source cleanup
- fixes for login rendering, docs routing, checkout behavior, and packaged migration rollout ordering

## Current release artifacts

The public v0.7.24 release currently publishes these files:

- `pharos_0.7.24_amd64.deb`
- `pharos-0.7.24-darwin.pkg`
- `pharos-0.7.24-windows-x86_64-msvc.zip`
- `dev_docs-app-0.7.24.tar.gz`
- `ucal-app-0.7.24.tar.gz`
- `SHA256SUMS-0.7.24.txt`

## Included packaged apps

The released Pharos packages include these version-coupled apps under `/srv/pharos/apps`:

- `todo_list` — a minimal database-backed SPA for adding and removing tasks
- `commerce_spa` — Beacon Beats, an audio sample preview and purchase demo
- `dynamic_app` — the compact dynamic reference app
- `static_app` — the minimal static-pages reference

`dev_docs` is published separately as `dev_docs-app-0.7.24.tar.gz`.

`ucal` is published separately as `ucal-app-0.7.24.tar.gz`.

`llight` and the live UCAL deployment remain online-deployed apps rather than version-coupled packaged release apps.

## Current Pharos feature set

Pharos v0.7.24 is a native web-app framework built around a simple split: apps declare intent, and the runtime owns execution. The framework is designed to let a web developer build the application itself without first assembling a stack of API handlers, client fetch code, background runtime glue, and custom deployment plumbing.

### Declarative app model

Pharos apps are authored as normal app directories with app-owned files such as:

- `pharos.app.yml` for the app manifest
- declarative route, surface, workflow, action, and UI contracts
- templates and fragments for rendered HTML
- fixtures and seed data
- static assets and media files
- app-local `app.conf` overrides

The authored source of truth is YAML and templates. The build pipeline compiles that source into runtime-ready JSON artifacts consumed by the native runtime.

### App hosting profiles

The active hosting profiles in the current release are:

- `static-pages`
- `dynamic-app`

`static-pages` is for fully materialized static documentation or content sites.

`dynamic-app` is for database-backed applications served by the shared Pharos runtime.

### Native shared runtime

Pharos ships a native Rust runtime that owns:

- request routing
- action execution
- query execution
- template rendering
- fragment rendering
- response shaping
- runtime probes
- shared listener and app loading behavior

This means a Pharos app does not need to ship its own handwritten application server just to handle ordinary web interactions.

### Server-authoritative UI flow

Pharos is built around ordinary browser interactions where forms and links remain primary. The framework handles the server-side work that developers normally have to spread across multiple layers.

In practice, this means Pharos can replace large amounts of routine glue such as:

- handwritten JSON API routes for simple app mutations
- custom browser fetch flows for standard forms
- client-side state stores used only to mirror server truth
- manual re-query and revalidation code after every mutation
- repeated loading, redirect, and fragment refresh wiring

### Declarative UI surfaces

Pharos supports app-authored UI through templates, fragments, forms, declared surfaces, and static assets. The framework is suited to server-rendered pages, SPA-style dynamic screens, fragment updates, generated CRUD/admin screens, and mixed static/dynamic shells.

### Data model and relational backends

Dynamic apps are database-driven by default. The current release supports:

- SQLite
- PostgreSQL

The framework is built for relational application state rather than scratch-file state as the primary source of truth.

### Build, verify, and package workflow

The `pharos` CLI is the main framework entrypoint. The current release includes CLI flows for:

- building apps
- verifying apps
- serving apps
- serving the shared runtime
- applying app migrations
- packaging release artifacts

### Multi-app hosting

One Pharos runtime can host multiple apps under separate mount points. Each app keeps its own declarative sources and app-local configuration while sharing a common runtime process and deployment shape.

### Configuration model

Pharos uses a two-level runtime configuration model:

- shared runtime configuration in `/etc/pharos/pharos.conf`
- app-local overrides in each app's `app.conf`

### Authentication, sessions, and protected app flows

Pharos already supports authenticated application flows as shown by the published example apps. The framework-owned runtime handles common application-layer concerns around session-backed user flows, protected routes and actions, and login-dependent application behavior.

### Operational runtime features

The current release includes built-in operational surfaces for:

- `/health`
- `/live`
- `/ready`
- version reporting
- shared runtime logging
- app-local log overrides
- runtime state paths

### Deployment shape

The packaged Linux deployment layout currently assumes:

- Pharos binary at `/usr/bin/pharos`
- configuration under `/etc/pharos`
- app bundles under `/srv/pharos/apps`
- databases under `/var/lib/pharos`
- runtime state under `/var/state/pharos`
- runtime logs under `/var/log/pharos`

### Example apps included in the current framework story

The current Pharos app path is illustrated by three main dynamic examples:

- `todo_list` for a minimal database-backed SPA
- `commerce_spa` for a relational commerce flow with products, carts, orders, and downloads
- `ucal` for a broader authenticated business application with users, roles, scheduling, and workflow complexity

### What Pharos replaces for a web developer

For many ordinary application features, Pharos is intended to replace or reduce the amount of:

- handwritten API-layer boilerplate
- repetitive server-controller scaffolding
- client fetch and state synchronization glue
- custom CRUD plumbing
- per-project runtime assembly
- extra application-layer frameworks required only to connect forms, routes, database operations, and rendered UI

## Future release targets

These targets are tracked in the workspace but are not part of the public v0.7.24 release artifact set:

- Linux x86_64 musl packages
- Linux ARM64 GNU packages
- Windows ARM64 MSVC packages
- `wasm32-wasi` packaged targets
- additional release-packaged apps beyond `todo_list`, `commerce_spa`, `dynamic_app`, and `static_app`
