# AGENTS.md - webshop-ts-angular

Repository contract for any AI coding agent working here. Read this file and the shared workflow it
links before editing.

This file adapts the DOX framework from `agent0ai/dox` at revision
`765ae4ac02cc884eefcd41a3d0f71941721adb89` (retrieved 2026-11-05 UTC). The upstream MIT notice is
kept verbatim in `docs/dox-LICENSE.txt`.

## Purpose

A small Angular client for a web store, generated with Angular CLI 16.1.3. The app bootstraps
`AppComponent` from `src/app/app.module.ts`, and `AppComponent` renders `<app-header>` plus a
`<router-outlet>`. The toolbar header shows the attribution sentence "Web Store App using TypeScript
and Angular by Anton Gulin" and a cart badge menu. The home page renders a filter drawer and a
products header with sort, item-count, and column-count controls.

This is a work-in-progress front end. There is no backend, no product catalogue, and no cart state:
the cart menu shows placeholder rows and a fixed total, and `routerLink="/cart"` has no matching
route in `src/app/app-routing.module.ts`. It is a public, work-in-progress repository, not a
published package. The GitHub repository setting has no homepage, and no GitHub Pages site or other
deployment is configured.

The repository is normally **archived** on GitHub. For an authorized publication, temporarily
unarchive it only when necessary, then restore and verify the original archive state afterward.
Reuse existing task authorization, and preserve archive state during local-only work.

## Ownership

