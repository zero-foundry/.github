# Repository Settings

This document records expected baseline GitHub repository settings for Zero
Foundry repositories.

These settings are configured in GitHub repository or organization settings.
GitHub does not automatically apply them from this repository. This file is the
version-controlled source of intent for humans and automation that configure
repository defaults.

## Pull Request Settings

Enable automatic deletion of head branches after Pull Requests are merged.

Expected setting:

```text
Automatically delete head branches: enabled
```

Why:

- keeps merged topic branches from accumulating;
- reduces stale branch noise when scanning active work;
- preserves the merged commits and Pull Request history;
- still allows branch restoration from the merged Pull Request when needed.

This setting complements the `Zero CI/CD` ruleset. It is not part of the
ruleset JSON.

## Merge Settings

Current baseline:

- allow merge commits;
- use Pull Requests for default-branch changes;
- delete merged head branches automatically.

Avoid enabling additional merge methods unless the repository has a clear
reason and documents the choice.

## New Repository Checklist

When a new Zero Foundry repository is created:

1. Confirm the default branch is `main`.
2. Confirm the `Zero CI/CD` ruleset applies to the default branch.
3. Enable automatic deletion of head branches after Pull Request merge.
4. Confirm the repository uses the expected merge method.
5. Confirm the organization pull request template appears on new Pull Requests.
