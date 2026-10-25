# Changelog

All notable changes to this project are documented here.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Changed

- Pull request template checklist now says a CHANGELOG.md update is only needed if the repo keeps one.

### Added

- CHANGELOG.md, added by [gh-factory](https://github.com/adamsuk/gh-factory).

## 2026-10-25 (Dependabot majors request a review)

### Added

- Dependabot auto-merge: new `request-review` (default `"true"`) and `reviewers` inputs. A Dependabot pull request the workflow won't merge (above `allowed-updates`, for example a major with the default `minor`; a skipped ecosystem; or one touching `.github/workflows/`) gets a review request once its required checks pass, instead of being left silently. `reviewers` defaults to the repository owner when that is a user account. Organisation-owned repos must set it. Requested in adamsuk/software-factory#10.

### Changed

- Dependabot auto-merge turns off any native auto-merge that was enabled on a pull request outside the policy, in both the label and merge jobs.
- A Dependabot pull request that changes `.github/workflows/` is classified as outside the policy up front in both jobs (label removed, native auto-merge turned off), rather than only being skipped just before the merge.
