# Initial release preparation

The [initial specification](../specs/touchtone.md) describes the implemented
scope and its limitations. Preparing or merging the package does not itself
publish an npm release.

## Package and naming

- [x] Use `pi-touchtone` for the package and repository metadata.
- [x] Use `touchtone` for the tool, custom message type, and runtime storage name.
- [x] Rename exported types, helpers, tests, and documentation consistently.
- [x] Replace the previous message imagery with handset imagery.
- [x] Remove obsolete public demo recordings rather than present them as the
  current interface.
- [x] Keep a narrow npm file allowlist and public repository/issue metadata.

## Validation and review

- [x] Run the package tests, TypeScript check, and package-content check.
- [x] Inspect `npm publish --dry-run --ignore-scripts` output without publishing.
- [ ] Complete review and merge the initial pull request.
- [ ] Record a fresh demonstration of the renamed interface before restoring
  demo links. This is not a prerequisite for the first npm release.

## Publishing

- [ ] Confirm the intended first version and npm publishing identity.
- [ ] Choose and configure the initial publication authorization method.
- [ ] Configure npm trusted publishing for subsequent GitHub Actions releases
  where supported, without storing a long-lived publishing token.
- [ ] Add a release workflow that verifies the tag against `package.json`, runs
  the package checks, and publishes with provenance.
- [ ] Prepare release notes before publication and publish them after npm succeeds.
- [ ] Obtain explicit release approval, then publish and verify a clean install
  from the registry.

Version-tag workflows, OIDC publishing, provenance, and changelog-based release
notes in [pi-cohort](https://github.com/jjuraszek/pi-cohort) and
[pi-gauntlet](https://github.com/jjuraszek/pi-gauntlet) are useful references.
Adapt their release boundary to this package rather than copying unrelated
build steps or assuming their credentials are available.
