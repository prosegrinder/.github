# ProseGrinder Default Community Health Files

Default
[community health files](https://help.github.com/en/github/building-a-strong-community/creating-a-default-community-health-file-for-your-organization)
for ProseGrinder.

## Workflows

Workflows are designed based on
[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).

In general, workflows should follow this pattern:

1. Default (typically main) is protected and only updated via PRs.
2. Every PR should pass linting and tests, found in the language’s CI workflow
3. On merge, the release workflow should

The following are reusable workflows per language.

### Python Poetry

Conventional commits will drive versioning via the Python implementation of
[commitizen](https://commitizen-tools.github.io/commitizen/).

- [Poetry Lint](.github/workflows/poetry-lint.yaml): Runs `pylint` and `black`.
- [Poetry Test](.github/workflows/poetry-test.yaml): Runs `pytest` tests.
- [Poetry CI](.github/workflows/poetry-ci.yaml):
  - Invoke on `push` to PR branch.
  - MUST pass in order to merge PR.
  - Combines Lint and Test into a single workflow.
- [Poetry Release](.github/workflows/poetry-release.yaml)
  - Invoke on `push` to `main`, typically via PR merge.
  - Runs both Lint and Test to ensure project integrity.
  - Bumps the project version and generates a changelog via Commitizen, based on
    Conventional Commits.
  - Tags the project and pushes changes to main.
  - Creates a GitHub release based on the tag and the changelog created by
    Commitizen.
- [Poetry Publish](.github/workflows/poetry-publish.yaml)
  - Invoke on `tag`, typically via Poetry Release.
  - Builds the project.
  - Optionally publishes to PyPi test. See workflow for details.
  - Publish to PyPi.

### NPM
