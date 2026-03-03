# Release Process

MosterHub uses [release-please](https://github.com/googleapis/release-please) to automate versioning and changelog generation. Releases are driven entirely by [Conventional Commits](https://www.conventionalcommits.org/) — no manual version bumping or changelog editing is required.

## How It Works

1. Contributors push commits to `master` using Conventional Commits format
2. The release-please GitHub Action runs automatically on each push
3. release-please analyzes all commits since the last release
4. If releasable commits exist (`feat` or `fix`), it creates or updates a **release PR**
5. The release PR contains:
   - Updated version in `.release-please-manifest.json`
   - Updated `CHANGELOG.md` with organized sections
6. When the release PR is merged, release-please creates a **GitHub Release** with a git tag (e.g., `v0.1.0`)

## Version Bumps

Version bumps follow [Semantic Versioning](https://semver.org/):

| Commit Type | Version Bump | Example |
| --- | --- | --- |
| `fix` | Patch | 0.1.0 → 0.1.1 |
| `feat` | Minor | 0.1.0 → 0.2.0 |
| Breaking change (`!` suffix or `BREAKING CHANGE` footer) | Major | 0.1.0 → 1.0.0 |

Other commit types (`docs`, `refactor`, `chore`, `perf`) do **not** trigger a release on their own. They are included in the changelog only when bundled with a releasable commit in the same release.

## Changelog Sections

The changelog groups entries by commit type. These mappings are defined in `release-please-config.json`:

| Commit Type | Changelog Section | Triggers Release |
| --- | --- | --- |
| `feat` | New Content | Yes (minor) |
| `fix` | Corrections | Yes (patch) |
| `docs` | Meta-Documentation | No |
| `refactor` | Restructuring | No |
| `chore` | Maintenance (hidden) | No |
| `perf` | Performance | No |

> `chore` commits are hidden from the changelog entirely. They are tracked internally but do not appear in release notes.

## Configuration Files

### release-please-config.json

Defines the release type (`simple`), package name, changelog path, tag format, and changelog section mappings. This is where changelog sections are customized.

### .release-please-manifest.json

Tracks the current released version. Automatically updated by release-please when a release PR is created.

### .github/workflows/release-please.yml

The GitHub Actions workflow that triggers release-please on pushes to `master`. Uses `googleapis/release-please-action@v4`.

## Overriding Version

To force a specific version for the next release, add a `Release-As` trailer to any commit message body:

```
chore: prepare for v1.0.0 milestone

Release-As: 1.0.0
```

This overrides the calculated version regardless of commit types.

## Related Resources

- [Commit Message Guidelines](../../AGENTS.md#commit-message-guidelines) — Formatting rules, types, scopes, and release-please footers
- [release-please](https://github.com/googleapis/release-please) — The tool powering automated releases
- [Conventional Commits](https://www.conventionalcommits.org/) — The commit message specification
- [Semantic Versioning](https://semver.org/) — The versioning scheme
