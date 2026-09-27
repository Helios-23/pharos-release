# Pharos Release Downloads

Public release downloads for Pharos v0.8.2.

This repository intentionally keeps its source contents minimal so the GitHub-generated source archives contain only this public release page.

## Downloads

- [Debian package](https://github.com/Helios-23/pharos-release/releases/download/v0.8.2/pharos_0.8.2_amd64.deb)
- [Linux x86_64 GNU tarball](https://github.com/Helios-23/pharos-release/releases/download/v0.8.2/pharos-0.8.2-linux-x86_64-gnu.tar.gz)
- [macOS x86_64 package](https://github.com/Helios-23/pharos-release/releases/download/v0.8.2/pharos-0.8.2-darwin-x86_64.pkg)
- [macOS arm64 package](https://github.com/Helios-23/pharos-release/releases/download/v0.8.2/pharos-0.8.2-darwin-arm64.pkg)
- [Windows `.zip`](https://github.com/Helios-23/pharos-release/releases/download/v0.8.2/pharos-0.8.2-windows-x86_64-msvc.zip)
- [SHA256 checksums](https://github.com/Helios-23/pharos-release/releases/download/v0.8.2/SHA256SUMS-0.8.2.txt)

## Release Notes: v0.8.2 — 2026-09-27


### New Features

- Architect is a model-driven app builder with a connected in-browser editor. It turns a product brief into generated Pharos source, opens the app for review, and keeps source export and validation tied to the generated project.
  - Create an app from a brief and optional context files.
  - Review generated source and open a validated running preview after the app has materialized.
  - Edit managed page elements in the browser with right-click editing, group selection, parent traversal, and compact style controls.
  - Reopen generated apps and imported source apps for later edits.
  - Inspect source, exports, data-model panels, and page-layout panels from the editor.
  - Generate dashboard and KPI app layouts with compact field rows, dynamic dropdown values, and date/time controls that fit the form.
  - Download full source archives that exclude runtime databases, runtime state, vault files, uploads, temp files, secrets, and `dist`.
  - Read app metadata from `pharos.app.yml` and preserve projects when the same output app id is built again.
  - Configure bounded LLM vendor settings for cloud or local providers while keeping source writes, migrations, validation, and exports under the built-in builder.
- Platform helper binaries move heavy optional work out of the main runtime. Media extraction, barcode/QR decode and encode work, docs generation, and ops orchestration use separate helper paths.
- QR and barcode support includes generation as well as reading. Apps can use the helper path for tickets, reservations, fast links, and scanned-code flows without loading that work during ordinary server startup.

### Included changes

- Release packaging keeps server and app versions separate. A runtime package upgrade does not require separately deployed app bundles to move to the same version.
- Debian, macOS, Windows, and Linux tarball packages include the split helper binaries alongside the main `pharos` runtime.
- Linux releases include both a Debian package and a GNU tarball built from the same release binaries.

### Performance and runtime work

- SQL-backed apps no longer use JSON runtime state as request-time authority. Sessions, declared feature actions, generated API mutations, jobs, webhooks, and app records use the relational backend when relational runtime authority is configured.
- JSON runtime state stays in the file-backed/static lane or in explicit import/export and backup/restore flows. A relational app may still declare a `runtime.state_path` for export compatibility, but normal requests skip JSON-state locks and mutation helpers.
- SQLite migration startup checks use a cache keyed by the migration ledger and migration contract checksums, avoiding false invalidation from normal SQLite DB/WAL/SHM touch behavior.
- SQLite migration drift verification batches migration ledger, journal, and required-table reads through one connection. This removed the repeated database open/query loops slowing down apps and app loading. Server startup speed is significantly faster after migration-cache work.
- `/health` and `/ready` report different states. `/health` can report that the process is alive, while `/ready` waits for the loaded app set so quarantined apps do not count as full app availability.

### Fixes and refinements

- Fixed UCAL startup behavior by removing the route-demanded runtime-state projection path from relational startup and keeping SQL as the active authority.
- Fixed migration drift in `commerce_spa`, `dynamic_app`, and `ucal`.
- Fixed release package assembly so helper binaries do not get treated as app roots and packaging strip steps do not overwrite the selected runtime binary.
- Fixed docs-builder coupling so `pharos-docs-builder` does not pull SQLite/Turso into its helper graph.
- Fixed media-helper coupling so media entrypoints live outside the general runtime media module and can run as separate work, not server startup work.

### Deployment notes

- External LLM vendors are optional. The built-in builder, local validation, source export checks, and runtime contracts remain authoritative for generated apps.
- SQL-backed apps should keep sessions and app records in SQL. Redis remains an optional cache layer in this release.
- Runtime data must live outside app install footprints. Replacing app bundles under `dist/apps` or a deployed app directory must not delete databases, generated source, vaults, uploads, logs, or state directories.
- Server and app versions are separate. The Debian package can update the runtime and package-owned built-in apps while separately deployed apps keep their own version until they are intentionally redeployed.

### Published artifacts

- `pharos_0.8.2_amd64.deb`
- `pharos-0.8.2-linux-x86_64-gnu.tar.gz`
- `pharos-0.8.2-darwin-x86_64.pkg`
- `pharos-0.8.2-darwin-arm64.pkg`
- `pharos-0.8.2-windows-x86_64-msvc.zip`
- `SHA256SUMS-0.8.2.txt`

### Packaged apps in the base release

- `todo_list`
- `commerce_spa`
- `dynamic_app`
- `static_app`

### Apps validated with this release

- `architect`
- `todo_list`
- `static_app`
- `dynamic_app`
- `commerce_spa`
- `ucal`
- `dev_docs`
- `menu_spa`
- `llight`

## Current Pharos feature set

Pharos v0.8.2 is a native web-app framework built around declared app source, a shared Rust runtime, and app-owned templates and contracts.

### App authoring

Pharos apps use normal app directories with `pharos.app.yml`, declarative route/action/policy/data contracts, templates, fragments, static assets, and app-local configuration. The build step compiles those sources into runtime-ready app bundles.

### Architect

Architect adds a browser-based app builder and editor. A user can start from a brief, attach context files, review generated source, open a validated preview, edit managed page elements, and export a clean source archive.

### Runtime and data

The shared runtime owns routing, action execution, query execution, template rendering, fragment updates, sessions, readiness checks, and multi-app hosting. SQL-backed apps use relational state as request-time authority. JSON runtime state stays in the static/file-backed lane and in explicit import/export or backup/restore flows.

### Packages

The public v0.8.2 release publishes Debian, Linux GNU tarball, macOS x86_64, macOS arm64, and Windows x86_64 MSVC packages. The packages include the main `pharos` runtime plus helper binaries for optional media, QR/barcode, docs, and ops work.
