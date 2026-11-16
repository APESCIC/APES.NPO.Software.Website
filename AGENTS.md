# Agent instructions for APES NPO Software Website

Cursor's user rules and skills set how work is done here (branches, issues, pull requests, merge, release, deploy, ship gate, decisions and safety). This file describes this repository and fills the named slots below. If anything here disagrees with them, Cursor's rules win and this file is corrected in the same milestone.

Cursor/agent layout standard: https://github.com/apescic-director/Cursor/blob/bmurphy/cursor-agent-standard-81b0/docs/cursor-agent-standards.md

The owner is Bambie Murphy, Director. Write UK English (organisation, behaviour, colour, licence) in the product, docs, issues and pull requests. Never print, paste or commit secrets.

## About the app

APES NPO Software Website is the APES CIC storefront and customer portal for NPO software and scripts. Licences and entitlements are provided by the sibling product [APES.Digital.Software](https://github.com/APESCIC/APES.Digital.Software); multi-tenant charity SaaS stays in [NPO.WorkDash](https://github.com/APESCIC/NPO.WorkDash).

- Repository: `APESCIC/APES.NPO.Software.Website`. Work only in this repository.
- Live URL and Cloudron app are not provisioned yet (scaffold outstanding; see open Epic [#1](https://github.com/APESCIC/APES.NPO.Software.Website/issues/1)).
- Every future Cloudron app is production. Read-only commands (status, logs) run freely; mutating or deploy actions follow Cursor's `cloudron-ops` and `cloudron-deploy` skills. Don't change DNS or Cloudflare.
- Security checks use GitHub's free features only: Dependabot, dependency review and CodeQL. Don't add paid or third-party scanners.

## Stack and architecture

Planned (from Epic #1; **not yet in this tree**): Laravel on Cloudron LAMP (PHP, Apache, MySQL), Vite front end, PHPUnit, root `VERSION` and changelog tooling, public storefront plus authenticated portal.

Current tree (verified 2026-11-16): only `README.md` and this agent config. There is no `composer.json`, `package.json`, `public/`, `.env.example`, CI workflow or application code yet. Do not invent stack commands until the scaffold lands — update this file when they do.

Sibling boundaries:

- **APES.Digital.Software** — licence / entitlement API and digital delivery; do not re-implement that contract here.
- **NPO.WorkDash** — hosted multi-tenant SaaS for charities; keep storefront and WorkDash concerns separate.

## Local development and preview

Laravel Herd is the only supported local stack once the app exists. Use fake demo data only. Do not document Laragon or `php artisan serve` as current practice.

| Item | Value |
| --- | --- |
| Clone | `C:\Users\BambieMurphy\Documents\GitHub\APES.NPO.Software.Website` |
| Herd site | Not linked yet (expected name when scaffolded: `apes-npo-software-website`) |
| Preview URL | None yet — skip the live preview gate until Herd can serve this repo |
| Preview command | None yet (add `scripts\preview.ps1` with the Laravel scaffold) |
| HMR port | None yet |
| Env file | None yet (key names only in `.env.example` when added; never values) |
| Database | None yet (Herd MySQL when scaffolded) |
| Mail | None yet (Herd mail catcher when scaffolded) |

### Local development with Laravel Herd

When the Laravel app is present:

- Run `herd site:info` for the URL, PHP version and connected services.
- Use `herd php` and `herd composer` so commands use this site's PHP version.
- Use `herd status` if something doesn't respond; `herd list` shows every command (`--json` for structured output).

Until then, treat this as a documents/scaffold repo: no local web preview.

## Tests and checks

| Check | Command |
| --- | --- |
| Tests | None yet (planned: PHPUnit / `composer test` after scaffold) |
| Lint / format | None yet (planned: Pint and front-end lint with the app) |
| CI workflows | None yet under `.github/workflows/` |

## Workflow slots

Shipping follows Cursor's `github-milestone-completion` and `ship-gate` skills. This repo fills these slots (refine when version tooling lands):

| Slot | Value |
| --- | --- |
| Milestone branch pattern | Prefer `milestone/vX-Y-Z-<slug>` once version helpers exist; until then use the issue/milestone naming already in GitHub |
| Version files | Planned: root `VERSION` (start `0.0.0`); not present yet |
| Release tooling | Planned: changelog / `releases.json` prepare-validate path; not present yet |
| Area labels | Existing area labels on issues (`area:public`, `area:admin`, `area:cloudron`, `area:docs`, `area:release`, …) |
| Issue title prefix | `[Type] Short title`, assignee `apescic-director` |

Development is tracked only in GitHub issues, sub-issues and `vMAJOR.MINOR.PATCH` milestones — never Linear.

Milestones already opened on this repository use titles such as `v0.1.x Beta — …`. Until beta exit, public and GitHub Release display is planned as `{VERSION} Beta` with git tags `v{VERSION}` (see Epic #1).

### Milestone shipping

1. Complete **all** issues in the milestone on its branch before the next stage.
2. One merge into `main`: a merge commit, never a squash or rebase.
3. One release (tag + GitHub Release).
4. One deploy of that release tag.

Nothing reaches `main`, and nothing is tagged, released or deployed, before stage 2. Hotfixes only with Bambie's written approval recorded on the issue.

An issue is done when its acceptance criteria are met and committed on the milestone branch; it closes when the milestone PR merges. The milestone is done only after the single merge, release and a verified deploy (once a deploy target exists).

## Deploy and health

| Item | Value |
| --- | --- |
| Target | Planned: Cloudron LAMP app (not provisioned yet) |
| Cloudron app ID | None yet |
| Domain | None yet |
| Deploy command | None yet |
| Deploys | The release tag (never a branch), once deploy tooling exists |
| Auto-deploy couplings | none |
| Health URL | None yet |
| Version field | None yet |
| Secrets live in | APES Vault (Bitwarden); never commit secrets |

## Decisions and gotchas

- 2026-11-16: Root `AGENTS.md` and `.cursorignore` added to match the APES Cursor/agent layout standard while the Laravel scaffold is still outstanding. Local stack is **Laravel Herd only** (not Laragon). Decided by Bambie via the org Cursor-agent alignment plan.
- Open issues that still say Laragon (for example [#2](https://github.com/APESCIC/APES.NPO.Software.Website/issues/2), [#47](https://github.com/APESCIC/APES.NPO.Software.Website/issues/47), Epic [#1](https://github.com/APESCIC/APES.NPO.Software.Website/issues/1)) describe historical planning text; update them to Herd when those issues are worked.
- Gotcha: this repository is effectively empty. Do not invent Composer, NPM, Herd or Cloudron commands until the matching files exist; extend this document when the scaffold lands.

## Where to find things

- GitHub issues and milestones: https://github.com/APESCIC/APES.NPO.Software.Website/issues
- Sibling licence API: https://github.com/APESCIC/APES.Digital.Software
- Sibling SaaS product: https://github.com/APESCIC/NPO.WorkDash
- Cursor/agent standards: https://github.com/apescic-director/Cursor/blob/bmurphy/cursor-agent-standard-81b0/docs/cursor-agent-standards.md
