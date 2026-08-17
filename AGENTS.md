# PGFB KPI site agent policy

## Purpose and scope

This repository owns the public static page that explains Il Mannarino's KPI
and bonus calculations. It contains presentation-only HTML and static assets;
it must not become an application backend, a source of operational KPI data,
or a store for employee information.

The current production model is GitHub Pages published from the root of
`main`. The repository owns page content and Pages configuration. It does not
own DNS, n8n workflows, Cloud Run, GCP infrastructure, email delivery, or the
runtime value of `KPI_URL`:

- DNS and a future `kpi.ilmannarino.it` custom domain are separate work;
- `pgfb-n8n-workflows` owns workflow references to `KPI_URL`;
- the relevant `pgfb-<env>-n8n` repository owns environment wiring.

## Source of truth

- `index.html` is the published page.
- `assets/`, when present, contains repository-owned static assets.
- `.nojekyll` keeps publication as plain static content.
- repository Pages settings select `main` and `/` as the publication source.

Inspect the current files and Pages settings before relying on prose or old
URLs.

## Inspect before editing

Start with:

```bash
git status --short
git branch --show-current
git log -5 --oneline
```

Review the complete page, links, external resources, responsive CSS, and the
business wording affected by the change. Preserve unrelated user changes.

## Public-content and security rules

- Everything committed here must be safe to publish to the internet.
- Never add secrets, credentials, tokens, analytics identifiers, employee or
  customer data, internal reports, unpublished targets, or operational KPI
  values.
- Do not add forms, dynamic APIs, browser storage, third-party scripts,
  trackers, remote JavaScript, or user-controlled HTML without an explicit
  privacy and security review.
- Prefer repository-owned assets. External assets must use HTTPS and an
  approved PGFB or Il Mannarino domain.
- Preserve semantic HTML, keyboard accessibility, readable contrast, mobile
  layout, and Italian-language content.
- Treat changes to formulas, eligibility conditions, thresholds, and payment
  descriptions as business-policy changes requiring explicit owner approval.

## Publication and release

Merging to `main` publishes the public site. A documentation or styling merge
is therefore a production content release, even though no server is deployed.

All normal changes use a pull request. Allowed branch prefixes are only:

```text
docs/
feature/
fix/
chore/
```

Do not create `agent/` branches. Commits created for this workspace must use:

```text
Alessandro Pezzotta <alessandropezzotta@proton.me>
```

Do not push, change Pages settings, configure DNS/custom domains, or merge a
pull request without explicit operator approval. The operator performs the
final merge unless explicitly delegated.

Avoid adding a GitHub Actions deployment workflow while direct branch
publication is sufficient. If a build becomes necessary, justify it and pin
third-party actions to reviewed immutable revisions.

## Validation

For every content change:

1. inspect all URLs and assets;
2. confirm the page contains no script, form, iframe, secret-like value, or
   personal URL unless explicitly approved;
3. serve the repository locally with a static HTTP server;
4. check desktop and narrow/mobile layouts;
5. verify the published Pages URL after merge.

Report checks as `PASSED`, `FAILED`, `NOT RUN`, or `BLOCKED`. Do not claim a
Pages release or DNS cutover succeeded until the public URL was observed.

## Multi-agent policy

Delegate only bounded, independent work that improves speed or confidence.

- Sol owns business-policy interpretation, architecture, approvals,
  publication decisions, integration, and final validation.
- Terra handles a bounded HTML/CSS/accessibility implementation or focused
  release review with an exclusive file scope before writing.
- Luna handles read-only content inventory, link and asset inspection,
  responsive/accessibility check collection, and Pages status summaries.

Parallel read-only work is fine. Never run parallel writers against
`index.html` or the same worktree. Agents must not publish Pages, modify DNS,
push, merge, or expose non-public data.

## Claude Code compatibility

`CLAUDE.md` imports this file. Keep shared policy here and add only genuinely
Claude-specific instructions there.

## Definition of done

A change is complete only when the public-content impact is approved, the page
and links are validated, mobile and accessibility implications are checked,
the diff contains no sensitive material, publication impact is explicit, and
remaining DNS or cross-repository work is listed.
