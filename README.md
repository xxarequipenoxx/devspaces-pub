# devspaces-pub

Public devfile for Red Hat OpenShift Dev Spaces (Eclipse Che). `devfile.yaml` declares a
minimal workspace (devfile schema 2.2.2, workspace name `devspaces-public`) with no
components yet, so a workspace started from this repository gets the default developer
image of the Dev Spaces instance.

## Usage

Start a workspace from the repository URL in the Dev Spaces dashboard, or open
`https://<devspaces-host>/#https://github.com/xxarequipenoxx/devspaces-pub`.

## Repository standards

Managed with the shared standards of
[github-standards](https://github.com/xxarequipenoxx/github-standards): Conventional
Commits, squash merges through pull requests, the standard pull request checks plus a
devfile lint job (yamllint and the devfile JSON schema), and tag-based releases.
