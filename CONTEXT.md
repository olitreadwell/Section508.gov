# GSA/Section508.gov context
> refreshed 2026-09-30 | upstream default: main @ 10a30545

## Identity & policies
- upstream: GSA/Section508.gov, default branch `main`, primary language JavaScript
  (Jekyll content + Angular ART in `src/`), English-first: yes (all content, issues,
  and maintainer conversation are English).
- CLA/DCO: none. CONTRIBUTING.md asks contributors to follow the GSA Open Source
  Software Policy and releases contributions under CC0 1.0; no CLA bot or DCO
  sign-off requirement found.
- AI-assisted PR policy: unstated (no AI mention in CONTRIBUTING or .github).
- signed commits required: no (branch protection API returns 404; no signature
  workflow in `.github/workflows/`).
- PR template: none (no `.github/PULL_REQUEST_TEMPLATE.md`,
  `.github/pull_request_template.md`, root variants, or GSA/.github default).
  Use the pipeline 3-section fallback body.
- external tracker: GitHub only (issues via `.github/ISSUE_TEMPLATE/` forms).
- CONTRIBUTING explicitly welcomes small fixes: "For small fixes, such as typos,
  broken links, metadata corrections, and focused bug fixes, opening a pull
  request directly is usually fine."

## Conventions (verified from merged PRs)
- branch naming: mixed. Maintainer (drewnielson) uses date-prefixed names
  (`2026-09-23_acr-supplement-patch`); dependabot uses its own; others use plain
  kebab (`MathML`, `itacm-oct13`, `new-word-courses-update`). No dominant
  external pattern -> fall back to `<type>/<kebab-description>`.
- commit style: plain imperative or short descriptive subjects
  ("Fix trademark symbol (#1494)", "MathML commit (#1491)"); no strict
  Conventional Commits. PR number is appended on merge by GitHub.
- test / validate commands:
  - `npm run validate:library:offline` (content-library front matter + document
    links; CI job `content-library-validation.yml` gates PRs touching
    `_data/content-library-*.yml`, `_pages/**`, `_posts/**`).
  - `npm run validate:library` adds remote asset checks (assets.section508.gov).
  - `npm run check:links` (build + linkinator), `npm run test:html`
    (html-validate `_site/**/*.html`), `npm run test:ang` (Angular unit tests).
- how outside PRs get merged: very responsive. 1300+ merged PRs; maintainer
  (drewnielson) merged dependency + content PRs within days through Sep 2026.
  Small typo PRs have been merged before (#1258 fix typo in Table 7 column
  header). #1256 "Fix small typo" was closed unmerged.

## Maintainer picture
- drewnielson: primary merger, dependency + content PRs, days or faster.
- michaelhortongsa, JAB-867, KMSOC: content PR authors merged in Sep 2026.
- active areas: Angular/ART updates, node/runtime bumps, annual assessment
  report refresh, Accessibility Bytes posts, training course updates.
- repo hygiene: dependabot weekly with `open-pull-requests-limit: 0` for routine
  version PRs (security updates still flow), stale dependency backlog kept small.

## Issue-area health
- open issues: 0 (as of 2026-09-30). Open PRs: 3 (all dependabot bumps).
- no contested/redesign signal: quiet repo, maintainers merge small fixes fast.

## Gap ledger (dedupe — READ FIRST, never re-pick)
- `2026-08-05` self-found — fix broken async import that broke whole Angular test
  suite — outcome: fork PR #1 (closed), re-opened as fork PR #6 (OPEN,
  `fix/section508/repair_angular_test_import`). Lesson: repo CI does not trigger
  on `src/`-only changes; content PRs do trigger `content-library-validation`.
- `2026-09-25..29` engine failures — run.sh exited 1 with no trace; logged as
  `engine-failure` rows. Lesson: the trivial loop must leave a tried-repos row.
- `2026-09-30` self-found — packed typo-cleanup pass across site content/docs
  (see "Mined gaps") — outcome: pr-opened
  https://github.com/olitreadwell/Section508.gov/pull/29 (fork PR #29, branch
  `fix/content-typos`, base `main`, 22 spellings across 10 files: README,
  events-iaaf-landing, buy-accessibility-in-procurement1, qasps,
  create-math-equations, usability-testing, Section-508-tester-pd,
  2025-gsa-efforts-upcoming, 2025-reading-view, tools-glossary-terms).
  Lesson: keep a packed trivial PR inside `max_files_per_trivial_pr` (10) by
  fixing the highest-value user-facing strings first; comment-only typos can
  wait for a later pass.

## Mined gaps (discovered, not yet attempted)
- `2026-09-30` typo sweep (codespell over the repo) found ~40 genuine
  misspellings in user-facing content and docs. 22 of them shipped in fork PR
  #29; remaining candidates for a later pass include:
  - `_pages/manage/annual-assessment/2023-report/2023-appx-d-entity-summary-report.html`
    and `2024-report/2024-appx-c-entity-summary-report.html`: "paremeter" ->
    "parameter" (JS comment).
  - `_pages/manage/2026-04-01-manage-budget-for-a-Section-508-program.md`:
    "provice" -> "provide".
  - `_pages/develop/2025-09-24-recruitment-questionnaire-process.md`:
    "confortable" -> "comfortable".
  - `_includes/meta.html`: comment typos "CONONICAL" / "TWITER".
  - `pa11y-ci-readme.md`: "exludes" -> "excludes".
  - `_config.yml`: "decending" -> "descending" (comment).
- `2026-09-30` dead external links: 982 unique external links checked; ~50
  returned 404. Almost all are expired Zoom/event registration URLs on event
  pages (e.g. `gsa.zoomgov.com/meeting/register/...`) where updating the link
  would change event meaning, or old gov-hosted PDFs with no verified
  replacement. No meaning-preserving trivial link fix found this cycle.
  Candidate to re-check: `http://universaldesign.ie/What-is-Universal-Design/`
  (404) — needs a verified replacement URL before touching.
