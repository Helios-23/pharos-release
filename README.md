# Pharos Release Downloads

Public release downloads for Pharos v0.8.4.

## Downloads

- [Debian package](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/pharos_0.8.4_amd64.deb)
- [Linux x86_64 GNU tarball](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/pharos-0.8.4-linux-x86_64-gnu.tar.gz)
- [macOS Intel installer](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/pharos-0.8.4-darwin-x86_64.pkg)
- [macOS ARM64 installer](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/pharos-0.8.4-darwin-arm64.pkg)
- [Windows x86_64 ZIP](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/pharos-0.8.4-windows-x86_64-msvc.zip)
- [Architect app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/pharos-app-architect-0.8.4.tar.gz)
- [Dev Docs app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/pharos-app-dev_docs-0.8.4.tar.gz)
- [UCAL app archive](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/pharos-app-ucal-0.8.4.tar.gz)
- [SHA-256 checksums](https://github.com/Helios-23/pharos-release/releases/download/v0.8.4/SHA256SUMS-0.8.4.txt)

## Release Notes: v0.8.4

### New features

#### Architect generation and intake

- Context-driven multi-page generation combines written instructions and accepted attachments. Follow-up builds continue the existing named app and preserve accepted source when planning, model validation or compilation fails.
- Optional ChatGPT account connections complement API-key LLM vendors. Connection management, model selection and generation use the shared OAuth foundation without enabling external account login for Pharos apps.
- Mixed-folder intake accepts context documents, CSV data and images together. Automatic CSV import creates data tables, normalizes matching labels and treats repeat imports idempotently. Data-bound views can associate imported records with their images.
- Image intake supports up to 1,000 images, with a 2 MiB per-image limit and batches of ten. Uploaded assets remain associated with the task and are included through app-relative source assets.
- Editable app IDs can be renamed from Recent builder tasks. Renaming keeps the project, context and preview records, updates source exports and subsequent builds, and safely rebases restored snapshots to the current identity. App-bound sessions and social connections require sign-in again after renaming.
- One shared source-import form accepts an app folder or ZIP, TAR, TAR.GZ or TGZ archive. Early size/file checks reject oversized sources before upload; imported YAML and JSON database contracts retain their authored format.

#### Visual editing

- Shared editable grouping gives page rows, element containers and native controls consistent selection targets across generated, imported and shipped interfaces.
- Element and group movement supports placement within containers and beside other elements while retaining the current preview view. Pointer Events and pointer capture replace mouse-only drag tracking.
- The property editor supports text and mouse-over text, icon selection/removal and pixel sizing, background colors, synchronized color/hex inputs, border opacity and shadows. Colors, images and borders share one panel, with consistent Apply controls.
- Preview authentication, navigation, assets and popups remain within the isolated app preview. Preview accounts support admin and user testing; these accounts are not production account provisioning.

#### Declarative CRM

- Declarative schemas, queries, actions and UI support contacts, organizations, leads, notes, activity, follow-ups and linked records.
- CRM capabilities include validated CRUD, database-backed search/filtering/ordering, policy and owner/tenant boundaries, transactional history writes, revision-guarded edits and declared archive/delete behavior. Schemas, migrations, permissions and templates define record types and presentation.
- Generated admin/API surfaces and app-owned HTMX fragments use the same framework services. See [Declarative CRM](https://pharos.llight.io/dev_docs/contracts/crm.html) for the authoring guide and links to transaction, validation and UI contracts.

#### Social connections

- Social connections provide scoped provider credentials, encrypted storage and background collection jobs through authenticated adapters and configuration.
- Persistent browser sign-in connections retain their scoped profile across restarts. Reconnect reuses the saved profile; disconnect clears the saved sign-in.
- Collection retains source evidence and distinguishes partial or unavailable access from an empty successful result. Publication uses declared permissions and validation rules.

### Fixes and refinements

- Removed binary-size budgets from native build and release verification. Distribution size no longer blocks a server release.
- Windows SQLite connections use their supported file-locking mode instead of requesting shared-WAL coordination that is unavailable in the Windows I/O backend.
- App builds on Windows write portable ownership paths so generated artifacts pass the same boundary checks as Unix builds.
- Architect upgrades remove the obsolete task-event restriction without changing existing records or earlier migration checksums. Constraint failures are reported separately from actual database contention.
- Architect task lists respect the logged-in user. Builder accounts can access their LLM settings; account administration remains role-gated.
- Build failures remain visible, and accepted-context history and expandable audit entries make generation outcomes easier to inspect. Readable errors show the error code, message and available correlation ID instead of raw error envelopes.
- Follow-up request classification ignores embedded existing-source reference metadata, so ordinary app edits do not acquire unrelated commerce prerequisites.
- Source import, project deletion, stale-plan handling and preview project registration no longer leave valid editable projects stranded behind unavailable actions.
- Saved typography, layout, icon and style changes persist across refreshed fragments and reopened editors. Exported CSS excludes internal preview-edit comments.
- Preview toolbars stay above the app without covering its controls. Shared rendering paths keep menus, import controls and editor panels consistent.
- Media and extraction models use separate configurable roots; model binaries no longer belong inside the Architect app source bundle.
- UCAL service initials ignore parentheses, and managed service cards place the service name above price and duration.

### Connection and upgrade requirements

- ChatGPT access depends on the connected account's model availability and provider limits. A successful sign-in does not guarantee access to every model.
- Social platforms may expire sessions, require verification or restrict collection. Browser sign-in is separate from provider API authorization; API connectors require the relevant registration and permissions. A partial rendered feed is not a complete scrape, and a connection alone does not guarantee access to every resource.
- Existing populated apps retain their configured database, external media, credentials and migration history. Back up external configuration and data before upgrading.
- YAML database contracts compile to JSON artifacts; imported JSON contracts remain supported.

### Published artifacts

Runtime downloads include the Linux x86_64 GNU Debian package and tarball, macOS Intel and ARM64 installers, and the Windows x86_64 ZIP. Architect, Dev Docs and UCAL have separate app archives. `SHA256SUMS-0.8.4.txt` covers the complete public asset set. Platform validation and publication evidence accompany the release.

### Packaged apps in the base release

The Debian package includes Todo List, Commerce SPA, Dynamic App and Static App, together with runtime helpers and source examples. Architect, Dev Docs and UCAL are separately distributed apps; they are not installed by the base Debian package.

### Platform compatibility

Native macOS ARM64 and Windows execution was not verified for this release. macOS ARM64 received cross-build and package integrity checks; Windows also received execution checks under Wine.
