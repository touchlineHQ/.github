# .github

Organisation profile and default community files for [@touchlineHQ](https://github.com/touchlineHQ).

The file that appears on the organisation Overview is [`profile/README.md`](profile/README.md).

This repository must stay **public**. GitHub only renders a public organisation profile README from a public `.github` repository.

## Reusable workflows

### Dependabot auto-merge

[`.github/workflows/dependabot-auto-merge.yml`](.github/workflows/dependabot-auto-merge.yml) merges Dependabot pull requests once CI has passed, up to a semver ceiling. It never checks out pull request code, skips GitHub Actions bumps by default, and needs no branch protection or ruleset.

Add this to a repository as `.github/workflows/dependabot-auto-merge.yml`. The only line that has to change per repository is `workflows:`: list the `name:` of every workflow whose completion may trigger a merge. In auto mode (empty `required-checks`), list every workflow that runs on `pull_request`: if the last one to finish is not listed, nothing triggers the merge and the pull request stays open.

```yaml
name: Dependabot auto-merge

on:
  pull_request_target:
    types: [opened, synchronize, reopened]
  workflow_run:
    workflows: ["Test"] # EDIT: workflow `name:` values, exactly; in auto mode, every pull_request workflow
    types: [completed]

permissions: {}

jobs:
  auto-merge:
    # Pin to a commit SHA: this runs with a write token.
    uses: touchlineHQ/.github/.github/workflows/dependabot-auto-merge.yml@<commit-sha>
    permissions:
      contents: write
      pull-requests: write
      issues: write # creates automerge-label on first use
      checks: read
      actions: write # always required: the merge job declares it, so granting less fails the run at startup
    with:
      allowed-updates: minor # patch | minor | major
      # allow-unclassified: "true"
      # skip-ecosystems: github_actions
      # required-checks: |       # empty = every pull_request workflow run must be green
      #   Tests with coverage
      # deploy-workflow: main.yml # needs workflow_dispatch; GITHUB_TOKEN merges don't fire push workflows
      # deploy-ref: main
      # merge-method: squash
      # automerge-label: automerge:ok
      # request-review: "true"  # ask for a review on PRs it won't merge (majors, by default), once checks pass
      # reviewers: adamsuk      # empty = the repo owner if that's a user; org-owned repos must set this
```

Dependabot pull requests the workflow won't merge (with `allowed-updates: minor`, every major) are never auto-merged. Once the same required checks have passed, including any preview build you list in `required-checks`, it requests a review from `reviewers` and turns off any native auto-merge left on the pull request. Someone already requested, or who already reviewed the head commit, isn't asked again.

Repository settings: none required. The `automerge-label` label is created on first use. GitHub Actions bumps, and any pull request touching `.github/workflows/`, are left for a manual merge because `GITHUB_TOKEN` cannot merge workflow changes.
