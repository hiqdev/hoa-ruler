# Fix CI failure caused by deprecated actions/cache@v2

## Description

CI is failing on every run (e.g. [run #24513393004](https://github.com/hiqdev/hoa-ruler/actions/runs/24513393004)) with:

```
This request has been automatically failed because it uses a deprecated version of `actions/cache: v2`.
Please update your workflow to use v3/v4 of actions/cache to avoid interruptions.
```

GitHub has begun hard-failing workflow runs that use `actions/cache@v1`/`v2`, per their
[deprecation notice](https://github.blog/changelog/2024-12-05-notice-of-upcoming-releases-and-breaking-changes-for-github-actions/#actions-cache-v1-v2-and-actions-toolkit-cache-package-closing-down).

`.github/workflows/test.yml` pins `actions/cache@v2` for the Composer package cache step, blocking all PHP test runs.

## Fix

- Bump `actions/cache` from `v2` to `v4` in `.github/workflows/test.yml`.
- Also bumped `actions/checkout` from `v2` to `v4` in the same file, since it's on the same deprecation track and not worth a separate ticket.

## Acceptance criteria

- [ ] CI workflow run completes without the `actions/cache` deprecation error.
- [ ] Composer cache step still restores/saves `vendor` correctly.
