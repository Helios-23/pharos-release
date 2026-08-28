# Release Notes: v0.7.23

Pharos v0.7.23 is available on the public release page:

- https://github.com/Helios-23/pharos-release/releases/tag/v0.7.23

## Release overview

Pharos v0.7.23 ships the native Pharos runtime, the `pharos` CLI, and a set of packaged example apps that show the current framework path from a minimal SPA to a larger dynamic application.

This release is centered on:

- a shared native runtime for hosted Pharos apps
- a CLI for build, verify, serve, migrate, and packaging flows
- packaged example apps that can be installed directly and run without cloning the repository

## Current release artifacts

The public v0.7.23 release currently publishes these files:

- `pharos_0.7.23_amd64.deb`
- `pharos-0.7.23-darwin.pkg`
- `pharos-0.7.23-windows-x86_64-msvc.tar.gz`
- `pharos-0.7.23-windows-x86_64-msvc.zip`
- `pharos-0.7.23-ucal.tar.gz`
- `SHA256SUMS-0.7.23.txt`

## Included packaged apps

The released Pharos packages include these version-coupled apps under `/srv/pharos/apps`:

- `todo_list` — a minimal database-backed SPA for adding and removing tasks
- `commerce_spa` — Beacon Beats, an audio sample preview and purchase demo
- `dynamic_app` — the compact dynamic reference app
- `static_app` — the minimal static-pages reference

`ucal` is published separately as `pharos-0.7.23-ucal.tar.gz`.

`dev_docs`, `llight`, and the live UCAL deployment remain online-deployed apps rather than version-coupled packaged release apps.

## Current Pharos feature set

Pharos v0.7.23 currently provides:

- declarative dynamic app authoring with app-owned manifests, routes, templates, fixtures, static assets, and media
- framework-owned request handling in the native runtime
- database-backed dynamic apps with SQLite and PostgreSQL support
- CLI flows for building, verifying, serving, migrating, and packaging apps
- shared multi-app hosting with per-app configuration under a common runtime
- health, readiness, liveness, and version probe surfaces
- packaged runtime installation that places apps under `/srv/pharos/apps`, data under `/var/lib/pharos`, runtime state under `/var/state/pharos`, and configuration under `/etc/pharos`

The active hosting profiles in the current release are:

- `static-pages`
- `dynamic-app`

## Future release targets

These targets are tracked in the workspace but are not part of the public v0.7.23 release artifact set:

- Linux x86_64 musl packages
- Linux ARM64 GNU packages
- Windows ARM64 MSVC packages
- `wasm32-wasi` packaged targets
- additional release-packaged apps beyond `todo_list`, `commerce_spa`, `dynamic_app`, and `static_app`
