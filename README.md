# Pharos Release Downloads

Public release downloads for Pharos v0.8.3.

This repository contains the public release page.

## Downloads

- [Debian package](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos_0.8.3_amd64.deb)
- [Linux x86_64 GNU tarball](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos-0.8.3-linux-x86_64-gnu.tar.gz)
- [macOS x86_64 package](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos-0.8.3-darwin-x86_64.pkg)
- [macOS ARM64 package](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos-0.8.3-darwin-arm64.pkg)
- [Windows ZIP](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos-0.8.3-windows-x86_64-msvc.zip)
- [architect app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos-app-architect-0.8.3.tar.gz)
- [ucal app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos-app-ucal-0.8.3.tar.gz)
- [menu_spa app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos-app-menu_spa-0.8.3.tar.gz)
- [dev_docs app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/pharos-app-dev_docs-0.8.3.tar.gz)
- [SHA256 checksums](https://github.com/Helios-23/pharos-release/releases/download/v0.8.3/SHA256SUMS-0.8.3.txt)

## Release Notes: v0.8.3 — 2026-10-09

### New Features

#### Architect

- Accepts multiple context files in one build request. The task keeps each accepted file for later review.
- Accepted context history shows the text and attachments used in successive builds of an app.
- Follow-up text requests can change an existing generated app. For example, a user can add a dashboard field or move a selected page element, then review the updated preview.
- The visual editor can add form rows, containers, text, and controls through an organized element menu.
- Drag-and-drop editing moves an element to a new position. Holding Alt or Option while dragging places it inside another element.
- Undo and redo restore recent visual edits. Use Command or Control+Z to undo, and add Shift to redo.
- Element editing reaches nested text and icons. Saved changes remain in the app when the user reopens its preview.
- Generates backend-independent apps that inherit its configured database backend. Generated apps keep the same logical schema when you choose another supported backend.
- Data-model edits convert stored field values alongside the schema change. Conversion checks reject incompatible values before changing existing records.

#### Database

- Human-readable YAML database contracts support reusable declarations through anchors and aliases. App builds validate and compile them to JSON; Architect generates and exports YAML source while runtime database loading remains JSON-only.
- Database-backed apps use one logical database interface with all supported primary backends. Choose the backend through configuration without rewriting app queries or migrations. Primary backends supported are: SQLite, PostgreSQL, MySQL, or MongoDB
- Portable database declarations cover entities, indexes, uniqueness, foreign keys, checks, and historical data updates. Each backend implements the same declared rules.
- Logical backups and restores support every primary backend. Restore checks validate the schema and records before committing changes.

### Included changes

- The context entry grows with longer instructions and scrolls when it reaches its height limit. Selected files appear beside the context label before the build starts.
- UCAL booking and business management, storefront carts and orders, and Architect project storage use the shared database contract.
- In-memory JSON working views support calculations and rendering. Guarded transactions persist changed records without exporting and importing the whole database for each interaction.
- Startup readiness checks verify the declared physical schema before serving database-backed apps.
- Separate runtime components support cached builds of unchanged helpers and database drivers.

### Database configuration

- New apps use the configured backend. Moving an existing populated app to another backend requires an explicit data export, import, and verification before accepting writes.
- Redis retains its existing role as an optional cache. It does not replace the configured primary database.

### Fixes and refinements

#### Database and deployment

- Commerce upgrades recover a missing store from its recorded owner membership, preserve existing ownership, and reject ambiguous ownership without changing historical migrations.
- Populated SQLite schema adoption installs missing nullability constraints and both column and table checks while preserving historical checks and existing records; repeat application retains the migration ledger.
- Menu SPA recognizes its verified historical schema-file checksum during logical contract adoption without replaying catalog seeds.
- Runtime deployment migrates only Debian-owned apps. External apps use their updated staged bundles for migration, avoiding attempts to migrate older installed contracts with a newer runtime.
- Runtime and app upgrades retain configured database connections, namespaces, and data locations so separate apps cannot be redirected into one global database during migration.

#### Runtime and Commerce

- Browser navigations receive readable error pages for missing routes and other HTTP failures; API and HTMX error responses retain their machine-readable contracts.
- App mount roots redirect to their trailing-slash URL so relative stylesheets and assets resolve within the app, including Dev Docs.
- App bundles include Bootstrap Icons stylesheets and fonts when referenced by CSS, even without standalone SVG icon references.
- New app builds invalidate browser HTTP caches once per build without clearing login sessions or local user storage. Unversioned assets require revalidation.
- Repeat purchases create fresh cart reservations instead of reusing confirmed reservations from prior orders, preventing provider checkout conflicts.

#### Architect

- Media extraction uses one platform-helper implementation; Architect artifact preparation and helper transport live in the Architect crate without duplicate OCR or speech engines in the root runtime.
- Editor history renders a bounded list when source-file history reaches the query limit, instead of failing the page.

- Source-edit results update their own panel without replacing the editor workspace; navigation retains its reusable target.
- Fixed visual edits that failed validation after deployment. A newly added form row now saves and remains available when the user reopens the app.
- Fixed element placement so new rows appear inside the editable page. Information cards below the page boundary remain separate from the app.
- Fixed deletion of nested elements, including icons, so the selected item disappears from the saved page.
- Fixed task context and preview behavior so accepted files and later requests stay associated with the same app.
- Imported YAML and JSON projects initialize previews on the configured database backend and become viewable after import instead of remaining in Preparing preview.
- Deleting an edited project removes its version chain without violating restrictive references or deleting another project.

#### UCAL

- Service editors use their declared icon controls and exclude inactive technicians from assignments and service summaries.
- Service assignment inputs match the save operation; valid short durations and display-order changes persist without being silently overwritten.
- Service editing places Cancel in the card header, groups bounded numeric controls, and aligns color and image controls. Image selection shows the filename and preview; removal shows None and the selected service color.
- Service image uploads persist after Save and appear on managed service cards. Deleted services disappear from the management list; compact cards overlay Edit Service on the image’s upper-right corner.
- Reopening Edit Service preserves the mounted image URL in the client preview. Editor rows use compact, consistent spacing.
- Managed service cards provide a lower-right Delete Service overlay with confirmation. Edit Service places image controls below the preview, technicians beside the image, and Save at the bottom-right.
- Service creation, editing, and deletion return to the business management page. The Services URL redirects to that consolidated workspace.
- Quick Add Service provides a linked color picker and hex field and persists the selected service color.
- Service cards and editor previews without images display their selected color and initials from every word in the service name.
- Service order pickers exclude deleted services; creation offers one new position and editing offers only existing active positions.
- Booking options use aligned, compact input rows with matching Add and Remove icon controls. Service deletion confirmations place the destructive action at the bottom-right.

- Reuse bounded SQLite/Turso database handles instead of reopening the engine for each logical operation, reducing authenticated page latency while preserving independent transactions and file-replacement detection.

- Business creation places Cancel beside the header and uses the shared Create Business icon.

- Managed business cards follow creation order through one shared query implementation, with new businesses appended last across all supported backends.

- Deleting a business returns to Manage Businesses. Business deletion dialogs align controls correctly and suppress unnecessary scrolling.

- Business editing keeps payment controls in independent forms, with valid HTMX targets and multipart uploads. Public/private buttons reflect the current status, and delete dialogs stay within the viewport.

- Business calendars open on today’s date instead of the latest appointment; explicit date and month navigation remains available.

- Restored UCAL business-detail pages for authorized owners.

#### Menu SPA

- Order numbers include the date so the daily sequence can restart without colliding with orders from earlier days.
- Cart and checkout Back controls work when opened directly and keep their navigation target available.

#### Dynamic App

- Rejected-action reports retry definite concurrent write conflicts instead of silently losing diagnostics to background worker updates.
- HTMX preview controls load the declared task-list fragment instead of a disabled runtime-state endpoint. Declared-page HTMX requests use their normal renderer when no feature renderer is assigned.

#### Payments

- Replacing provider credentials requires fresh account verification and invalidates pending OAuth callbacks. UCAL and storefront owners can verify new credentials after an unfinished connection without retaining the previous account’s capabilities.

- Connection-test success feedback confirms Stripe authentication and the configured account, rather than implying that saving credentials verifies a connection. Smoke tests distinguish rejected synthetic credentials from controlled provider success.

#### Database

- Business counts, tenant roles, management permissions and appointment access use shared domain policies through generic database operations. Credential and session lookup rules are shared across adapters, including expiry and revoked-session handling. Guards prevent these read policies from being reimplemented separately by each backend.

#### Server runtime

- Default developer checks and the full local app smoke enforce HTMX contract guards for declared routes/actions, target bindings, form structure, and rendered response fragments.

- Static app routes with trailing slashes resolve their declared page artifacts correctly, including mounted directory pages.

- Fixed intermittent bad-request pages during navigation. Unused browser connections close without receiving an error page.

#### Database

- Fixed backend-dependent ownership, session, and rate-limit handling so supported backends enforce the same security rules.

#### Developer documentation

- Documentation pages use mounted asset URLs, preserving CSS, icons, and scripts on directory URLs with or without trailing slashes.

- Documentation builds select the shipping runtime feature set instead of enabling every optional engine and host bridge. Cargo/Rustdoc orchestration belongs to the documentation crate and uses locked local dependencies.

### Platform validation

- Linux x86_64 GNU passed installed-package validation and the full nine-app QA smoke matrix. macOS x86_64 uses native host smoke checks.
- This release has an explicit operator-approved exception for native macOS ARM64 and Windows x86_64 execution because suitable systems are unavailable. macOS ARM64 receives cross-build and package integrity checks; Windows receives cross-build, package integrity and Wine smoke checks. These checks do not constitute native platform validation. The exception applies only to v0.8.3.

### Published artifacts

- pharos_0.8.3_amd64.deb
- pharos-0.8.3-linux-x86_64-gnu.tar.gz
- pharos-0.8.3-darwin-x86_64.pkg
- pharos-0.8.3-darwin-arm64.pkg
- pharos-0.8.3-windows-x86_64-msvc.zip
- SHA256SUMS-0.8.3.txt

### Packaged apps in the base release

- todo_list, commerce_spa, dynamic_app and static_app.

### Apps validated with this release

- Architect, UCAL, Commerce SPA, Menu SPA, Dynamic App, Todo List, Static App, Developer Docs and LLight passed QA smoke checks. Architect, UCAL, Menu SPA and Developer Docs app archives are published separately.