Maintained by Anton Gulin (`i@anton.qa`, https://anton.qa). Follow Anton's task scope and standing
publication and merge authority in the shared workflow. The public identity in metadata, README, and
rendered attribution strings is **Anton Gulin**; preserve historical Git authorship rather than
rewriting history.

## Local Contracts

Small, flat tree. The files that carry the contracts:

- `AGENTS.md` - this contract.
- `docs/dox-LICENSE.txt` - verbatim MIT notice for the DOX text adapted here.
- `package.json` - npm metadata and four scripts: `ng`, `start` (`ng serve`), `build` (`ng build`),
  and `watch`. There is no `test` script. Runtime dependencies are Angular 16.1, Angular
  Material/CDK 16.1.3, rxjs 7.8, tslib 2.3, and zone.js 0.13; dev dependencies are the Angular CLI
  and build tooling 16.1.3, Tailwind 3.3, postcss, autoprefixer, and TypeScript 5.1.
- `package-lock.json` - committed, lockfile version 3. It must stay in sync with `package.json`;
  dependency changes need explicit authorization.
- `angular.json` - project `webshop-ts-angular`, `sourceRoot` `src`, prefix `app`. The `architect`
  section defines only `build`, `serve`, and `extract-i18n`: there is no `test` target and no `e2e`
  target. The build writes to `dist/webshop-ts-angular`, defaults to the production configuration,
  and loads the Material prebuilt theme plus `src/styles.css` as global styles.
- `src/main.ts` - bootstraps `AppModule` with `platformBrowserDynamic`.
- `src/index.html` - page template; its only application element is `<app-root>`.
- `src/app/app.module.ts` - declares `AppComponent`, `HeaderComponent`, `HomeComponent`, and
  `ProductsHeaderComponent`, imports a broad set of Angular Material modules (several are not yet
  used by the templates), and bootstraps `AppComponent`.
- `src/app/app.component.ts` - inline template `<app-header></app-header> <router-outlet></router-outlet>`;
  this is the consumer of the header component.
- `src/app/app-routing.module.ts` - routes: `""` redirects to `home`, and `home` renders
  `HomeComponent`. Nothing else is routed.
- `src/app/components/header/header.component.ts` and `header.component.html` - the toolbar. The
  component only supplies `templateUrl: "./header.component.html"`; the header copy, cart bindings,
  and `routerLink` bindings live in the HTML file, and its home-link sentence is the repository's public
  attribution string.
- `src/app/pages/home/` - `home.component.ts` and `.html` (drawer shell with `cols` state) plus
  `components/products-header/` (sort, item count, and the `columnsCountChange` output).
- `src/styles.css` and `tailwind.config.js` - Tailwind layers over Material typography. The Tailwind
  content glob is `./src/**/*.{html,ts}`, so classes used in templates are scanned.
- `tsconfig.json` and `tsconfig.app.json` - strict TypeScript, with `strictTemplates` in the root
  file's Angular compiler options.
- `.github/workflows/code-review.yml` - the only workflow. It calls the shared Robin review workflow
  (`antongulin/robin/.github/workflows/review.yml@main`) and passes the `LLM_API_KEY`,
  `LLM_BASE_URL`, and `LLM_MODEL` secrets.
- `.vscode/extensions.json`, `.vscode/launch.json`, `.vscode/tasks.json` - Angular CLI editor
  defaults, tracked on purpose.
- `.gitignore` - ignores `/dist`, `/node_modules`, `/.angular/cache`, `/coverage`, and local editor
  and system files.
- `README.md` - human setup notes. It still carries the unmodified Angular CLI scaffolding sections,
  including `ng test` and `ng e2e`; neither runs in this repository.

Configuration and side effects:

- A fresh checkout has no `node_modules`. Any build or serve needs `npm ci` first, which is an
  install and needs task authorization.
- `dist/` and `.angular/cache/` are generated and gitignored; never commit them.
- The review workflow reads repository secrets. Never print, log, or commit secret values.

## Work Guidance

- Inspect the real files before changing them. Most tasks here change one string, one scalar, or one
  workflow input; keep the diff that small.
- Treat `package.json` and `package-lock.json` as contract files. Leave both untouched unless the
  task is explicitly about dependencies, and do not run installs, upgrades, or a package rename as a
  side effect.
- Identity and attribution are literal text. The public name is Anton Gulin, so a display-string fix
  is a one-line template edit with no dependency or routing change. Do not reintroduce the legacy
  name.
- GitHub Actions: new or changed jobs use the standard Ubicloud runner, `runs-on:
  ubicloud-standard-2`. This repository's only workflow is a reusable-workflow caller, so the label
  goes through its `runner` input as a JSON-encoded string: `runner: '"ubicloud-standard-2"'`.
- The Robin caller needs `actions: read`, `contents: read`, and `pull-requests: write`. The reusable
  workflow declares all three and reads `actions` to detect superseded runs; a caller can only
  narrow a callee's permissions, so keep them aligned.
- Merge strategy: squash by default for one cohesive PR. That default is subject to the gates that
  actually apply. As verified 2026-11-05 UTC, this repository allows squash, merge-commit, and rebase
  merges, has auto-merge off, and has no branch protection or ruleset. Verify permitted methods and
  current gates before merging, and do not change repository settings as a side effect of a content
  change.
- Publication here is source publication. There is no Pages site or deployment target, so do not add
  a deploy step or claim a live URL; verify the pushed commit instead.
- Keep stable rules here and execution evidence in task records. When Anton requests a durable
  behavior change, record it here or in the relevant child contract.
- Shared workflow rules are not duplicated here. Read `~/.agents/instructions/WORKFLOW.md`, or
  https://github.com/antongulin/baseline/blob/main/baseline/02-agents.md when that file is absent.

## Verification

Run only what the change can break.

- `python3 -c "import json; json.load(open('package.json'))"`, and the same for `angular.json` -
  confirms a manifest still parses. Because no `test` script and no `test` architect target exist,
  `ng test` and `ng e2e` from the README scaffolding are not runnable checks here.
- `python3 -c "import yaml; yaml.safe_load(open('.github/workflows/code-review.yml'))"`, or Ruby
  `Psych` where PyYAML is absent - confirms a workflow edit still parses as YAML.
- `git diff --check` - catches whitespace damage.
- `npm ci && npm run build` - production build into `dist/`; confirms the templates and strict
  template type checking still compile. It needs the install step, and there are no committed build
  artifacts to compare against.
- `npm start` - development server on http://localhost:4200, useful for reading the rendered toolbar
  text. It also needs the install step.
- CI: the only workflow is the Robin reviewer, which runs on pull requests and issue comments. It
  does not build or test the app, so a green run says nothing about compilation or the rendered page.

## DOX discipline

- `AGENTS.md` files are binding contracts for their subtrees. Before editing, read this root and
  every applicable child contract; the nearest contract adds local detail without weakening DOX.
- After a meaningful change, reconcile the affected contracts, file indexes, and human documentation.
  Changes to purpose, structure, commands, permissions, or durable workflow rules belong here.
- Add a child `AGENTS.md` only for a durable ownership boundary with its own rules, materials, or
  quality standards. Its sections are Purpose, Ownership, Local Contracts, Work Guidance,
  Verification, and Child DOX Index, and the parent indexes each direct child.
- Before closeout, recheck the changed paths against this contract, refresh any affected index, run
  the relevant existing checks, and report documents intentionally left unchanged with the reason.

## Child DOX Index

None. The tree is flat and small enough that this root file is the whole contract.
