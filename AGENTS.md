# AGENTS.md

Conventions for AI agents working in this repository. Account-wide rules (roles, separation
of duties, forbidden actions, security) live in `~/.ai/` on the maintainer's machine and are
not repeated here. Shared CI, versioning and branch policy come from
[github-standards](https://github.com/xxarequipenoxx/github-standards).

## What this repository is

devspaces-pub is a public repository holding a devfile for Red Hat OpenShift Dev Spaces
(Eclipse Che). Starting a workspace from its URL gives a workspace named
`devspaces-public`; the devfile declares no components yet, so the Dev Spaces default
developer image is used. It is public: never add internal hostnames, registries, cluster
names or any other employer identifier.

## Binding rules

- Code, comments, commit messages and documentation are written in English.
- Conventional Commits, checked by commitizen (`.cz.toml`). The pull request title becomes
  the squash commit on `main`, so it is conventional too and it drives the version bump:
  `feat` bumps the minor, `fix` and `perf` the patch; other types release nothing.
- No AI attribution anywhere: no `Co-Authored-By` trailer naming an AI vendor, no
  "generated with" footer, in commits, pull request titles, bodies or code comments.
- Never commit on `main`, never merge: open a pull request, the human merges.
- Versions come from Git tags only; never write a version number into a file.
- Workflows stay thin callers of github-standards. Any local workflow pins third-party
  actions by full commit SHA with a `# vX.Y.Z` comment, sets `permissions: {}` at the top
  and least privilege per job, and passes user-controlled values through `env:`.
- Never commit secrets; container images referenced by the devfile are pinned by tag or
  digest, never `latest`.
- `devfile.yaml` stays valid against the devfile 2.2.2 schema and passes yamllint
  (`.yamllint.yaml`).

## Layout

| Path | What lives there |
|---|---|
| `devfile.yaml` | the Dev Spaces workspace definition |
| `README.md` | overview and usage |
| `.github/workflows/pr.yml` | pull request checks: commits, security (gitleaks, zizmor), devfile lint |
| `.github/workflows/release.yml` | tags `vX.Y.Z` and publishes the GitHub release on merges to `main` |
| `.github/zizmor.yml` | zizmor pinning policy |
| `.github/dependabot.yml`, `renovate.json` | security updates (Dependabot) and version updates (Renovate) |
| `.cz.toml`, `.pre-commit-config.yaml`, `.yamllint.yaml` | commitizen, local hooks and yamllint settings |

## Commands

| Command | What it does |
|---|---|
| `pre-commit install` | install the pre-commit and commit-msg hooks |
| `pre-commit run --all-files` | run every hook on all files |
| `uvx yamllint==1.38.0 .` | lint the YAML as CI does |
